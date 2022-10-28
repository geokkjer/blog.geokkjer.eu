+++
title = "Red Hat Certified Engineer"
date = 2021-12-31
updated = 2022-02-01
description = "RHCE EX294"
[taxonomies]
tags = ["Red Hat","RHCE", "linux"]
+++

## Intro

So, I got challanged to do the RHCE(Red Hat Certified Engineer). This is my journey
The RHCE is about using ansible to configure and manage devices with the purpose of putting them into a desired state. This is a good way to get introducet to doing a declarative 

### Setting up a lab

My choice was to set a mixed lab envirnment with two AlmaLinux 8.5 server and one Ubuntu 18.04 server.
I installed ansible, GNOME and some graphical tools on the first AlmaLinux vm so this will where we do most of our work. All the server have cockpit installed. They are all on a nated network and accesible only from my workstation.
Installation of the Red Hat based and Ubuntu is somewhat trivial so we won't be going over that process here.

### The ansible config

Config hirarkey ANSIBLE_CONFIG environment variable is checked first, then the CWD(not world readable) folder is checkeced for an ansible.cfg, next ~/.ansible.cfg and finally /etc/ansible/ansible.cfg

check for your config with , in this case no config has been set and the system config is used:

```sh
$ ansible --version | grep 'config file'

  config file = /etc/ansible/ansible.cfg
```

Sometimes an adiminstrator might want to ensure that a specific ansible.cfg is used on a machine. The 

```sh 
declare -xr
```
command can then be used to set the ANSIBLE_CONFIG as a readonly variable. And if this is added to a login script , no other ansible config can be used.

```sh 
ansible-config view
ansible-config dump
ansible-config list 
```

These commands can be used to print the current config, print the effective settings or fully detail the setting that can be made. Very uselful commands for discovering fact about ansible and current settings and for finding explanations of optinons(use grep)


### The Ansible Inventory



### Sources
[Red Hat Certified Engineer
(RHCE) Study Guide: Ansible Automation for the Red Hat Enterprise Linux
8 Exam (EX294)](https://www.amazon.com/Certified-Engineer-RHCE-Study-Guide-ebook/dp/B08YW45QWP)




