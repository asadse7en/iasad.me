---
author: "Asad Ullah"
title: The Indecipherable Cipher - VishwaCTF
summary: forensics challenge with nested compressions and file types

date: 2023-04-02T16:03:37+05:00

Section: "write-ups"

categories: ["writeup", "ctftime.org", "cryptography"]
tags: ["cipher"]

draft: false

---


{{< 
ctftime 
name="The Indecipherable Cipher" 
difficulty="Medium"  
points="300"
category="Cryptography"
>}}

### **Description**

Our crypto specialist Mr.Kasiski is currently unavailable, so help us decode this string➡️`j3qrh4kgz3iptmyqxcw0zkm8i5xugs5lwl0lrwvirwktlqinexcw0zkmq5nqvpebpor5wqipqhw2ikzm4ipktzlr`

## Approach

The first step I took was to identify the encryption type. To achieve this, I used {{< url link="https://www.dcode.fr/cipher-identifier" text="Cipher Identifier" >}} which provided me with a list of possible encryptions

![list of possible ciphers](/write-ups/ctftime/the-indecipherable-cipher/1.webp#center "list of possible ciphers")

&nbsp;

At first, I attempted to use base32, but it didn't work. So, I tried the second-best option, the Vigenere cipher. Initially, it didn't give me the flag, but then I noticed that the ciphertext also included numbers. So I decided to include numbers in the alphabet set.

![alphabet parameter](/write-ups/ctftime/the-indecipherable-cipher/2.webp#center "alphabet parameter")

&nbsp;

**which resulted in this**

![results](/write-ups/ctftime/the-indecipherable-cipher/3.webp#center "results")

&nbsp;

I thought that the text was still random, but the word "Friedrich" caught my attention. Therefore, I proceeded to separate each word in order to understand it.

***"Friedrich Wilhelm Kasiski was the person who designed the AAA Kasiski Examination to decode Vigenere cipher.”***

However, the flag that was accepted was actually the original plaintext.

&nbsp;

---

**Flag: `VishwaCTF{friedrichwilhelmkasiskiwastheonewhodesignedtheaaakasiskiexaminationtodecodevignerecipher}`**

---

&nbsp;

&nbsp;
