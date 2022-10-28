+++
title = "Quick look at Fedora 35"
date = 2022-01-31
updated = 2022-02-01
description = "Let's check out Fedora 35"

[taxonomies]
tags = ["how-to", "Linux", "Fedora", "beginner", "GNOME", "quick look"]
+++

# Let's take a look at the install process for 
# [Fedora Workstation 35](https://getfedora.org/). 

<!-- more -->

Fedora is the upsteam distribution for [Red Hat Enterprise Linux](https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux) and as such is often released with the latest versions of many Linux projects, like GNOME and in this version the new sound subsystem PipeWire.

It currently comes in five different editions.Fedora 35 was released on november 2 2021.
The one we are taking a look at here is the workstation edition which is
the traditional desktop edition. They also offer the Fedora Silverblue edition, which is an imutable desktop where software is installed with flatpak. This is an intersting concept that might be worthy of another post.

It comes with the GNOME desktop, and in the 35 release that would be GNOME 41 which is the latest GNOME release.


[Fedora workstation 35 download direct link](https://download.fedoraproject.org/pub/fedora/linux/releases/35/Workstation/x86_64/iso/Fedora-Workstation-Live-x86_64-35-1.2.iso)

# Installing with Qemu/kvm and virt-manager

 Rule of thumb for me when I try new distors in a vm is to pick 1Gib per cpu core and when trying a deskop I generally stick to 4 cpus and 4Gib of ram. This is reasonable for a desktop install.

After going through the New VM wizard from virt-manager. You should now be booted into a live enviroment like this: 


<img src="/img/install fedora/1-step.png" width="800">

Click the install button to progress.

Choose your language, keyboard keymap and which hard drive to install to.


<img src="/img/install fedora/2-step.png" width="800">

Now click the "Begin Installation" button. Fedora will now partition your drive and copy the OS onto your hard drive.

After a little while, you will be greeted with this screen:

<img src="/img/install fedora/3-step.png" width="800">

Hit the "Finish Installation" to complete the install and reboot.


The setup guide will tak you through finishing the install. Enable the third-party repositories, making a logiing in to some online accounts creating a user with a password 

<img src="/img/install fedora/first-boot.png" width="800">

After this you will be greeted with a offer to take a tour of GNOME 42, highly encuraged especially if you are new to Linux, GNOME and/or Fedora.

<img src="/img/install fedora/gnome.png" width="800">

Congratulations! All done with the install and ready to explore the wonderful world of Open Source Software. :-)

Next post : [Installing Software with Flatpak](../flatpak) 

Addendum: 

Some housekeeping is in order. First you should run:

```sh
sudo dnf update
```
The longer time since the release the more packages need to be updated. As you can see below, on my install the first update amounts to 1236 updates and 1.1G to download. This can take a while mostly depending on you download speed and cpu power.

<img src="/img/install fedora/update.png" width="800">

Next you can name your computer with the hostnamectl tool.

```sh
sudo hostnamectl hostname <your desired name>
```



