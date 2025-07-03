---
title: Iteration 2
description: 
published: true
date: 2025-07-03T15:10:24.490Z
tags: 
editor: markdown
dateCreated: 2025-07-03T14:56:04.914Z
---

# Iteration 2 - Updated Concept

> created on 2025-07-03

## Diagram

## Key Changes from [Iteration 1](/home-lab/Infrastructure/Network_Designs/Iteration_1)
- Switched to OPNsense for the Corp-LAN for a better, more realistic and secure network design
- VLAN trunk on a single bridge instead of multiple flat bridges and NICs
- Dedicated DMZ network
- Subnets re-aligned - all client/server groups are now segmented

## Interface & VLAN Configuration
### pfSense


### OPNsense
| Interface | Bridge/VLAN | IP Address | Subnet Mask (CIDR) |
|---|---|---|---|


## Realization & Issues
My goal was to build a domain with a SOC (blue team) and an attack LAN from which I simulate attacks (as red team). But I realized it is not as structured and separated as I wanted it. I want this scenario to be more realistic and also want to learn and experiment as much as possible like networking in general, VLANs, DMZ, different firewalls (pfSense and OPNsense) etc. When I started to configure the pfSense I realized it so that I reevaluated my network design.


