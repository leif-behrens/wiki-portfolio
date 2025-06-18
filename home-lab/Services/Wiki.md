---
title: Wiki.js
description: 
published: true
date: 2025-06-18T10:40:50.798Z
tags: 
editor: markdown
dateCreated: 2025-06-18T10:26:51.405Z
---

# Wiki.js - Selfhosted Wiki Service

A central wiki, operated in a Docker container and versioned via Git. This document describes the setup and administration in the Homelab context.

## 🖥️ Technical Details
| Property         		| Value                                                |
|---------------------|-----------------------------------------------------|
| **Hostsystem**      | [Raspberry Pi 4B (8 GB RAM)](/home-lab/Server/raspberrypi)|
| **Betriebssystem**  | Raspberry Pi OS Lite / Debian 11 (Bullseye)         |
| **Architektur**     | ARMv7 / ARM64 (je nach OS)                          |
| **Docker Setup**    | Docker + Docker Compose                             |
| **IP-Adresse**      | 192.168.10.50 (statisch via DHCP oder `.network`)   |
| **Zugriffs-URL**    | http://wiki.local:3000                              |
| **Port-Forwarding** | `3000:3000` in `docker-compose.yml`                 |
| **Volumes**         | `./data`, `./db-data`, evtl. `./backup`             |
| **Docker-Netzwerk** | Standard (bridge) oder benannt (`homelab-net`)      |
| **Git Remote**      | `git@github.com:leif-behrens/wiki.git`              |
| **Backupziel(e)**   | GitHub Repo (SSH Push) + optional lokal             |
| **Inbetriebnahme**  | 2025-06-18                                          |
| **Zuständigkeit**   | Leif (Homelab Admin)                                |

## Host system
Wiki.js is running in a docker container on a Raspberry Pi 4 ([raspi4](/home-lab/Server/raspberrypi)).


