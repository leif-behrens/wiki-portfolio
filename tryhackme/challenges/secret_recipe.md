---
title: Secret Recipe
description: 
published: true
date: 2025-08-07T07:58:23.024Z
tags: 
editor: markdown
dateCreated: 2025-08-07T07:58:23.024Z
---

# Secret Recipe

## What is the computer name of the machine found in the registry?

Registry Explorer
Load in the SYSTEM Hive
ROOT\ControlSet001\Control\ComputerName\ComputerName

![1_1.png](/thm/challenges/secret_recipe/1_1.png)

> JAMES
{.is-success}


## When was the Administrator account created on this machine? (Format: yyyy-mm-dd hh:mm:ss)

Registry Explorer
Load in the SAM Hive
ROOT\SAM\Domains\Users

![2_1.png](/thm/challenges/secret_recipe/2_1.png)

> 2021-03-17 14:58:48
{.is-success}


## What is the RID associated with the Administrator account?

![3_1.png](/thm/challenges/secret_recipe/3_1.png)


> 500
{.is-success}

