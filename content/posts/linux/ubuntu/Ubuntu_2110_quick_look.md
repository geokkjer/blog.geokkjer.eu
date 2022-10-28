---
title: Installing Ubuntu 21.10
date: 2021-10-03T14:56:58+02:00
draft: false
author: Geir Okkenhaug Jerstad
---



## About the quick look/install this distro series

The post tagged with quick_look amd install is written both for me to get familiar with markdown/blogging and with the beginner in mind, if that is you I commend your choiche and wish good speed on your computing journey.

The task of taking controll of your computing by installing a Linux distro on your own hardware can be daunting for the beginner but is a vital step in the journy to digital svorignty??.  

## Let's take a look the install process for [Ubuntu](https://releases.ubuntu.com)

Ubuntu is one of the most popular Linux distributions. The first release was 04.10 back in 2004. It started as a project to make debian more user friendly. They follow a six month release schedule with a long-term support release every two years. The current long-term release is the 20.04 version.
There is a lot of history and some philosphy around Ubuntu and if you want to know more please check out the [About](https://ubuntu.com/about) page.
Under Canonicals stewardship it has grown to be almost synonomous with Linux espescially on the desktop. 
Although there always were good alternatives, and recently there has been some seriously good offerings from the likes of Pop_OS, Solus and Manjaro Linux. Even the classic distros like Fedora and Open Suse have been putting out some stellar releases.

<!-- more -->

## Downloading the isos

The first thing we need is the OS, Ubuntu provides iso images of their OS freely from their website. 
Head over to the Download page: [Ubuntu Download](https://ubuntu.com/download/desktop)

## Making a bootable usb

First descision to be made, install to metal or virtual machine.
If you want to install to your physical machine, first you have to burn your iso to an usb-key.
Here are three options which should cover most use cases, but there are more ways to do this. If you are so inclined, it should not be very difficult to find using [DuckDuckGo](https://duckduckgo.com/) or any similar search engine.

### Etcher

One of the most popular is etcher, it is an electoron app and is availiable on the major proprietary platforms. 

* [Etcher download](https://www.balena.io/etcher/)

Etcher is very easy, just pick the iso, chose the drive and hits the "Flash!" button.

![Etcher](../img/ubuntu2110/etcher.png)

#### Gnome-Disks

But if you alredy are on GNOME you could use gnome disk, like this:

Choose the restore image option.

![Gnome Disks](../img/ubuntu2110/disk-1.png)

Pick the iso you want to use and hit start restoring.

![Gnome Disks](../img/ubuntu2110/disk-2.png)

#### DD

Or you could use the trusty old dd utility from the command line.

~~~ bash

$ cd to/the/folder/of/your/iso/

$ sudo dd if=ubuntu-21.10-desktop-amd64.iso of=/path/to/usb-stick bs=1M 

$ sync

~~~

## Install using virt-manager 

Ubuntu boots you straight into a live session, where you can choose whether you want to try out the desktop or if you want to install the OS to disk. If you are unsure whether all your hardware is supported, the live-session is a good opportunity to test and see what works and what doesn't.
Highly recomended if you want to install to a laptop from a non-linux vendor.

Hit the "Install Ubuntu" button.

<img src="../img/ubuntu2110/ubuntu-1.png" width="600" class="center">

Pick your keyboard layout.

<img src="/img/ubuntu2110/ubuntu-2.png" width="600" class="center">

We'll do a normal install with updates and third-party software enabled.

<img src="/img/ubuntu2110/ubuntu-3.png" width="600" class="center">

If you have some special partitions scheme this is when you apply it. We'll choose the "Erease disk and install Ububntu" which is the nuke and pave option. If you want to use the ZFS filesystem the option is under the advanced features. Now hit the "Install Now" button and then the "Continue" button to start the installation.

<img src="/img/ubuntu2110/ubuntu-4.png" width="600" class="center">

 Pick your location on the next screen. Then enter your name, username and password for the account.

<img src="/img/ubuntu2110/ubuntu-5.png" width="600" class="center">

Sit back an relax while Ubuntu is busy installing itself to your hard drive.

<img src="/img/ubuntu2110/ubuntu-6.png" width="600" class="center">

Reboot when prompted.

# Conclusion

Ubuntu is almost trivial to install. The process is so streamlined that compared to some other OS it feels very polished.

Congratulation and welcome to your fresh Ubuntu install.

<img src="/img/ubuntu2110/ubuntu-reboot.png" width="600" class="center">

Go through the first login wizard.

<img src="/img/ubuntu2110/ubuntu-login.png" width="600" class="center">

And of course update your system with :

~~~ bash
$ sudo apt update && sudo apt dist-upgrade -y 
~~~
