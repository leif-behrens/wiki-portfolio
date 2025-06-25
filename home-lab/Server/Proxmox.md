---
title: Proxmox
description: 
published: true
date: 2025-06-25T16:27:00.587Z
tags: 
editor: markdown
dateCreated: 2025-06-24T20:48:54.604Z
---

# Proxmox Homelab

This is the central overview of my personal Proxmox VE homelab.  
It documents the setup, configuration, and management of my system.
<br>

## General Information
| Property | Value |
| ---- | ----- |
| FQDN | proxmox01.local |
| IP (static) | 192.168.178.200 |
| Webinterface | https://192.168.178.200:8006 |
| Hardware | HP ProDesk 400 G3 - Mini-PC System mit Intel Core i5-7500-T 16Gb |
| MAC |  |
| Model | Raspberry Pi 4 Model B Rev 1.4 (8 GB) |
| OS  | Proxmox GUI: 8.4.1 (2025/06/25)<br>Proxmox Kernel 6.8.12-11 (2025/06/25) |
| Status | *Active* |
<br>

## Structure

### 1. [Installation & Initial Configuration](/proxmox/installation)  
Installing Proxmox on my hardware, network setup, and user access.

### 2. [Repositories & Updates](/proxmox/repositories-updates)  
Repository setup, update configuration, and upgrade procedures.

### 3. [Web Interface & Overview](/proxmox/webgui)  
Interface structure, core functionality, and management areas.

### 4. [Virtual Machines (VMs)](/proxmox/vms)  
VM definitions, configuration, and resource allocation.

### 5. [Network Design](/proxmox/networking)  
Bridges, VLANs, NAT, and isolation from the home network.

### 6. [Backups & Restore](/proxmox/backups)  
Backup strategy, snapshot handling, and restore tests.

### 7. [Monitoring & System Load](/proxmox/monitoring)  
CPU, RAM, disk, and network monitoring using appropriate tools.

### 8. [Maintenance & Upgrades](/proxmox/maintenance-upgrades)  
Safe upgrade workflows, custom scripts, and change logging.

### 9. [Issues & Solutions](/proxmox/issues)  
Problems encountered, fixes, and lessons learned.

---




## Installation
USB drive with rufus and the downloaded ISO of Proxmox (insert link here). 

TODO
Make some screenshots of rufus.

## Setup
Boot from USB 
IP: 192.168.178.200
Gateway: 192.168.178.1
DNS: 192.168.178.40
FQDN: proxmox01.local

Webinterface: https://192.168.178.200:8006

## ISO Upload
Screenshots are already uploaded
virtioIO Drivers are drivers for the windows vms (https://pve.proxmox.com/wiki/Windows_VirtIO_Drivers)

## Create VMs
### Windows 10


# Sonstiges TODO

Subscription Enterprise deaktivieren (Screenshot)
Update Failed (Screenshot)
-> Auf freie "No-Subscription"-Repository umstellen
nano /etc/apt/sources.list.d/pve-enterprise.list
Auskommentieren
\# deb https://enterprise.proxmox.com/debian/pve bookworm pve-enterprise
Create File
nano /etc/apt/sources.list.d/pve-no-subscription.list
Insert
deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription

Ceph (Lookup, was das ist) List deaktivieren. Ist für Enterprise und High availability 
nano /etc/apt/sources.list.d/ceph.list und Eintrag auskommentieren

apt update && apt full-upgrade -y
(neueste Proxmox-Version installieren - 6.8 (6.8.12-11) von 6.8.12-9, also wurde eine neue Revision des Kernesls installiert.). Übers Webinterface wird kein dist-upgrade gemacht (nur apt update & apt upgrade) statt apt full-upgrade



## Windows 10 Installation
nach _32 kommt ein Reboot, um die aktuellen Updates zu installieren

Remove Network Adapter (currently the VM has the 2 I assigned, same subnet) (Screenshot 39)







### Proxmox Upgrade-Dokumentation

**Datum:** 2025-06-25  
**Kommando:** `apt full-upgrade -y`

**Kernel-Upgrade:**
- Vorher: `proxmox-kernel-6.8.12-9`
- Nachher: `proxmox-kernel-6.8.12-11` (+ signed)

**Proxmox Version (GUI):** 8.4.1  
**Laufender Kernel nach Reboot:** `6.8.12-1-pve` (ggf. durch `uname -r` bestätigen)

## Proxmox Upgrade-Doku

**Datum:** 2025-06-25  
**Host:** proxmox01

### Vor dem Upgrade:
- Proxmox GUI (pve-manager): 8.4.0
- Kernel: proxmox-kernel-6.8.12-9-pve-signed

### Nach dem Upgrade:
- Proxmox GUI (pve-manager): 8.4.1
- Kernel: proxmox-kernel-6.8.12-11-pve-signed

### Upgrade-Prozess:
- 08:49 Uhr → `apt upgrade`: kleinere System- & GUI-Komponenten
- 09:40 Uhr → `apt full-upgrade`: Kernel und Metapakete

### Proxmox Upgrade-Dokumentation

**Datum:** 2025-06-25  
**Kommando:** `apt full-upgrade -y`

**Kernel-Upgrade:**
- Vorher: `proxmox-kernel-6.8.12-9`
- Nachher: `proxmox-kernel-6.8.12-11` (+ signed)

**Proxmox Version (GUI):** 8.4.1  
**Laufender Kernel nach Reboot:** `6.8.12-1-pve` (ggf. durch `uname -r` bestätigen)



# Script upgrade 
TODO: Automated upgrades and information about full upgrades available.
Done: Scripts for Power Save and WoL
