---
title: Wiki.js
description: 
published: true
date: 2025-06-18T10:48:00.041Z
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
| **IP-Adresse**      | 192.168.178.40 |
| **Zugriffs-URL**    | http://raspi4:3000                              |
| **Port-Forwarding** | `3000:3000` in `docker-compose.yml`                 |
| **Volumes**         | `./data`, `./db-data`, evtl. `./backup`             |
| **Docker-Netzwerk** | Standard (bridge) oder benannt (`homelab-net`)      |
| **Git Remote**      | `git@github.com:leif-behrens/wiki.git`              |
| **Backupziel(e)**   | GitHub Repo (SSH Push) + optional lokal             |
| **Inbetriebnahme**  | 2025-06-18                                          |
| **Zuständigkeit**   | Leif (Homelab Admin)                                |

## Host system
Wiki.js is running in a docker container on a Raspberry Pi 4 ([raspi4](/home-lab/Server/raspberrypi)).


