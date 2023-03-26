---
author: "Asad Ullah"
title: Crack the Hash - TryHackMe
description: analyzing and cracking hashes using hashcat and diff online tools such as crackstation
summary: analyzing and cracking hashes using hashcat and diff online tools such as crackstation

date: 2023-03-25T02:54:51+05:00
tags: ["hash", "crackstation", "hashcat", "md5", "sha256", "NTLM", "ranbow tables"]
categories: [""]
draft: false

---


## Introduction

We will be tackling a hacking challenge today on tryhackme, where the community have created multiple challenges. you can participate in these challenges freely.

Specifically, I will be providing a walkthrough on the [crack the hash](https://tryhackme.com/room/crackthehash) challenge. This challenge comprises nine tasks, which I will explain in detail, one by one.

### Tools used for hash analyzing and cracking hashes

- **[hash-identifier](https://tools.kali.org/password-attacks/hash-identifier)**
- **[hash-analyzer](https://www.tunnelsup.com/hash-analyzer/)**
- **[hash-identification](https://www.onlinehashcrack.com/hash-identification.php)**
- **[hashcat](https://hashcat.net/wiki/doku.php?id=example_hashes)**
- **[crackstation](https://crackstation.net/)**
- **[hashes](https://hashes.com/en/tools/hash_identifier)**

## Task 1 - md5

**hash: `48bb6e862e54f2a795ffc4e541caed4d`**

First we need to identify the hash type using tools like `hash-identifier` or online hash analyzer sites like **[hash-analyzer](https://www.tunnelsup.com/hash-analyzer/)** 

![img1](/write-ups/tryhackme/crack-the-hash/1.png)

so it is an **`MD5`** hash now to crack it we can use tools like hashcat or online platform like **[crackstation](https://crackstation.net/)**

![img2](/write-ups/tryhackme/crack-the-hash/1.webp) 

&nbsp;
***
**Answer: `easy`**
***
&nbsp;

## Task 2 - sha1

**hash: `CBFDAC6008F9CAB4083784CBD1874F76618D2A97`**

similarly we can find this one also on **[crackstation](https://crackstation.net/).** this time it is a **`sha1`** hash

![img2](/write-ups/tryhackme/crack-the-hash/2.webp)


&nbsp;
***
**Answer: `password123`**
***
&nbsp;


## Task 3 - sha256

**hash: `1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032`**

again we will use **[crackstation](https://crackstation.net/).** this time it is a **`sha256`** hash

![img2](/write-ups/tryhackme/crack-the-hash/3.webp)

&nbsp;
***
**Answer: `letmein`**
***
&nbsp;

## Task 4 - bcrypt

**hash: `$2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom`**

Analyzing hash type using **[hash-analyzer](https://www.tunnelsup.com/hash-analyzer/)** we can see it is a **`bcrypt`** hash

![](/write-ups/tryhackme/crack-the-hash/4.webp)
This hash is difficult to crack using online tools, which is why we can use tools such as hashcat

## Hashcat

*Hashcat is a password cracking tool that uses brute-force, dictionary, and rule-based attacks to recover passwords from various types of hashed data.*

to install hashcat → **`sudo apt install hashcat`**. to crack hashes using hashcat we provide it the hash`hashed.txt` a wordlist i.e. `rockyou.txt` and **`-m`** switch for mode (*mode specify hash type*)for bcrypt mode is `-m 3200`

```
Asad@Kali:~/tools/hashcat$ ./hashcat64.bin -m 3200 hash.txt ../rockyou.txt
```

&nbsp;
***
**Answer: `bleh`**
***
&nbsp;

## Task 5 - md4

**Hash: `279412f945939ba78ce0758d3fd83daa`**

again the same process identify the hash using **[hash-analyzer](https://www.tunnelsup.com/hash-analyzer/)** and crack it using hashcat

`./hashcat64.bin -m 900 hash.txt rockyou.txt`

this one was also present on **[crackstation](https://crackstation.net/)**

![img2](/write-ups/tryhackme/crack-the-hash/5.webp)

&nbsp;
***
**Answer: `Ethernity22`**
***
&nbsp;


## Task 6 - sha256

**hash: `F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85`**

same drill - identify hash type → **[hash-analyzer](https://www.tunnelsup.com/hash-analyzer/)**

![img2](/write-ups/tryhackme/crack-the-hash/7.png)

### Hashcat

```bash
asad@kali:~/tools/hashcat$ ./hashcat64.bin -m 1400 hash.txt ../rockyou.txt
hashcat (v5.1.0) starting...

* Device #1: WARNING! Kernel exec timeout is not disabled.
             This may cause "CL_OUT_OF_RESOURCES" or related errors.
             To disable the timeout, see: https://hashcat.net/q/timeoutpatch
nvmlDeviceGetFanSpeed(): Not Supported

OpenCL Platform #1: NVIDIA Corporation
======================================
* Device #1: GeForce MX130, 501/2004 MB allocatable, 3MCU

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Applicable optimizers:
* Zero-Byte
* Early-Skip
* Not-Salted
* Not-Iterated
* Single-Hash
* Single-Salt
* Raw-Hash

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

ATTENTION! Pure (unoptimized) OpenCL kernels selected.
This enables cracking passwords and salts > length 32 but for the price of drastically reduced performance.
If you want to switch to optimized OpenCL kernels, append -O to your commandline.

Watchdog: Temperature abort trigger set to 90c

Dictionary cache hit:
* Filename..: ../rockyou.txt
* Passwords.: 14344385
* Bytes.....: 139921507
* Keyspace..: 14344385

f09edcb1fcefc6dfb23dc3505a882655ff77375ed8aa2d1c13f640fccc2d0c85:paule
                                                 
Session..........: hashcat
Status...........: Cracked
Hash.Type........: SHA2-256
Hash.Target......: f09edcb1fcefc6dfb23dc3505a882655ff77375ed8aa2d1c13f...2d0c85
Time.Started.....: Thu Sep  5 16:44:44 2019 (1 sec)
Time.Estimated...: Thu Sep  5 16:44:45 2019 (0 secs)
Guess.Base.......: File (../rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........: 12297.6 kH/s (3.26ms) @ Accel:1024 Loops:1 Thr:64 Vec:1
Recovered........: 1/1 (100.00%) Digests, 1/1 (100.00%) Salts
Progress.........: 196608/14344385 (1.37%)
Rejected.........: 0/196608 (0.00%)
Restore.Point....: 0/14344385 (0.00%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidates.#1....: 123456 -> piggy9
Hardware.Mon.#1..: Temp: 60c Util:  0% Core:1189MHz Mem:2505MHz Bus:4

Started: Thu Sep  5 16:44:42 2019
Stopped: Thu Sep  5 16:44:46 2019
```

**`f09edcb1fcefc6dfb23dc3505a882655ff77375ed8aa2d1c13f640fccc2d0c85:paule`**

### Crackstation

![img2](/write-ups/tryhackme/crack-the-hash/8.webp)

&nbsp;
***
**Answer: `pauke`**
***
&nbsp;

## task 7 - NTLM

**Hash: `1DFECA0C002AE40B8619ECF94819CC1B`**

this time it is a NTLM hash we can find it in crackstation

![img2](/write-ups/tryhackme/crack-the-hash/9.webp)
&nbsp;
***
**Answer: `n63umy8lkf4i`**
***
&nbsp;

## task 8 - sha512 (salted)

**hash: `$6$aReallyHardSalt$6WKUTqzq.UQQmrm0p/T7MPpMbGNnzXPMAXi4bJMl9be.cfi3/qxIf.hsGpS41BqMhSrHVXgMpdjS6xeKZAs02`**

**Salt: `aReallyHardSalt`**

**`$6$` is a sha512crypt**

it is a salted sha512 hash we can use hashcat to crack it

```bash
asad@kali:~/tools$ ./hashcat/hashcat64.bin -m 1800 sha512.hash rockyou.txt --session sha512
hashcat (v5.1.0) starting...

* Device #2: WARNING! Kernel exec timeout is not disabled.
             This may cause "CL_OUT_OF_RESOURCES" or related errors.
             To disable the timeout, see: https://hashcat.net/q/timeoutpatch
nvmlDeviceGetFanSpeed(): Not Supported

OpenCL Platform #1: Intel(R) Corporation
========================================
* Device #1: Intel(R) Core(TM) i5-8250U CPU @ 1.60GHz, skipped.

OpenCL Platform #2: NVIDIA Corporation
======================================
* Device #2: GeForce MX130, 501/2004 MB allocatable, 3MCU

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Applicable optimizers:
* Zero-Byte
* Single-Hash
* Single-Salt
* Uses-64-Bit

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

ATTENTION! Pure (unoptimized) OpenCL kernels selected.
This enables cracking passwords and salts > length 32 but for the price of drastically reduced performance.
If you want to switch to optimized OpenCL kernels, append -O to your commandline.

Watchdog: Temperature abort trigger set to 90c

Dictionary cache hit:
* Filename..: rockyou.txt
* Passwords.: 14344385
* Bytes.....: 139921507
* Keyspace..: 14344385

[s]tatus [p]ause [b]ypass [c]heckpoint [q]uit => s

Session..........: sha512
Status...........: Running
Hash.Type........: sha512crypt $6$, SHA512 (Unix)
Hash.Target......: $6$aReallyHardSalt$6WKUTqzq.UQQmrm0p/T7MPpMbGNnzXPM...ZAs02.
Time.Started.....: Thu Sep  5 18:23:56 2019 (10 mins, 59 secs)
Time.Estimated...: Thu Sep  5 19:27:46 2019 (52 mins, 51 secs)
Guess.Base.......: File (rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#2.........:     3746 H/s (18.22ms) @ Accel:64 Loops:32 Thr:32 Vec:1
Recovered........: 0/1 (0.00%) Digests, 0/1 (0.00%) Salts
Progress.........: 2463744/14344385 (17.18%)
Rejected.........: 0/2463744 (0.00%)
Restore.Point....: 2463744/14344385 (17.18%)
Restore.Sub.#2...: Salt:0 Amplifier:0-1 Iteration:2784-2816
Candidates.#2....: จคภจจ/ภ-ึจ -> zz336649
Hardware.Mon.#2..: Temp: 86c Util: 93% Core:1137MHz Mem:2505MHz Bus:4
```

&nbsp;
***
**Answer: `waka99`**
***
&nbsp;

## task 9 - sha1(salted)

**hash: `e5d8870e5bdd26602cab8dbe07a942c8669e56d6`**

**Salt**: **`tryhackme`**

can be solved using hashcat using mode **`-m 110`**

```
asad@kali:~/tools/hashcat$ ./hashcat64.bin -m 110 ../hash.sha1 ../rockyou.txt
```

&nbsp;
***
**Answer: `481616481616`**
***
&nbsp;

## Conclusion

*In conclusion, hash cracking is a process of attempting to recover passwords from hashed data using specialized software tools like Hashcat. It is a useful technique for security professionals to assess the strength of passwords and improve overall security measures. If you found this write-up helpful, please consider sharing it with others who may also benefit from learning about hash cracking.*