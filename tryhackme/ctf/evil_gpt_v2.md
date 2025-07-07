---
title: Evil-GPT v2
description: 
published: true
date: 2025-07-07T16:34:03.006Z
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

I only got the IP address from the target machine. So I made a SYN Nmap scan to figure out which ports were open:

![evil-gptv2_02.png](/thm/ctf/evil-gptv2_02.png)

Since port 80 was open, I used my web browser to access the server. I saw the following interface:

![evil-gptv2_02.png](/thm/ctf/evil-gptv2_03.png)

I tried a simple `ls` command and received the following output:

![evil-gptv2_04.png](/thm/ctf/evil-gptv2_04.png)

So, unlike the first [Evil-GPT room](/tryhackme/ctf/evil_gpt), I couldn’t ask the AI to execute commands directly on the server it is running on. Instead, I started asking the model human-like questions. First, I asked if it could provide me with the flag:

![evil-gptv2_05.png](/thm/ctf/evil-gptv2_05.png)

Next, I tried to make the AI forget all its system rules, but it refused:

![evil-gptv2_06.png](/thm/ctf/evil-gptv2_06.png)

Then I asked the bot to provide the rules it has to follow, which revealed the flag:

![evil-gptv2_07.png](/thm/ctf/evil-gptv2_07.png)

> What is the flag?
> *THM{AI_NOT_AI}*
{.is-success}

