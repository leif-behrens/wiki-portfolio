---
title: Wiki.js
description: 
published: true
date: 2025-06-19T12:12:54.856Z
tags: 
editor: markdown
dateCreated: 2025-06-18T10:26:51.405Z
---

# Wiki.js – Self-hosted Knowledge Platform
I wanted a way to document my technical projects and create a personal knowledge base. Someone recommended Wiki.js and found that it supports various self-hosting methods, including Docker.

Since I had already started working more with Docker and wanted to deepen my knowledge, I decided to run Wiki.js locally on my Raspberry Pi using containers.

This section documents the setup, configuration, hardening, and GitHub integration of my self-hosted Wiki.js instance.

- [Setup](/home-lab/Services/Wiki/Setup)
- [Configuration](./Configuration.md)
- [Hardening](./Hardening.md)
- [GitHub Integration](./GitHub_Integration.md)
- [Scripts](./Scripts.md)
<br>

# 🖥️ Technical Details
| Property | Value |
|---|---|
| **Hostsystem** | [Raspberry Pi 4B (8 GB RAM)](/home-lab/Server/raspberrypi)|
| **IP-Address** | 192.168.178.40 |
| **URL** | https://wiki.raspi4:4000 |

<br>




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

