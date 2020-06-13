---
layout: post
title: Require 2FA to unlock Linux user account
author: k0dk0d
feature-img: assets/img/posts/skeleton-key_header.png
excerpt_separator: <!--more-->
tags: [Security, Intermediate, Linux, Tutorials]
---

Most of us put their laptops very frequently to sleep instead of properly shutting it down. This means that the hard drive stays decrypted. If the computer is accessed by a malicious actor, the only thing that keeps this person away from our data is the user account password. In this article I will discuss how to protect your Linux (PureOS, Debian, Ubuntu) system with two-factor authentication (2FA).

<!--more-->

<a href="https://www.yubico.com/" target="_blank">YubiKeys</a> are great two factor devices and we can use them as a second factor for our Linux user accounts. The same can be done for Windows and OSX and I'm sure that working instructions can be found online. However, this is outside the scope of this article. Note that this post is written for YubiKeys. It should be possible to similarly set up similar keys from other suppliers, however, I do not have those keys available and thus cannot test it out.

The following instructions have been used and tested on <a href="https://pureos.net" target="_blank">PureOS</a> 9.0 (amber), on <a href="https://www.debian.org/" target="_blank">Debian</a> 10.4.0, and on <a href="https://ubuntu.com" target="_blank">Ubuntu</a> 20.04 LTS.

This post here is very much based on the Purism forum entry by dc3p, which can be found <a href="https://forums.puri.sm/t/pureos-how-to-system-u2f-authentication/5552" target="_blank">here</a>.

# The gist

Since you can actually lock yourself out of your computer, there's no gist this time. You should read and understand this article before you try to set this up. However, the post is fairly short, so it won't take too long to get started. Please make sure that you read the whole article, especially the part on testing, before you start.

Fortunately, locking yourself out with this method is not as bad as loosing your hard drive's encryption key. If you did lock yourself out, go to the bottom and read the troubleshooting section.

# Setting up the two factor requirement for authentication

## System prerequisites

You will need to install some packages first. This can be done by opening a console and typing:

    sudo apt update
    sudo apt install libpam-u2f scdaemon pamu2fcfg yubikey-manager



## Checking if universal two factor (U2F) is recognized

In the blog post mentioned above, dc3p mentions that udev rules need to be set up (their step 2). This does not seem to be necessary anymore. If you plug your YubiKey in and type `lsusb` you can check if it is properly recognized. My computer, for example, says something like:

    Bus 001 Device 017: ID 1050:0407 Yubico.com Yubikey 4 OTP+U2F+CCID

Clearly, the U2F option is recognized (and the test — see later and most importantly — works).


## Register your device with PAM

PAM is the <a href="http://www.linux-pam.org/" target="_blank">pluggable authentication modules</a> for Linux project and is what authenticates the user. To register a U2F device with PAM go through the following setup. First make a new folder named `u2f` where you will store the keys.

    mkdir u2f

Then, plug in the YubiKey you want to to add for authenitcation and type:

    pamu2fcfg --origin=pam://localhost > u2f/keys

You will have to touch the YubiKey when it lights up. This command will store the YubiKey configuration in the `u2f` folder in a file named `keys`. If you want to register a backup / secondary device (always a good idea), use the following command to add more YubiKeys to this file.

    pamu2fcfg -n --origin=pam://localhost >> u2f/keys

*Note*: Here we use `>>` instead of `>` in order to append to the file `keys` instead of creating a new file named `keys`. Repeat this step for every key you would like to be able to use as 2FA device for your user account. Then move the folder to `/etc`.

    sudo mv u2f /etc

## Require authentication with PAM

**Note**: You should test this before closing the file that you have opened for editing (see next section). Otherwise you might lock yourself out of your system!

Now let's open the PAM authentication file and edit it to require 2FA. Open the file `/etc/pam.d/common-auth` as root:

    sudo vim /etc/pam.d/common-auth

Feel free to use your favorite editor. If you have never used vim before and want to give it a try, search for cheat sheets or start with <a href="http://www.atmos.albany.edu/daes/atmclasses/atm350/vi_cheat_sheet.pdf" target="_blank">this one</a>. Add the end of this file add a line as following:

    auth required pam_u2f.so cue no detect origin=pam://localhost authfile=/etc/u2f/keys

You see here that the last path is the path that leads to your key file. The middle part `cue no detect` is a configuration option, other possible options:

* Omit `cue no detect` and leave blank: There will never be a mention of the device when you enter your password. You have to make sure the device is present and that you touch it after entering the password.

* `cue no detect`: Recommended option — will prompt you to touch the device when it is plugged in and will simply return as an incorrect password if a device is not present. This way an attacker would not know that a 2FA device is required.

* `no detect`: Least secure — Will always prompt to touch the device, even if the key is absent.

**Save, but do not close this file until you have tested the setup.**

## Testing

Open a second terminal. Type:

    sudo echo it works!

The terminal will prompt you for your password. Afterwards, depending on the chosen configuration, it will prompt you to touch the key. Also, the YubiKey will blink, which means it is waiting for a touch. If you see the words `it works!` printed out on the terminal, then you are all set up and good to go. If you do not see those words, remove the line you just added in the open editor in `/etc/pam.d/common-auth` and save the file. Without closing it, test again, it should now be successful and prompt you for your password only. 

Then delete the key folder by typing:

    sudo rm -r /etc/u2f

Go back to the beginning of the post, read more carefully, and try again.

# Adding more keys later

Before you try any of the following, open the `/etc/pam.d/common-auth` file in an editor as root and comment out the line that you added before. Don't close this file until testing is completed. Make sure you open it as root such that you write to it! 

To add more keys you can do two things:

 1. Remove the `/etc/u2f` folder by typing
     
        sudo rm -r /etc/u2f

    Then follow through the section on how to register new and additional devices. You will have re-register all devices that you want to use.

 2. If you only want to add a key, copy the `/etc/u2f` folder to your home folder. Make yourself the owner of that folder by typing:

        sudo chown --recursive user:user u2f
 
    Replace `user` with your username! Using the command for adding new keys above, add another key and move the folder back to `/etc`.

Again, it is crucial that you test your setup before you close the `/etc/pam.d/common-auth` file to ensure everything works as expected.


# Troubleshooting

If you locked yourself out, you can still recover your account. Remember, your account password simply prevents your account from being unlocked once the hard-drive is decrypted and the operating system is booted. The real protection for your data is the hard drive encryption. 

There are two ways of proceeding when you locked yourself out. You can boot into a recovery shell, e.g., the PureOS recovery shell will drop you, after decrypting the hard drive, into a prompt as root. From there open the `/etc/pam.d/common-auth` in an editor and comment out the line that requires the U2F authentication (see above).

Alternatively you can do the same from a Live OS, e.g., a USB stick that runs a live PureOS version. You will need to decrypt your internal hard drive using LUKS from the life system, so you will need your passphrase. Then you can simply edit the file on that hard drive that will again be in `/etc/pam.d/common-auth`. Comment out or remove the line that requires you to touch the U2F device for login. Then go ahead and reboot into your OS.

Stay safe  
-k0dk0d
