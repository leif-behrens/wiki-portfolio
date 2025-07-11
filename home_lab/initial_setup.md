---
title: Initial Setup Walkthrough
description: 
published: true
date: 2025-07-11T14:40:24.158Z
tags: 
editor: markdown
dateCreated: 2025-07-04T15:56:03.506Z
---

# Initial Setup Walkthrough

This walkthrough describes the chronological steps I took to build the home lab. Each entry includes context, goals, prerequisites, the commands I ran, any obstacles encountered, and lessons learned.

---

## Table of Contents

1. [Network Design Draft](#network-design-draft)  
2. [Proxmox Installation](#proxmox-installation)  
3. [Image Management](#image-management)  
4. [VM Creation and Initial Configuration](#vm-creation-and-initial-configuration)  
   - [Windows 10](#windows-10)  
   - [Windows Server 2022](#windows-server-2022)  
   - [Kali Linux](#kali-linux)  
   - [Kali Purple](#kali-purple)  
   - [Ubuntu Client](#ubuntu-client)  
   - [Ubuntu Server](#ubuntu-server)  
   - [pfSense](#pfsense)
5. [SPICE Setup for Desktops](#spice-setup-for-desktops)  
6. [Network Design Rework](#network-design-rework)  
7. [OPNsense Installation](#opnsense-installation)
8. [Reconfigure Proxmox and pfSense](#reconfigure)
	- [pfSense](#pfsense)
	- [Proxmox](#proxmox)
9. [OPNsense initial configuration](#opnsense-initial-configuration)

---

### 1. Network Design Draft {#network-design-draft}

**Date:** YYYY-MM-DD  
**Goal:** Erste Skizze des Subnetzes, VLAN-Aufteilung, IP-Plan  
**Prerequisites:** Zeichensoftware (draw.io), Anbindung am Router  


### 2. Proxmox Installation {#proxmox-installation}
PLACEHOLDER


### 3. Image Management {#image-management}
PLACEHOLDER


### 4. VM Creation and Initial Configuration {#vm-creation-and-initial-configuration}
PLACEHOLDER

#### Windows 10 {#windows-10}
PLACEHOLDER

#### Windows Server 2022 {#windows-server-2022}
PLACEHOLDER

#### Kali Linux {#kali-linux}
PLACEHOLDER

#### Kali Purple {#kali-purple}
PLACEHOLDER

#### Ubuntu Client {#ubuntu-client}
PLACEHOLDER

#### Ubuntu Server {#ubuntu-server}
PLACEHOLDER

#### pfSense {#pfsense}
PLACEHOLDER

### 5. SPICE Setup for Desktops {#spice-setup-for-desktops}
PLACEHOLDER

### 6. Network Design Rework {#network-design-rework}
PLACEHOLDER

### 7. OPNsense Installation {#opnsense-installation}
PLACEHOLDER

### 8. Reconfigure Proxmox and pfSense {#reconfigure}

#### pfSense {#pfSense}
According to the current network diagram I removed the network device net3 and net4.
Then I reconfigured the Attack LAN interface and the Point2Point Interface to the OPNsense.

| NIC | Interface | IP | CIDR |
| --- | --- | --- | --- |
| vtnet0 | WAN | 192.168.178.100 | /24 |
| vtnet1 | LAN | 10.10.10.1 | /30 |
| vtnet2 | OPT1 | 192.168.50.1 | /24 |

No IPv6, no DHCP for LAN
No IPv6, DHCP for OPT1 (192.168.50.100-200)

TODO: Configure OPT1 Interface via Web GUI. http://192.168.50.1

#### Proxmox {#proxmox}
I removed the network bridges vmbr1-vmbr5 and created two additional Linux bridges for the pfSense and its connected networks: vmbr1 (P2P-Link-LAN) and vmbr2 (Attack-LAN):
Then I created another bridge for the Corp-LAN for the OPNsens:
vmbr3 (Corp-LAN)

![bridges_pfsense.png](/homelab/infrastructure/bridges_pfsense.png)

Then I assigned the NICs of the pfSense to the bridges:

![assign_bridges_pfsense.png](/homelab/infrastructure/assign_bridges_pfsense.png)

### OPNsense Initial Configuration {#opnsense-initial-configuration}
I created a new network device (net1) and assigned it to vmbr3 (Corp-LAN) and assigned the network device net0 to vmbr1 (P2P-Link-LAN):

![assign_bridges_opnsense.png](/homelab/infrastructure/assign_bridges_opnsense.png)

I rebooted the OPNsense to make sure the new NICs are recognized (I am not sure if it was necessary but still I did it).

After the reboot the OPNsense wants me to configure the interfaces and the first question it asked me was "Do you want to configure LAGGs now? [y/N]". I had to look up, what it means and it stands for *Link Aggregation*, which means to bundle multiple interfaces to one virtual interface. Since I already have one virtual interface for each network segment and I don't need a higher throughput, I selected *N*.

Then it asked me to configure VLANs now. I selected *y*.
parent interface: vtnet1 
VLAN tags: 99 (Management), 10 (Admin), 20 (Client), 30 (Domain Services), 40 (Application)

Then I assigned the WAN, LAN and OPT interfaces as follows:

![opnsense_vlan_config.png](/homelab/infrastructure/opnsense_vlan_config.png)

After the assignment of the interfaces I configured the IP addresses of each interface:
LAN: 10.10.0.145/28 (Management), IPv6 disabled and DHCP enabled (10.10.0.146-.158), restore web gui access to default and enable HTTPS web GUI. New self signed web GUI cert -> y (for all interfaces), DHCP range alway first to last available address
OPT1: 10.10.0.129/28 (VLAN10/Admin)
OPT2: 10.10.0.1/26 (VLAN20/Clients)
OPT3: 10.10.0.65/27 (VLAN30/Domain Services)
OPT4: 10.10.0.97/27 (VLAN40/Applications)
WAN: 10.10.10.2/30, Upstream gateway address: 10.10.10.1 (pfSense), gateway name server = No, Name server for now: my pihole (192.168.178.40) which should be reachable if configured correctly. I'll take care of it later.

![opnsense_ip_config.png](/homelab/infrastructure/opnsense_ip_config.png)

Then I enabled *VLAN aware* on vmbr3 and for to access the web GUI via the management VLAN I set the bridge of the ubuntu-clt-01 machine to vmbr3 and also set the VLAN Tag to 99:

![ubuntu_clt_management_vlan.png](/homelab/infrastructure/ubuntu_clt_management_vlan.png)

