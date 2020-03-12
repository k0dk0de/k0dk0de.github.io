---
layout: post
title: Software for Scientists
author: k0dk0d
 # feature-img: assets/img/posts/header_electronics_rpi-cut.jpg
 # feature-img: assets/img/posts/header_security_padlock-cut.jpg
 # feature-img: assets/img/posts/header_privacy_cameras-cut.jpg
 # feature-img: assets/img/posts/header_colors-cut.jpg
feature-img: assets/img/posts/header_computer_code.jpg
 # color: rgb(48, 63, 80)     # Add the specified color as feature image, and change link colors in post
excerpt_separator: <!--more-->
tags: [Science, Software, Linux]
---

Many scientists need to create plots, edit images, write papers, etc. on a regular basis. All these tasks require dedicated software. Many colleagues spend thousands and thousands of dollars / euros / ... on such programs, however, for many specialized applications, very suitable open source alternatives exists. Here I discuss my preferred tools to get the job done.

<!--more-->

Most software that I am listing here is free to use and available as open source. There are some exceptions to this rule, and these are pointed out below. I am very much in favor of open source software and an open and honest statement on privacy and a company's business model.

Since I work cross platform most of the mentioned tools are available for Linux, OSX, and Windows. 

If you use great open source software or have some better alternatives you'd like to propose, **I would love to hear from you!**. You can find my contact information [here](/about).


# The Gist

Basically, the straight up link collection without explanations or anything. More information below. Non-free software is marked with an asterisk.

