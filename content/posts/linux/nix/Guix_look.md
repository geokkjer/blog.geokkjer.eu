+++
title = "Quick look at GNU Guix 2022"
date = 2022-06-09
updated = 2022-06-15
description = ""
[taxonomies]
tags = ["how-to", "Linux", "GNU", "Guix", "intermediate", "quick look", "GNOME"]
+++

# Checking out GNU Guix(pronounced [ɡiːks])

GNU Guix(pronounced [ɡiːks]) is a GNU/Linux distribuiton whith a little more emphasis on the GNU part than most distros.
This will be my first attempt at wrangeling it into something I can live in.
I am currently an Arch Linux and GNOME type person. 
I have used NixOS as a daily driver for a couple of months in 2021 and I liked it.  

<!-- more -->

# history and philosophy

The GNU Guix distribution saw the ligh of day in 2013
functional packaging
uses hashing to ensure reproducability - bitflipping maybe
uses symlinks to packages in the store to represent the standard linux filesystem hierachy 
GNU Guix follow standard gnu package with no non-free software
Reimplementation of Nix
implemented in gnu guile
both a packet manager and os just like Nix and NixOs both uses the store no linux filesystem hirarchy 
symlinks
reproducible builds

init system 

run echo PATH


# Install process 

Follow SystemCrafters , get nonguix ++.

Download here : [Guix iso](https://github.com/SystemCrafters/guix-installer/releases/latest)

I have documented the process of getting an iso onto usb stick in the [Ubuntu install](/ubuntu-2110-quick-look) post.

```sh
sudo dd if=guix-installer-<date number>.iso of=/dev/sdX status=progress && sync
```
dd is one of those nice Unix tools that does excactly what you tell it to, so be sure to double check that you are using the right harddrive.

In this post I will be using virt-manager as a ffrontend for Qemu/KVM, shich is the Linux native virtualization suite.
THe process will be very dimilar to indtalling on physical disk, there will probably be a post if or ehrn I devide to switch from Arch Linux to GNU Guix as my daily driver. The reasoning behind this decision is that I know that assembling a full? system configuration takes some time as there are many small and some not so small configuration changes I want. 
In the spirit of trying new stuff I also want to try to learn Emacs and EXWM, but I will keep GNOME as a backup desktop as I am really fond of it and . 

### Step by step graphical install
GNU Guix uses the ncurses framework for the installer. First we have to choose the lenguage we want to use during the install process.

<img src="/img/gnu_guix_install/guix_1.png" width="800" class="center">

Next we have to choose whether we want to use the graphical install or a shell. The shell option is mostly for when you already have made your system configuration. We will use the graphical/menu based installer. This is a good choice for a first time install.

<img src="/img/gnu_guix_install/guix_2.png" width="800" class="center">

Next we pick our timezone 
<img src="/img/gnu_guix_install/guix_3.png" width="800" class="center">

and keyboard layout.

<img src="/img/gnu_guix_install/guix_4.png" width="800" class="center">

And the hostname of the machine. I picked a generic name because the intended use for this vm is to develop a configuration to use on my main machine.

<img src="/img/gnu_guix_install/guix_5.png" width="800" class="center">

Next is internet access. I have no wifi on this vm so there is no configuration for me.
Here is where one of the benefits of using the SystemCrafters image will be apparent. It contains the full Linux Kernel and subseq
it has non-free wifi drivers. With the standard GNU Guix you might run into some difficulties here, since many wifi-cards in modern laptops comes with non-free drivers.
In this post I will use the linux-libre kernel
[SystemCrafters](https://www.youtube.com/watch?v=oSy-TmoxG_Y) does install and adds nonguix channel. I think that an usb to rj45 is less hassle, but this is very hands on and a valuable excersise if you want to learn some linux.

Then you will be presented with the option to enable or disable Substitutes , which in plain terms is installin packets from a server rather than directly from the iso. 
I will accept the risk and use the internet to download newer versions of the software.

<img src="/img/gnu_guix_install/guix_6.png" width="800" class="center">

Next we will have to make a root password and user.

<img src="/img/gnu_guix_install/guix_7.png" width="800" class="center">

Then we choose our desktop environment. I am going to pick GNOME and Emacs EXVM. This will ensure that i have the GNOME tools and something to fall back to when I start to experiment with Emacs EXVM.

<img src="/img/gnu_guix_install/guix_8.png" width="800" class="center">

Next we pick some network services.
Ssh is always usefull, if you want to connect to your machine remotly.
Tor if you want to surf the net anonymously or want to access the "dark web".
The Mozilla ssl sertificates is needed for https browsing and should be installed in most cases.

<img src="/img/gnu_guix_install/guix_9.png" width="800" class="center">

Then you can opt to install CUPS for printer support, I don't need it.

Now is about the time when some preperation is advised. It is time for partitioning you disk(s). You could of course use one of the guided option like I did, but you have the option for manual partitioning if needed.

<img src="/img/gnu_guix_install/guix_10.png" width="800" class="center">

I picked the guided install with everything on one partition. This is an easy an simple patition scheme that is sufficient for learning Guix in a vm, but if you want to dual boot or have a nice btrfs scheme 

<img src="/img/gnu_guix_install/guix_11.png" width="800" class="center">

Finally we have a configuration file for the system. This file is written in the guile programming language, which is scheme lisp 
parens. You can edit it here.

<img src="/img/gnu_guix_install/guix_12.png" width="800" class="center">

Downloading substitutions ie packages from the internet. This might take a while, depending on your internet speed and the server. 

<img src="/img/gnu_guix_install/guix_13.png" width="800" class="center">

Congratulations, let's reboot into our new system.

<img src="/img/gnu_guix_install/guix_14.png" width="800" class="center">


Next up is the fun stuff, learning guile and configuring the system. Next blog post.

<img src="/img/gnu_guix_install/guix_15.png" width="800" class="center">


### Conclusion

GNU Guix reprecent, toghethr with NixOS, a new way of thinking about the Linux distro. 
The install method of Guix is fairly straight forward and does not differ to much from a traditional install like Ubuntu or Fedora. The difference starts to become apparent when we are presented with the guile configuration file. More to come, check out some nice resources in the sources. 


#### Sources
* [Andrew Torpin youtube video](https://www.youtube.com/watch?v=S9V-pcTrdL8)
* [SystemCrafters playlist on GNU guix](https://www.youtube.com/playlist?list=PLEoMzSkcN8oNxnj7jm5V2ZcGc52002pQU)
* [FOSDEM Talk by Ludovic Courtès](https://www.youtube.com/watch?v=LnU8SYakZQQ)
* [GNU Guix Wikipedia](https://en.wikipedia.org/wiki/GNU_Guix)
* [GNU Guix manual](https://guix.gnu.org/en/manual/devel/en/guix.html)