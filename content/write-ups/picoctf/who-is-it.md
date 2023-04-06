---
author: "Asad Ullah"
title: "Who is it - PicoCTF (2023)"
description: 
summary: Easy challange where we need to find details from whois

date: 2023-04-06T17:02:36+05:00
Section: write-ups
categories:
- writeup
- picoctf
- forensics
tags:
- picoctf 2023
- whois
- ip lookup

draft: false

---

{{< 
picoctf
name="Who is it" 
difficulty="Easy"  
points="100"
creator_name="PicoCTF" creator_link="https://play.picoctf.org/practice/challenge/388" 
category="Forensics"
>}}


&nbsp;


## Description

Someone just sent you an email claiming to be Google's co-founder Larry Page but you suspect a scam.Can you help us identify whose mail server the email actually originated from?Download the email file [here](https://artifacts.picoctf.net/c/499/email-export.eml). Flag: picoCTF{FirstnameLastname}

## Approach

we need to find the IP address of the sender. In order to determine the sender's IP address, we should search for it within the provided `.eml` file.

![Untitled](/write-ups/picoctf/whoisit-eml.webp#center)

&nbsp;


we can perform a {{< url link="https://www.whois.com/whois/" text="WHOIS" >}} lookup using the IP address 173.249.33.206 to retrieve the owner's name.

![Untitled](/write-ups/picoctf/whoisit-whois.webp#center)

&nbsp;


---

**Flag: `picoCTF{WilhelmZwalina}`**

---

&nbsp;
