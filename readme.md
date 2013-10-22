kali-updater

Script to make Kali feel more like home.

WARNING: Will not install flash or nessus on Kali 32-bit x86 or ARM platforms. sorry charlie.

What does Kali Updater do?

Updater is a script specifically for Kali Linux that performs the following tasks:

.5: checks to see if you're root. If you're running on Kali, you should be, but still, it's a simple sanity check since everything done here typically requires root permission anyhow.

    Generates new ssh host keys for your Kali installation, starts the ssh daemon and makes it start on boot -- this was something that was somewhat of an annoyance to me. Kali has every other service and capability known to man on it, but doesn't have sshd started by default. Well, I fixed that.

    Adds the Kali Linux bleeding edge repository -- There isn't that much to say that hasn't already been said here. Basically there are certain tools that update frequently that were included by default with Kali. The bleeding edge repo was Kali's answer to those tools. Right now, the bleeding repo only has a small subset of tools, but dammit I want the latest and greatest, so I added the bleeding repo to Kali's /etc/apt/sources.lst

    The almightt apt-get update and apt-get -y upgrade (dist-upgrade) -- What would an update script be without apt-get update and upgrade? Just to give you fair warning: make sure you have ample time when running this script. This is the longest portion of the script. Why? Default Kali install pulls 400+ packages of varying size (some over 100+mb), then has to install all that. Took me an average of an hour or so to pull all the packages and install them.

You might wonder, why the hell would I choose to use dist-upgrade as opposed to just upgrade? I noticed when I ran the updates initially there was a number of packages that were "held back". Doing my homework, held back packages can be force updated via dist-upgrade when updating packages. I don't see a reason to hold back security tool packages, so I opted for the simplest way to fix it.

    Msfupdate -- So you've updated your OS installation core tools and bleeding edge tools, what next? Kali's heart is metasploit. So msfupdate seemed logical to me. Takes a moment or two, but not nearly as drawn out as the apt-get package pull and the benefits are definitely noticable if you have any tasks where you'll be using or relying on the framework.

    If you have the flash installer package for linux (.tar.gz) and/or the Nessus .deb package (with a home or professional feed provided to the script), they are automatically installed -- drop the adobe flash player for linux tarball package in the root ("/") directory and/or the nessus installer package in the root (again, "/") and provide the shell script with a home or professional feed key, and the script will auto install both.

To have the script automatically register nessus with a home or professional key, remove the comment symbol ("#" from lines 168 to 172. put your nessus home or professional key after the equal sign on line 168 (the line should look like nessus_key=xxxx-xxxx-xxxx-xxxx-xxxx where the x's are your actual product key, dashes and all.

Some of the more security conscious saw flash player and probably freaked out, but flash is required for a wide variety of web consoles (nessus included), so I included the option of installing it if the script detects you downloaded it and have it in the right place. If you don't want it installed, just don't download flash. That simple.

    Couple of minor customizations -- As a part of the updater, some packages that I found to be missing on a deafault Kali install I configured apt-get to install:

armitage -- The popular graphical front-end to the metasploit framework by Raphael Mudge of Strategic Cyber. Also installs the teamserver (armitage collaboration) program. Was very surprised this was not installed by default.

mimikatz -- a popular program for dumping plaintext passwords -- basically if a user is logged in, lsass stores a plaintext copy of that user's password within lsass' memory space in memory. mimikatz can dump it and reveal the passwords stored.

terminator - a terminal emulator program that supports tabbed terminal sessions and also has a unique feature that allows you to split your terminal screen vertically and horizontally as many times as you want. For those with an OSX background, think of this as the Linux version of iterm/iterm2

unicornscan - a leightweight asynchronous network scanner. Doesn't have all the fancy bells and whistles of nmap, but sometimes all you want is a list of open ports. unicornscan does this fast and it does it well.

zenmap - the graphical front-end to the ever popular nmap scanner. Was also very surprised that this was not installed by default as well.

    A collection of scripts and tools from other CTF veterans and pentesters alike who were willing to share their armaments, including:

    The github collection of Cortana .cna scripts for automated red-teaming and post-exploitation. Cortana is touted as a "Red team force multiplier". Translated from cyber-ese, Cortana is a bot platform for armitage. Basically you provide scripts to Cortana and they can do things ranging from updating functionality in Armitage and allowing you to do new things to, automated scanning, to automatically throwing exploits at new targets seen on the network that have certain points open and/or listening services to post-exploitation modules to maintain persistence to hard-won hosts. If you're familiar with the sleep language, (The strange perl dialect that much of Armitage is written in along with java) then you can write your own, or simply modify the pre-existing scripts to suite your needs.

    Unsploitable tools: Unsploitable is a collection of tools/scripts that when you feed them the results of a nessus scan will tell you what exact patch will fix the vulnerabilities listed. Good for situations where you have to perform triage quickly.

    Defense Tools for the Blind (DTFTB): a set of scripts for unix systems that sort of allow you to ghetto rig security for unix systems and kinda triage the system/provide emergency defensive countermeasures for when you don't have the time or resources to fully patch out your vulnerabilities. For example, one script is a while true that scans ps output for /bin/sh or nc or netcat and kills the associated processes, killing post-exploit shells and simple backdoors.

4.New custom build of smbexec by Brav0hax. Basically this is a copy of the smbexec functionality found in metasploit re-written to get around some security products catching metasploit smbexec and flagging it as a non-legitimate service installation.

That's it. Lot of simple things, that make Kali that much more awesome and makes it that much easier for you to gear up for that CTF or pentest.

As with the autosnort scripts, the script tells you what it's doing and gives you success or failure indicators. If there's a failure the script bails.

The script logs the entirety of output for each of the installation steps to a dedicated log file in /var/log named kali_updater.log

If you're looking for a challenge, troll through it, figure out what failed, fix it, contact me, tell me my script is broken and how you fixed it. If you're lazy or not looking for a challenge, tell me my script is broken and ship me a copy of the updater log. 