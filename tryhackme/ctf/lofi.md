---
title: Lo-Fi
description: 
published: true
date: 2025-07-10T12:21:52.856Z
tags: 
editor: markdown
dateCreated: 2025-07-10T12:21:52.856Z
---

# Lo-Fi

# General Information

> - Target IP: `10.10.84.219`
> - Room: [Lo-Fi](https://tryhackme.com/room/lofi)
> - Difficulty: Easy
> - Date: 2025-07-10

---

# Task
![lofi_1.png](/thm/ctf/lofi_1.png)

---

# Approach
I navigated to the page via firefox:

![lofi_2.png](/thm/ctf/lofi_2.png)

The task already provides the information, it might have to do something with a Path Traversal attack.
I clicked on one of the hyperlinks on the sidebar ("Coffee") and looked at the URL query.
`?page=coffee.php`
So the website accessed the file `coffee.php` on its file system. By default the 

/var/www/html/**\<website content>**

