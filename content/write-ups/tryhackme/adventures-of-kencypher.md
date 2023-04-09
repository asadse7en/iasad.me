---
author: "Asad Ullah"
title: Adventures Of Kencypher - TryHackMe
description: Explore The Life Story Of Kencypher And His Great Adventures.
summary: my writeup for cybrovert ctf challenges included osint, web, crypto and steg.
date: 2023-04-08T19:33:32+05:00

Section: "write-ups"

categories:
- tryhackme
tags:
- cybrovert
- web
- osint
- cryptography
- steganography

draft: false

---


{{< 
tryhackme 
name="Adventures Of Kencypher" 
os="Linux" 
difficulty="Beginner Friendly"  
points="720" 
creator_name="TryHackMe" creator_link="https://tryhackme.com/room/adventuresofkencypher" 
description="challanges on web, crypto, stego and OSINT"
>}}

&nbsp;

&nbsp;

&nbsp;


## Task 1 - Green Day Was My First Rock OSINT

&nbsp;

**Some OSINT on the author {{< url link="https://www.linkedin.com/in/waleed-amjad-069520217/" text="Waleed Amjad" >}}**

&nbsp;

### Find Kencypher Linkedin Profile Whats Username?

&nbsp;

**Answer: `Waleed`**

---

&nbsp;

### Which University Kencypher Studies?

&nbsp;

**Answer: `Muhammad Nawaz Shareef University of Agriculture, Multan`**

&nbsp;

---

### What Is Name Of First Blog Written By Kencypher?

&nbsp;

**Answer: `Time Is A Myth`**

&nbsp;


---

### How Many Blogs Has He Published So Far?

&nbsp;

**Answer: `14`**

&nbsp;

---

### Did The XSS Rat Interviewed Kencypher?

&nbsp;

**Answer: `Yes`**

&nbsp;

---

&nbsp;

### Kencypher Has Youtube Channel What Is Title Of His First  Video?

&nbsp;

**Answer: `Introduction Of TryHackMe and Channel In Urdu`**

&nbsp;

&nbsp;


---

## Task 2 - Jurassic Crypto

&nbsp;

### Crypto - 1

`WVZOQ2EySXpaSFZpUnpsb1drZFdhMGxJU21oaVUwSXpZVWRXZFVsSGEyZGtNa1o2U1VSWlBRPT0=`  it is a nested base64 code I used {{< url link="https://gchq.github.io/CyberChef/" text="Cyberchef">}} to decode it 

![base64](/write-ups/tryhackme/Adventures-Of-Kencypher/base64.webp)

&nbsp;

---

**Answer: `i downloaded ram when i was 6`**

---

&nbsp;


### Crypto - 2

`a61ae0b2c69dacd329d4c216da959665c9d94b5935a47368af02c102e922e209` 

Well Its Something About **BestFriend** Perhaps Its A Key

the hint suggested “RC2 Key Was Given In Question” so I again used {{< url link="https://gchq.github.io/CyberChef/" text="Cyberchef">}} rc2 decrypt with key “BestFriend” to decrypt it

![rc2](/write-ups/tryhackme/Adventures-Of-Kencypher/rc2.webp)

&nbsp;

&nbsp;

---

**Answer: `First Best Friend Was Abdullah`**

---

&nbsp;

### Crypto - 3

`$G678 %?KC y?7 +C8?J7J9E q2 !3G2 +?AFG2C` the hint suggested “Rotatory 47 And Rotatory 13 Combined To Form A Duo” so I first used **rot-47** then **rot-13**

![Untitled](/write-ups/tryhackme/Adventures-Of-Kencypher/rot47-13.webp)

&nbsp;

&nbsp;

---

**Answer: `First Game Was Metalslug On Coin Machine`**

---

&nbsp;


### Crypto - 4

```bash
-- -.--
..-. .- ...- --- ..- .-. .. - .
- --- -.--
.-- .- ...
-.-- --- -.-- ---
```

again used {{< url link="https://gchq.github.io/CyberChef/" text="Cyberchef">}} and converted from morse

![morse](/write-ups/tryhackme/Adventures-Of-Kencypher/morse.webp)

&nbsp;

&nbsp;

---

**Answer: `MY FAVOURITE TOY WAS YOYO`**

---

&nbsp;

### Crypto - 5

++++++++++[>+>+++>+++++++>++++++++++<<<<-]>>>++++++++.>+++++.------.++++++++.+++.-------------.++++++++++++.--------.<<++.>-----.>++++++++++++++.<<.>++++++++++++++.++++++++++.>-------..+++++++++++++.

