---
title: pfSense
description: 
published: true
date: 2025-06-26T13:28:14.848Z
tags: 
editor: markdown
dateCreated: 2025-06-26T13:28:14.848Z
---

# pfSense

# Download
https://atxfiles.netgate.com/mirror/downloads/ so I didnt have to create an account.
Checked the hashes and wanted to etract the gzip file with the windows built-in unpacker. I received an Directory instead of the iso. I figured that maybe a dedicated program like 7zip is a better option for unpacking archived files and it worked.

# Config
Creation of three Network Adapters because I wanted to have different network segments in my homelab (reference Infrastructure). 1 for the WAN (connected to the fritzbox for internet access), the rest for the different segments.

# Installation
Just booted the vm and agreed to the first things (default). Then a reboot was required and after that I had to configure the network interfaces (screenshot).
vtnet0 = WAN
vtnet1 = LAN (enabled full firewalling/NAT mode)
vtnet2 = optional 1 interface
vtnet3 = optional 2 interface

pfSense 2.7.2
