---
title: Wiki.js
description: 
published: true
date: 2025-06-19T10:06:16.154Z
tags: 
editor: markdown
dateCreated: 2025-06-18T10:26:51.405Z
---

# Wiki.js – Self-hosted Knowledge Platform

This section documents the setup, configuration, hardening, and GitHub integration of my self-hosted Wiki.js instance.

- [Setup](/home-lab/Services/Wiki/Setup)
- [Configuration](./Configuration.md)
- [Hardening](./Hardening.md)
- [GitHub Integration](./GitHub_Integration.md)
- [Scripts](./Scripts.md)



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

