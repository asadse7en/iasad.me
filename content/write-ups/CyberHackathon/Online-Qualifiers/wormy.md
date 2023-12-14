---
author: "Asad Ullah"
title: Wormy - CyberHackathon
description: Analyzing a network capture file using Wireshark.
summary: Analyzing a network capture file using Wireshark.

Section: "write-ups"

date: 2023-11-12T02:54:51+05:00
tags: 
- Wireshark
- RC4
categories:
- CyberHackathon
- writeup
draft: false

---

{{< 
ctf 
name="Wormy"
category="Network Security" 
difficulty="Easy"
points="50"  
creator_name="CyberHackathon" creator_link="https://patch.com.pk/competitions/digital-cyber-security-hackathon-2023-onlinequalifier/challenges" 
>}}


&nbsp;
&nbsp;

## Approach

We are given a network capture file that we can examine using Wireshark. The file contained a large number of packets. So, I decided to filter only the `http` traffic. moving through `http` packets I saw a `zip` file was downloaded.

&nbsp;

![Untitled](/write-ups/cyberhackathon/wormy/1.webp)

&nbsp;

I decided to export all `http` objects and doing so I saw some hints

&nbsp;

![Untitled](/write-ups/cyberhackathon/wormy/2.webp)

&nbsp;

now its clear that we have to find some encoded data and decode it with `RC4` using passphrase `secret`. Looking at the files I found this string interesting in file `data(8)`

&nbsp;

![Untitled](/write-ups/cyberhackathon/wormy/3.webp)

&nbsp;

I just copied the text and tried to decode it using [cyberchef](https://cyberchef.io/) 

&nbsp;

![Untitled](/write-ups/cyberhackathon/wormy/4.webp)

&nbsp;

It's clear that the string is indeed the flag, but some characters are not accurately represented. To fix this, we can convert the encoded flag to hexadecimal format and then decode it.

&nbsp;

```bash
┌──(n4ruto㉿iasad,me)-[~/CTFs/CyberHackathon/wormy]
└─$ cat data\(8\)

�Z�{����m�տ���C�X����3��b


┌──(n4ruto㉿iasad.me)-[~/CTFs/CyberHackathon/wormy]
└─$ cat data\(8\) | xxd -p
  
ab5ab37bf9f695926d8ed5bf819f8543c4581cbdb2809b1b403310b8ea041062
```

&nbsp;

I put the hex in [cyberchef](https://cyberchef.io/), converted the input format to hex, and we got the flag

&nbsp;

![Untitled](/write-ups/cyberhackathon/wormy/5.webp)

&nbsp;


{{< flag "flag" "Flag{RC4_Encryption_1s_G0Od_0nE}">}}

&nbsp;

&nbsp;
