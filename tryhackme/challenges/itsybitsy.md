---
title: ItsyBitsy
description: 
published: true
date: 2025-07-22T20:36:42.759Z
tags: 
editor: markdown
dateCreated: 2025-07-22T15:11:47.632Z
---

# ItsyBitsy

> **Date**: 2025-07-22
> **Difficulty**: ~~Unknown~~ | ~~Easy~~ | Medium | ~~Hard~~
> **Reference**: https://tryhackme.com/room/itsybitsy

---
<br> 

## Scenario

During normal SOC monitoring, Analyst John observed an alert on an IDS solution indicating a potential C2 communication from a user Browne from the HR department. A suspicious file was accessed containing a malicious pattern `THM:{ ________ }`. A week-long HTTP connection logs have been pulled to investigate. Due to limited resources, only the connection logs could be pulled out and are ingested into the connection_logs index in Kibana.

Our task in this room will be to examine the network connection logs of this user, find the link and the content of the file, and answer the questions.

---
<br>

### 1. How many events were returned for the month of March 2022?
I just set the time filter to March 1^st^ - March 31^st^:

![1_1.png](/thm/challenges/itsybitsy/1_1.png)

> 1482
{.is-success}

---
<br>

### 2. What is the IP associated with the suspected user in the logs?

There were 2 possible IPs. I assumed the IP with more traffic would be the suspicious one, that is communicating with the C2 server. But I was wrong, the IP with just 2 log entries was associated with the suspected user. But if you look closer to the connections of the host 192.166.65.52 you see all regular common user agents (Mozilla/5.0). The host 192.166.65.54 has a suspicious user agent (bitsadmin) which is an indicator that it's not a regular http connection of a user via browser.

![2_1.png](/thm/challenges/itsybitsy/2_1.png)


![2_2.png](/thm/challenges/itsybitsy/2_2.png)
^192.166.65.52^

![3_1.png](/thm/challenges/itsybitsy/3_1.png)
^192.166.65.54^

> 192.166.65.54
{.is-success}

---
<br>

### 3. The user’s machine used a legit windows binary to download a file from the C2 server. What is the name of the binary?

It was the user agent I mentioned in question 2 that has been used to download this file from the C2 server.

![3_1.png](/thm/challenges/itsybitsy/3_1.png)

> bitsadmin
{.is-success}

---
<br>

### 4. The infected machine connected with a famous filesharing site in this period, which also acts as a C2 server used by the malware authors to communicate. What is the name of the filesharing site?

According to the log the host is `pastebin.com` as you can see in the following screenshot:
![4_1.png](/thm/challenges/itsybitsy/4_1.png)

> pastebin.com
{.is-success}

---
<br>

### 5. What is the full URL of the C2 to which the infected host is connected?

The full URL is just the host and the URI that you can see in the log:

![5_1.png](/thm/challenges/itsybitsy/5_1.png)

> pastebin.com/yTg0Ah6a
{.is-success}

---
<br>

### 6. A file was accessed on the filesharing site. What is the name of the file accessed?

I opened the mentioned URL of question 5 (*pastebin.com/yTg0Ah6a*) and there was a text file uploaded:

![6_1.png](/thm/challenges/itsybitsy/6_1.png)

> secret.txt
{.is-success}

---
<br>

### 7 The file contains a secret code with the format THM{_____}.

The content of the file is `THM{SECRET__CODE}` as you can see in the following screenshot:

![7_1.png](/thm/challenges/itsybitsy/7_1.png)

> `THM{SECRET__CODE}`
{.is-success}


