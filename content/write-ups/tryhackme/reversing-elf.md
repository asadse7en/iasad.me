---
author: "Asad Ullah"
title: Reversing ELF - TryHackMe
description: Easy reversing engineering room where we have 8 crackmes ELF binaries to play with.
summary: Easy reversing engineering room where we have 8 crackmes ELF binaries to play with.

Section: "write-ups"

date: 2023-11-13T02:54:51+05:00
tags: 
- Crackme
- ELF
- ghidra
- ltrace
- r2
categories:
- tryhackme
- writeup
draft: false

---

{{< 
tryhackme 
info="room info"
name="Reversing ELF" 
os="Binaries" 
difficulty="Easy"  
creator_name="TryHackMe" creator_link="https://tryhackme.com/room/reverselfiles"
>}}


&nbsp;
&nbsp;

## Crackme1

Just executing the file gave us the flag

```bash
┌──(n4ruto㉿iasad.me)-[~/CTFs/tryhackme/reversing-ELF]
└─$ chmod +x crackme1

┌──(n4ruto㉿iasad.me)-[~/CTFs/tryhackme/reversing-ELF]
└─$ ./crackme1                                             
flag{not_that_kind_of_elf}
```

&nbsp;

{{<flag "flag" "flag{not_that_kind_of_elf}">}}

&nbsp;

## Crackme2

Our input is compared with a hard-coded string. retrievable using `strings` or `ltrace`.

![Untitled](/write-ups/tryhackme/reversing-elf/1.webp)

&nbsp;

{{<flag "flag" "super_secret_password">}}

&nbsp;


## Crackme3

Once again, we encounter a base64-encoded string within the character sequences. Decoding it reveals the password: `f0r_y0ur_5ec0nd_le55on_unbase64_4ll_7h3_7h1ng5`.

![Untitled](/write-ups/tryhackme/reversing-elf/2.webp)

&nbsp;

{{<flag "flag" "f0r_y0ur_5ec0nd_le55on_unbase64_4ll_7h3_7h1ng5">}}

&nbsp;

## Crackme4

Again our input is compared with actual flag that we can retrive using `ltrace` 

![Untitled](/write-ups/tryhackme/reversing-elf/3.webp)

&nbsp;

{{<flag "flag" "my_m0r3_secur3_pwd">}}

&nbsp;

## Crackme5

Opening the binary in Ghidra, we can see that every character of the password is saved in a separate veriable. We can retrieve the password by converting value of each variable from hex to char.


![Untitled](/write-ups/tryhackme/reversing-elf/4.webp)

Since the string is compared with our input, we can use `ltrace` to retrieve it easily.

![Untitled](/write-ups/tryhackme/reversing-elf/5.webp)

&nbsp;

{{<flag "flag" "OfdlDSA|3tXb32~X3tX@sX`4tXtz">}}

&nbsp;

## Crackme6

Again opening the binary in Ghidra, we can see the password is `1337_pwd`.

![Untitled](/write-ups/tryhackme/reversing-elf/6.webp)

&nbsp;

{{<flag "flag" "1337_pwd">}}

&nbsp;

## Crackme7

Analyzing the binary in Ghidra, we see that the flag is printed when we put option value `31337`

&nbsp;

![Untitled](/write-ups/tryhackme/reversing-elf/7.webp)

&nbsp;

```bash
┌──(n4ruto㉿iasad.me)-[~/CTFs/tryhackme/reversing-ELF]
└─$ ./crackme7
Menu:

[1] Say hello
[2] Add numbers
[3] Quit

[>] 31337
Wow such h4x0r!
flag{much_reversing_very_ida_wow}
```

&nbsp;

{{<flag "flag" "flag{much_reversing_very_ida_wow}">}}

## Crackme8

This one is similar to crackme7, we just have to put option value `-889262067` to get the flag.

![Untitled](/write-ups/tryhackme/reversing-elf/9.webp)

&nbsp;

```bash
┌──(n4ruto㉿iasad.me)-[~/CTFs/tryhackme/reversing-ELF]
└─$ ./crackme8 -889262067
Access granted.
flag{at_least_this_cafe_wont_leak_your_credit_card_numbers}
```

&nbsp;


![Untitled](/write-ups/tryhackme/reversing-elf/10.webp)

&nbsp;

{{<flag "flag" "flag{at_least_this_cafe_wont_leak_your_credit_card_numbers}">}}

&nbsp;

&nbsp;
