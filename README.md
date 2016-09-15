# Collection of shell scripts for Wicked Cool Shell Scripts, 2nd Edition
Full shell scripts for the second edition of Wicked Cool Shell Scripts

https://www.nostarch.com/wicked2

How to use
----

Sourcing the ```wcss_shell.sh``` script will set up your bash environment so that the scripts are callable from the PATH instead of needing to be called relatively or absolutely.

Chapters and layout
---

**Chapter 0: Crash Course**

This chapter focuses on bringing a novice command line user up to speed regarding what shell scripts are, how to build them, and why they are useful.


**Chapter 1: The Missing Code Library**

Programming languages in the Unix environment, particularly C, Perl, or Python have extensive libraries of useful functions and utilities to validate number formats, calculate date offsets, and perform many more useful tasks. When working with the shell, we’re left much more on our own, so this first chapter focuses on various tools and hacks to make shell scripts more friendly, both throughout the book and within our own scripts. I’ve included various input validation functions, a simple but powerful scriptable front-end to bc, a tool for quickly adding commas to improve the presentation of very large numbers, a technique for sidestepping Unixes that don’t support the helpful -n flag to echo, and an include script for using ANSI color sequences in scripts.


**Chapter 2 and Chapter 3: Improving Commands and Creating Utilities**

These two chapters feature new commands that extend and expand Unix in various helpful ways. Indeed, one wonderful aspect of Unix is that it’s always growing and evolving, as can be seen with the proliferation of command shells such as ksh and zsh and alternatives to bash. I’m just as guilty of aiding this evolution as the next hacker, so this pair of chapters offers scripts that implement a friendly interactive calculator, an unremove facility, two different reminder/event-tracking systems, a re-implementation of the locate command, a useful front-end for checking spelling, a multi-timezone date command, and a new version of ls that increases the usefulness of the directory listings.


**Chapter 4: Tweaking Unix**

This may be heresy, but there are aspects of Unix that seem broken, even after decades of development. If you move between different flavors of Unix, particularly between open-source Linux distributions and commercial Unixes such as OS X, Solaris, or Red Hat, you are aware of missing flags, missing commands, inconsistent commands, and similar issues. Therefore, this chapter includes both rewrites and front-ends to Unix commands to make them a bit more friendly or more consistent with other Unixes. Scripts includes a method of adding GNU-style full-word command flags to non-GNU commands and a couple of smart scripts to make working with various file-compression utilities considerably easier.


**Chapter 5 and Chapter 6: System Administration Tools**

If you’ve picked up this book, chances are that you have both administrative access and administrative responsibility on one or more Unix systems, even if it’s just a personal Ubuntu or BSD box. These two chapters offer quite a few scripts to improve your life as an admin, including disk usage, analysis tools, a disk quota system that automatically emails users who are over their allotted quota, a tool that summarizes which services are enabled regardless of whether you use inetd or xinetd, a killall reimplementation, a crontab validator, a log file rotation tool, and a couple of backup utilities.


**Chapter 7: Web and Internet Users**

The internet is ubiquitous in this day and age. This chapter includes a bunch of really cool shell script hacks that show how the Unix command line can offer some wonderful and quite simple methods of working with resources on the internet, including a tool for extracting URLs from any web page. A weather tracker, a movie database search tool, a stock portfolio tracker, and a change tracker for a website with automatic email notification when changes appear.


**Chapter 8: Webmaster Hacks**

The other side of the web coin, of course, is when you run a website, either from your own Unix system or on a shared server elsewhere on the network. If you’re a webmaster, the scripts in this chapter offer quite interesting tools for building web pages on the fly, processing contact forms, building a web-based photo album, and even the ability to log web searches.


**Chapter 9 and Chapter 10: Web and Internet Administration**

These two chapters consider the challenges facing the administrator of an internet-facing server, including two different scripts to analyze different aspects of a web server traffic log, tools for identifying broken internal or external links across a website, a web page spell check script, and a slick Apache web password management tool that makes keeping an .htaccess file accurate a breeze. Techniques for mirroring directories and entire websites with mirroring tools are also explored.


**Chapter 11: Mac OS X Scripts**

OS X is a tremendous leap forward in the integration of Unix and an attractive, commercially successful graphical user interface. More importantly, because every OS X system includes a complete Unix hidden behind the pretty interface, there are a number of useful and educational scripts that can be written, and that’s exactly what this chapter explores. In addition to a rewrite of adduser, allowing OS X user accounts to be set up in second from the command line, scripts in this chapter explore how OS X handles email aliases, how iTunes stores its music library, and how to change the Terminal window titles and improve the useful open command.


**Chapter 12: Fun and Games**

What’s a programming book without at least a few games? This chapter integrates many of the most sophisticated techniques and ideas in the book to present three fun and challenging games. While entertaining, the code for each is also well worth studying as you read through the chapter. Of special notes are the hangman game, which shows off some smart coding techniques and shell script tricks.


**Chapter 13: Working With the Cloud**

Since the first publication of this book, the internet has taken on more and more responsibilities in our daily lives. Many of these responsibilities revolve around synchronizing devices and files with cloud services such as iCloud, Dropbox, and Google Drive. This chapter covers shell scripts enabling us to take full advantage of these services for ensuring files or directories are backed up and synchronized, as well as a couple of shell scripts showing off specific features of OS X for photos or text-to-speech.


**Chapter 14: ImageMagick and Working With Graphics Files**

Command-line applications don’t have to be limited to just text-based data or graphics. This chapter is dedicated to identifying and manipulating images from the command line using the suite of image processing tools included in the open source software ImageMagick. From identifying image types to framing and watermarking images, we write shell scripts to accomplish common image tasks, plus a few more use cases.


**Chapter 15: Days and Dates**

We deal with dates and appointments all the time, and figuring out how long between two dates, what day a given date was, or how many days until a specified date are all common problems we are faced with. In the final chapter of this book, we cover how we can accomplish solving these problem with easy-to-use shell scripts.
