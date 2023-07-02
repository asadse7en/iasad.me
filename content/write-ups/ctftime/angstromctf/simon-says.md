---
author: "Asad Ullah"
title: "Simon says - ångstromCTF"
description: 
summary: Write-up on Misc challenge simon says.
date: 2023-04-27T00:33:24+05:00
Section: write-ups
categories:
- writeup
- ctftime.org
tags:
- angstormctf
- misc
- header

draft: false

---

{{< 
ctftime 
name="Simon says" 
difficulty="Easy"  
points="40"
category="Misc"
>}}

&nbsp;

&nbsp;


## Description

This guy named Simon gave me a bunch of tasks to complete and not a lot of time. He wants to run a unique zoo but needs the names for his animals. Can you help me?

`nc challs.actf.co 31402`

## Approach

when we connect to the server using `nc` we receive a prompt: `Combine the first 3 letters of {animal name} with the last 3 letters of {animal name}`   

However, we are need to provide the correct answer within 5 seconds and repeat this more than 10 times. Manually doing this task is not feasible, but this can be easily automated with a python script

```python
#!/usr/bin/env python3
import socket

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(('challs.actf.co', 31402))

while True:
    response = s.recv(1024).decode().strip()

    if response.startswith("actf{"):
        print(f"Received flag: {response}")
        break

    words = response.split()
    if len(words) < 7:
        print(f"Invalid response: {response}")
        break
    answer = f"{words[6][:3]}{words[-1][-3:]}"
    print(f"Request: {response}")
    print(f"Response: {answer}")
    print("\n")

    s.sendall(answer.encode() + b"\n")

s.close()
```

I attempted to run the script on my local machine, but didn't recieved any flag. However, when I used Google Shell, it worked without any issues. I think this could be latency issue.

![Untitled](/write-ups/ctftime/angstorm/google-shell.webp)

&nbsp;

---

**Flag: `actf{simon_says_you_win}`**

---

&nbsp;

&nbsp;
