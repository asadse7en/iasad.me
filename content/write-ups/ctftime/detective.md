---
author: "Asad Ullah"
title: "Detective - BucketCTF"
description: 
summary: Write-up on stegonograpy challenge Detective.
date: 2023-04-10T02:08:24+05:00
Section: write-ups
categories:
- writeup
- ctftime.org
tags:
- bucketctf
- stego
- stegsolve

draft: false

---

{{< 
ctftime 
name="Detective" 
difficulty="Easy"  
points="200"
category="Misc"
>}}

&nbsp;

&nbsp;

## Description

Watson: The criminal's wiped down the crime scene! How can we find them now? Holmes: Elementary, my dear Watson

Download Attachments {{< url link="https://storage.ebucket.dev/out.bmp" text="here" >}}

&nbsp;

## Approach

As this was a steganography challenge and the image appeared to be plain white, I decided to use `stegsolve.jar` to check for any hidden data in the color channels separately and discovered the flag within the `red plane 0`

 

![stegsolve](/write-ups/ctftime/bucket/detective.webp)

&nbsp;

---

**Flag: `bucket{r3plAc3_c0L0Rs!!}`**

---

&nbsp;

&nbsp;
