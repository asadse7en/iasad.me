---
author: "Asad Ullah"
title: "Zaza - ångstromCTF"
description: 
summary: Write-up on Rev challenge Zaza.
date: 2023-04-27T01:00:24+05:00
Section: write-ups
categories:
- writeup
- ctftime.org
tags:
- angstormctf
- rev
- binary

draft: false

---

{{< 
ctftime 
name="Zaza" 
difficulty="Easy"  
points="50"
category="Rev"
>}}

&nbsp;

&nbsp;

## Description

Bedtime!

`nc challs.actf.co 32760`

[zaza](https://files.actf.co/ea58fcd01cef923ea88d023f52548c7be73dcf74f7eeb9c0280a0d3ea7162213/zaza)

## Approach

 the program makes some checks before giving us flag

 &nbsp;

**check#1**

the program prompts `I'm going to sleep. Count me some sheep:`

looking into the binary we find that the number is `4919`

![Untitled](/write-ups/ctftime/angstorm/zaza-1.webp)

&nbsp;

**check#2**

it then prompts `Nice, now reset it. Bet you can't:` it asks for `x` such that `x * 4919 ≠ 1`

![Untitled](/write-ups/ctftime/angstorm/zaza-2.webp)

&nbsp;

**check#3**

it then asks `Okay, what's the magic word?` looking it the binary we can see that it perform `xor` on a string with a key

![Untitled](/write-ups/ctftime/angstorm/zaza-3.webp)
![Untitled](/write-ups/ctftime/angstorm/zaza-4.webp)
after the  `xor` we got the **magic words** 

![Untitled](/write-ups/ctftime/angstorm/zaza-5.webp)

&nbsp;

```bash
┌──(kali㉿iasad)-[~/CTFs/angstorm]
└─$ nc challs.actf.co 32760
I'm going to sleep. Count me some sheep: 4919
Nice, now reset it. Bet you can't: 1
Okay, what's the magic word?
SHEEPSHEEPSHEEPSHEEPSHEEPSHEEPSHEEPSHEEPSHEEPSHEEPkd

actf{g00dnight_c7822fb3af92b949}
```

&nbsp;

---

**Flag:  `actf{g00dnight_c7822fb3af92b949}`**

---

&nbsp;

&nbsp;
