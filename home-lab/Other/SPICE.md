---
title: Optimization
description: 
published: true
date: 2025-07-03T08:06:13.604Z
tags: 
editor: markdown
dateCreated: 2025-07-02T12:26:49.898Z
---

# Performance Optimization 
## SPICE
For better User experience I want to use SPICE on the Desktop VMs.

### Installation of the viewer
Windows:
https://virt-manager.org/download
I installed the viewer on my local machine.

### Apply to Windows VMs
Datacenter > proxmox01 > *\<WindowsVM>* > Hardware > Display > Edit > Graphic card: SPICE
image_02
Datacenter > proxmox01 > *\<WindowsVM>* > Hardware > Machine > Edit > Machine: q35
(virtual motherboard/emulated system-chipset -> hardware the proxmox
Both works together great because q35 is a modern intel chipset which provides PCIe, NVMe, SATA3, UEFI (lookup again)
Repeat on win22-01

### Install/run on Linux
sudo apt update
sudo apt install virt-viewer
sudo apt install spice-vdagent

sudo systemctl start spice-vdagentd.socket

### Open Console with SPICE
Console > SPICE > open Downloaded file

## Installation Guest Tools
### Windows
For better performance I then installed the guest tools I already downloaded and mounted to the Windows VMs (virtio-win-xxx.iso) when I created them.

### Linux
sudo apt update
sudo apt install qemu-guest-agent
(was already installed on kali-01)
