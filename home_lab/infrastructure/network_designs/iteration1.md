---
title: Iteration 1
description: 
published: true
date: 2025-07-03T14:58:46.682Z
tags: 
editor: markdown
dateCreated: 2025-07-03T14:12:19.851Z
---

# Iteration 1 - First Concept

> created on 2025-06-28

## Diagram
![first_approach.png](/homelab/infrastructure/first_approach.png)

## Idea
- Flat LAN structure: no VLAN segments, each VM/group has its own subnet
- pfSense as a central firewall/router
- virtual NICs for each subnet
- quick start: VMs are in separated net-bridges

## Configuration
### pfSense


## Realization & Issues
My goal was to build a domain with a SOC (blue team) and an attack LAN from which I simulate attacks (as red team). But I realized it is not as structured and separated as I wanted it. I want this scenario to be more realistic and also want to learn and experiment as much as possible like networking in general, VLANs, DMZ, different firewalls (pfSense and OPNsense) etc. When I started to configure the pfSense I realized it so that I reevaluated my network design.


