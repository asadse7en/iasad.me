---
author: "Asad Ullah"
title: "shortcircuit - ångstromCTF"
description: 
summary: Write-up on web challenge shortcircuit.
date: 2023-04-27T00:04:24+05:00
Section: write-ups
categories:
- writeup
- ctftime.org
tags:
- angstormctf
- javascript
- reverse
- flag

draft: false

---

{{< 
ctftime 
name="shortcircuit" 
difficulty="Easy"  
points="40"
category="Web"
>}}

&nbsp;

## Description

[Bzzt](https://shortcircuit.web.actf.co/)

## Approach

Looking at Source Code the JavaScript performs some manipulations on the input password by breaking it up into chunks and swapping characters around. The challenge requires reversing these manipulations to obtain the original password. This can be achieved by analyzing the JavaScript code and writing a Python script to reverse the manipulations.

Here's a Python script that reverses the operations of chunking and swapping on the given hard-coded string to obtain the original string.

```python
def reverse_swap(x):
    t = x[2]
    x[2] = x[3]
    x[3] = t

    t = x[3]
    x[3] = x[1]
    x[1] = t

    t = x[1]
    x[1] = x[2]
    x[2] = t

    t = x[0]
    x[0] = x[3]
    x[3] = t

    return x

def reverse_chunk(x, n):
    return ''.join(x)

password = '7e08250c4aaa9ed206fd7c9e398e2}actf{cl1ent_s1de_sucks_544e67ef12024523398ee02fe7517fffa92516317199e454f4d2bdb04d9e419ccc7'

password_chunks = [password[i:i+30] for i in range(0, len(password), 30)]
password_chunks = reverse_swap(password_chunks)
password = reverse_chunk(password_chunks, 30)
print(password)
```

&nbsp;

---

**Flag:`actf{cl1ent_s1de_sucks_544e67e6317199e454f4d2bdb04d9e419ccc7f12024523398ee02fe7517fffa92517e08250c4aaa9ed206fd7c9e398e2}`**

---

&nbsp;

&nbsp;
