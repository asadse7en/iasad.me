---
author: "Asad Ullah"
title: Cryptography - PicoCTF 2023
summary: writeups for cryptography cahllanges of picoctf 2023

date: 2023-03-30T02:54:51+05:00

Section: "write-ups"

tocopen: true
categories: 
- cryptography
- picoctf 2023
tags:
- albash cipher
- steghide
- base64
- rot 13
- rot 18

draft: false


---

&nbsp;

## **Hide to See - 100 pts**

&nbsp;

### Description

How about some hide and seek heh?Look at this image {{< url link="https://artifacts.picoctf.net/c/239/atbash.jpg" text="here" >}}.

### Approach

&nbsp;

![atbash.jpg](/write-ups/picoctf/2023/cryptography/hidetosee-1.webp#center)

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

![Untitled](/write-ups/picoctf/2023/cryptography/hidetosee-2.webp#center)

&nbsp;


---

**Flag: `picoCTF{atbash_crack_1f84d779}`**

---

&nbsp;

&nbsp;

## **ReadMyCert - 100 pts**

&nbsp;

### Description

How about we take you on an adventure on exploring certificate signing requests

Take a look at this CSR file [here](https://artifacts.picoctf.net/c/420/readmycert.csr)

> **Hint💡**   
> Download the certificate signing request and try to read it.

&nbsp;

### Approach

Dumping the contents of the `readmycert.cer` file reveals:

```bash
-----BEGIN CERTIFICATE REQUEST-----
MIICpzCCAY8CAQAwPDEmMCQGA1UEAwwdcGljb0NURntyZWFkX215Y2VydF9hNzE2
M2JlOH0xEjAQBgNVBCkMCWN0ZlBsYXllcjCCASIwDQYJKoZIhvcNAQEBBQADggEP
ADCCAQoCggEBAL6KBBqiFmUHDwT3NtVw+Ozveo9uAZ+c47X5n+MEsWPowsNIz9fG
kpLf9rgu9kR4ZR1H5IEddOGEsTA9qRUc1mwBuZeld5o9ltDU+6YzCKANDnwS61sB
w4FV54LTy33T1+1bc11o++3LM34pFCGWI3lwoj8GWDRJdxvvp5Iwh5kz4ki6Mwp/
HAKyyG9i9KMOXAm/Zw0FkL1UZppHa00cbdCieen7lZgeVpFlIs3uo8tL6fGmpYww
Ard6ZFzL1zCwgZukSHsul20gi9Ba4Uz3R4f6zA/PL0S7haAif96yyi/REREKUZGt
76Gt8zv2xVAqhZYYpFqOmv1ycRmZSyF8GWkCAwEAAaAmMCQGCSqGSIb3DQEJDjEX
MBUwEwYDVR0lBAwwCgYIKwYBBQUHAwIwDQYJKoZIhvcNAQELBQADggEBAI4mtS0h
2HQseRJfnySGJdsnquMyLSV1EdvAfb2qTosXuQH0vunk5NbnR9yjXKej0I2Uu6DW
f9UehV+QsgW1tmZKpjGXj602nESDBVwiyNw84AXaW74+vH1lVKu9YFf08GI40Fee
jYYjQLz6DatXL0Qsuyjjo/MF1W1z/N7ErLvox7tj+dIOfEs14LYx61JrwwcAw8Ak
1lo4gwusg/+aEpAhDcw62Bjh2iGfwydHV7vh04vWBzPoSz5xyrNG+w8kALKKRUTh
Z9wKzilfeMGpobC7at6ys5cMdrC3ePVxn0XWTQEWfjQwtr+UtOoOWlP8eJEstWQU
qbdZveR4nsgbnkU=
-----END CERTIFICATE REQUEST-----
```

&nbsp;

Looks base64 encoded, running through [CyberChef](https://gchq.github.io/CyberChef/) the flag is found in amongst the decoded output :


![Untitled](/write-ups/picoctf/2023/cryptography/base64-readmycert.webp)

&nbsp;

---

**Flag: `picoCTF{read_mycert_a7163be8}`**

---


&nbsp;

&nbsp;

## **Rotation - 100 pts**

&nbsp;

### Description

You will find the flag after decrypting this file Download the encrypted flag [here](https://artifacts.picoctf.net/c/388/encrypted.txt)

> **Hint💡**  
> Sometimes rotation is right

Given the name of this challenge, a rotation-based substitution cipher is suspected.

### Approach

The contents of the encrypted flag file are:

```bash
xqkwKBN{z0bib1wv_l3kzgxb3l_25l7k61j}
```

The encrypted text follows the flag structure `picoCTF{}` 

We can use [CyberChef](https://gchq.github.io/CyberChef/) to find the plaintext. By applying **ROT13** operation, and adjesting the amount to **18** we get the **Flag**

![Untitled](/write-ups/picoctf/2023/cryptography/rot18-rotation.webp)

&nbsp;

---

**Flag: `picoCTF{r0tat1on_d3crypt3d_25d7c61b}`**

---


&nbsp;

&nbsp;
