---
author: "Asad Ullah"
title: Equals - CyberHackathon
description: Medium Exploitation challenge
summary: Medium Exploitation challenge
Section: "write-ups"

date: 2023-12-13T02:54:51+05:00
tags: 
- magic header
categories:
- CyberHackathon
- writeup
draft: false

---


{{< 
ctf 
name="Equals"
category="Exploitation" 
difficulty="Medium"
points="100"  
creator_name="CyberHackathon" creator_link="https://patch.com.pk/" 
>}}


&nbsp;
&nbsp;
## Description

We have a binary file and a remote instance available for connection. `nc <machine_ip> 1337`

## Approach

By analyzing the binary code using Ghidra, we can clearly spot the presence of format string vulnerability.

![Untitled](/write-ups/cyberhackathon/equals/0.png)

the content of **`local_78`** is directly passed to the **`printf`** function without any format specifier. This can lead to format string vulnerability. if we provides a malicious format string. To print values from the stack in clear text we will use the `%s` format specifier. In this case the 13th value on the stack was the flag which we got using payload `%13$s`

![Untitled](/write-ups/cyberhackathon/equals/1.png#center)


&nbsp;

{{< flag "flag" "Flag{d393030523f14e81f97c2491c62dc8ada41e4a4a}">}}

&nbsp;

&nbsp;
