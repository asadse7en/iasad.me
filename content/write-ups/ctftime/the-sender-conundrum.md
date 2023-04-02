---
author: "Asad Ullah"
title: The Sender Conundrum - VishwaCTF
summary: A write-up on stegonograpy challenge The Sender Conundrum.

date: 2023-04-02T18:33:37+05:00

Section: "write-ups"

categories: ["writeup", "ctftime.org", "forenics"]
tags: ["hash cracking", "vishwactf-2023", "john", "zip2john"]

draft: false

---


{{< 
ctftime 
name="The Sender Conundrum" 
difficulty="Easy"  
points="200"
category="Forensics"
>}}

&nbsp;



## Description

Marcus Got a Mysterious mail promising a flag if he could crack the password to the file.****

**Download Attachments: TheEmail.eml  unzipme.zip**

## Approach

we were given two files **unzipme.zip** that require password and an **TheEmail.eml** which include a hint for the zip password in the form of a riddle

```bash
<p></p>Hello Marcus Cooper,<br>
 You are one step behind from finding your flag. <br>
 Here is a Riddle: <br>
 I am a noun and not a verb or an adverb.<br>
 I am given to you at birth and never taken away,<br>
 You keep me until you die, come what may.<br>
 What am I?<br>
```

My guessing was it is either ( name, soul, spirit, identity, breath, life ) or a name of person. I tried all these but nothing worked. I even tried to brute force it with ****top_1000_usa_malenames_english.txt**** which is well known for username enumeration but no success.

then i tried to bruteforce it with **rockyou.txt** and it worked.

```bash
┌──(kali㉿iasad)-[~/CTFs/VishwaCTF]
└─$ john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt 
Using default input encoding: UTF-8
Loaded 1 password hash (PKZIP [32/64])
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
BrandonLee       (unzipme.zip/unzipme/flag.txt)     
1g 0:00:00:02 DONE (2023-04-02 09:08) 0.3921g/s 4452Kp/s 4452Kc/s 4452KC/s
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
```

The flag was in plaintext after unzipping the "unzipme.zip" file using the password “BrandonLee”

&nbsp;

---

**Flag:** `vishwaCTF{1d3n7i7y_7h3f7_is_n0t_4_j0k3}`

---

&nbsp;

## My Thoughts

I feel somewhat let down by this challenge because the riddle hinted that the password might be a name, which turned out to be true. However, the password wasn't found in any of the popular name wordlists, such as **top_1000_usa_malenames_english.txt [🔗](https://github.com/x-o-r-r-o/Cracking/blob/master/top_1000_usa_malenames_english.txt)** or **names.txt [🔗](https://github.com/huntergregal/wordlists/blob/master/names.txt)** which I attempted to brute-force using the John, with no success. Frankly, it never occurred to me to use the **rockyou.txt** list for brute-forcing a name. this took up a lot of time 😿


&nbsp;
