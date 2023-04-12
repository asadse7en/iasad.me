---
author: "Asad Ullah"
title: "Enigma - BucketCTF"
description: 
summary: Write-up on cryptography challange enigma.
date: 2023-04-11T05:04:24+05:00
Section: write-ups
categories:
- writeup
- cryptography
tags:
- bucketctf

draft: false

---

&nbsp;


{{< 
ctftime 
name="Enigma" 
difficulty="Medium"  
points="484"
category="Cryptography"
>}}

&nbsp;

&nbsp;



## Description

I found an old enigma machine and was messing around with it. I put a secret into it but forgot it. I remember some of the settings and have the output. 

&nbsp;

**Model: `M3`**

**Reflector: `B`**

**Rotors: `I II III`**

**Plugboard: `AT BS DE FM IR KN LZ OW PV XY`**

**Output: `rvvrw dxyfi cctev o`** 

&nbsp;

There has been a new flag that some teams already found. The solution is not in the normal bucket{} syntax. Remove spaces. Lowercase

&nbsp;

## Approach

First I used {{< url link="https://gchq.github.io/CyberChef/" text="CyberChef" >}} to decrypt the Enigma but it didn't give the correct output

![Untitled](/write-ups/ctftime/bucket/enigma-1.webp)

&nbsp;
 
In the description we are given all the settings The only unknown option was the rotor ring setting Since there are three rings and each can have 26 possible values &nbsp; (A - Z) there are 26 x 26 x 26 possible ring settings to check.

To check all possible ring settings, I used a Python script that iterates through all possibilities and tries to decrypt the encoded flag. If the decrypted plaintext contains the flag pattern, the script prints the current ring settings and the decrypted plaintext.

This approach allowed me to find the correct ring settings for the Enigma machine and decrypt the flag pattern.

```python
from enigma.machine import EnigmaMachine

ciphertext = "rvvrwdxyficctevo"

for a in range(1, 26):
    for b in range(1, 26):
       for c in range(1, 26):
          machine = EnigmaMachine.from_key_sheet(
              rotors="I II III",
              reflector="B",
              ring_settings=[a, b, c],
              plugboard_settings="AT BS DE FM IR KN LZ OW PV XY"
          )
          plaintext = machine.process_text(ciphertext).lower()
          print(f"Testing configuration: {[a, b, c]} Decrypted message: {plaintext}")
          if "bucket" in plaintext:
              print(f"Decrypted message: {plaintext}")
              exit()
```

&nbsp;

It found the flag with rotor ring configuration: `[22, 22, 23]` --> `[W, W, X]` 

![Untitled](/write-ups/ctftime/bucket/solve.gif)

&nbsp;

```
┌──(kali㉿iasad)-[~/CTFs/BucketCTF]
└─$ python3 solve.py

Testing configuration: [22, 22, 10] Decrypted message: maelogrvlrudnqua
Testing configuration: [22, 22, 11] Decrypted message: uaaiqvjhuqdunchk
Testing configuration: [22, 22, 12] Decrypted message: gcabszuocgmdpsql
Testing configuration: [22, 22, 13] Decrypted message: xwcmlhjmlwkmwbus
Testing configuration: [22, 22, 14] Decrypted message: xnwukkmabsfkwalg
Testing configuration: [22, 22, 15] Decrypted message: sqnghfpnvheflpuj
Testing configuration: [22, 22, 16] Decrypted message: sdqxvtnnueaeqmdy
Testing configuration: [22, 22, 17] Decrypted message: qhdxgoiihrgawgyg
Testing configuration: [22, 22, 18] Decrypted message: cfhsecjadgbgkcsh
Testing configuration: [22, 22, 19] Decrypted message: lpfshnrulyebknal
Testing configuration: [22, 22, 20] Decrypted message: kkpqmvrztxteqidy
Testing configuration: [22, 22, 21] Decrypted message: kckcsczpmzvtzvfw
Testing configuration: [22, 22, 22] Decrypted message: ncclqcjjbubvccen
Testing configuration: [22, 22, 23] Decrypted message: bucketngmcdbdbaa


---------------------------------------
  Decrypted message: bucketngmcdbdbaa
---------------------------------------


```

&nbsp;

I then tried checking the correct ring setting `[W, W, X]` in {{< url link="https://gchq.github.io/CyberChef/" text="CyberChef" >}} to verify if it will produce the correct flag or not and as expected with the correct ring options it produced the correct flag

![Untitled](/write-ups/ctftime/bucket/enigma-3.webp)

&nbsp;

&nbsp;

---

**Flag: `bucketngmcdbdbaa`**

---

&nbsp;

&nbsp;
