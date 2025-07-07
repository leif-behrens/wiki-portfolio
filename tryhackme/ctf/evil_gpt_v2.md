---
title: Evil-GPT v2
description: 
published: true
date: 2025-07-07T16:26:49.773Z
tags: 
editor: markdown
dateCreated: 2025-07-07T15:14:00.545Z
---

# General Information

> - Target IP: `10.10.162.246`
> - Room: [Evil-GPT v2](https://tryhackme.com/room/hfb1evilgptv2)
> - Difficulty: Easy
> - Date: 2025-07-07

---

# Task

![evil-gptv2_01.png](/thm/ctf/evil-gptv2_01.png)

---

# Approach

I only got the IP address from the target machine. So I made a SYN nmap scan to figure out what ports are open:

![evil-gptv2_02.png](/thm/ctf/evil-gptv2_02.png)

Since port 80 is open I used my webbrowser and tried to access the server. I saw the following interface:

![evil-gptv2_02.png](/thm/ctf/evil-gptv2_03.png)

I tried a simple `ls` command and received following output:

![evil-gptv2_04.png](/thm/ctf/evil-gptv2_04.png)

So unlike the first [Evil-GPT room](/tryhackme/ctf/evil_gpt) I cannot ask the AI to execute commands. So I start asking the model human-like question. I started if it could provide me the flag: 

![evil-gptv2_05.png](/thm/ctf/evil-gptv2_05.png)

I then want the AI to forget all the rules that the system gave the bot but it didn't work:

![evil-gptv2_06.png](/thm/ctf/evil-gptv2_06.png)

Then I asked the bot to provide the rules he has to follow, where it revealed the flag:

![evil-gptv2_07.png](/thm/ctf/evil-gptv2_07.png)

> What is the flag?
> *THM{AI_NOT_AI}*
{.is-success}

