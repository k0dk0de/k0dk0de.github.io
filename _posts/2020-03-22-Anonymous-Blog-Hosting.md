---
layout: post
title: https&#58;//k0dk0d.xyz&#58; Anonymous Blog and Domain Hosting
author: k0dk0d
feature-img: assets/img/posts/header_spider_web.jpg
 # color: rgb(48, 63, 80)     # Add the specified color as feature image, and change link colors in post
excerpt_separator: <!--more-->
tags: [Privacy, About]
---

**Announcing: [https://k0dk0d.xyz](https://k0dk0d.xyz)** is now up an running. In this post I use this opportunity to discuss anonymous / private web hosting and the associated risks with it. Furthermore, I present the contingency plan for this blog. 

<!--more-->

# Introduction

This is the first post in which I welcome you this website under its new domain name: [https://k0dk0d.xyz](https://k0dk0d.xyz). I would also like to take the opportunity to briefly describe how domain name registration works, what you need to keep in mind, and how you can protect your privacy when you do want your own domain name, as well as the associated risks with the presented strategy. 

Please note that I will basically discuss this website and will tell how I chose the products to keep this website anonymous. This approach is appropriate for my website, however, would likely not be the right way to get your company online. 

If you are planning on putting a website online, I would highly recommend you to listen to this episode of the "The Privacy, Security, & OSINT Show", [episode 131](https://inteltechniques.com/blog/2019/07/19/the-privacy-security-osint-show-episode-131/){:target="_blank"}, especially if you have a small business website. This episode of Michael's show discusses in detail how to protect your privacy when publishing a website. The blog post in front of you will go a lot further, but the presented strategy is also associated with some risks. You have been warned.

## Registrars, DNS, and web hosting

Every top-level domain (TLD), e.g., .xyz, .com, .org, .net, is managed by one governing authority which could be either associated with a country in the case of a country-specific TLD (e.g., .it for Italy) or could be a generic, generally non-government affiliated authority for generic TLDs. 

The end user generally registers a domain name with a so-called registrar. Registrars are companies or organizations that have the authority to sell TLDs. The domain name registration has two purposes: (1) assign the domain name to an owner and (2) to define the domain name service (DNS) for a given name. The ownership of any domain can be looked up in a whois database, e.g., via [https://www.whois.com](https://www.whois.com){:target="_blank"}. The DNS is basically a "phone book" for internet servers. The DNS entry will point your domain name to your hosting provider, i.e., the server your website is actually located at.

Finally, the hosting service represents the server where your material is stored and served as a website, i.e., the place your website, service, etc. actually lives.

## An example: [k0dk0d.xyz](https://k0dk0d.xyz)

Let's use this website as an example. Looking up the whois record shows us that the Canadian company tucows is the registrar of the domain. The registrar ensures that the domain name points to the DNS servers, which are hosted with [https://njal.la](https://njal.la){:target="_blank"}. These nameservers then point to the actual website, which is hosted on [github](https://www.github.com){:target="_blank"}.

# The privacy solution

This blog is anonymous because I do enjoy my privacy and would like to keep it that way. I can always undo this decision, however, I'll never be able to go back. With this in mind I will discuss the approach I have taken to keep this website anonymous.

## Domain registration
Regular domain name registrars require you to disclose your name. This is because you buy the ownership to the domain name and thus have the right to own it, but you are also the responsible individual for it. Simply registering a domain name in a fake name can lead to issues, because if something goes wrong or you are locked out of your domain, you will not be able to proof to the registrar that you actually own the domain and have the right to it. 

[![Njalla](/assets/img/posts/2020-03-22-Webhosting-k0dk0d/njalla.jpg)](https://njal.la){:target="_blank"}

My chosen approach for this website was thus to purchase the domain through [Njalla](https://njal.la){:target="_blank"}. They basically own the domain for you and grant you the rights to manage it. Furthermore, [Njalla](https://njal.la){:target="_blank"} requires solely an e-mail address or XMPP user name to sign up. You can and should use a unique e-mail address here to which you have access, but which does not need to come back to your name. Thus you have purchased the rights to manage the domain. [Njalla](https://njal.la){:target="_blank"} is located in Nevis and does not log any information on you. Even if they do: all they would have been able to log from me in addition to information I provided is my browser (Firefox) and my IP: a ProtonVPN IP address.

In addition to owning the domain and granting you the rights to manage it, [Njalla](https://njal.la){:target="_blank"} also serves as the DNS for this website. I can thus point these DNS entries to wherever I want. Currently they are pointing to github.

**Risk**: Of course there is some risk involved with this strategy. If Njalla goes out of business, is down, runs away with all the domain names, I have no way of fighting for the rights of my domain name. If you own a business and rely on your domain name, this is most likely not what you want, thus this strategy is not appropriate for you (see Introduction for more information). For this website this might be a hassle, but then again, if somebody ever reads this, they probably also read the contingency plan in place at the end of this blog post.

## Host

The next question to consider is where to host the website or service. This can be either self-hosted, i.e., you own the server and have to do the maintenance, etc., or you can buy hosting space from a reputable company. This will allow you to run anything you like on your webserver as long as it is allowed by the host. Again, a good summary is provided for this on [Michael's podcast](https://inteltechniques.com/blog/2019/07/19/the-privacy-security-osint-show-episode-131/){:target="_blank"}

[![Octocat](/assets/img/posts/2020-03-22-Webhosting-k0dk0d/Octocat_250px.jpg)](https://www.github.com){:target="_blank"}

For this website I decided to have it hosted on [github](https://www.github.com){:target="_blank"}. This has the advantage that I don't have to deal with much security, because github does all of it. It is also very simple to host a blog on github using a jekyll template. As you can see on the bottom of this website, I'm using the [Type on Strap](https://github.com/sylhare/Type-on-Strap){:target="_blank"} template. This template is oriented towards scientists and allows you to write your site, posts, etc. in markdown. You will still be able to include the occasional LaTeX formatted equation.


The reason I decided to go this route is also because I have a full copy of my website at all times on my hard drive and in my backups. This puts me always in control of my files, i.e., if github goes down, kicks me out for some reason, etc., I can bring the website back up somewhere else. 

Github is only good for the cases in which you want a static website, i.e., no user interactions and nothing dynamic like a forum or so that is backed by a database. This might not be the ideal solution for many people, however, you should ask yourself if you really need a dynamic site. There are possibilities to hosting a discussion forum on this website too by outsourcing it to another service. I'm not doing that for multiple reasons, first and foremost, because this would put user comments, etc. under the control of somebody else / another service. I want my content, etc., to be under my control at all points. I also don't want to have a fancy website with lots of scripts in the background because it makes it vulnerable to attacks. Last but not least, if you would like to comment on something I write, feel free to [contact me](/about) via e-mail. I'm happy to have a discussion, but I'm not willing, neither do I have the time to moderate a comment section or a forum.


## E-Mail
One more question that you have to answer for yourself is if you want to be able to receive e-mails on your domain. For me, at the time of this writing, the answer is clearly no. I have no interest in taking care of an additional email address. I am providing a masked e-mail address to which you can write using the [Masqt](https://masqt.com/){:target="_blank"} service. This allows me to put a burner e-mail address on my website for you to contact me. I can answer you from this e-mail address and we can have discussion while I retain my anonymity and privacy. This is basically all I need from this e-mail address at this point. If somebody decides to troll me, no harm done, I burn the e-mail and come up with another solution.

[![Protonmail](/assets/img/posts/2020-03-22-Webhosting-k0dk0d/protonmail-logo-dark.png)](https://protonmail.com){:target="_blank"}

If I would want to be able to receive e-mails on the k0dk0d.xyz domain I would bring my domain and use it with a paid [protonmail](https://protonmail.com){:target="_blank"} account. Detailed help and instructions on how to deal with bringing in custom domains are published [here](https://protonmail.com/support/){:target="_blank"} on the protonmail support page.


## Backups
No matter what you choose, make sure you have a copy of the database, your website, etc. at all times in your possession. If your webhost kicks you out for some reason, you will be able to bring your website back online. Again, if you haven't done so by now, listen to [Michael's podcast](https://inteltechniques.com/blog/2019/07/19/the-privacy-security-osint-show-episode-131/){:target="_blank"} on why this was important for his site.

Since this blog runs on github my solution is very simply: I just have the git repository also on my computer which automatically backs up to my backup system so everything is saved multiple times.

# The sustainability of this website

I mentioned a few times the reason why I chose [Njalla](https://njal.la){:target="_blank"}. I also mentioned that they officially own my domain and that I simply pay to be able to manage it and, if I choose to do so, move it away from them. My website is not associated with any business and the domain name is just a thing I thought would be cool. If for any reason Njalla goes belly up, their servers go down, they are taken over by the government, etc., my domain will probably be lost as well. At that point, I'm gonna loose at most 15€, which is the amount I pay for the domain per year. Oh well... 

However, loosing control of the domain would be another issue. Since I don't have e-mail address with my domain name, receiving information won't be an issue. Furthermore since I do use github to host this site it also has a github address under which you can reach it. This github address is:  
[https://k0dk0de.github.io](https://k0dk0de.github.io)  
In case k0dk0d.xyz goes down, you will always be able to reach this website on the github host directly.

This contingency plan is also expressed in the [about](/about) section of the website, so you can always find the latest update there in case something happens. 

In case github kicks me out, I will simply be able to put my website on another hosting provider and point my DNS entries that Njalla is hosting there. This should be easy enough. In this case I would also update the contingency plan on the [about](/about) page. 

What happens if github and Njalla kick me out simultaneously: tough luck. I guess that's the risk one has to take for staying fully private and anonymous. I don't expect this to happen though since there's nothing illegal on this website or its domain. Keeping a low profile should surely help. 

Stay private!  
-k0dk0d
