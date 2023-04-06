---
author: "Asad Ullah"
title: "MSB - PicoCTF (2023)"
description: 
summary: medium difficulty challange where flag is hidden in most significent bits

date: 2023-04-06T17:02:36+05:00
Section: write-ups
categories:
- writeup
- picoctf
- forensics
tags:
- picoctf 2023
- MSB
- LSB

draft: false

---

{{< 
picoctf
name="MSB" 
difficulty="Medium"  
points="200"
creator_name="PicoCTF" creator_link="https://play.picoctf.org/practice/challenge/359" 
category="Forensics"
>}}


&nbsp;

## Description

This image passes LSB statistical analysis, but we can't help but think there must be something to the visual artifacts present in this image...Download the image {{< url link="https://artifacts.picoctf.net/c/306/Ninja-and-Prince-Genji-Ukiyoe-Utagawa-Kunisada.flag.png" text="here">}}

## Approach

Based on the name and description, it appears that the flag may be hidden in the most significant bit (MSB). I searched for ways to extract the data from MSB, and found a Python tool {{< url link="https://raw.githubusercontent.com/Pulho/sigBits/master/sigBits.py" text="Sigbit.py" >}}

```bash
┌──(kali㉿iasad)-[~/CTFs/PicoCTF]
└─$ python sigBits.py -t=msb Ninja-and-Prince-Genji-Ukiyoe-Utagawa-Kunisada.flag.png
Done, check the output file!
```

&nbsp;

I search for “picoCTF” in the output and found the flag

![output](/write-ups/picoctf/msb-output.webp#center)

&nbsp;

---

**Flag: `picoCTF{15_y0ur_que57_qu1x071c_0r_h3r01c_06326238}`**

---

&nbsp;
