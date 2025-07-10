---
title: Lo-Fi
description: 
published: true
date: 2025-07-10T12:42:01.776Z
tags: 
editor: markdown
dateCreated: 2025-07-10T12:21:52.856Z
---

# Lo-Fi

# General Information

> - Target IP: `10.10.14.132`
> - Room: [Lo-Fi](https://tryhackme.com/room/lofi)
> - Difficulty: Easy
> - Date: 2025-07-10

---

# Task
![lofi_1.png](/thm/ctf/lofi_1.png)

---

# Approach

I navigated to the page using Firefox:

![lofi_2.png](/thm/ctf/lofi_2.png)

The task description suggests a path traversal attack. I clicked one of the sidebar links ("Coffee") and examined the URL query:

`?page=coffee.php`

This indicates the site loads the file coffee.php from its file system. On Linux, web pages are typically stored under:

`
/var/www/html/<website content>
`

To reach the filesystem root, I modified the query to:

`?page=../../../flag.txt`. 

I guessed the file name `flag.txt` because that is commonly used in TryHackMe CTF challenges.

| Command | Path |
| --- | --- |
|../ | /var/www |
| ../../ | /var |
| ../../../ | / |

I then retrieved the flag:

![lofi_3.png](/thm/ctf/lofi_3.png)

I must admit, I thought it would be more challenging and was surprised to find the flag so quickly. But that was the point of this challenge.

> Climb the filesystem to find the flag!
> flag{e4478e0eab69bd642b8238765dcb7d18}\
{.is-success}

