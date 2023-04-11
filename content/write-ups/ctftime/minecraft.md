---
author: "Asad Ullah"
title: "Minecraft - BucketCTF"
description: 
summary: Write-up on Misc challenge Minecraft.
date: 2023-04-10T02:08:24+05:00
Section: write-ups
categories:
- writeup
- ctftime.org
tags:
- bucketctf
- misc
- log

draft: false

---

{{< 
ctftime 
name="Minecraft" 
difficulty="Easy"  
points="200"
category="Misc"
>}}

&nbsp;

&nbsp;

## Description

I just started playing Minecraft for my computer science class and forgot to remove a sign with my password before exiting the world. Could you please check what my password is.

Download Attachments {{< url link="https://storage.ebucket.dev/bucketctfMC.mcworld" text="here" >}}

&nbsp;

## Approach

The file was named bucketctfMC.mcworld and had a file extension of `.mcworld` However, upon checking the file type, I discovered that it was actually a zip file in disguise. To access its contents, I simply renamed the file extension to .zip and extracted it.

 &nbsp;

```bash
┌──(kali㉿iasad)-[~/CTFs/BucketCTF]
└─$ file bucketctfMC.mcworld                   
bucketctfMC.mcworld: Zip archive data, at least v4.5 to extract

┌──(kali㉿iasad)-[~/CTFs/BucketCTF]
└─$ mv bucketctfMC.mcworld bucketctfMC.zip     

┌──(kali㉿iasad)-[~/CTFs/BucketCTF]
└─$ unzip bucketctfMC.zip 
Archive:  bucketctfMC.zip
  inflating: db/000003.log           
  inflating: db/CURRENT              
  inflating: db/MANIFEST-000002      
  inflating: level.dat               
  inflating: level.dat_old           
  inflating: levelname.txt           
  inflating: world_icon.jpeg
```

&nbsp;

one particularly interesting file was `db/000003.log` so I checked its contents using `glogg` tool.
I just searched for bucket in the logs and got the flag

&nbsp;

![logs](/write-ups/ctftime/bucket/minecraft.webp)

&nbsp;

---

**Flag: `bucket{1L0V3MIN3CRAFT_1c330e9105f1}`**

---

&nbsp;

&nbsp;

