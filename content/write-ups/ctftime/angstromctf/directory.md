---
author: "Asad Ullah"
title: "directory - ångstromCTF"
description: 
summary: Write-up on web challenge directory.
date: 2023-04-27T00:04:24+05:00
Section: write-ups
categories:
- writeup
- ctftime.org
tags:
- angstormctf
- bruteforce
- subdir
- curl

draft: True

---

{{< 
ctftime 
name="directory" 
difficulty="Easy"  
points="40"
category="Web"
>}}

&nbsp;

&nbsp;

## Description

[This](https://directory.web.actf.co/) is one of the directories of all time, and I would definitely rate it out of 10.

## Approach

The website has 5000 sub-directories and the objective is to identify the directory that contains the flag.

Since we know the format of the flag, we can develop a Python script that requests all pages on the website and checks if the response includes the flag format `actf{`.

```python
import concurrent.futures
import requests

# Set the URL pattern for the subpages
subpage_url_pattern = 'https://directory.web.actf.co/{}.html'

def check_subpage(i):
    subpage_url = subpage_url_pattern.format(i)
    subpage_response = requests.get(subpage_url)
    subpage_content = subpage_response.text
    if 'actf{' in subpage_content:
        print('Found the file in subpage:', subpage_url)
        return subpage_url
    else:
        print('Not found in subpage:', subpage_url)
        return None

# Use multiple threads to check the subpages in parallel
with concurrent.futures.ThreadPoolExecutor() as executor:
    futures = [executor.submit(check_subpage, i) for i in range(5000)]
    for future in concurrent.futures.as_completed(futures):
        if future.result():
            break
```

&nbsp;

found the flag in page `3054`

```bash
┌──(kali㉿iasad)-[~/CTFs/angstorm]
└─$ python3 solve.py
Not found in subpage: https://directory.web.actf.co/3044.html
Not found in subpage: https://directory.web.actf.co/3041.html
Not found in subpage: https://directory.web.actf.co/3049.html
Not found in subpage: https://directory.web.actf.co/3048.html
Not found in subpage: https://directory.web.actf.co/3043.html
Not found in subpage: https://directory.web.actf.co/3053.html
Not found in subpage: https://directory.web.actf.co/3051.html
Not found in subpage: https://directory.web.actf.co/3052.html
Not found in subpage: https://directory.web.actf.co/3050.html

Found the flag in subpage: https://directory.web.actf.co/3054.html
```

```bash
┌──(kali㉿iasad)-[~/CTFs/angstorm]
└─$ curl https://directory.web.actf.co/3054.html

actf{y0u_f0und_me_b51d0cde76739fa3}

```

&nbsp;

---

**Flag: `actf{y0u_f0und_me_b51d0cde76739fa3}`**

---

&nbsp;

&nbsp;
