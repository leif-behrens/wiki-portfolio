---
title: Wiki.js
description: 
published: true
date: 2025-06-18T10:56:59.884Z
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
| **Zugriffs-URL**    | http://wiki.raspi4:3000 |
| **Responsibility**   | Leif B. (Homelab Admin) |

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

