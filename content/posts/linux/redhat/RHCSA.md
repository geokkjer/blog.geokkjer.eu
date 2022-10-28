+++
title = "Red Hat Certified System Administrator"
date = 2022-03-18
updated = 2022-03-18
description = "RHCSA"
[taxonomies]
tags = ["Red Hat","RHCSA", "linux"]
+++

So I have decided to get certified, my picks are the Red Hat Certified System Administrator(RHCSA), the Red Hat Cetrified Engineer(RHCE) and the Certified Kubernetes Administrator(CKA).

Let's start from the beginning with the most fundamental one, the RHSCA. This cert ensures that the student knows how to preform basic Linux system admin tasks and some Red Hat specific stuff.

<!-- more -->

- [Introduction to Linux](#introduction-to-linux)
- [Installation](#installation)
- [Bootprocess](#bootprocess)
- [Directories](#directories)
- [Manage files from the cli](#manage-files-from-the-cli)
- [Create view and edit text files](#create-view-and-edit-text-files)
- [Manage local users and groups](#manage-local-users-and-groups)
- [Control access to files](#control-access-to-files)
- [Monitor Linux processes](#monitor-linux-processes)
- [Services and daemons](#services-and-daemons)
- [SSH](#ssh)
- [Logs](#logs)
- [Intro to Linux networking](#intro-to-linux-networking)
- [Archive and transfer files](#archive-and-transfer-files)
- [Software management](#software-management)
- [More on Linux file system](#more-on-linux-file-system)
- [improving-command-line-productivity](#improving-command-line-productivity)
- [Sources](#sources)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>


### Introduction to Linux

Linux is a kernel, a monolithic kernel and not a micro kernel. It's purpose is to make computers hardware usable. An operating System is a kernel plus a userland, such as GNU(Gnu is not Unix). Is linux about [choice](http://www.islinuxaboutchoice.com/).
Linux kernel interacts directly with the hardware and provides low level services to upper layer components.
A Linux distibution is sometimes a curated(read: configured) collection of software that is bundeled on top of, and along side, a Linux kernel. Sometimes it is not curated but the delivered either as build scripts or binary packages from upstream, we call this a meta-distribution. The Linux kernel is one of the biggest software projects that has ever existed, this is often attributed to the adoption of the GNU(GPL v2) lisence, which forces people and companies to collaborate and contribute their changes back upstream to the Linux kernel. The originator, and still, main maintainer of Linux is Linux Thorvalds. Some notable fetures of the Linux kernel is that is sort of reimplementation of UNIX and it follows the POSIX standard. Everthing in Linux is a file, a for the most part the UNIX philosphy of one program that does one task very well is the standard. They(the kernel maintainers) also have a strict rule of never breaking userland.

### Installation 

In our case enterprise linux, [AlmaLinux 8](https://almalinux.org/) which is a bug by bug reproduction of the Red Hat Enterprise Linux. Or register and download the Red Hat Enterprise Linux iso from [Red Hat](https://developers.redhat.com/products/rhel/download). This requires registration and a (free)subscribtion. 
DD the iso to an usb stick and boot, follow the graphical instructions.

### Bootprocess

Booting -> bootloader -> linuk kernel -> pid1/systemd - userland

### Directories
Linux uses the [Filesystem Hierarchy Standars](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html)

>This standard consists of a set of requirements and guidelines for file and directory placement under UNIX-like operating systems. The guidelines are intended to support interoperability of applications, system administration tools, development tools, and scripts as well as greater uniformity of documentation for these systems.

```sh
tree -d -L1 /

/
├── bin -> usr/bin
├── boot
├── dev
├── etc
├── home
├── lib -> usr/lib
├── lib64 -> usr/lib
├── mnt
├── opt
├── proc
├── root
├── run
├── sbin -> usr/bin
├── srv
├── sys
├── tmp
├── usr
└── var

18 directories
```

* bin or /usr/bin or /sbin are symlinked as you can see in the tree output above. They are for binary programs. 

* /boot is where the bootloader stores files needed in the boot process such as initramfs, conf files and more.

* /dev is for devices and since everthing in Linux is a file here are hardware represented as files

* /etc is for host-specific system-configuration files like fstab(mounting of partitions)

* /home is where the users of the system lives and stores their files. A machine user does not need a home and can be created whitout one.

* /lib is for shared libraries and kernel modules

* /lib64 is for 64bit share libraries, in modern Linux all libs are found in /usr/lib

* /mnt is for manual mounting point

* /opt add-on application software

* /proc de-facto standard Linux method for handling process and system information

* /root home folder for the root user.

* /run runtime variable data

* /sbin same as /usr/bin

* /sys information about devices, drivers, and some kernel features is exposed. Linux only

* /tmp for temporary files will be wiped on reboot

* /usr stands for UNIX/User System Resources and contains shareable,read-only data.

* /var variable data files. includes spool and administartive and logging data also transient and temporary files

### Manage files from the cli

### Create view and edit text files 

### Manage local users and groups

Tools to manage users and groups on a Linux system.

```sh
useradd  <username> # add a user to the system
useradd -g <groupname> -s <shell> -c <"description"> -m -d <create home directory> <username>
groupadd <groupname> # add a group to the system
userdel -r <username> # remove a user from the system -r to remove home directory
groupdel <groupname> # delete a group
usermod -G <group> <username> # add user to group
chgrp -R <groupname> <username> # set primary group
passwd <username> # set the users password
chage <switch> user # change user password expiry 

su  # run a command with substitute user and group ID
sudo # execute a command as another user
visudo # edit sudoers file
```
files:

* /etc/passwd
* /etc/group
* /etc/shadow
* /etc/login.def
* /etc/sudoers

### Control access to files

In linux everything is a file, there are 3 types of permissions r - read, w - write and x -execute. 
File permissions can be controlled at three levels: u - user, g -group and o - other.
The first bit shows what kind of file it is, - file. d - directory, l -link b - blockdevice and c - 

```sh
$ ls -l /

lrwxrwxrwx 7 root  7 Dec  2021 bin -> usr/bin
drwxr-xr-x - root  1 Jan  1970 boot
drwxr-xr-x - root 23 Mar 09:53 dev
drwxr-xr-x - root 23 Mar 13:23 etc
drwxr-xr-x - root 10 Jun  2021 home
lrwxrwxrwx 7 root  7 Dec  2021 lib -> usr/lib
lrwxrwxrwx 7 root  7 Dec  2021 lib64 -> usr/lib
drwxr-xr-x - root 31 May  2021 mnt
drwxr-xr-x - root 14 Mar 16:48 opt
dr-xr-xr-x - root 23 Mar 09:52 proc
drwxr-x--- - root 23 Feb 18:32 root
drwxr-xr-x - root 23 Mar 13:30 run
lrwxrwxrwx 7 root  7 Dec  2021 sbin -> usr/bin
drwxr-xr-x - root 26 Oct  2021 srv
dr-xr-xr-x - root 23 Mar 13:30 sys
drwxrwxrwt - root 23 Mar 13:30 tmp
drwxr-xr-x - root 23 Mar 09:52 usr
drwxr-xr-x - root 23 Mar 09:52 var

chmod (+/- permissions ie x/r/w),()

```


### Monitor Linux processes

```sh
```

### Services and daemons

### SSH

### Logs

### Intro to Linux networking

### Archive and transfer files

### Software management

### More on Linux file system

### improving-command-line-productivity






### Sources 
* [Tech Arkit Youtube](https://www.youtube.com/watch?v=-wNfs5fRazI)
* [MyLinuxGig Youtube](https://www.youtube.com/watch?v=3Qo5_Is0VsY)
* [Udemy course by Imran Afzal](https://www.udemy.com/course/unofficial-linux-redhat-certified-system-administrator-rhcsa-8/)
