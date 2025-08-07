---
title: Secret Recipe
description: 
published: true
date: 2025-08-07T09:34:49.856Z
tags: 
editor: markdown
dateCreated: 2025-08-07T07:58:23.024Z
---

# Secret Recipe

## 1. What is the computer name of the machine found in the registry?

Registry Explorer
Load in the SYSTEM Hive
ROOT\ControlSet001\Control\ComputerName\ComputerName

![1_1.png](/thm/challenges/secret_recipe/1_1.png)

> JAMES
{.is-success}


## 2. When was the Administrator account created on this machine? (Format: yyyy-mm-dd hh:mm:ss)

Registry Explorer
Load in the SAM Hive
ROOT\SAM\Domains\Users

![2_1.png](/thm/challenges/secret_recipe/2_1.png)

> 2021-03-17 14:58:48
{.is-success}


## 3. What is the RID associated with the Administrator account?

ROOT\SAM\Domains\Users

![3_1.png](/thm/challenges/secret_recipe/3_1.png)


> 500
{.is-success}

## 4. How many user accounts were observed on this machine?

ROOT\SAM\Domains\Users

![4_1.png](/thm/challenges/secret_recipe/4_1.png)

> 7
{.is-success}

## 5. There seems to be a suspicious account created as a backdoor with RID 1013. What is the account name?

ROOT\SAM\Domains\Users

![5_1.png](/thm/challenges/secret_recipe/5_1.png)

> bdoor
{.is-success}

## 6. What is the VPN connection this host connected to?

After a quick reseach where to look for network connections I found it in the following registry hive: 
Load in the SOFTWARE Hive
ROOT\Microsoft\Windows NT\CurrentVersion\NetworkList

I found one Network indicating a VPN connection: 

![6_1.png](/thm/challenges/secret_recipe/6_1.png)

> ProtonVPN
{.is-success}

## 7. When was the first VPN connection observed? (Format: YYYY-MM-DD HH:MM:SS)

Same Hive as in the question before

![7_1.png](/thm/challenges/secret_recipe/7_1.png)

> 2022-10-12 19:52:36
{.is-success}

## 8. There were three shared folders observed on his machine. What is the path of the third share?

According to the [Microsoft documentation](https://learn.microsoft.com/en-us/troubleshoot/windows-client/networking/saving-restoring-existing-windows-shares) shared folders are listed in SYSTEM\CurrentControlSet\Services\LanmanServer\Shares

![8_1.png](/thm/challenges/secret_recipe/8_1.png)
![8_2.png](/thm/challenges/secret_recipe/8_2.png)

> C:\RESTRICTED FILES
{.is-success}

## 9. What is the last DHCP IP assigned to this host?

In the SYSTEM Hive I found under 
ROOT\ControlSet001\Services\Tcpip\Parameters\Interfaces three different interfaces that has assigned IPs:

![9_1.png](/thm/challenges/secret_recipe/9_1.png)

It was kinda unsatisfying because the correct answer is 172.31.2.197 even though the last write for this interface was before the interface with the assigned IP 10.10.210.64. I couldn't figure out why it was this network interface. But according to the hint of THM and the possible answer format it had to be 172.31.2.197.

> 172.31.2.197
{.is-success}

## 10. The suspect seems to have accessed a file containing the secret coffee recipe. What is the name of the file?

For the recent activities I loaded in the NTUSER.DAT to Registry Explorer.

The location of recent files is in ROOT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs:

![10_1.png](/thm/challenges/secret_recipe/10_1.png)

> secret-recipe.pdf
{.is-success}

## 11. The suspect executed multiple commands using the Run window. What command was used to enumerate the network interfaces?

The evidence is found in the NTUSER.DAT as well
\ROOT\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU

![11_1.png](/thm/challenges/secret_recipe/11_1.png)

> pnputil /enum-interfaces
{.is-success}

## 12. The user searched for a network utility tool to transfer files using the file explorer. What is the name of that tool?

The evidence is found in the NTUSER.DAT as well
\ROOT\Software\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery

![12_1.png](/thm/challenges/secret_recipe/12_1.png)

> netcat
{.is-success}

## 13. What is the recent text file opened by the suspect?

Recent files are stored in ROOT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\\.txt of the NTUSER.DAT hive:

![13_1.png](/thm/challenges/secret_recipe/13_1.png)

> secret-code.txt
{.is-success}

## 14. How many times was PowerShell executed on this host?

I checked the NTUSER.DAT hive in Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist and clicked through all the subkeys . In the key {CEBFF5CD-ACE2-4F4F-9178-9926F41749EA}\count i found the different programs that were executed with a counter. I filtered for "powershell" and found the answer:

![14_1.png](/thm/challenges/secret_recipe/14_1.png)

> 3
{.is-success}

## 15. The suspect also executed a network monitoring tool. What is the name of the tool?

In the same key as in question 14 I seareched through the program name, set the filter for "Run Count" in the Registry Explorer to >= 1 and noticed wireshark, which is a network monitoring tool:

![15_1.png](/thm/challenges/secret_recipe/15_1.png)

> wireshark
{.is-success}

## 15. Registry Hives also note the amount of time a process is in focus. Examine the Hives and confirm for how many seconds was ProtonVPN executed?
