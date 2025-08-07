---
title: Snapped Phish-ing Line
description: 
published: true
date: 2025-08-07T17:41:54.481Z
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

I used VirusTotal to check the hash value from question 5:

![6_1.png](/thm/challenges/snapped_phish-ing_line/6_1.png)

> 2020-04-08 21:55:50 UTC
{.is-success}

---
<br>

### 7. When was the SSL certificate the phishing domain used to host the phishing kit archive first logged? (format: YYYY-MM-DD)

I had no idea to figure it out. So I checked the hint from the THM room and it says:

![7_1.png](/thm/challenges/snapped_phish-ing_line/7_1.png)

> 2020-06-25
{.is-success}

---
<br>

### 8. What was the email address of the user who submitted their password twice?

I continued enumerating the URL and found the file log.txt in the Update365 directory:

![8_1.png](/thm/challenges/snapped_phish-ing_line/8_1.png)

I downloaded and analyzed it. Since there are just a few users and entries I didn't need to use some filters, the answer was obvious:

![8_2.png](/thm/challenges/snapped_phish-ing_line/8_2.png)

> michael.ascot@swiftspend.finance
{.is-success}

---
<br>

### 9. What was the email address used by the adversary to collect compromised credentials?

I unzipped the archive and navigated through the folders. I found an interesting script "updat.cmd" which I investigated using cat and I found the email address jamestanner2299@gmail.com. But this wasn't the correct answer. I found the same email address in the file "script.st". 
![9_1.png](/thm/challenges/snapped_phish-ing_line/9_1.png)

![9_2.png](/thm/challenges/snapped_phish-ing_line/9_2.png)

Then I thought how the password submission would be triggered and it makes sense it would be triggered when the user submits his password when beeing redirected after opening the html file in the email. I navigated to the folder "Validation" and saw the file "submit.php":

![9_3.png](/thm/challenges/snapped_phish-ing_line/9_3.png)

Inside this file I found the email address the password is sent after the user submits:

![9_4.png](/thm/challenges/snapped_phish-ing_line/9_4.png)

> m3npat@yandex.com
{.is-success}

---
<br>

### 10. The adversary used other email addresses in the obtained phishing kit. What is the email address that ends in "@gmail.com"?

I already solved this question in the previous question, where I found the email address in the "updat.exe" and "script.st" files:

![10_1.png](/thm/challenges/snapped_phish-ing_line/10_1.png)

> jamestanner2299@gmail.com
{.is-success}

---
<br>

### 11. What is the hidden flag?

I wanted to solve the question without help and I was navigating through the directories and was looking for hints. I looked into the robots.txt without success. Then I wanted to enumerate the URL kennaroads[.]buzz with gobuster or dirb but these tools are not installed on the machine. After some time without success I looked at the hint from THM:

![11_1.png](/thm/challenges/snapped_phish-ing_line/11_1.png)

I already solved a lot of challenges on THM and most of the time the filename of a flag is "flag.txt". That's why I just tried to add flag.txt to the different directories of the phishing URL:

![11_1.png](/thm/challenges/snapped_phish-ing_line/11_1.png)
![11_2.png](/thm/challenges/snapped_phish-ing_line/11_2.png)
![11_3.png](/thm/challenges/snapped_phish-ing_line/11_3.png)
![11_4.png](/thm/challenges/snapped_phish-ing_line/11_4.png)
![11_5.png](/thm/challenges/snapped_phish-ing_line/11_5.png)

When I found the flag I noticed that the string is encoded, probably base64. So I used cyberchef again and the output was kinda nonsense at first sight: 

![11_6.png](/thm/challenges/snapped_phish-ing_line/11_6.png)

I realized real quick that the string is just reversed so I used the reverse "recipe" from cyberchef and got the flag:

![11_7.png](/thm/challenges/snapped_phish-ing_line/11_7.png)

> `THM{pL4y_w1Th_tH3_URL}`
{.is-success}
