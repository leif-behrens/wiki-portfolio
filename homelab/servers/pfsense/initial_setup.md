---
title: 02 - Initial Setup
description: 
published: true
date: 2025-07-03T14:54:25.058Z
tags: 
editor: markdown
dateCreated: 2025-07-03T14:32:35.298Z
---

# Initial Setup of the pfSense

## Creation of the Network Bridges in Proxmox
According to my [network design](/home-lab/Infrastructure/Network_Designs/Iteration_1) I created the following network bridges. I navigated to *Datacenter > proxmox01 > System > Network* and created an empty bridge with comments for each bridge.
![create_bridge_02.png](/homelab/server/pfsense/create_bridge_02.png)

## Assignment of the Interfaces
- WAN (vtnet0)
	- IPv4-WAN address (static): 192.168.178.100/24
  - IPv6-WAN address: DHCP6
  - MAC: BC:24:11:8B:51:92
  - Default Gateway: 192.168.178.1 (Fritz!Box/Home Router)
- LAN (vtnet1): 10.0.1.1/24 (Admin-LAN)
  - IPv4 (static): 10.10.1.1/24
  - IPv6: DHCP6
  - DHCP for the Clients: Activated
  - DHCP range: 10.10.1.100-10.10.1.199
  - MAC: BC:24:11:37:C9:28
- OPT1 (vtnet2): 10.0.2.1/24 (Corp-LAN)
	- IPv4 (static): 10.10.2.1/24
  - IPv6: DHCP6
  - DHCP for the Clients: Activated
  - DHCP range: 10.10.2.100-10.10.2.199
  - MAC: BC:24:11:6C:10:07
- OPT2 (vtnet3): 10.0.3.1/24 (Server-LAN)
	- IPv4 (static): 10.10.3.1/24
  - IPv6: DHCP6
  - DHCP for the Clients: Activated
  - DHCP range: 10.10.3.100-10.10.3.199
  - MAC: BC:24:11:C3:38:04
- OPT3 (vtnet4): 10.0.4.1/24 (Attack-LAN)
	- IPv4 (static): 10.10.4.1/24
  - IPv6: DHCP6
  - DHCP for the Clients: Activated
  - DHCP range: 10.10.4.100-10.10.4.199
  - MAC: BC:24:11:04:0A:E1
