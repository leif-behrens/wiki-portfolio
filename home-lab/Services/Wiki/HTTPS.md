---
title: HTTPS
description: 
published: true
date: 2025-06-19T11:31:47.203Z
tags: 
editor: markdown
dateCreated: 2025-06-19T10:27:40.620Z
---

# HTTPS
In this section I documented the implementation of HTTPS.

## DNS
I wanted the rasp

## Self-Signed Certificate
### Background
Before my Wiki.js was accessable just via unencrypted HTTP and I wanted to enhance the security by enabling encrypted HTTP traffic with TLS. Since my Raspberry Pi is in a private network and only accessible internally in my home network, I implemented a self-signed Certificate.

### Generation
First of all I decided to use an ECC (Elliptic Curve Cryptography) algorithm for the key generation because it's a secure and less resource consumptive as RSA even with a smaller key. In my small home lab and with very little going on in here, it's not as important but I want to make good choices and correct approaches to internalize such things.

With the following command I generated a private key (`-genkey`) with the secure **NIST P-256** (`prime256v1`) elliptic curve and got the output in the file `wiki.key`.

```bash
openssl ecparam -name prime256v1 -genkey -noout -out wiki.key
```

With previous generated private key I generated a self-signed X.509 certificate that lasts 5 years like this:

```bash
openssl req -new -x509 -key wiki.key -out wiki.crt -days 1825 -subj "/CN=wiki.raspi4"
```


## Setting up a Reverse Proxy

## Reconfigure Docker Compose


