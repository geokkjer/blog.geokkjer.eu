+++
title = "Bootstrapping a DevOps buisiness part 1 What is DevSecOps?"
date = 2022-02-02
updated = 2022-02-02
description = "linux"

[taxonomies]
tags = ["how-to", "Linux", "talos", "beginner","intermediate", "devops", "k8s", "alpine"]
+++

# What is Kubernets

# What is do we want from k8s ?

# How did we do it ?
## Choosing a distribution ?

k3s vs talos

## virt vs metal
Proxmox 
two nics in each machine an unmanaged switch and ...  
tow lxc containers one for the routing and reverse proxying no dhcp

## layout

```sh
╭┈┈┈╮   ╭┈┈┈╮   ╭┈┈┈┈┈╮   ╭┈┈┈┈┈╮  ╭┈┈┈┈┈┈╮
┊ I ┊---┊ R ┊---┊ O/W ┊---┊ G   ┊--┊ k8s  ┊
╰┈┈┈╯   ╰┈┈┈╯   ╰┈┈┈┈┈╯   ╰┈┈┈┈┈╯  ╰┈┈┈┈┈┈╯
Internet - Router - Office/work - Gateway - K8s
```

## alpine nat gateway and router and dns

alpine router 
kernel forwarding

```sh
#!/bin/ash

set -eu

# install and add iptables
apk add iptables
rc-update add iptables

# enable packet forwarding and add sysctl
echo "net.ipv4.ip_forward = 1" >> /etc/sysctl.conf
sysctl -p
rc-update add sysctl

# Make iptables forward packets

iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
iptables -A FORWARD -i eth1 -j ACCEPT
/etc/init.d/iptables save
/etc/init.d/iptables restart
```

## Setting up unbound DNS server


## k3s with metallb how to
| Hostname |      IP      |    Role    |
|----------|--------------|------------|
| cp01     | 10.0.0.20 | controller |
| cp02     | 10.0.0.21 | controller |
| cp03     | 10.0.0.22 | controller |
| n01      | 10.0.0.30 | worker     |
| n02      | 10.0.0.31 | worker     |
| n03      | 10.0.0.32 | worker     |
| n04      | 10.0.0.33 | worker     |

1. install alpine & 

1.1 setup-alpine reboot add curl nano 
nano /etc/apt/repositories and add latest-stable to make it a rolling release

1.2 make a template

1.3 boot cloned template disable network for clone 2 etc
Some knowledge of your network static ip
set static ip
```sh
# edit the interface file to the right IP
nano /etc/network/interfaces

echo "node-name" > /etc/hostname

hostname -F /etc/hostname


sed -i 's/^default_kernel_opts=.*/default_kernel_opts="quiet rootfstype=ext4 cgroup_enable=cpuset cgroup_memory=1 cgroup_enable=memory"/g' /etc/update-extlinux.conf

update-extlinux

reboot
```
## 2. install k3s controlplane(s) and nodes

On the first controlplane: 

```sh
curl -sfL https://get.k3s.io | K3S_TOKEN=SECRET sh -s - server \ --cluster-init --disable servicelb
 ```
On the next controlpanes:

```sh 
curl -sfL https://get.k3s.io | K3S_TOKEN=SECRET sh -s - server \ --disable servicelb --server https://10.0.0.20:6443
```
4. transfer config and check cluster 
from /etc/rancher/k3s/k3s.yaml to wherever you want to connect to the cluster from. Edit the yaml and replace 127.0.0.1 ip with the ip of the control-plane 

On the k3s node(s):

```sh
curl -sfL https://get.k3s.io | K3S_URL=https://10.0.0.20:6443 K3S_TOKEN=SECRET sh -
```
4. transfer config and check cluster


5. Insyall Metallb  
```sh
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.13.3/config/manifests/metallb-native.yaml
```


```yaml
apiVersion: metallb.io/v1beta1
kind: IPAddressPool
metadata:
  name: first-pool
  namespace: metallb-system
spec:
  addresses:
  - 10.0.0.150-10.0.0.250
---
apiVersion: metallb.io/v1beta1
kind: L2Advertisement
metadata:
  name: example
  namespace: metallb-system
spec:
  ipAddressPools:
  - first-pool
```
the end next gitops and IaC



#### Sources - Further reading 
* [alpine-router](https://github.com/bobfraser1/alpine-router/blob/main/scripts/iptables.sh)
* [Setting up unbound DNS server](https://wiki.alpinelinux.org/wiki/Setting_up_unbound_DNS_server)
* [Nginx as reverse proxy with acme (letsencrypt)](https://wiki.alpinelinux.org/wiki/Nginx_as_reverse_proxy_with_acme_(letsencrypt))
* [Airfield @ Altitude: Building A Network Gateway With Alpine Linux](https://medium.com/@privb0x23/airfield-altitude-building-a-network-gateway-with-alpine-linux-454a56457d53)
* [How to set up Alpine as a wireless router](https://wiki.alpinelinux.org/wiki/How_to_set_up_Alpine_as_a_wireless_router)
* [Setting up Alpine Linux as a Home Router](https://riedstra.dev/2022/02/alpine-linux-home-router)
* [Configure Networking](https://wiki.alpinelinux.org/wiki/Configure_Networking)
* [Metallb Installation](https://metallb.universe.tf/installation/)