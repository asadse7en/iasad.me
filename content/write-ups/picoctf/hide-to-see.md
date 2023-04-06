---
author: "Asad Ullah"
title: "Hide to See - PicoCTF (2023)"
description: 
summary: easy cryptography challange with albash cipher

date: 2023-04-06T02:42:42+05:00
Section: write-ups
categories:
- writeup
- picoctf
- cryptography
tags:
- albash cipher
- picoctf 2023
- steghide
- dcode.fr

draft: false

---

{{< 
picoctf
name="hide to see" 
difficulty="Easy"  
points="100"
creator_name="PicoCTF" creator_link="https://play.picoctf.org/practice/challenge/351"
category="Cryptography"
>}}


&nbsp;

## Description

How about some hide and seek heh?Look at this image {{< url link="https://artifacts.picoctf.net/c/239/atbash.jpg" text="here" >}}.

## Approach

&nbsp;

![atbash.jpg](/write-ups/picoctf/hidetosee-1.webp#center)

&nbsp;


The image hinted at the `Albash cipher`, but I didn't found any encrypted data. After examining the metadata and trying different steganography tools, I eventually discovered the encrypted data hidden within the image using `steghide`.

```bash
┌──(kali㉿iasad)-[~/CTFs/PicoCTF]
└─$ steghide extract -sf atbash.jpg 
Enter passphrase: 
wrote extracted data to "encrypted.txt".



┌──(kali㉿iasad)-[~/CTFs/PicoCTF]
└─$ cat encrypted.txt 
krxlXGU{zgyzhs_xizxp_1u84w779}
```

&nbsp;

decoded it on {{< url link="https://www.dcode.fr/atbash-cipher" text="Atbash Cipher" >}} and got the flag

&nbsp;

![Untitled](/write-ups/picoctf/hidetosee-2.webp#center)

&nbsp;


---

**Flag: `picoCTF{atbash_crack_1f84d779}`**

---

&nbsp;

&nbsp;
