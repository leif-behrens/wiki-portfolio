---
title: Iteration 2
description: 
published: true
date: 2025-07-03T15:20:53.401Z
tags: 
editor: markdown
dateCreated: 2025-07-03T14:56:04.914Z
---

# Iteration 2 - Updated Concept

> created on 2025-07-03

## Diagram
![final_design_v1.png](/homelab/infrastructure/final_design_v1.png)

## Key Changes from [Iteration 1](/home-lab/Infrastructure/Network_Designs/Iteration_1)
- Switched to OPNsense for the Corp-LAN for a better, more realistic and secure network design
- VLAN trunk on a single bridge instead of multiple flat bridges and NICs
- Dedicated DMZ network
- Subnets re-aligned - all client/server groups are now segmented

## pfSense Interface Mapping
| Interface | Proxmox Bridge | Role | IP Address | CIDR |
|---|---|---|---|---|
| **WAN** | vmbr0 | Internet uplink | 192.168.178.100 | /24 |
| **LAN** | vmbr1 (untagged) | Point-to-Point link to OPNsense (WAN) | 10.10.10.1 | /30 |
| **OPT2**  | vmbr2 | Attack-LAN | 192.168.50.1 | /24 |

## OPNsense
| Interface | Bridge/VLAN | Role | IP Address | Subnet Mask |
| --- | --- | --- | --- | --- |
| **WAN** | vmbr1 | P2P from pfSense | 10.10.10.2 | /30 |
| **DMZ** | vmbr3 | DMZ network | 172.16.10.1 | /24 |
| **VLAN10 (Admin)** | vlan10@vmbr0 | Admin-LAN | 10.10.0.1 | /28 |
| **VLAN20 (Clients)** | vlan20@vmbr0 | Client-LAN | 10.10.0.17 | /26 |
| **VLAN30 (Domain)** | vlan30@vmbr0 | Domain-Services | 10.10.0.81 | /27 |
| **VLAN40 (Apps)** | vlan40@vmbr0 | Application-LAN | 10.10.0.113 | /27 |
| **VLAN99 (Mgmt)** | vlan99@vmbr0 | Management-LAN | 10.10.0.145 | /28 |


## Realization & Issues
My goal was to build a domain with a SOC (blue team) and an attack LAN from which I simulate attacks (as red team). But I realized it is not as structured and separated as I wanted it. I want this scenario to be more realistic and also want to learn and experiment as much as possible like networking in general, VLANs, DMZ, different firewalls (pfSense and OPNsense) etc. When I started to configure the pfSense I realized it so that I reevaluated my network design.


