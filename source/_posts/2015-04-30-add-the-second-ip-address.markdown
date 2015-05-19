---
layout: post
title: "Add the second IP address"
date: 2015-04-30 22:10:53 +0000
comments: true
categories: 
---

### The senario is like this

I need my Arch Linux to be able to work in two different network environments, and I hate the idea of adding another network adapter to it, although it is running in a VMWare virtual machine.

### Solution: adding new IP address

It was configured to get dynamic IP address by running the following command:
```
$ sudo systemctl enable dhcpcd@net0.service
```
Note: /usr/lib/systemd/system/dhcpcd@.service should be there if dhcpcd was installed.

Now add the following files:
```
/etc/conf.d/network@net0
address=10.255.255.77
netmask=24
broadcast=10.255.255.255
```
```
/etc/systemd/system/network@net0.service
[Unit]
Description=Network connectivity (%i)
Wants=network.target
Before=network.target
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
Type=oneshot
RemainAfterExit=yes
EnvironmentFile=/etc/conf.d/network@%i

ExecStart=/usr/bin/ip link add link %i name %i.1 type vlan id 1
ExecStart=/usr/bin/ip link set dev %i.1 up
ExecStart=/usr/bin/ip addr add ${address}/${netmask} dev %i.1 broadcast ${broadcast}

ExecStop=/usr/bin/ip addr flush dev %i.1
ExecStop=/usr/bin/ip route flush dev %i.1
ExecStop=/usr/bin/ip link set dev %i.1 down

[Install]
WantedBy=multi-user.target
```
Then enable network@net0.service.
