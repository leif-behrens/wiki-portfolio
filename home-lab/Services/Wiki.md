---
title: Wiki.js
description: 
published: true
date: 2025-06-18T12:43:49.681Z
tags: 
editor: markdown
dateCreated: 2025-06-18T10:26:51.405Z
---

# Wiki.js - Selfhosted Wiki Service

As part of my Homelab setup, I wanted a structured and accessible place to document my infrastructure, projects, tools, and learning. After evaluating several solutions, I chose [Wiki.js](https://js.wiki) for its markdown support, modern interface, and Docker compatibility.

This documentation outlines how I deployed Wiki.js using Docker Compose on a Raspberry Pi 4, configured it to run securely behind an HTTPS reverse proxy using Nginx and ECC certificates, and structured the content to serve both as a personal knowledge base and technical reference.

While this project started as an internal utility, I also treat it as a showcase of my ability to design, secure, and maintain lightweight services within constrained environments — using Linux, Docker, networking principles, and scripting.


## 🖥️ Technical Details
| Property         		| Value                                                |
|---------------------|-----------------------------------------------------|
| **Hostsystem**      | [Raspberry Pi 4B (8 GB RAM)](/home-lab/Server/raspberrypi)|
| **IP-Adresse**      | 192.168.178.40 |
| **Zugriffs-URL**    | http://wiki.raspi4:4000 |
| **Responsibility**   | Leif B. (Homelab Admin) |

--- 

## Getting started
I wanted to run wiki.js in `docker compose` on my Raspberry Pi 4. I used the [official documentation](https://docs.requarks.io/install/docker) from wiki.js for the implementation.

### Setting up



## HTTPS

### Certificate creation



--- 

## ⚙️ Setup (Docker)

- `docker-compose.yml` mit Postgres
- Volumes und SSH-Key Mounts
- Konfigurationspfade

## 🔐 GitHub Integration

- SSH-Key-Generierung (ed25519)
- Mount im Container
- Wiki.js Git-Speicherkonfiguration

## 💾 Backups

- Git als primäres Backup
- Lokale tägliche Archive (Storage Target: File System)
- Struktur der Repository-Dateien

## 🛡️ Zugriff & Sicherheit

- Admin-Zugänge
- Reverse Proxy (optional)
- HTTPS / Auth

## 🧠 Tipps

- Struktur im Git (Glossar, Home, Tools...)
- Templates, CSS-Anpassung, Tabellen-Sortierung

