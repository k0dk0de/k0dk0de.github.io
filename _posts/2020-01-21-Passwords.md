---
layout: post
title: Account Security - Passwords
author: k0dk0d
 # feature-img: assets/img/posts/header_electronics_rpi-cut.jpg
feature-img: assets/img/posts/header_security_padlock-cut.jpg
 # feature-img: assets/img/posts/header_privacy_cameras-cut.jpg
 # color: rgb(48, 63, 80)     # Add the specified color as feature image, and change link colors in post
excerpt_separator: <!--more-->
tags: [Basics, Security]
---



Fitting for the start of this blog and still almost the start of the year, I want to discuss passwords and account security. I will discuss topics such as: How to choose passwords? How many passwords do you have to remember? How do you store your passwords? Why should you do things this way?

<!--more-->

This article is intended to give you some basic best practices on how to keep your accounts secure. Account security is not complicated but requires a little bit of time to set up. How much depends heavily on how many steps you have already completed. In the end you will save time when following these best practices and stay more secure!

# The Gist

The shortest possible explanation of everything you find below without much explanation:

 * Every account requires a unique and strong password, which contains >50 characters including numbers and symbols
 * Use a password manager, it will make your life easier, more secure, and more convenient compared to whatever you have now
   * The safest password manager strategy is an offline password manager like [KeePassXC](https://keepassxc.org/){:target="_blank"}
   * The more convenient way is to have an online password manager. Choose a reputable one, examples of such are [Bitwarden](https://bitwarden.com/){:target="_blank"} or [LastPass](https://www.lastpass.com/){:target="_blank"}
   * Your password manager needs to be protected with a strong and unique password
   * You need to have a backup of your password manager
 * In addition to passwords all of your accounts should be protected with two factor authentication (2FA)
   * The best way to do 2FA is with a hardware token, such as a [Yubikey](https://www.yubico.com/){:target="_blank"}
   * If no hardware token is available / possible, use a software token
   * The least favorable 2FA method is via SMS. If necessary, do not use your cell phone number, but set SMS 2FA it up using a VOIP number, e.g., Google Voice
 * Any of your accounts is only as secure as the recovery method:
   * Use unique and random answers to security questions. Ideally generate these answers using a password generator
   * Your recovery e-mail address needs to be secure
   * Try to log into your account without credentials and find out how easy / hard it is by trying to recover your password

# Passwords

You always hear that you should use random passwords with numbers, symbols, upper, and lower case letters. Let’s see why this is true, what you need to consider, and why you should not be able to remember your passwords. Working through this post and implementing it will take some time and some getting used to. However, you will gain a lot of account security and will, once all is set up and you are used to your new workflow and tools, have more convenience as well.

The most crucial constraint for the average user of today is that you have unique and strong passwords for every account. The importance of this cannot be stressed enough! The reasons for this requirement lay in data breaches. Have you ever been in a data breach? I myself have been in multiple data breaches. One of my older e-mail addresses for example was alone part of 5 different ones. To check if you were in a data breach with one of your e-mail addresses the Australian security researcher Troy Hunt compiled a unique database of data breaches. This database is publicly searchable and allows you to check if you have been part of a data breach. Go to the following website 
[https://haveibeenpwned.com/](https://haveibeenpwned.com/){:target="_blank"}
and enter your e-mail addresses. Troy’s website will immediately search a large database of breached data to check if you were breached. If you were in a data breach ask yourself: Do you use the password for that service somewhere else? What could a hacker do if they pick your e-mail address and password and try to log into your bank, your retirement account, etc.? Also: there are surely data breaches out there that have not been included in any web databases. While you might not be a target per se, hackers have started to use data breaches and automatically test all usernames and passwords that are in such databases on other sites. This is known as credential stuffing and even if you are not a target you can become a victim if you recycle passwords. If you never recycle passwords (and ideally neither usernames, just to be even more secure), credential stuffing will not work on you.

Why a strong password? Let’s assume your password is flower and you only use it for your bank account. A hacker won’t get into your account by credential stuffing, but could still get into your account by a brute-force method, i.e., by password guessing. In this case, the password flower is a standard word in the English dictionary. If a hacker simply tries through the whole dictionary, your account would be wide open in no time. So what should you do?

Use randomly generated passwords that contain numbers, symbols, upper, and lower case letters! Let us go through how to create randomized passwords, look at how describe it in physical terms, and how to make your life safer and easier by using a password manager.

## Random Password Generators

While my actions often seem random to me, they are not really. To come up with truly random passwords you want to have software that actually truly randomizes this process. Many password managers (discussed further down) come with a random password generator. These usually let you choose multiple settings:

 * Letters
 * Numbers
 * Symbols and special characters
 * Extended ASCII characters (in some cases)
 * Length of the password

Play around with these random password generators and see how to use them and how the settings work. Generally you want to turn on as many special characters as are allowed for a given password. When it comes to length, why not choose a password that is as long as is allowed? With a password manager you won’t have to remember it anyway. Personally I started playing the game on how long of a password am I allowed to choose for a given website… some already drop out at 20 characters, some make it up to 60, some a lot more. How many characters do your services allow in a password?

## Maximizing Entropy

A detailed break down on randomized passwords, entropy, and password strength can be found on [Wikipedia](https://en.wikipedia.org/wiki/Password_strength){:target="_blank"}. Let us consider the following scenario: we choose a password of length $$k$$. If there is a total of $$N$$ symbols available to choose from, the number of possible passwords with that length are $$N^k$$. Your ATM PIN, assuming it consists of 4 out of 10 possible digits can be guessed in 10000 tries. Assuming it takes 5 seconds to test a pin for a (very dedicated) human being, your ATM PIN could be guessed by such a manual brute-force hacker in roughly 14 hours. A computer will be much faster.

It is common to give password strength in terms of information entropy, which is measured in bits. Instead of giving the number of possibilities (as calculated above), the entropy $$H$$ of a password is simply defined as:

$$H= \log_{2} \left(N^{k}\right) $$

These numbers are a bit handier to deal with. If you think about computers and binary the makes sense. In binary you have 2 possibilities per bit to guess, 1 and 0. For a password of length $$k$$, you thus have $$2^k$$ possibilities. Here, this would result in the entropy $$k$$.

A more complicating password will contain more characters and draw the characters from a larger pool. All printable ASCII characters (so most of the things on your keyboard) are 95 characters. If you have a password of 10 characters, you will have an entropy of 65.7. This means, that guesses are necessary to surely guess your password. I let you calculate the actual number.

## Password Managers

The question now poses itself: How do you remember high entropy passwords that are completely random. The answer is simple: You don’t. Fortunately there are tools that do this for you. These tools are password managers. Password managers, which often come with random password generators, safe your unique passwords in an encrypted database and make them available to you with a master password. This means that all your password will be protected by one password, and (hopefully) by a second factor authentication key.

There are two kind of password managers: online and offline password managers. Examples and recommendations are discussed below. You have to answer the question on what you want: do you want to have your passwords online and easily sync-able, however, give up some privacy / security in order to have a (hopefully reputable) company manager your passwords, or do you do everything yourself offline. I will outline both approaches below. For most people, the online password manager approach is likely the best way to go. However, if you are slightly paranoid (like myself), the offline method is for sure safer. But backups, file corruptions, etc. are all completely up to you if you go the offline way. This should not scare you however.

As so often in science, a mixture of the two methodologies - an online and and offline password manager - might be even more in the sweat spot for you!

### Online Password Managers

A reputable online password manager will have the following features:

 * It lets you log in with your master password and a second factor authentication (if set up)
 * Encrypts the password (using strong encryption) on your device prior to sending it to the storage
 * Never sees your password!
 * Provides you with plugins such that you can easily auto-fill passwords in browsers and on mobile devices

Don’t choose the latest super password manager with all bells and whistles that you have just read about on some social media post from a friend. You should choose a reputable password manager. I will discuss two online password managers. This is not meant as a comprehensive list but rather as two examples of reputable online password managers that I have tested.

*Note*: Your password manager is only as secure as your master password (and your second factor authentication). If you use your standard password that has been leaked all over the internet already along with your standard e-mail address, your security will be fairly poor. Thus, come up with a strong master password! You can write it down (in hand writing) somewhere at home until you have memorized it.

Now that the ground rules are established, let’s have a look on how you should approach password managers. Choose one, go ahead, and open a free account. Make sure you add 2 factor authentication right away in order to get that extra security layer on your account. First add one or two accounts that you use fairly frequently, but which are not extremely important. For example, add your newspaper credentials. Install the plugins for your browsers and test them out by logging into your newspaper. How easy is it? Change the password and have it stored automatically in your password manager’s vault. To come up with a new password, find the password generator and create one (don’t forget what you just learned on entropy). If you don’t like a password manager not much has gone wrong at this point. Choose another password manager and start over. Make sure that (1) you delete your account on the password manager you did not like, (2) you change the passwords that you have given to that password manager, and (3) don’t reuse the master password (you probably haven’t memorized it just yet anyway, and if you did, are you sure you choose a strong master password?).

Once you decide that a password manager suits your needs go ahead and add your important accounts. These are likely banks, financial services, and e-mail accounts. Go through every account and change your passwords. Set strong passwords that were auto-generated by the password generator of your manager. Once you have your crucial accounts added and all the passwords are set to be long, randomized, and unique, take a break: you deserved it! Form now on whenever you log into a less important account, e.g., your online shopping account, go ahead and change the password in the same way to set something unique. Ideally, everything in your life will be in your password manager soon enough. You hopefully also realized how convenient these password managers are. This means you are actually secure and don’t have to type that much anymore either - even better.

Let’s have a look at some online password managers now:

#### Bitwarden

[![Bitwarden logo](/assets/img/posts/2020-01-21-Passwords/bitwarden_logo_320px.png){:style="float: right; margin-right: 0px; margin-top: 6px; margin-left: 0px, margin-bottom: 0px"}](https://bitwarden.com/){:target="_blank"}
[Bitwarden](https://bitwarden.com/){:target="_blank"} is an online password manager with several advantages over other competitors, so if you don’t have a password manager and want to go with an online solution, this might be a good one to start with. The reasons I like bitwarden are:

 * Source code has been independently reviewed and is available open source on github
 * You can self-host your own password manager (however, you could simply go with an offline version in that case)
 * Clear business model: always free accounts are great for testing, additional features with a paid account
 * Paid account with additional features is very cheap at $10/year

For bitwarden I highly recommend a paid account. A paid account will let you add a Yubikey as your second factor authentication. This is to be preferred over a software token (see below for details). In addition you get 1GB to store files. This can be useful if you need certain documents available on the go.

#### LastPass

[![LastPass logo](/assets/img/posts/2020-01-21-Passwords/200px-LastPass_logo.png){:style="float: right; margin-right: 0px; margin-top: 6px; margin-left: 0px, margin-bottom: 0px"}](https://www.lastpass.com/){:target="_blank"}
[LastPass](https://www.lastpass.com/){:target="_blank"} is another commercially available password manager that follows the freemium model, i.e., you can create a free account which has a decent number of options, but certain options and features require an extra subscription. I have tested and used LastPass. In general, it is fairly similar to bitwarden. The features of LastPass:

 * Reputable company: Yes you’ll find information on data breaches online that talk about LastPass. Don’t let this information drive you crazy: no passwords have - as far as is known today - been compromised and the company has disclosed the data breaches in a rapid way. The questions should never be if a website get breached, but when.
 * Clear business model: Freemium

The paid / professional accounts are $36/year, which is significantly more than bitwarden. At first glance, you also get Yubikey support (so again, you want to have a paid account). This will also allow you to store files, up to a total of 1GB.

### Offline Password Managers

[![KeePassXC logo](/assets/img/posts/2020-01-21-Passwords/200px-KeePassXC.png){:style="float: right; margin-right: 0px; margin-top: 6px; margin-left: 0px, margin-bottom: 0px"}](https://keepassxc.org/){:target="_blank"}
So you’re paranoid (that’s a compliment in this context!), congratulations! The safest way to protect a file from getting stolen in a data breach is to never have it online! An offline password manager will help to exactly do this.

Here, [KeePassXC](https://keepassxc.org/){:target="_blank"} is my recommended password manager and also the one I use heavily. It comes for every operating system and you can also have browser plugins for Firefox and Chrome/Chromium/Vivaldi. Let’s be honest, if you are using an offline password manager, you are most likely using Firefox as your web browser anyway, or you don’t want the plugin feature anyway.

For two factor authentication with your Yubikey you will have to set one slot of your Yubikey up with an HMAC-SHA1 challenge response. [Here](https://www.yubico.com/products/services-software/personalization-tools/challenge-response/){:target="_blank"} is a video on how to do this. If you have never personalized your Yubikey, it should be save to configure slot 2 for the HMAC-SHA1 challenger response. Note: if you want to use the Android password manager mentioned below, make sure to select Variable input for the HMAC-SHA1 Mode, otherwise it won’t work. Once your Yubikey is written the configuration manager will ask you to save your secret into a file. Do so and store the file in a secure location. You can use the same Secret Key to program another backup Yubikey as well.

At this point you should have your KeePassXC ready to go and can go ahead and get used to it. However, even an offline password database could have its use on mobile devices. For android, use [Keepass2Android](https://github.com/PhilippC/keepass2android){:target="_blank"}. For iOS use [Strongbox](https://strongboxsafe.com/){:target="_blank"}. These two apps are the ones that are also recommended by KeePassXC.

To set up [Keepass2Android](https://github.com/PhilippC/keepass2android){:target="_blank"} with your Yubikey, you want to additionally install [ykDroid](https://play.google.com/store/apps/details?id=net.pp3345.ykdroid&hl=en_US){:target="_blank"}. This app exposes the challenge response from your Yubikey and makes it available to other apps. KeePass2Android requires this in order to accept the challenge response for database decryption. Then load your database, select Password and Challenge Response for KeePassXC, allow the usage of ykDroid to read your challenge response, and insert or tap your Yubikey (with NFC) to respond. You should be logged in.

For [Strongbox](https://strongboxsafe.com/){:target="_blank"}, there is currently no way of using a Yubikey. This will likely change in the near future since Yubico, the maker of Yubikeys, is developing keys that will also work with iOS. However, as of this writing, you will have to manually copy the secret into Strongbox. This defeats the 2FA on this device, since you’ll need the Yubikey secret (which you stored into a file above) and type it into the app. You can find more details on the current development on the [Strongbox' github](https://github.com/strongbox-password-safe/Strongbox){:target="_blank"} site and in [this issue tracker](https://github.com/strongbox-password-safe/Strongbox/issues/95){:target="_blank"}.

## Backups

No matter what password manager you choose, you must have a backup of the database. This is obvious for your offline password manager but should also be done if you go the online route: What happens if the service suddenly goes away? What happens if the server of the company gets hacked and is offline for an extended period of time until it gets get patched?

In case of your KeePassXC it’s simple: back up your kdbx database. This is an encrypted file. In addition you want to consider to save a new version of the file every now and then and keep a manual history in case of file corruption. And furthermore, you want to have at least two backups of your database in two different locations!

For online password managers you should have an offline copy. You will only use it in case the company goes out of business, if their server gets hacked or wrecked, or if it is down for an extended period of time. For all online password managers you can export the database, usually as un-encrypted files. These files you want to store in a secure location, e.g., on an encrypted hard drive, or even better, in an encrypted [Veracrypt](https://www.veracrypt.fr/en/Home.html){:target="_blank"} container (a blog post on hard drive security will come soon). Since this password file is readable by anybody that has access to it, make sure you store it somewhere safe. Under absolutely no circumstances store it in the cloud! The cloud is not a location for unencrypted (password) files!

# Two-Factor Authentication (2FA)

Two factor authentication should be used for any account that allows it. Basically, it adds a second part to the login process, you will need something you know (your password) and something you have (a [Yubikey](https://www.yubico.com/){:target="_blank"}, phone, etc.). Here only the basics are given, a more detailed write-up on 2FA will come soon.

As with the password manager, you will need a backup of your 2FA token or the security code that can defeat it (which is usually given when you set it up). Store this code in a safe location!

## Hardware Tokens

Surely the best way to stay secure is a hardware token. These are generally devices that you can plug in via USB and that provide the second factor authentication. Yubikeys, sold by [Yubico](https://www.yubico.com/){:target="_blank"}, are some of the most widely used hardware tokens and should be part of any security plan.

If you use a hardware token you’ll need to have at least two, one for daily use and one as a backup that you keep in a secure location. If your whole family has hardware tokens (and you trust them), it is okay to share the backup key.

Have a look at the [Yubico’s website](https://www.yubico.com/){:target="_blank"}, they have a lot of step-by-step instructions on how to set up Yubikeys with various services.

## Software Tokens

Many websites don’t allow hardware tokens but can be setup to use 2FA with software tokens by using an authenticator app (such as, e.g., [Authy](https://authy.com/){:target="_blank"}). These software tokens can also be stored on Yubikeys, instructions can be found [here](https://www.yubico.com/products/services-software/download/yubico-authenticator/){:target="_blank"}.

## SMS 2FA

The least secure two factor authentication is SMS 2FA (see the section on security risks below). If there is absolutely no other way to get 2FA going, SMS should be used - it’s better than not having 2FA. If you need to make use of SMS 2FA make sure you DO NOT use your cell phone number. Use a VOIP number instead (e.g., Google Voice) that, e.g., forwards all incoming text messages to a secure e-mail address. Otherwise, you will be a potential target for a SIM swapping attack.

# Security Risks

No system is perfect, but if you follow the outlined tactics, you will have made yourself a harder target than most and should be safe from broad attacks that use credential stuffing, etc. If a hacker or nation state actor targets you specifically the basic steps lined out here are probably not going to cut it!

## SMS 2FA and its issues

As mentioned above, SMS 2FA should only be used if no other way to setup 2FA is available. The issue here is that it has become very easy, especially in the US, to do SIM swapping attacks. A detailed article can be found [here](https://www.vice.com/en_us/article/5984zn/listen-to-sim-jacking-account-ransom-instagram-email-tmobile){:target="_blank"} on Motherboard’s website. Basically, in a SIM swapping attack an attacker calls up the phone company and pretends to be you. The hacker will claim that you lost your phone and has your phone number ported to a new SIM card, which is in the hackers possession. You will loose your network at this point, however, by the time you have notified the phone company the hacker will likely already have used your phone number to reset accounts and receive 2FA authentication codes. Therefore, it is recommended that you use a VOIP number in order to setup 2FA. Google has fairly good account security. With a strong password and Yubikey U2F authentication, your google voice number will be fairly secure from any attacks, for sure much better than your actual SIM phone number.

## Open Source Intelligence Gathering and Security Questions

Another thing to consider is the following: Not only your passwords can get leaked, but also the answers to your security questions. Ask yourself: can you reset an account and 2FA by simply answering the questions “What was your first car” and “What’s the name of your first pet”? Also: ask yourself if you actually posted a photo of you and your first car on Facebook or tweeted an RIP statement about your first pet? Your questions could easily be out there. Security questions should always be answered with random characters that are generated by your password manager and should be stored in a secure location, e.g., your password manager. Since you have appropriate backups in place now there are not any good reasons to remember the answer to these questions anyway!

## Account recovery

Finally, another word of caution: What happens if you actually loose your password. You won’t do this, of course, but ask yourself: How easy would it be for a hacker to reset the password? Can your password be reset? It is worth, especially for your valuable account, to test how you would get into them. Do you have weak security questions / answers pairs set up? Is your password super long and you use a Yubikey with U2F but the password can be reset via your old hotmail e-mail address that uses the password flower, which has been in 17 data breaches? You get my point: your account is only as secure as the possibility to reset it. Test how you would get into your own account and make it more secure by randomizing security questions, and by using unique usernames, unique e-mail addresses, etc. If your bank gets breached, you are likely going to experience some inconvenience but your money should be insured. If your account gets breached because you are not using appropriate safety measures this could be different.

Stay safe!  
-k0dk0d

