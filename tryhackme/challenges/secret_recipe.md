---
title: Secret Recipe
description: 
published: true
date: 2025-08-07T10:16:25.844Z
tags: 
editor: markdown
dateCreated: 2025-08-07T07:58:23.024Z
---

# Secret Recipe

> **Date**: 2025-08-07  
> **Difficulty**: ~~Unknown~~ | ~~Easy~~ | Medium | ~~Hard~~  
> **Reference**: https://tryhackme.com/room/registry4n6

---
<br> 

## Storyline

Jasmine owns a famous New York coffee shop Coffely which is famous city-wide for its unique taste. Only Jasmine keeps the original copy of the recipe, and she only keeps it on her work laptop. Last week, James from the IT department was consulted to fix Jasmine's laptop. But it is suspected he may have copied the secret recipes from Jasmine's machine and is keeping them on his machine. Image showing a Laptop with a magnifying glass

His machine has been confiscated and examined, but no traces could be found. The security department has pulled some important registry artifacts from his device and has tasked you to examine these artifacts and determine the presence of secret files on his machine.

---
<br> 

### 1. What is the computer name of the machine found in the registry?

Registry Explorer  
Load the SYSTEM Hive  
ROOT\ControlSet001\Control\ComputerName\ComputerName

![1_1.png](/thm/challenges/secret_recipe/1_1.png)

> JAMES  
{.is-success}

---
<br> 


### 2. When was the Administrator account created on this machine? (Format: yyyy-mm-dd hh:mm:ss)

Registry Explorer  
Load the SAM Hive  
ROOT\SAM\Domains\Users

![2_1.png](/thm/challenges/secret_recipe/2_1.png)

> 2021-03-17 14:58:48  
{.is-success}

---
<br> 

### 3. What is the RID associated with the Administrator account?

ROOT\SAM\Domains\Users

![3_1.png](/thm/challenges/secret_recipe/3_1.png)

> 500  
{.is-success}

---
<br> 

### 4. How many user accounts were observed on this machine?

ROOT\SAM\Domains\Users

![4_1.png](/thm/challenges/secret_recipe/4_1.png)

> 7  
{.is-success}

---
<br> 

### 5. There seems to be a suspicious account created as a backdoor with RID 1013. What is the account name?

ROOT\SAM\Domains\Users

![5_1.png](/thm/challenges/secret_recipe/5_1.png)

> bdoor  
{.is-success}

---
<br> 

### 6. What is the VPN connection this host connected to?

After a quick research on where to look for network connections, I found it in the following registry hive:  
Load the SOFTWARE Hive  
ROOT\Microsoft\Windows NT\CurrentVersion\NetworkList

I found one network indicating a VPN connection:

![6_1.png](/thm/challenges/secret_recipe/6_1.png)

> ProtonVPN  
{.is-success}

---
<br> 

### 7. When was the first VPN connection observed? (Format: YYYY-MM-DD HH:MM:SS)

Same hive as in the previous question.

![7_1.png](/thm/challenges/secret_recipe/7_1.png)

> 2022-10-12 19:52:36  
{.is-success}

---
<br> 

### 8. There were three shared folders observed on this machine. What is the path of the third share?

According to the [Microsoft documentation](https://learn.microsoft.com/en-us/troubleshoot/windows-client/networking/saving-restoring-existing-windows-shares), shared folders are listed in SYSTEM\CurrentControlSet\Services\LanmanServer\Shares

![8_1.png](/thm/challenges/secret_recipe/8_1.png)  
![8_2.png](/thm/challenges/secret_recipe/8_2.png)

> C:\RESTRICTED FILES  
{.is-success}

---
<br> 

### 9. What is the last DHCP IP assigned to this host?

In the SYSTEM Hive, I found under  
ROOT\ControlSet001\Services\Tcpip\Parameters\Interfaces three different interfaces that had assigned IPs:

![9_1.png](/thm/challenges/secret_recipe/9_1.png)

It was a bit unsatisfying because the correct answer is 172.31.2.197, even though the last write for this interface was before the interface with the assigned IP 10.10.210.64. I couldn't figure out why it was this network interface. But according to the THM hint and the possible answer format, it had to be 172.31.2.197.

> 172.31.2.197  
{.is-success}

---
<br> 

### 10. The suspect seems to have accessed a file containing the secret coffee recipe. What is the name of the file?

For the recent activities, I loaded the NTUSER.DAT into Registry Explorer.

The location of recent files is ROOT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs:

![10_1.png](/thm/challenges/secret_recipe/10_1.png)

> secret-recipe.pdf  
{.is-success}

---
<br> 

### 11. The suspect executed multiple commands using the Run window. What command was used to enumerate the network interfaces?

The evidence is found in the NTUSER.DAT as well:  
\ROOT\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU

![11_1.png](/thm/challenges/secret_recipe/11_1.png)

> pnputil /enum-interfaces  
{.is-success}

---
<br> 

### 12. The user searched for a network utility tool to transfer files using the file explorer. What is the name of that tool?

The evidence is found in the NTUSER.DAT as well:  
\ROOT\Software\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery

![12_1.png](/thm/challenges/secret_recipe/12_1.png)

> netcat  
{.is-success}

---
<br> 

### 13. What is the recent text file opened by the suspect?

Recent files are stored in ROOT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\\.txt of the NTUSER.DAT hive:

![13_1.png](/thm/challenges/secret_recipe/13_1.png)

> secret-code.txt  
{.is-success}

---
<br> 

### 14. How many times was PowerShell executed on this host?

I checked the NTUSER.DAT hive in Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist and clicked through all the subkeys. In the key {CEBFF5CD-ACE2-4F4F-9178-9926F41749EA}\count, I found the different programs that were executed with a counter. I filtered for "powershell" and found the answer:

![14_1.png](/thm/challenges/secret_recipe/14_1.png)

> 3  
{.is-success}

---
<br> 

### 15. The suspect also executed a network monitoring tool. What is the name of the tool?

In the same key as in question 14, I searched through the program names, set the filter for "Run Count" in Registry Explorer to >= 1, and noticed Wireshark, which is a network monitoring tool:

![15_1.png](/thm/challenges/secret_recipe/15_1.png)

> wireshark
{.is-success}

---
<br> 

### 16. Registry Hives also note the amount of time a process is in focus. Examine the Hives and confirm for how many seconds ProtonVPN was executed?

In the same key as both questions before, you can see the "Focus Time". I filtered for "proton" in the program name and the focus time was 5 minutes and 43 seconds (343 seconds):

![16_1.png](/thm/challenges/secret_recipe/16_1.png)

> 343
{.is-success}

---
<br> 

### 17. Everything.exe is a utility used to search for files in a Windows machine. What is the full path from which everything.exe was executed?

![17_1.png](/thm/challenges/secret_recipe/17_1.png)

> C:\Users\Administrator\Downloads\tools\Everything\Everything.exe  
{.is-success}
