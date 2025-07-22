---
title: ItsyBitsy
description: 
published: true
date: 2025-07-22T20:02:12.886Z
tags: 
editor: markdown
dateCreated: 2025-07-22T15:11:47.632Z
---

# ItsyBitsy


10.10.201.130

Medium
https://tryhackme.com/room/itsybitsy


## Scenario

During normal SOC monitoring, Analyst John observed an alert on an IDS solution indicating a potential C2 communication from a user Browne from the HR department. A suspicious file was accessed containing a malicious pattern `THM:{ ________ }`. A week-long HTTP connection logs have been pulled to investigate. Due to limited resources, only the connection logs could be pulled out and are ingested into the connection_logs index in Kibana.

Our task in this room will be to examine the network connection logs of this user, find the link and the content of the file, and answer the questions.


## How many events were returned for the month of March 2022?
1482


## What is the IP associated with the suspected user in the logs?

There were 2 possible IPs. I assumed the IP with more traffic would be the suspicious one, that is communicating with the C2 server. But I was wrong, the IP with just 2 log entries was associated with the suspected user. But if you look closer to the connections of the host 192.166.65.52 you see all regular common user agents (Mozilla/5.0). The host 192.166.65.54 has a suspicious user agent (bitsadmin) which is an indicator that it's not a regular http connection of a user via browser.
