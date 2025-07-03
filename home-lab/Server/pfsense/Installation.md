---
title: 01-Installation
description: 
published: true
date: 2025-07-03T14:11:29.993Z
tags: 
editor: markdown
dateCreated: 2025-07-03T13:54:54.240Z
---

# Installation pfSense VM

**Date:** 2025-06-28
**pfSense-Version:** 2.7.2
**Proxmox-Version:** 8.

## Steps
### 1. Download ISO
I navigated to the [mirros page](https://atxfiles.netgate.com/mirror/downloads/) of netgate  so I didnt have to create an account:
![create_pfsense_vm_1.png](/homelab/server/pfsense/create_pfsense_vm_1.png)

Then I checked the hashes:
![create_pfsense_vm_2.png](/homelab/server/pfsense/create_pfsense_vm_2.png)

![create_pfsense_vm_3.png](/homelab/server/pfsense/create_pfsense_vm_3.png)

and wanted to etract the gzip file with the windows built-in unpacker. I received an Directory instead of the iso. I figured that maybe a dedicated program like 7zip is a better option for unpacking archived files and it worked. Finally I uploaded the ISO to my Proxmox.

### 2. VM creation
I just followed the Proxmox VM creation wizard, enabled the *Qemu Agent* and assigned following ressources:

**Disk size (GiB):** 50
**CPU - Sockets:** 1
**CPU - Cores:** 2
**Memory (MiB):** 5120
**Bridge:** vmbr0 (default)

The rest I left with the predefined values for now.

3. NICs

