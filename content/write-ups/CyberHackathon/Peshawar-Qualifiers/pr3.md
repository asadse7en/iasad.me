---
author: "Asad Ullah"
title: Pr3 - CyberHackathon
description: Medium Forensics challenge
summary: Medium Forensics challenge
Section: "write-ups"

date: 2023-12-13T02:54:51+05:00
tags: 
- prefetch
categories:
- CyberHackathon
- writeup
draft: false

---


{{< 
ctf 
name="Pr3"
category="Forensics" 
difficulty="Medium"
points="100"  
creator_name="CyberHackathon" creator_link="https://patch.com.pk/" 
>}}


&nbsp;
&nbsp;

## Description

Hello my friend I'm sure my PC infected by malicious program. Can you locate where that program was?

Flag Format: Flag{\*****\****\*******\*****\****\***********}

## Approach

We have a 7z file containing many prefetch files. Utilizing [PECmd](https://github.com/EricZimmerman/PECmd) from Eric Zimmerman, we can generate a single CSV file from all the prefetch files.

After downloading the tool, we can use it to produce a CSV file.

```bash
PECmd.exe -d "C:\Users\asads\Downloads\PECmd" --csv "C:\Users\asads\PECmd"
```

&nbsp;

![Untitled](/write-ups/cyberhackathon/pr3/Untitled%20(82).png)

Legitimate dllhost.exe runs only from System32. Other locations point to an imposter. And indeed, it turned out to be one.


&nbsp;

{{< flag "flag" "Flag{\USERS\WORK\APPDATA\LOCAL\TEMP\DLLH0ST.EXE}">}}

&nbsp;

&nbsp;
