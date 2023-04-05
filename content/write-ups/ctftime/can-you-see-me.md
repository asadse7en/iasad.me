---
author: "Asad Ullah"
title: Can You See Me - VishwaCTF
summary: A write-up on stegonograpy challenge Can You See Me.

date: 2023-04-02T16:33:37+05:00

Section: "write-ups"

categories: ["writeup", "ctftime.org", "steganography"]
tags: ["binwalk", "sonic visualizer", "vishwactf 2023", "stectrogram", ".wav"]

draft: false

---


{{< 
ctftime 
name="Can You See Me" 
difficulty="Easy"  
points="100"
category="steganography"
>}}

&nbsp;

## Description

A magician made the seven wonders disappear. But people claim they can still feel their presence in the air.

**Download Attachments: {{< url link="https://drive.google.com/file/d/1cpbMiz-Oh1FdSQdRPHJVV8Ne2D824PEU/view?usp=sharing=" text="havealook.jpg" >}}**


## Approach

First, I checked filetype using **`file`** command. Then, I used **`exiftool`** to examine the metadata, but nothing interesting was there. Next, I used **`binwalk`** to search for any embedded files, and discovered an audio file. I extracted it using the command **`binwalk --dd=".*"`**.

```bash
┌──(kali㉿iasad)-[~/CTFs/VishwaCTF]
└─$ binwalk --dd=".*" havealook.jpg 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
134855        0x20EC7         Zip archive data, uncompressed size: 219888
323796        0x4F0D4         name: hereissomething.wav
```



The audio sounded like random noise. However, since it was a steganography challenge, I suspected that there might be a hidden message in the audio. I opened the file in Sonic Visualizer and added a spectrogram layer, which is commonly used for hiding text in audio files. To do this, go to "**Pane**" menu and select "**Add Spectrogram**". As expected, the flag was hidden in the audio file in plaintext and became visible in the spectrogram layer.

![spectrogram in sonic visualizer](/write-ups/ctftime/can-you-see-me/1.webp#center "spectrogram in sonic visualizer")


&nbsp;

---

**Flag: `VishwaCTF{n0w_y0u_533_m3}`**

---

&nbsp;

&nbsp;

