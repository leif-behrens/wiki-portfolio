---
title: Boogeyman 1
description: 
published: true
date: 2025-08-08T15:07:37.291Z
tags: 
editor: markdown
dateCreated: 2025-08-08T14:34:09.156Z
---

# Boogeyman 1

https://tryhackme.com/room/boogeyman1

## Introduction - New threat in town

*Uncover the secrets of the new emerging threat, the Boogeyman.*

In this room, you will be tasked to analyse the Tactics, Techniques, and Procedures (TTPs) executed by a threat group, from obtaining initial access until achieving its objective. 

Investigation Platform

Before we proceed, deploy the attached machine by clicking the Start Machine button in the upper-right-hand corner of the task. It may take up to 3-5 minutes to initialise the services.

The machine will start in a split-screen view. In case the VM is not visible, use the blue Show Split View button at the top-right of the page.

### Artefacts

For the investigation proper, you will be provided with the following artefacts:

- Copy of the phishing email (dump.eml)
- Powershell Logs from Julianne's workstation (powershell.json)
- Packet capture from the same workstation (capture.pcapng)

Note: The powershell.json file contains JSON-formatted PowerShell logs extracted from its original evtx file via the evtx2json tool.

You may find these files in the /home/ubuntu/Desktop/artefacts directory.

### Tools

The provided VM contains the following tools at your disposal:

- Thunderbird - a free and open-source cross-platform email client.
- LNKParse3 - a python package for forensics of a binary file with LNK extension.
- Wireshark - GUI-based packet analyser.
- Tshark - CLI-based Wireshark. 
- jq - a lightweight and flexible command-line JSON processor.

To effectively parse and analyse the provided artefacts, you may also utilise built-in command-line tools such as:

- grep
- sed
- awk
- base64

Now, let's start hunting the Boogeyman!

---
<br>

## 1. Email Analysis - Look at the headers!

Julianne, a finance employee working for Quick Logistics LLC, received a follow-up email regarding an unpaid invoice from their business partner, B Packaging Inc. Unbeknownst to her, the attached document was malicious and compromised her workstation.

![0_1.png](/thm/challenges/boogeyman_1/0_1.png)

The security team was able to flag the suspicious execution of the attachment, in addition to the phishing reports received from the other finance department employees, making it seem to be a targeted attack on the finance team. Upon checking the latest trends, the initial TTP used for the malicious attachment is attributed to the new threat group named Boogeyman, known for targeting the logistics sector.

You are tasked to analyse and assess the impact of the compromise.

---
<br>

### 1.1 What is the email address used to send the phishing email?

I used `cat` and `grep` to extract the sending email address:

![1_1.png](/thm/challenges/boogeyman_1/1_1.png)

> `agriffin@bpakcaging.xyz`
{.is-success}

### 1.2 What is the email address of the victim?

Same approach as the question before:

![2_1.png](/thm/challenges/boogeyman_1/2_1.png)

> `julianne.westcott@hotmail.com`
{.is-success}

### 1.3 What is the name of the third-party mail relay service used by the attacker based on the DKIM-Signature and List-Unsubscribe headers?

The information is written in the header of the mail. I read the mail with `cat` and used `head -n 50` to get the first 50 lines of the mail. I found the DKIM-Signature of the third-party mail relay service:

![3_1.png](/thm/challenges/boogeyman_1/3_1.png)

> elasticemail
{.is-success}

### 1.4 What is the name of the file inside the encrypted attachment?

To get the attachment of the mail I finally opened the mail in Thunderbird and downloaded the zip-file. Then I opened it (and I presume that I'm working on a secure, sandboxed environment) and saw the name of the file that is inside the archive: 

![4_1.png](/thm/challenges/boogeyman_1/4_1.png)

> Invoice_20230103.lnk
{.is-success}
