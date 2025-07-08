---
title: Initial Setup Walkthrough
description: 
published: true
date: 2025-07-08T15:54:59.829Z
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
8. [Reconfigure Proxmox and pfSense](#reconfigure-proxmox-pfsense)
9. 

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

### 8. Reconfigure Proxmox and pfSense {#reconfigure-proxmox-pfsense}
According to the current network diagram I removed the network device net3 and net4.
Then I reconfigured the Attack LAN interface and the Point2Point Interface to the OPNsense.
