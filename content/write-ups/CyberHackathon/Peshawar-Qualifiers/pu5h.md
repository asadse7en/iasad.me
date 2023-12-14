---
author: "Asad Ullah"
title: Pu5H - CyberHackathon
description: Simple OSINT challenge
summary: Simple OSINT challenge

Section: "write-ups"

date: 2023-12-13T02:54:51+05:00
tags: 
- archive.org
categories:
- CyberHackathon
- writeup
draft: false

---


{{< 
ctf 
name="Pu5H"
category="OSINT" 
difficulty="Easy"
points="50"  
creator_name="CyberHackathon" creator_link="https://patch.com.pk/" 
>}}


&nbsp;
&nbsp;


## Description

In 2018 Pushshift it is primarily known for its complete dump of the public Reddit API data got leaked of the DB on the internet. so can you find that DB?

Flag Format: Flag{MD5}

## Approach

Searching for information about the breach, we come across this [webpage](https://archive.org/download/files.pushshift.io_201812).

![Untitled](/write-ups/cyberhackathon/pu5h/Untitled%20(80).png)

Following the instructions in the description, we have to download the SQLite database and retrieve its MD5.

```bash
┌──(n4ruto㉿iasad.me)-[~/CTFs/CyberHackathon/pu5h]
└─$ md5sum files.pushshift.io_201812_meta.sqlite

c4457118752e840486a452d4df7264dd
```

&nbsp;

{{< flag "flag" "Flag{c4457118752e840486a452d4df7264dd}">}}

&nbsp;

&nbsp;
