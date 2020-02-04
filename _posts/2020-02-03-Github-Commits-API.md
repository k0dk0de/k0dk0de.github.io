---
layout: post
title: "Github: Keeping accounts separate & API introduction"
author: k0dk0d
 # feature-img: assets/img/posts/header_electronics_rpi-cut.jpg
 # feature-img: assets/img/posts/header_security_padlock-cut.jpg
 # feature-img: assets/img/posts/header_privacy_cameras-cut.jpg
 # feature-img: assets/img/posts/header_colors-cut.jpg
feature-img: assets/img/posts/header_alphabeth-cut.jpg
 # color: rgb(48, 63, 80)     # Add the specified color as feature image, and change link colors in post
excerpt_separator: <!--more-->
tags: [Tutorials, Privacy, Basics, Linux]
---

Have you ever wondered on how to use github with two user accounts? Do you want to get a short introduction to githubs API and how to find information faster and directly? Then this brief tutorial is for you.

<!--more-->

# Github commits from two independent accounts

I'm hosting this website currently on github and as you might have noticed, I'm not disclosing my name but try to stay private. Furthermore I have a github account that hosts code in my real name. How do I feed both github accouts from one computer? Here's a brief tutorial on how to do command line commits for two accounts without cross contamination.

## RSA key pair setup

You can follow the [github tutorial](https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent){:target="_blank"} for this.

You will need to create a key for each user, so this process needs to be done twice.

From the terminal, create a new key pair

    ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

Note that you don't need to actually use your real e-mail address! For example, for this website I'm using github's own no-reply e-mail address for the rsa key.

Follow the on screen commands. Usually these keys are saved in `~/.ssh` under a default name. Since you need two users, choose a key file name that is not the default name, but something that you can identify easily. Check out the new files. For each setup name you will have gotton something like (these are the default file names):

    id_rsa
    id_rsa.pub

The `*.pub` file is your public key. The other file that has no extension is your private key. **Do not** upload your private key to a website or anywhere else!

You can work with a passphrase if you like, up to you if it's necessary or not. This will depend on your target profile: where do you store these keys? Analyze, then decide.

## Add your public key to github

Log into your github account. Click on your icon on the top right of the screen, then go to settings. Select `SSH and GPG keys`. Then add `New SSH key`. 

Give your key a title, something that is readable and makes you remember later where the key belongs. In the `Key` field copy the public key. Then hit add.

You will need to add the respective key that you want to use to each of your github profiles. So far so good.

## Set up profiles in `~/.ssh`

Let us assume you have two github accounts an account named `user1` (which is your default account) and an account named `user2`. You also have the following keys just created:

    id_rsa_user1
    id_rsa_user1.pub
    id_rsa_user2
    id_rsa_user2.pub

Furthermore you have added the `id_rsa_user1.pub` file as an SSH key to your github profile for user 1, and the same for user 2.

Assuming your keys are in the default `~/.ssh/` folder: go into that folder and create a new text file named `config`. Copy the following text into your file and adjust to your needs: 

	# key configuration for user1 - the default user
	Host github.com
	  HostName github.com
	  PreferredAuthentications publickey
	  IdentityFile ~/.ssh/id_rsa_user1
	
	# key configuration for user2
	Host user2.github.com
	  HostName github.com
	  PreferredAuthentications publickey
	  IdentityFile ~/.ssh/id_rsa_user2

Note the big and important difference is the Host. This will become important next when you check your github repository out.

## `git clone` for a given user

If you want to checkout your test repository (named testrepo) from your default (user1) github account, you can run the following command now in the terminal:

    git clone git@github.com:user1/testrepo

*Note:* You will be using the `ssh` style cloning and not the https style! In this case, you will automatically check out as user 1 and this repo will be configured under your default user (user1). That's what you wanted. 

You have a repository called `privacynerd` saved in your user2 account and want to work on this one. To clone this repo as user2 you would now run the command:

    git clone git@user2.github.com:user2/privacynerd

