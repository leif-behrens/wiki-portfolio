---
title: Snapped Phish-ing Line
description: 
published: true
date: 2025-08-07T15:51:06.548Z
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

The only mail that contained an obvious pdf file is the mail "Quote for Services Rendered processed on June 29 2020 100132 AM.eml"

I just searched for the symbol "@" in this mail to filter the receipient where I found the answer to the first question:


> William McClean
{.is-success}
