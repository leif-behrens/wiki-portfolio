---
title: Migration to my public server
description: 
published: true
date: 2025-07-09T11:42:37.021Z
tags: 
editor: markdown
dateCreated: 2025-07-09T10:37:11.214Z
---

# Migration to my public server

## DNS
Created 2 records for wiki: A and AAAA
Reduced the TTL from 86400 to 300 for now during the migration

## Apache2
VirtualHost
```apache
<VirtualHost *:80>
  ServerName wiki.leifbehrens.de
  Redirect permanent / https://wiki.leifbehrens.de/
</VirtualHost>

<VirtualHost *:443>
  ServerName wiki.leifbehrens.de
  SSLEngine on
  SSLCertificateFile /etc/letsencrypt/live/wiki.leifbehrens.de/fullchain.pem
  SSLCertificateKeyFile  /etc/letsencrypt/live/wiki.leifbehrens.de/privkey.pem

  Header always set Strict-Transport-Security "max-age=63072000; includeSubDomains"
  ProxyPreserveHost On
  ProxyPass / http://127.0.0.1:3000/
  ProxyPassReverse / http://127.0.0.1:3000/
  RequestHeader set X-Forwarded-Proto "https"
</VirtualHost>
```

## User creation
Created user wiki
