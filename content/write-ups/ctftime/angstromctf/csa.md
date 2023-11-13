---
author: "Asad Ullah"
title: "Celeste Speedrunning Association - ångstromCTF"
description: 
summary: Write-up on web challenge Celeste Speedrunning Association.
date: 2023-04-27T00:04:24+05:00
Section: write-ups
categories:
- writeup
- ctftime.org
tags:
- angstormctf
- web
- epoch

draft: false

---

{{< 
ctf
name="Celeste Speedrunning Association" 
difficulty="Easy"  
points="20"
category="Web"
>}}

&nbsp;

&nbsp;


## Description

I love Celeste Speedrunning so much!!! It's so funny to watch!!!

[Here's my favorite site!](https://mount-tunnel.web.actf.co/)

## Approach

Upon examining the Source Code, it appears that the website is utilizing a hidden input field called "start" that utilizes the `Unix` epoch time to verify the present time.

![Untitled](/write-ups/ctftime/angstorm/source.webp)

Once the button is clicked, the server calculates the duration from the start time to when the request is received by the server. If the duration is less than 0 sec the flag will be displayed. However, this can only be accomplished by modifying the epoch value to a future time (higher value), then send the data to server

This can be done using a simple Python script.

```python
import requests

url = 'https://mount-tunnel.web.actf.co/submit'
data = {'start': '16825199999'}

response = requests.post(url, data=data)

print(response.text)
```

![Untitled](/write-ups/ctftime/angstorm/flag.webp)

&nbsp;

---

**Flag: `actf{wait_until_farewell_speedrun}`**

---

&nbsp;

&nbsp;
