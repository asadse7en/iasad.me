---
author: "Asad Ullah"
title: Just Files - VishwaCTF
summary: A write-up on steganography challenge Just Files.
date: 2023-04-02T19:33:37+05:00

Section: "write-ups"

categories: ["writeup", "ctftime.org", "steganography"]
tags: ["steghide", "morse cdoe", "vishwactf 2023","binwalk", "steg"]

draft: false

---


{{< 
ctftime 
name="Just Files" 
difficulty="Easy"  
points="200"
category="steganography"
>}}

&nbsp;


## Description
They are not what you see. They are different. Believe me.


**Download Attachments : {{< url link="https://drive.google.com/file/d/1g_rO8ATVC1_CURqJFTsB_OPadB1ixRNd/view?usp=sharing" text="yes_its_a_zip_file_withnosecurity.zip" >}}**

## Approach

Upon extracting the zip archive, we discovered two images, but one of them, a `PNG` was unusually large at 11MB. This raised suspicions that there may be something hidden or embedded within the file.

![extracted files](/write-ups/ctftime/just-files/1.webp#center "extracted files")

&nbsp;

 i used binwalk to extract it 

```bash
┌──(kali㉿iasad)-[~/CTFs/VishwaCTF]
└─$ binwalk -e Get_It_2.png

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 1920 x 1080, 8-bit/color RGBA
26927         0x692F          Zip archive data, at least v2.0 to extract
11276693      0xAC1195        name: Its_a_Morse_not_a_joke_take_it_seriously.wav
```

&nbsp;

I attempted to decrypt `.wav`  containing Morse code using {{< url link="https://morsecode.world/international/decoder/audio-decoder-adaptive.html" text="Morse Decoder" >}}, and here are the results.

![decrypting morse code from audio](/write-ups/ctftime/just-files/2.webp#center "decrypting morse code from audio")

&nbsp;

After deciphering the Morse code. it instructed me to reverse the audio and identify the protagonist. Therefore, I used {{< url link="https://mp3cut.net/reverse-audio" text="Audio Reverser" >}} to reverse the file. upon listening to the reversed audio, I discovered that it was a scene from the TV series Lucifer. I entered the flag as `vishwaCTF{lucifer}` but it was rejected.

Next, I searched for any hidden data using `steghide` with the passphrase "lucifer" and discovered some hints.

```bash
┌──(kali㉿iasad)-[~/CTFs/VishwaCTF]
└─$ steghide extract -sf Its_a_Morse_not_a_joke_take_it_seriously.wav 
Enter passphrase: 
wrote extracted data to "nothing.txt".

cat nothing.txt 
There is nothing here
listen it carefully 
You should check the another picture(is it really a png)

And i want to tell you a story : 
Once upon a time i got a name and it was password of something i was listening.

soo just listen it carefully.
```

&nbsp;

Although `steghide` doesn't support `PNG` files, the hint suggested that the file might not actually be a PNG. As I knew that there is a `WAV` file embedded in `PNG` Therefore, I attempted to use `steghide` on the `WAV` file instead, with the passphrase "lucifer." I was successful in extracting the flag format.

```bash
┌──(kali㉿iasad)-[~/CTFs/VishwaCTF]
└─$ steghide extract -sf Its_a_Morse_not_a_joke_take_it_seriously.wav 
Enter passphrase: 
wrote extracted data to "flag.txt"

cat flag.txt 
Nice 
The flag is {the name of protagonist_S01E03}.

name of protagonist should be in small case.
```

&nbsp;

the name of the protagonist is lucifer so the flag will be `{lucifer_S01E03}`

&nbsp;

---

**Flag: `vishwaCTF{lucifer_S01E03}`**

---

&nbsp;
