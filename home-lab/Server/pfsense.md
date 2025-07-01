---
title: pfSense
description: 
published: true
date: 2025-07-01T12:48:05.764Z
tags: 
editor: markdown
dateCreated: 2025-06-26T13:28:14.848Z
---

# pfSense

# Download
https://atxfiles.netgate.com/mirror/downloads/ so I didnt have to create an account.
Checked the hashes and wanted to etract the gzip file with the windows built-in unpacker. I received an Directory instead of the iso. I figured that maybe a dedicated program like 7zip is a better option for unpacking archived files and it worked.

# Config
Creation of four Network Adapters because I wanted to have different network segments in my homelab (reference Infrastructure). 1 for the WAN (connected to the fritzbox for internet access), one admin LAN and the rest for the different segment (Server LAN, User LAN, Attack LAN).

# Installation
Just booted the vm and agreed to the first things (default). Then a reboot was required and after that I had to configure the network interfaces (screenshot).
vtnet0 = WAN
vtnet1 = LAN (enabled full firewalling/NAT mode)
vtnet2 = optional 1 interface
vtnet3 = optional 2 interface

pfSense 2.7.2

# WAN Interface
IPv4-WAN address (static): 192.168.178.100/24
IPv6-WAN address: DHCP6
Default Gateway: 192.168.178.1 (Fritz!Box)

# LAN Interfaces 
## Admin-LAN
IPv4 (static): 10.10.1.1/24
IPv6: DHCP6
DHCP for the Clients: Activated
DHCP range: 10.10.1.100-10.10.1.199
MAC: BC:24:11:37:C9:28

## Corp-LAN
IPv4 (static): 10.10.2.1/24
IPv6: DHCP6
DHCP for the Clients: Activated
DHCP range: 10.10.2.100-10.10.2.199
MAC: BC:24:11:6C:10:07

## Server-LAN
IPv4 (static): 10.10.3.1/24
IPv6: DHCP6
DHCP for the Clients: Activated
DHCP range: 10.10.3.100-10.10.3.199
MAC: BC:24:11:C3:38:04

## Attack-LAN
IPv4 (static): 10.10.4.1/24
IPv6: DHCP6
DHCP for the Clients: Activated
DHCP range: 10.10.4.100-10.10.4.199

## Overview
INSERT IMAGE <create_pfsense_vm_21.png>
I could also use VLANs but for now I leave it as is with different virtual network interfaces for each LAN.

# Network Bridges
Under Datacenter > proxmox01 > System > Network I created Linux Bridges for each LAN so that the Proxmox is handeling (routing) all the traffic between the networks. Each virtual NIC of the different LANs is their gateway. This way they are all segmented and separated.
INSERT IMAGE for CREATION OF THE BRIDGES
After I created the bridges
