---
author: "Asad Ullah"
title: "Find and Open - PicoCTF (2023)"
description: 
summary: easy difficulty forensics challange includes pcap analysis

date: 2023-04-06T17:02:36+05:00
Section: write-ups
categories:
- writeup
- picoctf
- forensics
tags:
- picoctf 2023
- wireshark
- pcap

draft: false

---

{{< 
picoctf
name="Find and Open" 
difficulty="Medium"  
points="200"
creator_name="PicoCTF" creator_link="https://play.picoctf.org/practice/challenge/348" 
category="Forensics"
>}}


&nbsp;

## Description

Someone might have hidden the password in the trace file.Find the key to unlock [this file](https://artifacts.picoctf.net/c/492/flag.zip). [This tracefile](https://artifacts.picoctf.net/c/492/dump.pcap) might be good to analyze.

## Approach

We have two files: a password-protected `ZIP` file and a `PCAP` file. Upon inspecting the PCAP file in Wireshark, a base64 string was discovered.

![wireshark](/write-ups/picoctf/findandopen-wireshark.webp)

&nbsp;

Decoded the base64 string and found half flag

```bash
┌──(kali㉿iasad)-[~/CTFs/PicoCTF]
└─$ echo VGhpcyBpcyB0aGUgc2VjcmV0OiBwaWNvQ1RGe1IzNERJTkdfTE9LZF8= | base64 -d
This is the secret: picoCTF{R34DING_LOKd_
```

&nbsp;


I tried the half flag as a password on the zip and it worked got the flag.

&nbsp;

---

**Flag: `picoCTF{R34DING_LOKd_fil56_succ3ss_cbf2ebf6}`**

---

&nbsp;
