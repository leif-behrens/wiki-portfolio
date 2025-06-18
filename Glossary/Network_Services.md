---
title: Network Services
description: 
published: true
date: 2025-06-17T21:24:23.716Z
tags: 
editor: markdown
dateCreated: 2025-06-17T21:20:24.295Z
---

# Network Services

This section lists commonly used network-related services and protocols, along with ports and encryption status.
<br>

| Service / Protocol | Expanded Form/Description | Protocol Type / Port(s) | Encrypted? |
|--------------------|----------------------------|---------------------------|-------------|
| BGP                | Border Gateway Protocol    | TCP / 179                 | ❌          |
| CIFS               | Common Internet File System | TCP / 445                | ❌          |
| DHCP               | Dynamic Host Configuration Protocol | UDP / 67, 68      | ❌          |
| DNS                | Domain Name System         | UDP / 53<br>TCP / 53      | ❌ (Usually) |
| FTPS               | File Transfer Protocol Secure | TCP / 990, TCP / 21     | ✅          |
| FTP                | File Transfer Protocol     | TCP / 21                  | ❌          |
| HTTP               | Hypertext Transfer Protocol | TCP / 80                 | ❌          |
| HTTPS              | HTTP Secure (HTTP over TLS/SSL) | TCP / 443           | ✅          |
| ICMP               | Internet Control Message Protocol | N/A (Layer 3)     | ❌          |
| IMAP               | Internet Message Access Protocol | TCP / 143           | ❌          |
| IMAPS              | IMAP Secure                | TCP / 993                 | ✅          |
| IPsec              | Internet Protocol Security | UDP / 500<br>ESP (50)<br>AH (51) | ✅    |
| IRC                | Internet Relay Chat        | TCP / 6660–6669, 6697 (SSL) | ❌ / ✅    |
| iSCSI              | Internet Small Computer Systems Interface | TCP / 3260   | ❌ (Optional TLS) |
| Kerberos           | Authentication Protocol    | UDP / 88<br>TCP / 88      | ✅ (partially) |
| LDAP               | Lightweight Directory Access Protocol | TCP / 389       | ❌          |
| LDAPS              | LDAP over SSL              | TCP / 636                 | ✅          |
| L2TP               | Layer 2 Tunneling Protocol | UDP / 1701                | ❌ (with IPsec: ✅) |
| MGCP               | Media Gateway Control Protocol | UDP / 2427, 2727     | ❌          |
| MQTT               | Message Queuing Telemetry Transport | TCP / 1883        | ❌ (TLS optional) |
| NFS                | Network File System        | TCP / 2049                | ❌          |
| NNTP               | Network News Transfer Protocol | TCP / 119            | ❌          |
| NTP                | Network Time Protocol      | UDP / 123                 | ❌          |
| POP3               | Post Office Protocol v3    | TCP / 110                 | ❌          |
| POP3S              | POP3 Secure                | TCP / 995                 | ✅          |
| PPTP               | Point-to-Point Tunneling Protocol | TCP / 1723        | ❌ (Deprecated) |
| RADIUS             | Remote Authentication Dial-In User Service | UDP / 1812, 1813 | ❌ (with IPsec or TLS: ✅) |
| Redis              | Remote Dictionary Server   | TCP / 6379                | ❌          |
| RDP                | Remote Desktop Protocol    | TCP / 3389                | ✅          |
| RIP                | Routing Information Protocol | UDP / 520              | ❌          |
| RPC                | Remote Procedure Call      | TCP / 135<br>Dynamic Ports | ❌          |
| RTMP               | Real-Time Messaging Protocol | TCP / 1935             | ❌          |
| RTP                | Real-time Transport Protocol | UDP / 5004–5005         | ❌          |
| SFTP               | SSH File Transfer Protocol | TCP / 22                  | ✅          |
| SIP                | Session Initiation Protocol | UDP/TCP / 5060<br>5061 (TLS) | ❌ / ✅ |
| SMB                | Server Message Block (Samba) | TCP / 139, 445         | ❌          |
| SNMP               | Simple Network Management Protocol | UDP / 161, 162   | ❌          |
| SMTP               | Simple Mail Transfer Protocol | TCP / 25              | ❌          |
| SMTPS              | SMTP Secure (via SSL)      | TCP / 465                 | ✅          |
| SNTP               | Simple Network Time Protocol | UDP / 123              | ❌          |
| SQL Server         | Microsoft SQL Server       | TCP / 1433, 1434          | ❌          |
| SSH                | Secure Shell               | TCP / 22                  | ✅          |
| Telnet             | Telnet                     | TCP / 23                  | ❌          |
| TFTP               | Trivial File Transfer Protocol | UDP / 69             | ❌          |
| VNC                | Virtual Network Computing  | TCP / 5900                | ❌ (Optional TLS) |
| VPN                | Virtual Private Network (generic) | Various (e.g., UDP 1194 OpenVPN) | ✅ |
| WebDAV             | Web Distributed Authoring and Versioning | TCP / 80, 443  | ✅ (if over HTTPS) |
| XMPP               | Extensible Messaging and Presence Protocol | TCP / 5222, 5223 | ✅ (optional) |


