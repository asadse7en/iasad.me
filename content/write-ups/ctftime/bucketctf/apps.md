---
author: "Asad Ullah"
title: "Apps - BucketCTF"
description: 
summary: Write-up on Misc challenge Apps.
date: 2023-04-10T02:04:24+05:00
Section: write-ups
categories:
- writeup
- ctftime.org

tags:
- bucketctf
- misc

draft: false

---

{{< 
ctftime 
name="Apps" 
difficulty="Easy"  
points="200"
category="Misc"
>}}

&nbsp;

&nbsp;

## Description

I made a small app when I was 9 years old first learning to code.

Download Attachments {{< url link="https://storage.ebucket.dev/CTF.aia" text="here" >}}

&nbsp;

## Approach

The `CTF.asa` file was, in fact, a zip archive containing the application source code. Upon extraction of the archive, the flag was discovered in the `screen1.bky` file located within the src directory.

![apps](/write-ups/ctftime/bucket/apps.webp)

&nbsp;

---

**Flag: `bucket{M1T_4PP_1NV3NT0R_bf0285c53}`**

---

&nbsp;

&nbsp;
