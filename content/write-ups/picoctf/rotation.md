---
author: "Asad Ullah"
title: Rotation - PicoCTF
summary: A very simple rotation-based substitution cipher - (ROT-18)

date: 2023-03-30T04:54:51+05:00

Section: "write-ups"

categories: ["writeup", "picoctf", "cryptography"]
tags: ["rotation", "picoctf", "picoctf 2023", "rot13", "rot18", "ctf", "cryptography"]

draft: false

---


{{< 
picoinfo 
name="Rotation" 
difficulty="Easy"  
points="100"
creator_name="PicoCTF" creator_link="https://play.picoctf.org/practice/challenge/373" 
category="Cryptography"
>}}


## Description

You will find the flag after decrypting this file Download the encrypted flag [here](https://artifacts.picoctf.net/c/388/encrypted.txt)

> **Hint💡**
> Sometimes rotation is right

Given the name of this challenge, a rotation-based substitution cipher is suspected.

The contents of the encrypted flag file are:

```bash
xqkwKBN{z0bib1wv_l3kzgxb3l_25l7k61j}
```

The encrypted text follows the flag structure `picoCTF{}` 

We can use [CyberChef](https://gchq.github.io/CyberChef/) to find the plaintext. By applying **ROT13** operation, and adjesting the amount to **18** we get the **Flag**

![Untitled](/write-ups/picoctf/rot18-rotation.png)

&nbsp;

---

**Flag: `picoCTF{r0tat1on_d3crypt3d_25d7c61b}`**

---

## Conclusion

*while rotation ciphers have been used historically and can be a fun puzzle to solve, they are not considered very secure in modern cryptography. As a result, they are not commonly used in practical applications where data security is critical. CTFs use ROT ciphers so that participant understand the limitations of these ciphers and to explore more advanced encryption techniques for better data protection.*