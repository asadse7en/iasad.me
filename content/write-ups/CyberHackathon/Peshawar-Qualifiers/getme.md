---
author: "Asad Ullah"
title: GetMe - CyberHackathon
description: Easy Web challenge
summary: Easy Web challenge
Section: "write-ups"

date: 2023-12-13T02:54:51+05:00
tags: 
- gitdump
categories:
- CyberHackathon
- writeup
draft: false

---


{{< 
ctf 
name="GetMe"
category="Web" 
difficulty="Easy"
points="50"  
creator_name="CyberHackathon" creator_link="https://patch.com.pk/" 
>}}


&nbsp;
&nbsp;

## Description
Web instance

## Approach

1. I initiated a search for subdirectories.
2. found `/.git` directory.
3. Used [this](https://github.com/arthaud/git-dumper) tool to extract data from `.git` using command: `sudo ./gitdumper.py http://ip/.git/ /tmp`.       
4. To view all commits, I executed the command: git log.
5. For detailed information about a specific commit, I used the command: git show AcommitHashABCDEF123, where "AcommitHashABCDEF123" is the actual commit hash. This is where you can find the flag.


&nbsp;

{{< flag "flag" "Flag{QCFANjVhSkR3dnl1R2VtZ2t2UmRQbmJiQT09NzVmNTc4MzZkMmEzN2M1NQ==}">}}

&nbsp;

&nbsp;