for this one I did not knew what it is so I used {{< url link="https://www.dcode.fr/cipher-identifier" text="Cipher Identifier" >}} which suggested it is an encryption called **brainfuck**

![Untitled](/write-ups/tryhackme/Adventures-Of-Kencypher/cipher-id.webp)

so I used {{< url link="https://www.dcode.fr/brainfuck-language" text="Brainfuck Interpreter">}} to decode it 

![Untitled](/write-ups/tryhackme/Adventures-Of-Kencypher/brainfuck.webp)

&nbsp;

&nbsp;

---

**Answer: `Nickname Is Wally`**

---

&nbsp;

&nbsp;

&nbsp;

## Task 3 - GTA Steg

GTA Was My First Game. It Was GTA Sandreas. "**Ahh Shit Here We Go Again**". I Have Some Images From This Memory Sequence. Gather All The Fragments.
download challenge files {{< url link="https://drive.google.com/file/d/11XN7SyNlDpM3auqn03yXPgPBrPipSunN/view?usp=sharing" text="here">}}


![gta](/write-ups/tryhackme/Adventures-Of-Kencypher/gta-bike.webp)

&nbsp;

&nbsp;


### Who Is Character In Image1.jpg?

The Character In Image is the Main Antagonist Of This Game named `Big Smoke`

&nbsp;

---

**Answer: `Big Smoke`**

---

&nbsp;

### What Is Content Of Grains.txt?

the grains.txt is embedded in the gym.jpg file we can extract the hidden data using `steghide`

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme/kencipher/gta]
└─$ steghide extract -sf gym.jpg      
Enter passphrase: 
wrote extracted data to "grains.txt".

┌──(kali㉿iasad)-[~/CTFs/tryhackme/kencipher/gta]
└─$ cat grains.txt 
People Are Temporary Grains Are Eternal
```
&nbsp;

---

**Answer: `People Are Temporary Grains Are Eternal`**

---

&nbsp;

### What Is Content Of America.txt?

Passphrase Is Name Of Final Mission Of This Game

again the data can be extracted with steghide. this time The Passphrase Is Name Of Final Mission Of This Game which is **End of the Line**

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme/kencipher/gta]
└─$ steghide extract -sf guns.jpg 
Enter passphrase: 
wrote extracted data to "america.txt".

┌──(kali㉿iasad)-[~/CTFs/tryhackme/kencipher/gta]
└─$ cat america.txt 
Same Place I Buy My Pants Homes This Is America
```
&nbsp;

---

**Answer: `Same Place I Buy My Pants Homes This Is America`**

---

&nbsp;

### Look Inside Gang.jpg

I looked into it using string command and found this

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme/kencipher/gta]
└─$ cat gang.jpg
Exif
0210
"PUo520a
U\d\}GG
/=*Y
nu7V
337]
0Dh.
:)ii;
LlpsQ99
Welcome To Sanandreas Im CJ From Groove Street
```
&nbsp;

---

**Answer: `Welcome To Sanandreas Im CJ From Groove Street`**

---

&nbsp;

### What Is Object In police.tar.gz?

by looking the filetype using file command I found out that it is a `jpg` not a tar

so I just changed the extension and opened it

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme/kencipher/gta]
└─$ file police.tar.gz 
police.tar.gz: JPEG image data, JFIF standard 1.01, aspect ratio

mv police.tar.gz police.jpg
```
&nbsp;

---

**Answer: `Helicopter`**

---

&nbsp;

&nbsp;

&nbsp;

## Task 4 - Collage Fuzz

A custom wordlist was given for this task, so I decided to perform subdirectory enumeration using Durb and was able to discover three interesting pages.

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme/kencipher]
└─$ dirb http://10.10.24.112/ wordlist.txt 

-----------------
DIRB v2.22    
By The Dark Raver
-----------------

START_TIME: Sat Apr  8 15:45:06 2023
URL_BASE: http://10.10.24.112/
WORDLIST_FILES: wordlist.txt

-----------------

GENERATED WORDS: 33
---- Scanning URL: http://10.10.24.112/ ----
==> DIRECTORY: http://10.10.24.112/nishat/
==> DIRECTORY: http://10.10.24.112/singing/                       
==> DIRECTORY: http://10.10.24.112/guns/   
 
