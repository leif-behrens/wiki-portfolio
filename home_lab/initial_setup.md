---
title: Initial Setup Walkthrough
description: 
published: true
date: 2025-07-20T17:03:25.792Z
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

After starting the ubuntu machine, I pinged the OPNsense and got a response, so its reachable. 

I logged in to the management interface with firefox:

https://10.10.0.145

After the Login process I realized, that I use the live version and my config will be erased after reboot. After a little research on the [documentation](https://docs.opnsense.org/manual/install.html#installation-instructions) of opnsense I found that I have to login via ssh with the user **installer** and password **opnsense** to start the installation process. Then I followed the installation wizard and left everything at default. After installation I left the root password as is for now and change it later. Before the installation and to avoid configuration again from scratch I downloaded the configuration in the opnsense webinterface (System->Configuration->Backups->Download->Download configuration) because I wasn't sure if the installation from the live version to disk would erase the config.

I forgot to implement the DMZ. So I created a new Bridge (vmbr4) in proxmox and a NIC on the OPNsense, which I assigned to the vmbr4. 
In the web interface I assigned the new NIC (vtnet2) to OPT5, enabled the interface, set the IP address to 172.16.10.1, enabled DHCPv4

I renamed the description of the interfaces for a better overview:

![opnsense_interface_description.png](/homelab/infrastructure/opnsense_interface_description.png)

## Hardening
In the web interface I set a new root password. #A..
I just want the management vlan to be able to access the web GUI.
System -> Settings -> Administration -> Web GUI -> Listen Interfaces: VLAN99

Secure Shell -> Only Listen Interfaces: VLAN99

## Network Design - added VMs

I added some VMs to my [network design](/home_lab/infrastructure/network_designs/iteration3) so my network design looks like this:

![final_design_v2.png](/homelab/infrastructure/final_design_v2.png)

I configured the VMs accordingly in proxmox (bridges and NICs).

| VM | Bridge | VLAN Tag |
| --- | --- | --- |
| kali-prpl-01 | vmbr3 (Corp-LAN) | 10 |
| win10-01 | vmbr3 (Corp-LAN) | 20 |
| win22-01 | vmbr3 (Corp-LAN) | 30 |
| ubuntu-srv-01 | vmbr3 (Corp-LAN) | 40 |
| ubuntu-clt-01 | vmbr3 (Corp-LAN) | 99 |
| kali-01 | vmbr2 (Attack-LAN) | - |

## pfSense config
I want the pfSense to be "invisable" for the Corp and Attack LAN. It should be like "the internet"/ISP/Gateway for Corp and Attack LAN and works as a router. So its job is just routing and NAT between the different LANs (in this case Attack-LAN and Corp-LAN). To configure the pfSense accordingly I temporarily switched the subnet of the p2p link between pfsense and opnsense to /29 so I have an available ip address in the net 10.10.10.0. I temporarily switched the IP address and network bridge of the ubuntu-clt-01 accordingly so I was able to access the web GUI.

### General Setup
System -> General Setup

#### System
Hostname: pfsense-01
Domain: home.arpa (default)

#### DNS Server Settings
![dns_settings.png](/homelab/infrastructure/dns_settings.png)

#### Localization
![localization.png](/homelab/infrastructure/localization.png)

### Enforce HTTPS
Under System->Advanced->Admin Access I clicked on HTTPS and saved the settings.

### Firmware Update
First I saw an update is available (2.8.0) which I installed. 

### Backup

### SSH-Access
Is disabled

### Restrict access to Web GUI of the pfSense

### Change password
System->User Manager->Users
Changed the admin User password (saved it in password manager)

### Interface config
- Allow/route

