---
title: NFS
description: 
published: true
date: 2025-06-24T08:19:24.577Z
tags: 
editor: markdown
dateCreated: 2025-06-24T07:50:20.866Z
---

# NFS

## Full Name
Network File System

## Description
NFS is a distributed file system protocol originally developed by Sun Microsystems. It allows a user on a client computer to access files over a network much like local storage is accessed. NFS enables file sharing between systems in a seamless and transparent manner.

## Protocol Type and Port(s)
- **Protocol:** TCP and UDP  
- **Ports:** 2049 (commonly used), along with various dynamic ports depending on the version and configuration

## Encryption
- Not encrypted by default  
- Encryption can be added using additional layers such as Kerberos (with NFSv4)

## Usage / Use Cases
NFS is widely used in Unix/Linux environments for sharing files across systems, particularly in enterprise networks, academic labs, and cloud environments. It is often used to:
- Mount shared directories across multiple systems
- Enable centralized file storage
- Facilitate collaboration in multi-user environments

## Security Considerations
- NFS traffic is unencrypted by default, making it vulnerable to eavesdropping if transmitted over untrusted networks
- Access control is based on client IP addresses, which can be spoofed
- NFSv4 offers enhanced security features, such as strong authentication with Kerberos and support for access control lists (ACLs)
- It is recommended to use NFS over a secure network (e.g., VPN or within an isolated LAN) or add encryption manually (e.g., via stunnel, IPsec)

## Related Protocols / Alternatives
- **SMB/CIFS:** Common alternative in Windows environments  
- **FTP / SFTP:** For file transfer rather than file system mounting  
- **WebDAV:** HTTP-based file system access  
- **AFS (Andrew File System):** Another distributed file system with stronger authentication and caching
