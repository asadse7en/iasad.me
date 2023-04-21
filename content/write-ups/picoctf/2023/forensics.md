---
author: "Asad Ullah"
title: Forensics - PicoCTF 2023
summary: writeups for forensics cahllanges of picoctf 2023

date: 2023-03-30T02:54:51+05:00

Section: "write-ups"

tocopen: true
categories: 
- forensics
- picoctf 2023
tags:
- msb
- lsb
- whois
- pcap

draft: false


---

&nbsp;

## Who is it - 100 pts

&nbsp;

### Description

Someone just sent you an email claiming to be Google's co-founder Larry Page but you suspect a scam.Can you help us identify whose mail server the email actually originated from?Download the email file [here](https://artifacts.picoctf.net/c/499/email-export.eml). Flag: picoCTF{FirstnameLastname}

### Approach

we need to find the IP address of the sender. In order to determine the sender's IP address, we should search for it within the provided `.eml` file.

![Untitled](/write-ups/picoctf/2023/forensics/whoisit-eml.webp#center)

&nbsp;


we can perform a {{< url link="https://www.whois.com/whois/" text="WHOIS" >}} lookup using the IP address 173.249.33.206 to retrieve the owner's name.

![Untitled](/write-ups/picoctf/2023/forensics/whoisit-whois.webp#center)

&nbsp;


---

**Flag: `picoCTF{WilhelmZwalina}`**

---

&nbsp;

&nbsp;

## Find and Open - 200 pts

&nbsp;

### Description

Someone might have hidden the password in the trace file.Find the key to unlock [this file](https://artifacts.picoctf.net/c/492/flag.zip). [This tracefile](https://artifacts.picoctf.net/c/492/dump.pcap) might be good to analyze.

### Approach

We have two files: a password-protected `ZIP` file and a `PCAP` file. Upon inspecting the PCAP file in Wireshark, a base64 string was discovered.

![wireshark](/write-ups/picoctf/2023/forensics/findandopen-wireshark.webp)

&nbsp;

Decoded the base64 string and found half flag

```bash
┌──(kali㉿iasad)-[~/CTFs/PicoCTF]
└─$ echo VGhpcyBpcyB0aGUgc2VjcmV0OiBwaWNvQ1RGe1IzNERJTkdfTE9LZF8= | base64 -d
This is the secret: picoCTF{R34DING_LOKd_
```

&nbsp;


I tried the half flag as a password on the zip and it worked got the flag.

&nbsp;

---

**Flag: `picoCTF{R34DING_LOKd_fil56_succ3ss_cbf2ebf6}`**

---

&nbsp;

&nbsp;

## MSB - 200 pts

&nbsp;

### Description

This image passes LSB statistical analysis, but we can't help but think there must be something to the visual artifacts present in this image...Download the image {{< url link="https://artifacts.picoctf.net/c/306/Ninja-and-Prince-Genji-Ukiyoe-Utagawa-Kunisada.flag.png" text="here">}}

### Approach

Based on the name and description, it appears that the flag may be hidden in the most significant bit (MSB). I searched for ways to extract the data from MSB, and found a Python tool {{< url link="https://raw.githubusercontent.com/Pulho/sigBits/master/sigBits.py" text="Sigbit.py" >}}

```bash
┌──(kali㉿iasad)-[~/CTFs/PicoCTF]
└─$ python sigBits.py -t=msb Ninja-and-Prince-Genji-Ukiyoe-Utagawa-Kunisada.flag.png
Done, check the output file!
```

&nbsp;

I search for “picoCTF” in the output and found the flag

![output](/write-ups/picoctf/2023/forensics/msb-output.webp#center)

&nbsp;

---

**Flag: `picoCTF{15_y0ur_que57_qu1x071c_0r_h3r01c_06326238}`**

---

&nbsp;

&nbsp;
