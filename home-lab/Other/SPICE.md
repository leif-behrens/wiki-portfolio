---
title: Optimization
description: 
published: true
date: 2025-07-02T13:30:13.970Z
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

### Install on Linux
sudo apt update
sudo apt install spice-vdagent
(was already installed on ubuntu)

sudo systemctl start spice-vdagent

According to the documentation I found (link) I should enable the agent by doing following:
sudo systemctl enable spice-vdagent (startup)

I received following warning (Screenshot SPICE_07):

I researched this and apparently the SPICE-agent is in newer distributions actived under `socket`.
Because I executed the command, I changed the config, but it should be like 
spice-vdagentd.service: static/indirect
spice-vdagentd.socker: enabled

Because I just installed it and don't want to misconfigure anything I just removed the spice-vdagentd
sudo apt remove spice-vdagent

And installed it again

sudo apt install spice-vdagent

Then I checked the current systemctl status (Screnshot)

And enabled the socket as well as started the service with `--now`:
sudo systemctl enable --now spice-vdagentd.socket

All bs

I found this video:
https://www.youtube.com/watch?v=MuEOQFGwOW4
Installed virt viewer

### Open Console with SPICE
Console > SPICE > open Downloaded file

## Installation Guest Tools
### Windows
For better performance I then installed the guest tools I already downloaded and mounted to the Windows VMs (virtio-win-xxx.iso) when I created them.

### Linux
sudo apt update
sudo apt install qemu-guest-agent
(was already installed on kali-01)
