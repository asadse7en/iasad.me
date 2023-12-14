---
author: "Asad Ullah"
title: c0r - CyberHackathon
description: Easy forensics challenge
summary: Easy forensics challenge
Section: "write-ups"

date: 2023-12-13T02:54:51+05:00
tags: 
- magic header
categories:
- CyberHackathon
- writeup
draft: false

---


{{< 
ctf 
name="c0r"
category="Degital Forensics" 
difficulty="Easy"
points="50"  
creator_name="CyberHackathon" creator_link="https://patch.com.pk/" 
>}}


&nbsp;
&nbsp;

## Description

I don't why why my image is not working. can you help me fix it?

Flag Format: Flag{}

## Approach

Looking at the hex of the image reveals that its a `JPEG` with corrupted header bytes. We can verify the correct header information [here](https://en.wikipedia.org/wiki/List_of_file_signatures).

```bash
┌──(n4ruto㉿iasad.me)-[~/CTFs/CyberHackathon/pu5h]
└─$ xxd file | head

00000000: ff6b ff79 0010 4a4e 5546 0001 0101 0060  .k.y..JNUF.....`
00000010: 0060 0000 ffe1 0022 4578 6a76 0000 4d4d  .`....."Exjv..MM
00000020: 002a 0000 0008 0001 0112 0003 0000 0001  .*..............
00000030: 0001 0000 0000 0000 ffdb 0043 0002 0101  ...........C....
00000040: 0201 0102 0202 0202 0202 0203 0503 0303  ................
00000050: 0303 0604 0403 0507 0607 0707 0607 0708  ................
00000060: 090b 0908 080a 0807 070a 0d0a 0a0b 0c0c  ................
00000070: 0c0c 0709 0e0f 0d0c 0e0b 0c0c 0cff db00  ................
00000080: 4301 0202 0203 0303 0603 0306 0c08 0708  C...............
00000090: 0c0c 0c0c 0c0c 0c0c 0c0c 0c0c 0c0c 0c0c  ................
```

Header Bytes changed to `FF D8 FF E0 00 10 4A 46 49 46 00 01`

```bash
┌──(n4ruto㉿iasad.me)-[~/CTFs/CyberHackathon/pu5h]
└─$ xxd fixed.jpg | head

00000000: ffd8 ffe0 0010 4a46 4946 0001 0101 0060  ......JFIF.....`
00000010: 0060 0000 ffe1 0022 4578 6a76 0000 4d4d  .`....."Exjv..MM
00000020: 002a 0000 0008 0001 0112 0003 0000 0001  .*..............
00000030: 0001 0000 0000 0000 ffdb 0043 0002 0101  ...........C....
00000040: 0201 0102 0202 0202 0202 0203 0503 0303  ................
00000050: 0303 0604 0403 0507 0607 0707 0607 0708  ................
00000060: 090b 0908 080a 0807 070a 0d0a 0a0b 0c0c  ................
00000070: 0c0c 0709 0e0f 0d0c 0e0b 0c0c 0cff db00  ................
00000080: 4301 0202 0203 0303 0603 0306 0c08 0708  C...............
00000090: 0c0c 0c0c 0c0c 0c0c 0c0c 0c0c 0c0c 0c0c  ................
```

After repairing the header and viewing the image, we got the flag.

![Untitled](/write-ups/cyberhackathon/c0r/Untitled%20(81).png)


&nbsp;

{{< flag "flag" "Flag{Y0u_F1x3D_Th3_JpG_1M493}">}}

&nbsp;

&nbsp;
