---
title: CTF - Level One
description: 
published: true
date: 2025-06-19T20:38:23.814Z
tags: 
editor: markdown
dateCreated: 2025-06-19T19:39:51.723Z
---

# General information
- Target IP: `10.10.220.25`
- SSH Username: `ctf`
- SSH Password: `ctf`
- Room: [CTF Level One](https://tryhackme.com/room/ctflevelone)

---

# File System Flags
## 1. File System Flag

I logged into the target machine by using:

`ssh ctf@10.10.220.25`

According to the [instruction](https://www.notion.so/Cybersecurity-Capture-The-Flag-1-CTF-Overview-1c39418319f38068aee5e70ff5cffe9c?pvs=21), the first file system flag was located in a file named *find_flag.txt*.

I ran the command:

`find / -name "find_flag.txt" 2>/dev/null`

![file_system_flag_1.png](/thm/file_system_flag_1.png)

> Found Flag: ***{F1nd_Fl4g_Fun}***
{.is-success}

<br>

## 2. File System Flag

With `ls -a` in the home directory of the user `ctf`, I listed all files/directories, including hidden ones. I found `.f.txt`, which contained the second flag.

![file_system_flag_2.png](/thm/file_system_flag_2.png)

> Found Flag: ***{H1d3_1n_pl41n_s1gh7}***
{.is-success}

<br>

## 3. File System Flag

In the `flag` directory of the home folder, there was a file named `story.txt`.

![file_system_flag_3_1.png](/thm/file_system_flag_3_1.png)

I retrieved its content with:

`cat story.txt`

![file_system_flag_3_2.png](/thm/file_system_flag_3_2.png)

> Found Flag: ***{St0ry_Fl4g}***
{.is-success}

<br>

## 4. File System Flag

In the `flag` directory, there were eight subdirectories. I navigated into the first one, named `1`, using:

`cd 1`

and listed its contents with: 

`ls`

There was another directory named `d`. I realized that this manual approach could go on for a while and wasn't efficient.
I went back to the `flag` directory and searched for files in all subdirectories with:

`find . -type f`

I found a file `f_l_a_g.txt` in `flag/6/m/a/s/t/e/r/s/c/h/o/o/l/` that contained the last file system flag.

![file_system_flag_4.png](/thm/file_system_flag_4.png)

> Found Flag: ***{Y0u_G0T_1t}***
{.is-success}

---

# Hash Flags
The directory *hash_to_crack* contained following files:

![hash_flag_general.png](/thm/hash_flag_general.png)

To retrieve all files, I used an FTP connection with the `ctf` user and downloaded the contents of `hash_to_crack`. Then I used tools on my attackbox: `hashid` to identify the hashing algorithm and `john the ripper` to crack the hashes.

## 1. Hash Flag

The hash algorithm was likely MD2, MD5, or MD4.
![hash_flag_1.png](/thm/hash_flag_1.png)

I tried MD5 first. I ran the following command using john the ripper and the downloaded wordlist `wordlist.txt` from the target server: 

`john --format=raw-md5 --wordlist=wordlist.txt hash1.txt`

![hash_flag_1_2.png](/thm/hash_flag_1_2.png)

> Found Flag: ***C0d3_0b5cur3r_Flag***
{.is-success}

<br>

## 2. Hash Flag

I used the same procedure as before.

![hash_flag_2_1.png](/thm/hash_flag_2_1.png)

`john --format=raw-sha1--wordlist=wordlist.txt hash2.txt`

![hash_flag_2_2.png](/thm/hash_flag_2_2.png)

> Found Flag: ***C0d3_5l4y3r_Flag***
{.is-success}

<br>

## 3. Hash Flag

![hash_flag_3_1.png](/thm/hash_flag_3_1.png)

`john --format=raw-sha512--wordlist=wordlist.txt hash3.txt`

![hash_flag_3_2.png](/thm/hash_flag_3_2.png)

> Found Flag: ***H4ck3r_Flag***
{.is-success}

<br>

## 4. Hash Flag

![hash_flag_4_1.png](/thm/hash_flag_4_1.png)

`john --format=raw-sha256--wordlist=wordlist.txt hash4.txt`

![hash_flag_4_2.png](/thm/hash_flag_4_2.png)

> Found Flag: ***L0ck_Flag***
{.is-success}

<br>

## 5. Hash Flag

![hash_flag_5_1.png](/thm/hash_flag_5_1.png)

`john --format=raw-md5--wordlist=wordlist.txt hash5.txt`

![hash_flag_5_2.png](/thm/hash_flag_5_2.png)

> Found Flag: ***S3cur1ty_Flag***
{.is-success}

---

# Webpage Flags
## 1. Webpage Flag

I accessed the target machine in Firefox and found the first flag.

![webpage_flags_1.png](/thm/webpage_flags_1.png)

> Found Flag: ***{STUDENT_CTF_Web}***
{.is-success}

<br>

## 2. Webpage Flag

I opened the development tools in Firefox (F12) and found comments in the HTML source code containing the second flag.

![webpage_flags_2.png](/thm/webpage_flags_2.png)

> Found Flag: ***{Another_Web_Flag}***
{.is-success}

<br>

## 3. Webpage Flag

The webserver directory was located at `/var/www/html`. I navigated to this location via my existing SSH connection and listed all the files:

```bash
cd /var/www/html
ls
```

![webpage_flags_3_1.png](/thm/webpage_flags_3_1.png)

I visited `http://10.10.220.25/hide.html` and found the third webpage flag.

![webpage_flags_3_2.png](/thm/webpage_flags_3_2.png)

> Found Flag: ***{H1d3_Fl4g}***
{.is-success}

<br>

## 4. Webpage Flag

In the `/var/www/html` folder, there was also `index2.html`. I opened it in the browser and found a modified Apache2 default page that contained the fourth flag.

![webpage_flags_4.png](/thm/webpage_flags_4.png)

Found Flag: ***{C0nf1gur4t10n_Fl4g}***
<br>

## 5. Webpage Flag

In the */var/www/html* folder was also the file *secret.txt* which contained the next webpage flag:

![webpage_flags_5.png](/thm/webpage_flags_5.png)

Found Flag: ***{S3cr3t_Fl4g}***
<br>

## 6. Webpage Flag

In the */var/www/html* folder was also the file *robots.txt* which contained the next webpage flag:

![webpage_flags_6.png](/thm/webpage_flags_6.png)

Found Flag: ***{Robots_Flag}***
<br>

## 7. and 8. Webpage Flags

In the */var/www/html* folder was also the folder *flag*, which has another subdirectory *flag* which contained the next two flags:

![webpage_flags_7_8_general.png](/thm/webpage_flags_7_8_general.png)
<br>

### 7. Webpage Flag

![webpage_flags_7.png](/thm/webpage_flags_7.png)

Found Flag: ***{Fl4g_fl4g_fl4g}***
<br>

### 8. Webpage Flag

![webpage_flags_8.png](/thm/webpage_flags_8.png)

The content of *flag2.txt* was a base64 encoded string which I decoded with the online GitHub-Tool CyberChef:

![webpage_flags_9.png](/thm/webpage_flags_9.png)

Found Flag: ***{Fl4g2_fl4g2_fl4g2}***

---

# Other Flags

## 1. Other Flag

The first other flag was shown after starting a ssh session:

![other_flag_1.png](/thm/other_flag_1.png)

Found Flag: ***{h4ck3r5_r_us}***
<br>

## 2. Other Flag

I knew from a previous task that the target server runs an ftp service. I also tried to log in as anonymous because this user has another storage area and the login worked. In the anonymous-directory were two files - *flag.txt* and *files.zip*.

![other_flag_2_1.png](/thm/other_flag_2_1.png)

I downloaded both to my AttackBox.

![other_flag_2_2.png](/thm/other_flag_2_2.png)

The content of *flag.txt* was the next flag:

![other_flag_2_3.png](/thm/other_flag_2_3.png)

It also contained a hint, that I should know the password for *files.zip*

Found Flag: ***{ftp_server_4_lyfe}***

---

# files.zip password & John flag

The zip-file I downloaded from the ftp server before - *files.zip* - contains 2 files (*secret.zip* and *wordlist.txt*) and it required a password.

![file.zip_john_flag_1_1.png](/thm/file.zip_john_flag_1_1.png)

I had no idea how to get the password for the files.zip. It’s not a common password in a known wordlist list like *rockyou.txt.* I asked my mentor from masterschool and fellow students but they didn't know it either, how to figure it out. The hint from the previous flag "that I should know the password for *files.zip*" didn't help me either. I could've brute force it with *hydra* but this could take a long time. Thats why I searched online.

I found the password in an [CTF Walkthrough](https://medium.com/@ronjvo/masterschool-ctf-d4849d3c5bf1). The password was ***Masterschool***.

![file.zip_john_flag_1_2.png](/thm/file.zip_john_flag_1_2.png)

The other zip-file also required a password:
![file.zip_john_flag_1_3.png](/thm/file.zip_john_flag_1_3.png)

I extracted the used hash or encryptionkey of *secret.zip* with zip2john and saved the output to a new file *secret.txt*:

![file.zip_john_flag_1_9.png](/thm/file.zip_john_flag_1_9.png)

Then I tried to get the password for *secret.zip* by using john the ripper and the extracted wordlist of *files.zip:*

![file.zip_john_flag_1_6.png](/thm/file.zip_john_flag_1_6.png)

The password was ***CTF_TIME***

I unzipped the *secret.zip* file with the cracked password and in this zip archive was the file *john_flag.txt,* which contained the last flag:

![file.zip_john_flag_1_7.png](/thm/file.zip_john_flag_1_7.png)

John flag: ***{LetMe1n123!@#}***