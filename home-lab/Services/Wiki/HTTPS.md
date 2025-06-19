---
title: HTTPS
description: 
published: true
date: 2025-06-19T12:39:05.772Z
tags: 
editor: markdown
dateCreated: 2025-06-19T10:27:40.620Z
---

# HTTPS
In this section I documented the implementation of HTTPS.

## DNS
I wanted the Wiki to be accessable with the subdomain https://wiki.raspi4 which is why I created a new DNS record on my PiHole DNS server.

## Self-Signed Certificate
### Background
Before my Wiki.js was accessable just via unencrypted HTTP and I wanted to enhance the security by enabling encrypted HTTP traffic with TLS. Since my Raspberry Pi is in a private network and only accessible internally in my home network, I implemented a self-signed Certificate.

### Generation
First of all I decided to use an ECC (Elliptic Curve Cryptography) algorithm for the key generation because it's a secure and less resource consumptive as RSA even with a smaller key. In my small home lab and with very little going on in here, it's not as important but I want to make good choices and correct approaches to internalize such things.

With the following command I generated a private key (`-genkey`) with the secure **NIST P-256** (`prime256v1`) elliptic curve and got the output in the file `wiki.key`.

```bash
openssl ecparam -name prime256v1 -genkey -noout -out wiki.key
```

With previous generated private key, first I created a new directory where I want my certificate should be placed. I generated a self-signed X.509 certificate that lasts 5 years like this:

```bash
sudo mkdir -p /etc/wiki/certs
cd /etc/wiki/certs
openssl req -new -x509 -key wiki.key -out wiki.crt -days 1825 -subj "/CN=wiki.raspi4"
```

---
<br>

## Setting up a Reverse Proxy
I decided to implement a reverse proxy with *nginx* that listens to port 4000 and receives every requests from a client, terminates the TLS encryption, checks the certificate and forwards the request to the docker container.

### nginx Installation
I installed nginx with the following command:

```bash
sudo apt update && sudo apt install nginx -y
```

### Configure nginx
I created the file `/etc/nginx/sites-available/wiki` and wrote the configuration file (with the help from ChatGPT):

```nginx
server {
    listen 4000 ssl;
    server_name wiki.raspi4;

    ssl_certificate     /etc/wiki/certs/wiki.crt;
    ssl_certificate_key /etc/wiki/certs/wiki.key;

    location / {
        proxy_pass         http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header   Host $host;
        proxy_set_header   X-Real-IP $remote_addr;
        proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header   X-Forwarded-Proto $scheme;
    }
}
```

Then I activated the wiki by creating a symbolic link to the `sites-available`, removed the default page (which is listening to port 80, which is already occupied), tested the configuration and reloaded *nginx*:

```bash
sudo ln -s /etc/nginx/sites-available/wiki /etc/nginx/sites-enabled/wiki
sudo rm /etc/nginx/sites-enabled/default
sudo nginx -t && sudo systemctl reload nginx
```

---
<br>

## Reconfigure Docker Compose
To make the Wiki.js only available via HTTPS and through the reverse proxy, I had to make a little change in my `docker-compose.yml` file.
From: 
```yaml
ports:
	- "3000:3000"
```
to 
```yaml
ports:
	- "127.0.0.1:3000:3000"
```

This way the container is only available from localhost e.g. the Raspberry Pi itself. 
