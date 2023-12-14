---
author: "Asad Ullah"
title: t00ls - CyberHackathon
description: Easy Cryptography challenge
summary: Easy Cryptography challenge
Section: "write-ups"

date: 2023-12-13T02:54:51+05:00
tags: 
- base32
categories:
- CyberHackathon
- writeup
draft: false

---


{{< 
ctf 
name="t00ls"
category="Cryptography" 
difficulty="Easy"
points="50"  
creator_name="CyberHackathon" creator_link="https://patch.com.pk/" 
>}}


&nbsp;
&nbsp;

## Description

```bash
2d 2d 20 2d 2d 20 2d 2d 2e 2e 20 2e 2d 2d 20 2d 2e 2d 2d 20 2e 2e 2e 2e 2e 20 2e 2d 2e 2e 20 2e 20 2e 2d 2d 2d 20 2d 2e 2e 2e 20 2e 2e 2d 2d 2d 20 2e 2e 2e 2e 20 2d 2d 2e 2d 20 2d 20 2d 20 2d 2e 2d 20 2d 2e 2d 20 2d 2d 2e 2e 20 2e 2e 2e 2e 2d 20 2e 2e 2d 20 2e 2e 2e 2e 2d 20 2d 2e 2e 2e 2e 20 2e 2e 2e 20 2e 2e 2d 2e 20 2d 2d 2e 20 2d 2e 20 2e 2d 2e 20 2e 2d 2d 20 2e 2e 2d 20 2d 20 2e 2d 2e 2e 20 2e 2e 2d 2d 2d 20 2d 2d 20 2e 2e 20 2d 2d 2e 2e 20 2d 2e 2e 20 2e 2e 2e 20 2e 2e 2e 2e 2e 20 2e 2e 2e 2d 2d 20 2d 2e 2e 20 2d 2e 20 2e 2d 2d 2d 20 2e 2d 2e 2e 20 2e 2e 2e 2e 20 2d 2d 2e 2d 20 2d 20 2e 2e 2d 2d 2d 20 2e 2e 2e 2e 20 2d 2d 2e 20 2d 2d 2e 2d 20 2d 2e 2d 2d 20 2e 2e 2d 20 2e 2e 2d 2d 2d 20 2e 2e 2d 2d 2d 20 2e 2e 2e 20 2d 2e 2d 2e 20 2d 2d 2d 20 2e 2e 2e 2e 2e 20 2e 2d 2e 20 2d 20 2d 2d 2e 20 2d 2d 2e 2d 20 2e 2d 2d 2d 20 2e 2d 2e 20 2e 2d 2d 2d 20 2d 2d 2e 2e 20 2d 2e 2d 20 2e 20 2e 2e 2e 2e 2d 20 2d 2e 2e 2e 2e 20 2d 2e 2e 20 2d 2e 2e 20 2e 2d 2d 2e 20 2e 2d 2d 2d 20 2d 2d 2e 20 2d 2e 2e 2d 20 2d 2d 2d 20 2d 2e 2d 2d 20 2e 2e 2d 2d 2d 20 2e 2e 20 2e 2e 20 2d 2d 2e 2e 20 2e 2e 2e 2e 2e 20 2e 20 2e 2e 2e 2e 2d 20 2e 2d 2e 20 2d 2d 2e 2e 20 2e 2e 2d 20 2d 2d 2e 20 2d 2e 20 2e 2e 2e 2e 20 2e 20 2d 2d 2e 2d 20 2e 2d 2e 20 2d 20 2d 2e 2d 2d 20 2d 2d 20 2d 2d 2e 2e 20 2e 2e 20 2d 20 2e 2e 2d 2d 2d 20 2e 2d 2d 2e 20 2e 2e 20 2d 2e 2e 2e 2d
```

## Approach

Multiple encodings were applied: `hex` > `morse` > `base32` > `base64` > `rot13` leading us to unveil the flag. 

Here is the CyberChef recipe for decrypting the flag

```bash
From_Hex('Auto')
From_Morse_Code('Space','Line feed')
From_Base32('A-Z2-7=',true)
From_Base64('A-Za-z0-9+/=',true)
ROT13(true,true,false,13)
```

&nbsp;

{{< flag "flag" "Flag{d65e717e33bbce5d8a520cfc553df30cdf4a74dd}">}}

&nbsp;

&nbsp;
