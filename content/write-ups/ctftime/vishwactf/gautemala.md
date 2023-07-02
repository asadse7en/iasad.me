---
author: "Asad Ullah"
title: Gautemala - VishwaCTF
summary: A write-up on stegonograpy challenge Gautemala.

date: 2023-04-02T17:33:37+05:00

Section: "write-ups"

categories: ["writeup", "ctftime.org", "steganography"]
tags: ["exiftool", "base64", "vishwactf", "metadata"]

draft: false

---


{{< 
ctftime 
name="Gautemala" 
difficulty="Easy"  
points="200"
category="steganography"
>}}

&nbsp;

## Description

My friend wanted to install an antivirus for his computer, but the creator of the antivirus was caught!
**Download Attachments: {{< url link="https://drive.google.com/file/d/1v6Sj7Pr-2X1EI6DH_1-_LBrpu8-kzdn1/view?usp=sharing" text="AV.gif" >}}**

## Approach

Got no success with tools such as **strings**, **binwalk**, and **stegsolve**, I decided to inspect the metadata using exiftool, where I found this.

```bash
┌──(kali㉿iasad)-[~/CTFs/VishwaCTF]
└─$ exiftool AV.gif 
ExifTool Version Number         : 12.57
File Name                       : AV.gif
Directory                       : .
File Size                       : 1112 kB
File Modification Date/Time     : 2023:03:31 07:10:45-04:00
File Access Date/Time           : 2023:04:02 09:04:34-04:00
File Inode Change Date/Time     : 2023:03:31 07:10:52-04:00
File Permissions                : -rw-r--r--
File Type                       : GIF
File Type Extension             : gif
MIME Type                       : image/gif
GIF Version                     : 89a
Image Width                     : 498
Image Height                    : 498
Has Color Map                   : Yes
Color Resolution Depth          : 8
Bits Per Pixel                  : 8
Background Color                : 0
Animation Iterations            : Infinite
Comment                         : dmlzaHdhQ1RGe3ByMDczYzdfdXJfM1gxRn0=
Frame Count                     : 17
Duration                        : 2.04 s
Image Size                      : 498x498
Megapixels                      : 0.248
```

&nbsp;

**Decoded the base64 and got the flag**

```bash
┌──(kali㉿iasad)-[~/CTFs/VishwaCTF]
└─$ echo "dmlzaHdhQ1RGe3ByMDczYzdfdXJfM1gxRn0=" | base64 -d

vishwaCTF{pr073c7_ur_3X1F}
```

&nbsp;

---

**Flag: `vishwaCTF{pr073c7_ur_3X1F}`**

---

&nbsp;

