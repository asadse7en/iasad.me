---
author: "Asad Ullah"
title: Cookie Bakery - CyberHackathon
description: Medium Web challenge
summary: Medium Web challenge
Section: "write-ups"

date: 2023-12-13T02:54:51+05:00
tags: 
- cookie temparing
categories:
- CyberHackathon
- writeup
draft: false

---


{{< 
ctf 
name="Cookie Bakery"
category="Web" 
difficulty="Medium"
points="100"  
creator_name="CyberHackathon" creator_link="https://patch.com.pk/" 
>}}


&nbsp;
&nbsp;

## Description
Web instance

## Approach

1. Initiated a search for subdirectories with`ffuf -u http://ip/FUZZ -w /wordlists/dirb/common.txt`  
2. Found /register directory
3. Created an account & login to it.
4.  A cookie was assigned to me:  `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTcwMjM3NjAwMCwianRpIjoiY2E4MmZlNzUtZTcyNi00NWY5LWE0ODctYzM2Y2EyZWRjNGJkIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6Im1hbGlrIiwibmJmIjoxNzAyMzc2MDAwLCJleHAiOjE3MDIzNzY5MDB9.NXnbWTOMpZLnHCacJ-KI-uRPL3faJ7a5tpeYwG3_1BM`
5. Tried different attacks but nothing worked, then I tried to bruteforce the secret key of JWT token using jwt_tool
    ![new](/write-ups/cyberhackathon/cookie-bakery/0.png)
6. Grabbed the secret key & pasted in [jwt.io](jwt.io) & then it allowed me to make changes to jwt token. I changed my username ‘malik’ to ‘admin’ & removed the "exp": 1702376900 
    ![new](/write-ups/cyberhackathon/cookie-bakery/1.png)

7. Copied the new jwt token & replaced with original token in burpsuite & got this flag:

&nbsp;

{{< flag "flag" "Flag{QCFANjVhSkR3dnl1R2VtZ2t2UmRQbmJiQT09NzVmNTc4MzZkMmEzN2M1NQ==}">}}

&nbsp;

&nbsp;