END_TIME: Sat Apr  8 15:46:00 2023
DOWNLOADED: 132 - FOUND: 0
```

&nbsp;

&nbsp;

### Whats The Song On One Of Web Pages?

on subdirectory `/singing` found this

![Untitled](/write-ups/tryhackme/Adventures-Of-Kencypher/singing.webp)

&nbsp;

---

the song playing on the page was `minority` from band green day

---

&nbsp;

### What Is Decoded Morse Code?

on subdirectory `/nishat` found this in the page source.

![Untitled](/write-ups/tryhackme/Adventures-Of-Kencypher/nishat-1.webp)

![Untitled](/write-ups/tryhackme/Adventures-Of-Kencypher/nishat-2.webp)

&nbsp;

---

the morse code translated to : `THE FINAL COUNT DOWN`

---

&nbsp;

### What Is Hidden Text?

on subdirectory `/guns` found the answer in `h1` of page

![Untitled](/write-ups/tryhackme/Adventures-Of-Kencypher/login.webp)

&nbsp;

---

Answer : `ROCK YOU LIKE A HURRICANE`

---

&nbsp;

&nbsp;

&nbsp;


## Task 5 - You Give Love A Bad Name (Web)

lightsaber123

Dont Let Go Of This String It Will Help You. Im Afraid I Cannot Guide You Any Further You Have To Proceed Without Me.

Good Luck

&nbsp;

### Nmap Scan

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme/kencipher]
└─$ nmap -A 10.10.120.178
Starting Nmap 7.93 ( https://nmap.org ) at 2023-04-08 15:00 EDT
Nmap scan report for 10.10.120.178 (10.10.120.178)
Host is up (0.29s latency).
Not shown: 998 closed tcp ports (conn-refused)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 6cc11cdbcd40579843a894400083cd18 (RSA)
|   256 35decdf59c546f9ad272df63e1fcbc04 (ECDSA)
|_  256 f032f5d727adcd4777e6e8baa275f2a3 (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: OuterSpace 
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed.
Nmap done: 1 IP address (1 host up) scanned in 36.60 seconds
```

&nbsp;

&nbsp;

### User Flag

from nmap scan we know `ssh` is open and the user flag is called yoda flag so `yoda` must be a user. now for the password I tried brute forcing with hydra but got no success. then I saw something in the description  `lightsaber123` I tried it as a password and success! got the user flag

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme/kencipher]
└─$ ssh yoda@10.10.8.0
yoda@10.10.8.0's password: 

Last login: Thu Aug  4 11:36:40 2022
yoda@rickroll:~$ 
yoda@rickroll:~$ ls
flag.txt  +sudo.txt

yoda@rickroll:~$ cat flag.txt
MNS{C1MB3R}

```

&nbsp;

&nbsp;

---

**Yoda flag: `MNS{C1MB3R}`**

---

&nbsp;

### Root Flag

there was another file `+sudo.txt` 

```bash
yoda@rickroll:~$ cat +sudo.txt 
e8885ce0fe2668e5e7ac322f2574d259
this is sudo password LMAO JUST KIDDING
BUT IT IS IM NOT KIDDING
ITS MASKED
```

the string was an md4 hash so I cracked it with John and found the password for the root `horizon` I used `su` to switch to root and got the flag

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme/kencipher]
└─$ john hash.txt --format=Raw-md4 --wordlist=/usr/share/wordlists/rockyou.txt
Using default input encoding: UTF-8
Loaded 1 password hash (Raw-MD4 [MD4 128/128 AVX 4x3])
Warning: no OpenMP support for this hash type, consider --fork=4
Press 'q' or Ctrl-C to abort, almost any other key for status
horizon          (?)     
1g 0:00:00:00 DONE (2023-04-08 17:48) 100.0g/s
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
```

```bash
yoda@rickroll:~$ su
Password: 
root@rickroll:/home/yoda# cd
root@rickroll:~# ls
flag.txt  snap
root@rickroll:~# cat flag.txt 
MNS{R0OT_B43ACH3D_OOPS}
```

&nbsp;

&nbsp;

---

**Root Flag: `MNS{R0OT_B43ACH3D_OOPS}`**

---

&nbsp;

### Web Flag

now for the web flag I looked in `/var/www/html`  where I found some interesting folders. i checked all but found the flag in `/space/ride/pocket/index.html`

![Untitled](/write-ups/tryhackme/Adventures-Of-Kencypher/web-flag.webp)

&nbsp;

&nbsp;


---

**Web Flag: `MNS{w3b_h4cked}`**

---

&nbsp;

## Conclusion
I hope you found my writeup informative and please feel free to share your thoughts in the comments. Special thanks to {{< url link="https://tryhackme.com/p/Kencypher69" text="kencypher69" >}} for creating these fantastic challenges.

&nbsp;
