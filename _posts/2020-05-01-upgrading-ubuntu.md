---
layout: post
title: "Upgrading Ubuntu to 20.04 LTS"
tags: tech
---


<center> <img src = "https://ubuntucommunity.s3.dualstack.us-east-2.amazonaws.com/optimized/2X/0/0921cb27d5604b464218a64ae88a3f43c7b7371a_2_690x345.png"> </center>

I am very excited about the new version of Ubuntu. The beta version was released a month ago. But since it was fairly stable, 
I didn't installed it. I killed my excitement and waited for the LTS version. And finally, on April 23rd Ubuntu 20.04 LTS was
released. In this post, I'm going to share the process I used to upgrade my Ubuntu from 19.10 to 20.04.

Note: This is only when you are already running some ubuntu version and want to upgrade it to the new version. This is not the process for fresh installation of Ubuntu.

If you want to upgrade the Ubuntu version, you do need to download any .iso file or boot any USB drive. All you need is:
* **A good internet connection**
* **And a bit of patience**

Note: You can upgrade from either Ubuntu 18.04 or Ubuntu 19.10 to 20.04LTS. But, If you are running the 16.04 version
you will need to upgrade to 18.04 first and then to 20.04 LTS.

Another Note: Backup of important data is always required while performing a major upgrade. (But, I forgot to backup my data and luckily all the data is safe.)

This can be done using Ubuntu's built-in do release upgrade tool which is also an easy way to upgrade. But I upgraded manually by updating the sources list with 
the guidance of [Nerd on the street](https://www.youtube.com/watch?v=3nD56JYfF_o&t=1131s). The reason for upgrading manually is simply to
enjoy the essence of linux. 
<center> <img src = "https://i.redd.it/orcgyjw150c21.jpg"> </center>

Alright, here are the steps I followed to upgrade - 

### Step 1: Open the terminal and type the following commands

> jithendra@hp:~$ cd /etc/apt

> jithendra@hp:/etc/apt$ ls

The sources.list file tells ubuntu to what repositories to check in addition to any files in sources.list.d that end in the former one. 
In order to manually update, both of these should be updated. I started with sources.list

### Step 2: Update 'sources.list'

> jithendra@hp:/etc/apt$ sudo gedit sources.list

### Step 3: On active lines, replace the codename of previous Ubuntu version with codename of Ubuntu 20.04

* The codename for Ubuntu 19.10 is eano and for Ubuntu 18.10, it is bionic.
* Go through all active lines and replace these with focal. 
* * **Note:** Active lines are the lines that are not starting with '#'.
* The codename for Ubuntu 20.04 is Focal fossa and the keyword is focal.
* Since I was using Ubuntu 19.10, I changed the keyword from eano to focal.
* If the version is 18.04, then change from bionic to focal.
* If the version is 19.04, then change it from disco to focal.
* Save the file

After updating sources.list file, I went back and check sources.list.d to see any 3rd party apps and ppa's that also need to be upgraded. 
For example, google-chrome, spotify, and ppa's that I might have installed. But, I dont want any third party applications and ppa's in the new version.
So I simply removed all the existing ppas from source.list.d using this command 

> sudo rm /etc/apt/sources.list.d/*

But, If you want your ppa's and apps do the following

### Step 4: Come back and verify 'sources.list.d'

> jithendra@hp:/etc/apt$ cd sources.list.d/

> jithendra@hp:/etc/apt/sources.list.d$ ls

* This outputs files like google-chrome.list, spotify.list, or ppa's.
* Third party apps dont use any codename in their repository. But this is not case for all third party repositories
like ppa's(personal package archives) hosted on launchpad. 
* If the repositories uses codenames, then gedit them manually in the same way I did for sources.list
* Google-chrome, Spotify and many other third-party applications use stable codename in their repositories. There is no need
in updating these codenames. Even some apps use xenial in codenames which need not be updated.

### Step 5: Update and Upgrade

> jithendra@hp:/etc/apt/sources.list.d$ cd

> jithendra@hp:~$ sudo apt update

* I got a whole lot of stuff and all the gits of the updates are pointed out to focal. 
* This is just telling apt manually to look into focal and not into eano.(in my case)
* In my case, I got like this 1873 packages can be upgraded. Run 'apt list --upgradable' to see them.`
* This means 1873 packages are upgradable which are new.

> jithendra@hp:~$ sudo apt dist-upgrade

or

> jithendra@hp:~$ sudo apt full-upgrade

* There will be four kinds of packages in here
    * The following packages were automatically installed and are no longer required (Use 'sudo apt autoremove' to remove them)
    * The following packages will be REMOVED
    * The following NEW packages will be installed
    * The following packages have been kept back
    * The following packages will be upgraded

* Press yes and it will download all the packages and they will be unpacked one by one.
* A question will be asked whether to restart servieces during package upgrades without asking - Select YES
* Another question will be asked after sometime, whether I want to install package maintainer's version of the configuration file
or user currently installed version - select package manager's version - select Y
* **ALMOST DONE**

### Step 6: Remove the older clutter

> jithendra@hp:~$ sudo apt autoremove --purge

* purge removes configuration files too

### Step 7: REBOOT when everything is completed

* **When I start using my laptop then I faced an issue.**
* Because the new versions are on the harddrive. 
* To load all of that - 

> jithendra@hp:~$ sudo systemctl reboot


Without any errors, My laptop was succesfully upgraded to Ubuntu 20.04 LTS. 
--- 
Thank you for reading.Hope you find this post helpful.
