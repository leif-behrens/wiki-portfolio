---
title: HTTPS
description: 
published: true
date: 2025-06-23T13:08:15.687Z
tags: 
editor: markdown
dateCreated: 2025-06-19T10:27:40.620Z
---

# HTTPS
This section documents how I implemented HTTPS for my local Wiki.js instance to secure traffic within my home network.

## DNS
To access Wiki.js via `https://wiki.raspi4:4000`, I created a custom DNS record using my Pi-hole DNS server.


## Self-Signed Certificate
### Background
Initially, my Wiki.js instance was only accessible via unencrypted HTTP. To improve security, I wanted to enable encrypted HTTPS using TLS. Since the Raspberry Pi is only reachable inside my private home network, I decided to use a self-signed certificate.

### Generation
I chose ECC (Elliptic Curve Cryptography) for key generation because it provides strong security with lower computational overhead compared to RSA — even with shorter key lengths.
Even though it's not strictly necessary in a small home lab, I wanted to follow good practices and develop the right mindset from the start.

With the following command I generated a private key (`-genkey`) with the secure **NIST P-256** (`prime256v1`) elliptic curve and got the output in the file `wiki.key`.

```bash
openssl ecparam -name prime256v1 -genkey -noout -out wiki.key
```

I then created a directory to store the certificate files and generated a self-signed X.509 certificate valid for five years (or 1825 days):


```bash
sudo mkdir -p /etc/wiki/certs
cd /etc/wiki/certs
openssl req -new -x509 -key wiki.key -out wiki.crt -days 1825 -subj "/CN=wiki.raspi4"
```

---
<br>

## Setting up a Reverse Proxy
I set up an *nginx* reverse proxy that listens on port 4000, terminates TLS connections, validates the certificate, and forwards requests to the Docker container.

### nginx Installation
I installed nginx with the following command:

```bash
sudo apt update && sudo apt install nginx -y
```

### Configure nginx
I created the configuration file `/etc/nginx/sites-available/wiki` with the following content (with some help of ChatGPT):

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

This ensures that only secure HTTPS traffic reaches the Wiki.js container.

---
<br>

## Docker Compose Change
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

This change ensures the container is only accessible from `localhost`, i.e., only by the Raspberry Pi itself, and not directly from the network.

## Conclusion
With this setup, all traffic to Wiki.js is now encrypted, and the service is only exposed via Nginx on port 4000 using HTTPS.