* [File manager: fman*](https://fman.io){:target="_blank"}
* [Image editing for scientists: ImageJ](https://imagej.net/){:target="_blank"}
* [Image editing - photoshop alternative: GIMP](https://gimp.org){:target="_blank"}
* [Image editing - vector graphics: Inkscape](https://inkscape.org){:target="_blank"}
* [PDF annotations: PDF Studio*](https://www.qoppa.com/){:target="_blank"}
* [PDF stitching, cutting: pdftk](https://www.pdflabs.com){:target="_blank"}
* [Plotting with a graphical user interface: Veusz](https://veusz.github.io){:target="_blank"}
* [Python editor: PyCharm](https://www.jetbrains.com/pycharm/){:target="_blank"}
* [Python environment: yt-project](https://yt-project.org){:target="_blank"}
* [Python & PyQt builder for compiled software: fbs](https://build-system.fman.io/){:target="_blank"}
* [Python plotting: matplotlib](https://matplotlib.org/){:target="_blank"}
* [Synchronization of files: FreeFileSync](https://freefilesync.org/){:target="_blank"}
* [Writing LaTeX: TeXStudio](https://www.texstudio.org){:target="_blank"}
* [Writing Markdown: Ghostwriter](https://wereturtle.github.io/ghostwriter/){:target="_blank"}
* [Writing Notes: Standard Notes](https://standardnotes.org/){:target="_blank"}


# Jump to...
* TOC
{:toc}



# Backup & File management
## FreeFileSync
Everybody needs a backup! [FreeFileSync](https://freefilesync.org/){:target="_blank"} makes it easy to synchronize your files to external hard drives, USB sticks, etc. This is not the same as having an incremental backup, i.e., a backup that lets you go in time and keeps different version of the same file. However, if you want to sync hard drives between each other, e.g., to carry files between a laptop and a desktop, and you don't feel comftable using straight up rsync from the terminal, FreeFileSync is perfect for you. It is also amazingly fast and can save synchronization profiles, so synchronizing your files becomes easy and convenient.

![FreeFileSync](https://freefilesync.org/images/screenshots/openSUSE.png)

## fman
[fman](https://fman.io){:target="_blank"} is a dual-pane file manager that is ideal for navigating and moving files around. Many keyboard shortcuts make your life easier. Furthermore, fman has a very powerful plugin API and these plugins are written in python. 

![fman screenshot](https://fman.io/static/public/img/screenshot-small.png)

Note that fman is not open source / freeware. It costs €18, which includes updates for the first year. Updates in following years (a subscription) will cost €12/yr. This seems like a fair price for a program that has so many capabilities. Furthermore, fman's creator promises that if he stops developing the file manager, he will put the code as open source on github, which would allow the community to keep on developing it / fixing bugs. Have a look [here](https://fman.io/blog/){:target="_blank"}; in the section "fman's Open Source Promise" it is stated that:
>If no commit is made to fman in more than 6 months, then it will be open sourced under a BSD license. 

# Image Editing
## ImageJ
Every scientist dealing with images (not plots, see separate plotting category below) probably knows about [ImageJ](https://imagej.net/){:target="_blank"} and if you use it you likely develop a love-hate relationship with it. Originally developed with support of the National Institute of Health and the National Science Foundation (both USA), ImageJ is a complete suite of image analysis and editing software suite. It is completely free and if you download the FIJI version (Fiji Is Just ImageJ), it comes preloaded with tons of plugins. Want to do particle tracking? There's a plugin. Need to stitch images together, there's a plugin. The best thing, most of these plugins and features come with their algorithms and instructions published in peer-reviewed articles thus making it possible to cite them. 

Very powerful and worth mentioning is ImageJ's macro language. The macro editor has an integrated help feature that supports you in writing macros. Furthermore, you can also "record a macro", meaning that you click and run and the macro editor is filled with the text commands. This can be very helpful in guiding you in creating some small automation in your image processing routines.

All in all, ImageJ has many features that are useful and is mostly used in the biological sciences for microscopy image analyses. However, it can surely be used for other applications too. 



## Inkscape
[Inkscape](https://inkscape.org){:target="_blank"} is a vector graphics editor. It is generally compared to Adobe Illustrator, however, it's not as bloated and comes at a much better prize - it's open source and free.

![Inkscape screenshot](https://media.inkscape.org/media/resources/file/Voronoi-and-dulaney.png)

You have a pdf that you need to extract an image from: use Inkscape. Want to make a figure that will never look pixelated / a flow chart / a schematic diagram? use Inkscape. Generally, whenever you need a program that can deal with vector graphics (and can handle / import / place regular pixel graphics as well) Inkscape is the right tool to use. 

The Inkscape standard format is `svg`: scalable vector graphics. Some of the best features of Inkscape are its powerful export machine, which makes it easy to transform images into vector pdfs or pixelated graphics of any size and resolution you want. An additional benefit is that there is directly a LaTeX to vector graphics plugin if you need to add an equation to annotate your figure. 

## GIMP
As Inkscape can be compared to Illustrator, [GIMP](https://gimp.org){:target="_blank"} is the analog to Photoshop. I wanted to mention it here for completeness, however, I do not use GIMP very frequently. However, whenever I have a pixelated graphic to edit / change something in, GIMP is there and can usually get the job done. It will generally take me a while, which however solely attests to my ignorance and not at all to the software.

A nice thing about open source software, not just with GIMP: There are lots and lots of tutorials and instructions online. Don't be afraid to [do a web search](https://www.duckduckgo.com){:target="_blank"} to find out what you need to know.


# PDF
## pdftk
[pdftk](https://www.pdflabs.com){:target="_blank"} is a very simple command line tool that can be used to arrange, re-arrange, merge, split, ... pdf files. The command line tool is free and runs on Linux and OSX, I have not had any experience with the Windows version. The nice thing about pdftk is that it is very simple and straightforward. You can find some help online on how to put two pdfs together, etc. The program is fairly fast. To merge two pdfs (which is what I do most of the time with it):

    pdftk pdf1.pdf pdf2.pdf cat output output.pdf

Interesting here: since pdftk is a command line tool, feel free to script your way around stiching together more complex documents and to interface pdftk from your preferred programming language.


## PDF Studio
[PDF Studio*](https://www.qoppa.com/){:target="_blank"} is a bit of an outlier in this whole list. There is a free version (PDF Studio Viewer; see discussion at the end of this section). The full version is fairly expensive at $89 for the standard edition and $129 for the professional version. This purchase will get you updates to the current major version, i.e., if you purchase today, you will get all the updates for the 2019 version. The version numbering seems to be a lot like last year and a new version might come out soon.
If you are working in academia there is a 50% discount to this price, and a 25% discount if you work for a non-profit organization. This makes the price a bit more reasonable.

I was thinking and rethinking for a while if I want to mention PDF Studio at all or just leave it out. However, annotating pdf files is an absolute key capability for every scientist - you will need to correct what your colleagues wrote here and there, send comments on things back, etc. While Adobe Acrobat seems to be the default, it is (like every Adobe product), very expensive and bloated. Also, it does not exist for Linux, neither Adobe Acrobat, nor the Adobe Acrobat Reader. This is a major downside for me. PDF Studio Viewer, Standard, and Professional are truly cross platform and work excellently on all operating systems.

Unfortunately, I have not found any open source solution that comes even close to what Adobe Acrobat can do and that is cross-platform. My requirements for a pdf editor are:
 * Annotate with notes, edits, deletions, insertions, typewriter, such that these annotations compatible with Acrobat
 * Have a list with check marks of all the annotations in a given file
 * Filter capability for annotations by author, checked / unchecked, ... 
 * Fill in forms and save them properly
In addition what I like to see for a pdf editor, but is not crucial:
 * Capability to actually redact information properly
 * Sign documents electronically
 
PDF Studio allows you to test there software for free. They will add a big mark at the top when you save that file that you have used a testing version. That's annoying (which is surely the point), however, really let's you test the functionality. 

Finally, PDF Studio also has [free viewer](https://www.qoppa.com/pdfstudioviewer/download/){:target="_blank"}. This program is analogous to the Adobe Acrobat Reader and basically has all my must have features already included. Especially if you are on Linux, PDF Studio Viewer is the way to go. 

In conclusion: Sure, it will cost you a little bit of money if you want the professional edition. If you need the capability the program is worth it however. Give the free [PDF Studio Viewer](https://www.qoppa.com/pdfstudioviewer/download/){:target="_blank"} a try and have a look at the [comparison chart](https://www.qoppa.com/pdfstudioviewer/){:target="_blank"} on what the individual versions can do.

If you know of an open source / different product that is cross-platfrom and has the discussed features, please [let me know](/about). I'd be more than happy to test it out and maybe even write about it.

# Plotting
## Veusz
A plotting program that is open source, cross-platform compatible is something that I couldn't find for the longest time. I first used Origin, then Igor, looked at ProFit and tested it out... These were all not cross-platform, not open source, and expensive solutions. Finally, I discovered [Veusz](https://veusz.github.io){:target="_blank"} and have used it ever since.

When you first start Veusz you get an interactive help menu with a quick tour. Please look through it, it helps with navigating everything. I noticed very quickly, Veusz is written by a scientist who knows a lot about writing software - it was exactly the way I was thinking as well :) Thus, it immediately felt very intuitive with widgets, etc. It's obviously written in PyQt and even uses some of the same language that you know if you ever wrote software within the Qt framework. But I'm nerding out here...

Veusz also comes with a very sweet collection of examples. Go to `Help` -> `Example documents` and you see a whole list of plots that are examples. You can also check out the examples [here on the website](https://veusz.github.io/examples/){:target="_blank"}. Here's the first example from that page:

![Veusz Spectral Analysis](https://veusz.github.io/examples/spectrum.png)

Most features you need come pre-loaded. You can also directly use LaTeX commands in all annotations and labels and even make [3d plots](https://veusz.github.io/examples3d/){:target="_blank"} right off the bat. 

One of my favorite features is that Veusz does not come with a very convenient data editor. However, it allows you to link the data files directly as a data source. For example: You have your data in a comma separated text file, you can now load the data into a Veusz plotting file and plot them. You want to update the data interactively: Just use LibreCalc or Excel to edit the file, save it, go to the Veusz data list and update from the data from the source. You're all set and once you're used to this workflow you won't miss the interactive data management feature in the plotting software itself. If your data is, e.g., from a model run and you have updated values you can just hit update as well! This is very powerful and helps you to not copy data between different programs. One more advantage of Veusz over other software: the `vsz` files that are saved by the program can be read by a regular text editor! So if you ever have an issue with data files that cannot be found, you can always go into the text file and update the paths.

There's also a suite of tutorials and help files [online](https://veusz.github.io/help-support/){:target="_blank"} to get you started.

One caveat: If you are used to a very expensive program, e.g., Igor, don't expect Veusz to contain all the fitting routines and special filtering methods, etc. Veusz comes with basic fitting, sure. These are perfectly fine enough if you just need a black box for fitting. In that case you probably don't care what routines are used anyway. If you need more, you might have to implement it yourself, find another way to get the job done, e.g., in python and matplotlib.

## matplotlib
[Matplotlib](https://matplotlib.org/){:target="_blank"}, a module for python, is the ideal tool to plot if you want to write a script in order to make your figure. Highly customizable, matplotlib will make your plot look gorgeous. This is especially useful when you have a suite of simulations or need to make the same plot over and over again for various data sets. Sure, it will take longer to make one individual plot, however, it can be really time efficient once you have to do a certain figure over and over again.

If you're programming in python, you most likely know matplotlib anyway, so I'm keeping this short. If you really don't or you don't use it often enough to be fluent, have a look at their [tutorials page](https://matplotlib.org/tutorials/index.html){:target="_blank"} and use their [search function](https://matplotlib.org/search.html?q=){:target="_blank"}. All the examples come with well commented code that you can download and try out for yourself in order to understand what it does. This is extremely helpful when making your own figure. And matplotlib figures really look great if you put a bit of effort in.

Fun fact: The logo for matplotlib is actually created in matplotlib. The code to make the logo can be found [here](https://matplotlib.org/gallery/misc/logos2.html?highlight=logo){:target="_blank"}. This gives you some demonstration on how powerful it can actually be.

![Matplotlib logo](https://matplotlib.org/_images/sphx_glr_logos2_003.png)


# Programming
I personally use python for pretty much everything I do. This programming section thus only contains tools to work with python. This is not intended to be a comprehensive list, but rather shows my favorites.

## PyCharm
If you have programmed in python for a while [PyCharm](https://www.jetbrains.com/pycharm/){:target="_blank"} is the IDE for you. The community version is fully free and comes with most tools that you want. The one thing I wish was free in the community version is to edit code remotely via ssh, however, if you want this feature you'll need to upgrade to the professional version. The pro version costs $199/yr for the first year, $159/yr for the second year, and $119/yr for all subsequent years. Honestly, in years and years of programming, I only wished a handful of times that I had the pro version. The community edition generally gives me plenty of features. There is a free trial for the professional version if you want to go that route. The following description is based on the community version.

![PyCharm](https://www.jetbrains.com/pycharm/img/screenshots/complexLook@2x.jpg)

PyCharm comes with full git and svn support. You can directly commit to github from PyCharm if you feel like doing so, however, it color codes the files that have been changed / are new since the last push / pull. You can also directly do a comparison of different versions, which sometimes is very handy.

Command completion can be very powerful. Furthermore, you can manage your virtual environments (or your environment) directly from the editor. This can be useful, especially if you write a `requirements.txt` file for your project and run it on a different / new computer. PyCharm will read this file and will help you to install all the requirements.

Shortcuts to run your software can be created and you can decide what you want to run where and have a menu with shortcuts to directly start it up. The editor also has a linter that helps you to keep your code neat and tidy, according to the python PEP8 formatting guidelines. 

PyCharm comes with many more features, such as a refractor, safe delete to check for cross-dependencies, etc. If you're new to programming, this might **not** be the editor for you, because the amount of features probably overwhelm you. However, if you're a seasoned python coder give PyCharm a try.

## yt-project
The python installation manager you use is completely up to you. I honestly use several different installations, from straight up python and installing everything by hand for very clean projects, to using anaconda, which I generally recommend to students who want to start coding python and come from a windows environment. You can also use miniconda, especially on a Linux or OSX operating system.

**Whatever you do, do not use your system's provided python installation!** This cannot be overstated. OSX comes preloaded with some weird Apple python, you'll just start getting many many problems if you use this out of the box.

A nice in between version between anaconda and installing everything from scratch is the [yt-project](https://yt-project.org){:target="_blank"}. This is basically a conda environment that is built for *analyses of volumentric data* - whatever that means. yt is installed via bash script that allows you to specify individual modules that should be standard for science. So all together, a neat packaged script to install your python environment. Check it out, you'll notice that yt loves you!

## fbs
One of the major downsides of python can be the fact that it is fairly difficult to compile your software. Let's say you wrote a GUI and want to give it to your colleague who does not use python: You will need to install a python environment, all the required packages, etc., or go through the long and weary process of finding out how to compile the software yourself. 

[fbs](https://build-system.fman.io/){:target="_blank"}, which stands for "fman build system" (see entry for fman above) is written by Michael Hermann. He states that he wrote fbs in order to facilitate what I just mentioned: easy compilation and distribution of python. fbs is open source and free to use and distribute if you write open source software with it. Otherwise, you'll need to pay a developer's license (see the website for more information). 

fbs very much facilitates writing code and GUI in python and PyQt and then build and deploy it. Have a look at the [tutorial on github](https://github.com/mherrmann/fbs-tutorial){:target="_blank"} to see some of fbs' power. Once you get into it, you will need to also read the [manual](https://build-system.fman.io/manual/){:target="_blank"} and might want to have a preventative look at the [troubleshooting section](https://build-system.fman.io/troubleshooting){:target="_blank"}.

One of the most common problems that you can run into with fbs is that you do not have the correct dependencies installed. It is crucial that you use the correct dependencies, or you might get weird compilation errors. The best way to work with specific dependencies is to use a virtual environment for each specific project. **Do not** use your standard python installation with all its packages, you will run into issues this way! Also, if you work on Windows, have a look at the additional software that is required in order to use fbs.

Finally: If you have dealt with python for a while but have not written a GUI application (but want to start doing so), [Michael's book](https://build-system.fman.io/pyqt5-book){:target="_blank"} could get you started. It costs €29.95 and is well worth the money. You'll get a DRM free pdf immediately and can start enjoying it. The book is very well written and gives you a great start into GUI programming with Python and PyQt. Together with fbs, you'll deploy compiled GUIs written in python that your colleagues can use in no time!


# Writing
## Ghostwriter
[Ghostwriter](https://wereturtle.github.io/ghostwriter/){:target="_blank"} is a very well designed open source editor for writing in markdown. This blog post is actually written and edited in ghostwriter. 

![Ghostwriter](https://wereturtle.github.io/ghostwriter/images/dark-theme-thumnail.png)

Ghostwriter has overlays that give you a markdown cheat sheet (who can remember all the things?), a table of contents, and stats of your document. It has different themes that all look good, and in general is a very clean and well done editor. It also has a live preview and comes with a distraction free mode.

Ghostwriter comes with what the authors call a "Hemingway Mode", where your delete key will be rendered useless. I guess the idea is that you'll be writing and not editing - a funny idea.

Unfortunately, Ghostwriter does not come natively for OSX. However, it can be built for MacOSX, you can find the appropriate [readme file here](https://github.com/wereturtle/ghostwriter/blob/master/BUILD_MAC.md){:target="_blank"}. *Note*: I have not tried this out.

## Standard Notes
[Standard Notes](https://standardnotes.org/){:target="_blank"} is a note taking app that is cross platform and syncs between your various devices. Compared to all the other free ¨services" that are out there, the beauty of standard notes is that it is end-to-end encrypted and that only you can decrypt it (zero-knowledge provider). This means that nobody at standard notes can read your great ideas! This also means: if you loose your passwords, you have to come up with those ideas again.

![Standard Notes](https://camo.githubusercontent.com/aa8eb2f8a9497620ec1b10c80198e1d563c061bd/68747470733a2f2f7374616e646172646e6f7465732e6f72672f6173736574732f686f6d65706167652d6865726f2e706e67)

I have tested standard notes on OSX, Linux, Android, and iOS and it works great. The basic version is free, the pro version, which costs as little as $2.48/months if you subscribe for 5 years ($149 total) comes with many extensions such as advanced editors (including a LaTeX editor!), a github push functionality, and the file save function, which lets you save files fully end-to-end encrypted to an online service, e.g., dropbox, or similar. Check out the [extensions here](https://standardnotes.org/extensions){:target="_blank"}. 

This is a note taking app that respects your privacy, and respects your ideas as your own! 

Even if you don't have the extension version, standard notes also has a note taker independent service that let's you share files with your friends (up to 50 MB). Their [FileSend](https://filesend.standardnotes.org/){:target="_blank"} is free to use and end-to-end encrypted as well. Furthermore, it gives you only a limited time to keep the file around, automatically deleting it after this time span.

## TeXStudio
Finally, when it comes to writing your manuscripts, theses, books, there's only one way to write: LaTeX. If you don't agree, I hope the rest of this article was useful. I will not go into discussion on why LaTeX is my perferred choice but will rather present you with my favorite editor.

I recently found the [TeXStudio](https://www.texstudio.org){:target="_blank"} editor, which is very powerful. Sure, it could need some work on icons and theme support, but it has some very key features that I think are crucial.

The pdf preview can be decoupled from the main window and shifted to a secondary monitor. Furthermore, you can turn on / off synchronized scrolling between the preview and the source and synchronize your pointer between editor and preview (and vice verse). This is especially useful when editing. 

On the left side the editor has a menu to display a current table of contents. Click on a section and the editor jumps there. This is especially helpful to navigate large documents such as proposals, books, and a theses. There's no need anymore to split your work into separate documents and use the `\include` command.

![TeXStudio](https://a.fsdn.com/con/app/proj/texstudio/screenshots/structureView.png/max/max/1)

Finally, TeXStudio comes with autocompletion and a very elaborate help menu that allows you to look for that math symbol you hardly ever use and can't remember. All in all, a powerful editor that makes your LaTeX experience so much smoother. 

This product is fully offline so there is no need to share your work with the world before its ready. For privacy reasons, I do not think that online editors that are not zero-knowledge, end-to-end encrypted should be a thing. Your files belong to you, they should be in your control, and you should be in charge of them.

Have fun with these programs and [let me know](/about) what you think and if you have additions.  
-k0dk0d
