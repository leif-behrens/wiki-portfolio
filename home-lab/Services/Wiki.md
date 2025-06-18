---
title: Wiki.js
description: 
published: true
date: 2025-06-18T21:22:41.143Z
tags: 
editor: markdown
dateCreated: 2025-06-18T10:26:51.405Z
---

# Running Wiki.js Locally in Docker on Raspberry Pi

I wanted a way to document my technical projects and create a personal knowledge base. After looking into different options, I came across Wiki.js and found that it supports various self-hosting methods — including Docker.

Since I’ve recently started working more with Docker and wanted to deepen my understanding, I decided to run Wiki.js locally on my Raspberry Pi inside a container.

<br>

## 🖥️ Technical Details
| Property | Value |
|---|---|
| **Hostsystem** | [Raspberry Pi 4B (8 GB RAM)](/home-lab/Server/raspberrypi)|
| **IP-Adresse** | 192.168.178.40 |
| **Zugriffs-URL** | https://wiki.raspi4:4000 |

<br>

## Getting started
As already mentioned in the beginning I wanted to run wiki.js in a docker container. I used the [official documentation](https://docs.requarks.io/install/docker) from wiki.js for the implementation.

---
<br>

### Setting up the Raspberry Pi
I have already installed Docker on my Rasperry Pi, as I have already run MISP at another time. At that time, I had already created the user **docker** on my Raspberry Pi, in whose context my Docker containers run. So I just created a new folder in the home directory `/home/docker/wikisj-docker` in which Wiki.js should run.

<br>

### Setting up docker compose
To manage the setup cleanly and handle the connection to the PostgreSQL database, I used Docker Compose.
I created the `docker-compose.yml` file, copied the information from the official documentation into this file and changed some parameters.
By default, or as stated in the official documentation, sample credentials were in plain text in `docker-compose.yml`. I have moved these to an `.env` file and access them with the notation `${<variable>}`.
I changed the port from `“80:3000”` to `“3000:3000”` as port 80 is already used elsewhere on my Raspberry Pi.


```yaml
services:

  db:
    image: postgres:15-alpine
    environment:
      POSTGRES_DB: ${POSTGRES_DB}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
      POSTGRES_USER: ${POSTGRES_USER}
    logging:
      driver: none
    restart: unless-stopped
    volumes:
      - db-data:/var/lib/postgresql/data

  wiki:
    image: ghcr.io/requarks/wiki:2
    depends_on:
      - db
    environment:
      DB_TYPE: ${DB_TYPE}
      DB_HOST: ${DB_HOST}
      DB_PORT: ${DB_PORT}
      DB_USER: ${DB_USER}
      DB_PASS: ${DB_PASS}
      DB_NAME: ${DB_NAME}
    restart: unless-stopped
    ports:
      - "3000:3000"

volumes:
  db-data:
```

Then I pulled the images with `docker compose pull` and wanted to run the containers with `docker compose up -d`. I kept getting error (I don't remember the exact error). Then I tried to use the default `docker-compose.yml` from the official documentation, with the given credentials and just changed the receiving port. It was a success 


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

