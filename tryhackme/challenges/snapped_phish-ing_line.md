---
title: Snapped Phish-ing Line
description: 
published: true
date: 2025-08-07T16:37:49.696Z
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

> hxxp[: //]kennaroads[.]buzz/data/Update365/office365/40e7baa2f826a57fcf04e5202526f8bd/?email=zoe[.]duncan@swiftspend[.]finance&error
{.is-success}

---
<br>

### 4. What is the URL to the .zip archive of the phishing kit? (defanged format)

I had issues how to proceed since I would never just click on a suspicous link. But the hint was to enumerate the url and so I assumed it is a isolated test VM, thats why I proceeded to enumerate the URL from the question before:

![4_1.png](/thm/challenges/snapped_phish-ing_line/4_1.png)

![4_2.png](/thm/challenges/snapped_phish-ing_line/4_2.png)

> hxxp[: //]kennaroads[.]buzz/data/Update365[.]zip
{.is-success}

---
<br>

### 5. What is the SHA256 hash of the phishing kit archive?

I downloaded the file and used sha256sum in the shell to get the hash:

![5_1.png](/thm/challenges/snapped_phish-ing_line/5_1.png)

> ba3c15267393419eb08c7b2652b8b6b39b406ef300ae8a18fee4d16b19ac9686
{.is-success}

---
<br>

### 6. When was the phishing kit archive first submitted? (format: YYYY-MM-DD HH:MM:SS UTC)