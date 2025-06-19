---
title: CTF - Level One
description: 
published: true
date: 2025-06-19T19:39:51.723Z
tags: 
editor: markdown
dateCreated: 2025-06-19T19:39:51.723Z
---

# General information
IP address of the target machine: **10.10.220.25**

SSH username: *ctf*
SSH password: *ctf*

THM Room: https://tryhackme.com/room/ctflevelone

---

# File System Flags
## 1. File System Flag

I logged into the target machine by using `ssh ctf@10.10.220.25`

Due to the [instruction](https://www.notion.so/Cybersecurity-Capture-The-Flag-1-CTF-Overview-1c39418319f38068aee5e70ff5cffe9c?pvs=21), the first file system flag is *find_flag.txt*

I ran the command `find / -name "find_flag.txt" 2>/dev/null`

![file_system_flag_1.png](/thm/file_system_flag_1.png)

Found Flag: ***{F1nd_Fl4g_Fun}***
<br>

## 2. File System Flag

With `ls -a` in the home directory of the user *ctf* it listed all files/directories, including hidden files/directories. I found *.f.txt*, where I found the second flag.

![file_system_flag_2.png](/thm/file_system_flag_2.png)

Found Flag: ***{H1d3_1n_pl41n_s1gh7}***
<br>

## 3. File System Flag

In the directory *flag* of the home directory was a file *story.txt*

![file_system_flag_3_1.png](/thm/file_system_flag_3_1.png)

I retrieved the content of that file with`cat story.txt` and in there was the third flag.

![file_system_flag_3_2.png](/thm/file_system_flag_3_2.png)

Found Flag: ***{St0ry_Fl4g}***
<br>

## 4. File System Flag

In the directory *flag* were eight subdirectories. I navigated in the first subdirectory with the name *1* by using `cd 1`*,* listed all the files/directory in this subdirectory with `ls`and there was another directory with name *d.* Then I decided that this could go for a while and is not very efficient. Then I decided to go back into the *flag* directory and was searching for files in general through all directories and subdirectories by using `find . -type f`

I found the textfile *f_l_a_g.txt* in *flag/6/m/a/s/t/e/r/s/c/h/o/o/l/* that contained the last file system flag:

![file_system_flag_4.png](/thm/file_system_flag_4.png)

Found Flag: ***{Y0u_G0T_1t}***

---

# Hash Flags
The directory *hash_to_crack* contained following files:

![hash_flag_general.png](/thm/hash_flag_general.png)

To get all the files I tried using an ftp connection with the ctf-user and downloaded all the files in *hash_to_crack.* Then I was able to use the tools installed on my attackbox *hashid* to get the hash algorithm that was used for each hash and *john the ripper* for cracking the hash.

## 1. Hash Flag

![hash_flag_1.png](/thm/hash_flag_1.png)

The hash algorithm for the first flag was probably MD2, MD5 or MD4. I tried MD5 first. 

I ran the following command using john the ripper and the downloaded wordlist *wordlist.txt* from the target server: 

`john --format=raw-md5 --wordlist=wordlist.txt hash1.txt`

![hash_flag_1_2.png](/thm/hash_flag_1_2.png)

Found Flag: ***C0d3_0b5cur3r_Flag***
<br>

## 2. Hash Flag

I used the same procedure as I did for the first hash flag.

![hash_flag_2_1.png](/thm/hash_flag_2_1.png)

`john --format=raw-sha1--wordlist=wordlist.txt hash2.txt`

![hash_flag_2_2.png](/thm/hash_flag_2_2.png)

Found Flag: ***C0d3_5l4y3r_Flag***
<br>

## 3. Hash Flag

![hash_flag_3_1.png](/thm/hash_flag_3_1.png)

`john --format=raw-sha512--wordlist=wordlist.txt hash3.txt`

![hash_flag_3_2.png](/thm/hash_flag_3_2.png)

Found Flag: ***H4ck3r_Flag***
<br>

## 4. Hash Flag

![hash_flag_4_1.png](/thm/hash_flag_4_1.png)

`john --format=raw-sha256--wordlist=wordlist.txt hash4.txt`

![hash_flag_4_2.png](/thm/hash_flag_4_2.png)

Found Flag: ***L0ck_Flag***
<br>

## 5. Hash Flag

![hash_flag_5_1.png](/thm/hash_flag_5_1.png)

`john --format=raw-md5--wordlist=wordlist.txt hash5.txt`

![hash_flag_5_2.png](/thm/hash_flag_5_2.png)

Found Flag: ***S3cur1ty_Flag***

---

# Webpage Flags
## 1. Webpage Flag

I navigated to the target machine using firefox and found the first flag.

![webpage_flags_1.png](/thm/webpage_flags_1.png)

Found Flag: ***{STUDENT_CTF_Web}***
<br>

## 2. Webpage Flag

I opened the development tools in firefox (F12) and there were comments in the html structure. This was the second flag.

![webpage_flags_2.png](/thm/webpage_flags_2.png)

Found Flag: ***{Another_Web_Flag}***
<br>

## 3. Webpage Flag

The directory where the webserver is located is`/var/www/html`

I navigated to this directory with my existing ssh-session and listed all the files and directories by using `ls`.

![webpage_flags_3_1.png](/thm/webpage_flags_3_1.png)

First I visited *http://10.10.220.25/hide.html* and found the 3. webpage flag:

![webpage_flags_3_2.png](/thm/webpage_flags_3_2.png)

Found Flag: ***{H1d3_Fl4g}***
<br>

## 4. Webpage Flag

In the */var/www/html* folder was also *index2.html* which I opened in my browser. There was the Apache2 default page but modified with the fourth flag.

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

![image.png](attachment:7cc38c68-69ae-4911-878a-689969479fb3:image.png)

No idea how to get the password for the files.zip. It’s not a common password in a known wordlist list like *rockyou.txt.*

I found the password in an CTF Walkthrough (https://medium.com/@ronjvo/masterschool-ctf-d4849d3c5bf1) because I had no idea how to find it. The password was ***Masterschool***

![image.png](attachment:0f1b01b8-7afc-4073-8d51-1f68f435bb97:image.png)

The other zip-file also required a password:

![image.png](attachment:df587c3e-1ebe-402e-b9e3-43a68149dfad:image.png)

I extracted the used hash or encryptionkey of *secret.zip* with zip2john and saved the output to a new file *secret.txt*:

![image.png](attachment:c2a830b5-f598-42ec-bc4a-a4e186ea40c8:image.png)

Then I tried to get the password for *secret.zip* by using john the ripper and the extracted wordlist of *files.zip:*

![image.png](attachment:31c2589d-41e0-43ce-a14f-387f1fd9a2fb:image.png)

The password was ***CTF_TIME***

I unzipped the *secret.zip* file with the cracked password and in this zip archive was the file *john_flag.txt,* which contained the last flag:

![image.png](attachment:49bc51a5-5a8d-46de-aabb-2b7171a30ed2:image.png)

John flag: ***{LetMe1n123!@#}***