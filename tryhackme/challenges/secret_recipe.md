---
title: Secret Recipe
description: 
published: true
date: 2025-08-07T08:14:44.505Z
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