*Note:* The difference is alone in the hostname! make sure you use the same hostname here as you configured in the `config` file above!

You can now edit and commit from both repositories as user1 and user2. The right ssh keys are selected automatically. **But be aware of the user setup!**

## User setup

This is a common pitfall. You need to know what the global user settings are! The first time you used git, a global user setting file was created, this one contains your name and your e-mail address (or whatever you told it to contain). If you only have one file, then all your commits are going to happen from this name and address (even though with the right keys). To check your settings you can run:

    git config --global user.name
    git config --global user.email

You can also see these global variables by looking at the file, which is usually at `~/.gitconfig`. This file will contain something like:

    [user]
	    name = username
	    email = username@domain.com

Here is your global file. Feel free to edit this to none / none and you'll be set for anonymity. What though if you'd like to have two different user setups? Here again is why it's nice to have a default account and a separate account. 

In every project folder, e.g., the one you just checked out named `privacynerd`, here is a folder named `.git`. Inside this folder is a file named `config`. Open this file in a text editor. This file contains the local settings. Usually, it will not contain a `[user]` section, since this setting is set globally. However, you can set a local configuration here, this will allow you to commit with a different name and email address than your global settings. For this to work just add an entry at the end of the file that reads as following:

    [user]
        name = your_alias
	    email = privacyemail

If you now commit from this specific project folder, than this name and e-mail address will be used and not your global one. *Note* that you will be required to set this up for every user. If you make a mistake, there will be a commit in your real name. So it might just be safer to set your real name to an alias too. 


# API Introduction

As most websites these days, github also has an application programming interface: an API. It's actually really useful to know your way around the API a little bit, because certain information can be grabbed much faster this way. Sure you can grab a lot of the information you can find here also from the website, but sometimes it's just easier to read a well structured json file, even if you're human :)

Let's use the [Hak5](https://github.com/hak5){:target="_blank"} site as an example. The reason to do this: I learned about the API some time ago from one of their youtube tutorials. 

## The user site

Wanna check out a user? Simply browse to [here](https://api.github.com/users/hak5){:target="_blank"}:

    https://api.github.com/users/hak5

You can already see the structure, e.g., if you replace `hak5` with some other username, you'll get their API interface site. Fun thing, you can directly see the e-mail address that they have given on their site. This can give you a really fast way to check if an account has a public e-mail address on their github page. 

## `api.github.com/...` json entries

You can also see some json entries that look someting like this:

    https://api.github.com/users/hak5/repos

These entries are links to other pages on the github API site. Click around and browse.

## The repos site

Fine, you can get json tables for stuff that you can also see directly and easily on the user profile page. Cool...

The repo site is more interesting however. For example, browse to [here](https://api.github.com/repos/hak5/bashbunny-payloads){:target="_blank"}:

    https://api.github.com/repos/hak5/bashbunny-payloads

This gives you an overview of a given repo, in this case from the `hak5` user, the `bashbunny-payloads` repository. This is also great but you can also directly browse to [see the commits](https://api.github.com/repos/hak5/bashbunny-payloads/commits){:target="_blank"}:

    https://api.github.com/repos/hak5/bashbunny-payloads/commits

At first, this looks fairly boring. However, with a more detailed look you can learn a lot on how a repo is set up. 

* Every commit gets a different number, go ahead open a commit.
* In the commit section you can see the user, i.e., who commited to the repo. This can give you a clue on who it is! This is also the reason for the above described pitfall. If you follow the instructions above and keep your secondary github repository private, you can still screw up your privacy if you don't change the global username of the commit.

## The overview - where to find more

If you like to find out more about the API, go to its start site: [https://api.github.com/](https://api.github.com/){:target="_blank"}

A decent overview on keys is given here and you can follow other fields, such as followers, etc. through, which I have not gone into detail here. 

You can also go ahead to write your own script to look for data on github using the API, this is kind of what it's made for. Have a look, play around!

-k0dk0d
 