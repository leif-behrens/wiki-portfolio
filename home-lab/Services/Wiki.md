---
title: Wiki.js
description: 
published: true
date: 2025-06-19T18:22:15.401Z
tags: 
editor: markdown
dateCreated: 2025-06-18T10:26:51.405Z
---

# Wiki.js – Self-hosted Knowledge Platform
I wanted a way to document my technical projects and create a personal knowledge base. Someone recommended Wiki.js and found that it supports various self-hosting methods, including Docker.

Since I had already started working more with Docker and wanted to deepen my knowledge, I decided to run Wiki.js locally on my Raspberry Pi using containers.

This section documents the entire implementation and configuration of my self-hosted Wiki.js

- [Setup](/home-lab/Services/Wiki/Setup)
- [Configure HTTPS](/home-lab/Services/Wiki/HTTPS)
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



---

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

