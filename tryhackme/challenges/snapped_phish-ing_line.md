---
title: Snapped Phish-ing Line
description: 
published: true
date: 2025-08-07T16:12:41.455Z
tags: 
editor: markdown
dateCreated: 2025-08-07T15:51:06.547Z
---

# Snapped Phish-ing Line

## Scenario
 As an IT department personnel of SwiftSpend Financial, one of your responsibilities is to support your fellow employees with their technical concerns. While everything seemed ordinary and mundane, this gradually changed when several employees from various departments started reporting an unusual email they had received. Unfortunately, some had already submitted their credentials and could no longer log in.

You now proceeded to investigate what is going on by:

1. Analysing the email samples provided by your colleagues.
2. Analysing the phishing URL(s) by browsing it using Firefox.
3. Retrieving the phishing kit used by the adversary.
4. Using CTI-related tooling to gather more information about the adversary.
5. Analysing the phishing kit to gather more information about the adversary.

Note: The phishing emails to be analysed are under the phish-emails directory on the Desktop. Usage of a web browser, text editor and some knowledge of the grep command will help. 

---
<br>

### 1. Who is the individual who received an email attachment containing a PDF?

At first I used grep to filter for the file ending .pdf:

![1_1.png](/thm/challenges/snapped_phish-ing_line/1_1.png)

The only mail that contained an obvious pdf file is the mail "Quote for Services Rendered processed on June 29 2020 100132 AM.eml"

I just searched for the symbol "@" in this mail to filter the receipient where I found the answer to the first question:

![1_2.png](/thm/challenges/snapped_phish-ing_line/1_2.png)

> William McClean
{.is-success}

---
<br>

### 2. What email address was used by the adversary to send the phishing emails?

I switched to using a text editor because it's better to read through the raw mail instead of using cat and grep in the terminal.
I was looking for the From-field and found the sender address:

![2_1.png](/thm/challenges/snapped_phish-ing_line/2_1.png)

> Accounts.Payable@groupmarketingonline.icu
{.is-success}

---
<br>

### 3. What is the redirection URL to the phishing page for the individual Zoe Duncan? (defanged format)

I was looking at the mail "Group Marketing Online Direct Credit Advice - zoe.duncan@swiftspend.finance.eml" via text editor and found an attachment "Direct Credit Advice.html" base64 encoded:

![3_1.png](/thm/challenges/snapped_phish-ing_line/3_1.png)

I used CyberChef to decode the content of the html file and also used the defang URL "recipe":

![3_2.png](/thm/challenges/snapped_phish-ing_line/3_2.png)
