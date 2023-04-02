---
author: "Asad Ullah"
title: ReadMyCert - PicoCTF (2023)
summary: certificate signing request with base64 encoding

date: 2023-03-30T06:54:51+05:00

Section: "write-ups"

categories: ["writeup", "picoctf", "cryptography"]
tags: ["picoctf", "picoctf 2023", "base64", "base64decode", "cyberchef", "cryptography"]

draft: false

---


{{< 
picoctf 
name="ReadMyCert" 
difficulty="Easy"  
points="100"
creator_name="PicoCTF" creator_link="https://play.picoctf.org/practice/challenge/367" 
category="Cryptography"
>}}

## Description

How about we take you on an adventure on exploring certificate signing requests

Take a look at this CSR file [here](https://artifacts.picoctf.net/c/420/readmycert.csr)

> **Hint💡**
> Download the certificate signing request and try to read it.

&nbsp;

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


![Untitled](/write-ups/picoctf/base64-readmycert.png)

&nbsp;

---

**Flag: `picoCTF{read_mycert_a7163be8}`**

---

## Conclusion

The given text is a simple base64 encoding. We can use tools like [base64 decoder](https://www.base64decode.org/) and [CyberChef](https://gchq.github.io/CyberChef/) to decode it. In Linux, you can pipe the base64 encoded text to `base64 -d` to decode it.   

&nbsp;
**i.e.** to decode QXNhZCBVbGxhaA== use **`echo "QXNhZCBVbGxhaA==" | base64 -d`**