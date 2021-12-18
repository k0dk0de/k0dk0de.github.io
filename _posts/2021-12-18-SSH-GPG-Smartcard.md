---
layout: post
title: SSH login via GPG keys on a smart card
author: k0dk0d
feature-img: assets/img/posts/header_doors.jpg
excerpt_separator: <!--more-->
tags: [Security, Advanced, Linux, Tutorials]
---


If you are logging in to multiple systems from multiple systems via SSH, you are probably already used to the regular SSH key management. Now you get a new laptop and need to set up keys for everything again - that's kind of annoying, but there's a better solution: You can authenticate SSH logins via GPG. 

<!--more-->

Here we'll go through the setup on to configure your workstation to work with GPG authentication, assuming that your GPG keys are on a smart card, e.g., a [Yubikey](https://yubico.com). We assume that the smart card is already set up. If not, check out chapter "Set up your GPG smart card" [here](/2020/06/07/LUKS-setup.html#set-up-your-gpg-smart-card). For this tutorial you will need your public key and the smart card. *Note*: This is a short and advanced tutorial, we will skip a lot of introduction, etc., and get right to the point.

## GPG setup

We assume you already have used GPG, especially since you have set up your smart cards. Furthermore, you need to know the ID of your key. You can get the key ID via: `gpg -k` (for long format, see "Configure GPG" section below).

### Import public key

Import the public key that goes with the secret key that is stored on the smart card.

```
gpg --import public_key.asc
```

Trust your own public key:

```
gpg --edit-key KEYID
```

Type `trust`, then `5` for ultimate (its your own public key), finally confirm. 

Then plug in your smart card and type `gpg --card-status`. If you now type `gpg --list-secret-keys`, you should see that a secret key for the one on your smart card is available. It is indeed available, but only on the smart card. GPG has created shadow private keys that link the smart card.

### Configure GPG agent

In `~/.gnupg/gpg-agent.conf`, add the following line and save: 

```
enable-ssh-support
```

### Configure GPG

If you have multiple GPG secret keys, add a line to `~/.gnupg/gpg.conf` that says:

```
default-key KEYID
```

This selects this specific key as the default one. In addition, my configuration contains the following defaults:

```
keyid-format 0xlong
with-fingerprint
with-keygrip
use-agent
```


## Fish configuration

[Resource](https://www.foxk.it/blog/gpg-ssh-agent-fish/)

For the fish shell, add the following configuration parameters,  e.g., to `~/.config/fish/config.fish`:

```shell
# Use gpg-agent for ssh authentication
set -e SSH_AUTH_SOCK
set -U -x SSH_AUTH_SOCK (gpgconf --list-dirs agent-ssh-socket)

# GPG TTY
set -x GPG_TTY (tty)
gpgconf --launch gpg-agent
```

Then reload your console.

## Bash configuration

The analog configuration of above's script for your `~/.bashrc` should look like this, but see also [here](https://opensource.com/article/19/4/gpg-subkeys-ssh) and [here](https://linux.die.net/man/1/gpg-agent).

```shell
export SSH_AUTH_SOCK=$(gpgconf --list-dirs agent-ssh-socket)
export GPG_TTY=$(tty)
gpgconf --launch gpg-agent
```

## Find SSH public key config

If all went well, you can type 

```
ssh-add -L
```

and get back an entry with your card.  You can recognize it since it has `cardno:###` at the end, specifying the given card number. 

Add this entry to your remote server's `~/.ssh/authorized_keys` and try logging in. You should be prompted for your PIN.

## Using multiple cards

[Resource](https://github.com/drduh/YubiKey-Guide/issues/19#issuecomment-419622290)

If you have multiple Yubikeys with the same secret key, e.g., for redundancy, GPG will complain that the card you used first is missing.  You need to associate the shadow-keys that GPG created and associated with the first card with the currently present one. In the folder where your private keys are stored, i.e., in `~/.gnupg/private-keys-v1.d`, your secret keys are stored using their key grip values and the qualifier `.key`. If you run

```
gpg -K --with-keygrip KEYID
```

you will see the key grips for your three subkeys that are on the smart card. You will also find the key grip of your public key. You will need to delete the shadow keys in the private key folder for the smart card you have set up.

### Fish function

In order to associate another smart card with the keys, the following fish function (adopted from [here](https://github.com/drduh/YubiKey-Guide/issues/19#issuecomment-434844635)) might help.  Store this function in `~/.config/fish/functions/yubiclean_gpg.fish` (new file). Then unplug your key, plug in the new one, and run the function by typing `yubiclean_gpg`.

```shell
function yubiclean_gpg
    # save current folder
    set current_folder (pwd)
        
    # delete the associated keys
    set keyid 0x7E38D9E54FE78CE8
    gpgconf --kill gpg-agent
    cd (gpgconf --list-dirs homedir)/private-keys-v1.d
    gpg -K --with-keygrip --with-colons $keyid | \
    awk -F: '/^grp/ { print $10".key"; }' | \
    xargs rm -vf
        
    # go back to current folder
    cd $current_folder
        
    # load the new ones by calling the card
    gpg --card-status
end

```

This deletes the private shadow keys associated with your smart card, then pings the now plugged-in Yubikey which associates the public key with the secret keys stored on it.

### Bash setup

Alternatively, you can use the following bash script instead of the fish function:

```bash
#!/bin/bash
# save current folder
currfolder=$(pwd)

# delete the associated keys
keyid=0x7E38D9E54FE78CE8
gpgconf --kill gpg-agent
cd "$(gpgconf --list-dirs homedir)/private-keys-v1.d"
gpg -K --with-keygrip --with-colons $keyid | \
awk -F: '/^grp/ { print $10".key"; }' | \
xargs rm -vf

# load the new ones
gpg --card-status

# go back to current folder
cd $currfolder
```

## Require touch on your Yubikey

If you are using a Yubikey, you can require that the key needs to be touched in order to work with GPG. In order to do so, you can use the yubikey-manager program `ykman`. The following commands will set the authentication `AUT`, encryption `ENC`, and signing `SIG` keys to require you to touch the Yubikey.

```
ykman openpgp keys set-touch AUT ON
ykman openpgp keys set-touch ENC ON
ykman openpgp keys set-touch SIG ON
```

When running these codes, you'll have to confirm your choice by entering the smart card's admin pin and confirming with `y`.

## Sign in with your SSH keys

If you still need to log in to a computer with your regular SSH key, you can simply unplug the smart card and log in normally. This will fall back on your already existing SSH key.

### Multi-user GitHub

If you have a setup similar to the one described [here](/2020/02/03/Github-Commits-API.html), you have to make a couple of changes:

- For your special / work repos for which you want to use an SSH key for, set up the following file in `~.ssh/config-work` (replace `work` and `id_rsa_work` with the respective repo name and key name):
  ```
  Host work.github.com
      HostName github.com
      User git
      PreferredAuthentications publickey
      IdentityFile ~/.ssh/id_rsa_work
  ```
- In your repo, run the following command to set up your local (not global) repo in order to work together with this config file: 
  ```
  git config core.sshCommand "ssh -F ~/.ssh/config-work"
  ```
 
Keep your smart card unplugged. Your config should work now.

Stay safe!  
-k0dk0d