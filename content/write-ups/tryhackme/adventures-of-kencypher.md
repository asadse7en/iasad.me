---
author: "Asad Ullah"
title: Adventures Of Kencypher - TryHackMe
description: Explore The Life Story Of Kencypher And His Great Adventures.
summary: my writeup for cybrovert ctf challenges included osint, web, crypto and steg.
date: 2023-04-08T19:33:32+05:00

Section: "write-ups"

categories:
- tryhackme
tags:
- cybrovert
- web
- osint
- cryptography
- steganography

draft: false

---


{{< 
tryhackme 
name="Adventures Of Kencypher" 
os="Linux" 
difficulty="Beginner Friendly"  
creator_name="TryHackMe" creator_link="https://tryhackme.com/room/adventuresofkencypher" 
description="challanges on web, crypto, stego and OSINT"
>}}

&nbsp;

&nbsp;

&nbsp;


## Task 1 - Green Day Was My First Rock OSINT

&nbsp;

To gather OSINT on the author **{{< url link="https://www.linkedin.com/in/waleed-amjad-069520217/" text="Waleed Amjad" >}}**, a quick search for "Kencypher" on Google yields his LinkedIn, Medium, and Youtube profiles, providing all the necessary information.


&nbsp;

### OSINT - 1

&nbsp;

**Find Kencypher Linkedin Profile Whats Username?**

**Answer: `Waleed`**

&nbsp;

---

&nbsp;

### OSINT - 2

&nbsp;

**Which University Kencypher Studies?**

**Answer: `Muhammad Nawaz Shareef University of Agriculture, Multan`**

&nbsp;

---

### OSINT - 3

&nbsp;

**What Is Name Of First Blog Written By Kencypher?**


**Answer: `Time Is A Myth`**

&nbsp;


---

### OSINT - 4

&nbsp;

**How Many Blogs Has He Published So Far?**

**Answer: `14`**

&nbsp;

---

### OSINT - 5

&nbsp;

**Did The XSS Rat Interviewed Kencypher?**

**Answer: `Yes`**

&nbsp;

---

&nbsp;

### OSINT - 6

&nbsp;

**Kencypher Has Youtube Channel What Is Title Of His First  Video?**

**Answer: `Introduction Of TryHackMe and Channel In Urdu`**

&nbsp;

&nbsp;

&nbsp;

---

## Task 2 - Jurassic Crypto

&nbsp;

### Crypto - 1

`WVZOQ2EySXpaSFZpUnpsb1drZFdhMGxJU21oaVUwSXpZVWRXZFVsSGEyZGtNa1o2U1VSWlBRPT0=`  it is a nested base64 code I used {{< url link="https://gchq.github.io/CyberChef/" text="Cyberchef">}} to decode it 

![base64](/write-ups/tryhackme/Adventures-Of-Kencypher/base64.webp)

&nbsp;

---

**Answer: `i downloaded ram when i was 6`**

---

&nbsp;


### Crypto - 2

`a61ae0b2c69dacd329d4c216da959665c9d94b5935a47368af02c102e922e209` 

Well Its Something About **BestFriend** Perhaps Its A Key

the hint suggested “RC2 Key Was Given In Question” so I again used {{< url link="https://gchq.github.io/CyberChef/" text="Cyberchef">}} rc2 decrypt with key “BestFriend” to decrypt it

![rc2](/write-ups/tryhackme/Adventures-Of-Kencypher/rc2.webp)

&nbsp;

&nbsp;

---

**Answer: `First Best Friend Was Abdullah`**

---

&nbsp;

### Crypto - 3

`$G678 %?KC y?7 +C8?J7J9E q2 !3G2 +?AFG2C` the hint suggested “Rotatory 47 And Rotatory 13 Combined To Form A Duo” so I first used **rot-47** then **rot-13**

![Untitled](/write-ups/tryhackme/Adventures-Of-Kencypher/rot47-13.webp)

&nbsp;

&nbsp;

---

**Answer: `First Game Was Metalslug On Coin Machine`**

---

&nbsp;


### Crypto - 4

```bash
-- -.--
..-. .- ...- --- ..- .-. .. - .
- --- -.--
.-- .- ...
-.-- --- -.-- ---
```

again used {{< url link="https://gchq.github.io/CyberChef/" text="Cyberchef">}} and converted from morse

![morse](/write-ups/tryhackme/Adventures-Of-Kencypher/morse.webp)

&nbsp;

&nbsp;

---

**Answer: `MY FAVOURITE TOY WAS YOYO`**

---

&nbsp;

### Crypto - 5

++++++++++[>+>+++>+++++++>++++++++++<<<<-]>>>++++++++.>+++++.------.++++++++.+++.-------------.++++++++++++.--------.<<++.>-----.>++++++++++++++.<<.>++++++++++++++.++++++++++.>-------..+++++++++++++.

for this one I did not knew what it is so I used {{< url link="https://www.dcode.fr/cipher-identifier" text="Cipher Identifier" >}} which suggested it is an encryption called **brainfuck**

![Untitled](/write-ups/tryhackme/Adventures-Of-Kencypher/cipher-id.webp)

so I used {{< url link="https://www.dcode.fr/brainfuck-language" text="Brainfuck Interpreter">}} to decode it 

![Untitled](/write-ups/tryhackme/Adventures-Of-Kencypher/brainfuck.webp)

&nbsp;

&nbsp;

---

**Answer: `Nickname Is Wally`**

---


&nbsp;

### Crypto - 6

Well This Is Big Program With Key "cartoon”

```bash
00100011 01101001 01101110 01100011 01101100 01110101 01100100 01100101 00100000 00111100 01101001 01101111 01110011 01110100 01110010 01100101 01100001 01101101 00111110 00001010 00100011 01101001 01101110 01100011 01101100 01110101 01100100 01100101 00100000 00111100 01110011 01110100 01110010 01101001 01101110 01100111 00111110 00001010 00100011 01101001 01101110 01100011 01101100 01110101 01100100 01100101 00100000 00111100 01100001 01101100 01100111 01101111 01110010 01101001 01110100 01101000 01101101 00111110 00001010 00001010 01110101 01110011 01101001 01101110 01100111 00100000 01101110 01100001 01101101 01100101 01110011 01110000 01100001 01100011 01100101 00100000 01110011 01110100 01100100 00111011 00001010 00001010 01110011 01110100 01110010 01101001 01101110 01100111 00100000 01100101 01101110 01100011 01110010 01111001 01110000 01110100 00101000 01110011 01110100 01110010 01101001 01101110 01100111 00100000 01101101 01110011 01100111 00101100 00100000 01110011 01110100 01110010 01101001 01101110 01100111 00100000 01101011 01100101 01111001 00101001 00100000 01111011 00001010 00100000 00100000 00100000 00100000 01110011 01110100 01110010 01101001 01101110 01100111 00100000 01100101 01101110 01100011 01110010 01111001 01110000 01110100 01100101 01100100 01011111 01101101 01110011 01100111 00100000 00111101 00100000 00100010 00100010 00111011 00001010 00100000 00100000 00100000 00100000 01101001 01101110 01110100 00100000 01101010 00100000 00111101 00100000 00110000 00111011 00001010 00100000 00100000 00100000 00100000 01100110 01101111 01110010 00100000 00101000 01101001 01101110 01110100 00100000 01101001 00100000 00111101 00100000 00110000 00111011 00100000 01101001 00100000 00111100 00100000 01101101 01110011 01100111 00101110 01101100 01100101 01101110 01100111 01110100 01101000 00101000 00101001 00111011 00100000 01101001 00101011 00101011 00101001 00100000 01111011 00001010 00100000 00100000 00100000 00100000 00100000 00100000 00100000 00100000 01100101 01101110 01100011 01110010 01111001 01110000 01110100 01100101 01100100 01011111 01101101 01110011 01100111 00100000 00101011 00111101 00100000 01101101 01110011 01100111 01011011 01101001 01011101 00100000 01011110 00100000 01101011 01100101 01111001 01011011 01101010 01011101 00111011 00001010 00100000 00100000 00100000 00100000 00100000 00100000 00100000 00100000 01101010 00100000 00111101 00100000 00101000 01101010 00100000 00101011 00100000 00110001 00101001 00100000 00100101 00100000 01101011 01100101 01111001 00101110 01101100 01100101 01101110 01100111 01110100 01101000 00101000 00101001 00111011 00001010 00100000 00100000 00100000 00100000 01111101 00001010 00100000 00100000 00100000 00100000 01110010 01100101 01110100 01110101 01110010 01101110 00100000 01100101 01101110 01100011 01110010 01111001 01110000 01110100 01100101 01100100 01011111 01101101 01110011 01100111 00111011 00001010 01111101 00001010 00001010 01110011 01110100 01110010 01101001 01101110 01100111 00100000 01100100 01100101 01100011 01110010 01111001 01110000 01110100 00101000 01110011 01110100 01110010 01101001 01101110 01100111 00100000 01101101 01110011 01100111 00101100 00100000 01110011 01110100 01110010 01101001 01101110 01100111 00100000 01101011 01100101 01111001 00101001 00100000 01111011 00001010 00100000 00100000 00100000 00100000 01110011 01110100 01110010 01101001 01101110 01100111 00100000 01100100 01100101 01100011 01110010 01111001 01110000 01110100 01100101 01100100 01011111 01101101 01110011 01100111 00100000 00111101 00100000 00100010 00100010 00111011 00001010 00100000 00100000 00100000 00100000 01101001 01101110 01110100 00100000 01101010 00100000 00111101 00100000 00110000 00111011 00001010 00100000 00100000 00100000 00100000 01100110 01101111 01110010 00100000 00101000 01101001 01101110 01110100 00100000 01101001 00100000 00111101 00100000 00110000 00111011 00100000 01101001 00100000 00111100 00100000 01101101 01110011 01100111 00101110 01101100 01100101 01101110 01100111 01110100 01101000 00101000 00101001 00111011 00100000 01101001 00101011 00101011 00101001 00100000 01111011 00001010 00100000 00100000 00100000 00100000 00100000 00100000 00100000 00100000 01100100 01100101 01100011 01110010 01111001 01110000 01110100 01100101 01100100 01011111 01101101 01110011 01100111 00100000 00101011 00111101 00100000 01101101 01110011 01100111 01011011 01101001 01011101 00100000 01011110 00100000 01101011 01100101 01111001 01011011 01101010 01011101 00111011 00001010 00100000 00100000 00100000 00100000 00100000 00100000 00100000 00100000 01101010 00100000 00111101 00100000 00101000 01101010 00100000 00101011 00100000 00110001 00101001 00100000 00100101 00100000 01101011 01100101 01111001 00101110 01101100 01100101 01101110 01100111 01110100 01101000 00101000 00101001 00111011 00001010 00100000 00100000 00100000 00100000 01111101 00001010 00100000 00100000 00100000 00100000 01110010 01100101 01110100 01110101 01110010 01101110 00100000 01100100 01100101 01100011 01110010 01111001 01110000 01110100 01100101 01100100 01011111 01101101 01110011 01100111 00111011 00001010 01111101 00001010 00001010 01101001 01101110 01110100 00100000 01101101 01100001 01101001 01101110 00101000 00101001 00100000 01111011 00001010 00100000 00100000 00100000 00100000 01110011 01110100 01110010 01101001 01101110 01100111 00100000 01110000 01110010 01101111 01101101 01110000 01110100 00100000 00111101 00100000 00100010 01011100 01111000 00110100 01100100 01011100 01111000 00110111 00111001 01011100 01111000 00110010 00110000 01011100 01111000 00110100 00110110 01011100 01111000 00110110 00110001 01011100 01111000 00110111 00110110 01011100 01111000 00110010 00110000 01011100 01111000 00110100 00110011 01011100 01111000 00110110 00110001 01011100 01111000 00110111 00110010 01011100 01111000 00110111 00110100 01011100 01111000 00110110 01100110 01011100 01111000 00110110 01100110 01011100 01111000 00110110 01100101 01011100 01111000 00110010 00110000 01011100 01111000 00110100 00111001 01011100 01111000 00110111 00110011 01011100 01111000 00110010 00110000 01011100 01111000 00110100 00110010 01011100 01111000 00110110 00110101 01011100 01111000 00110110 01100101 01011100 01111000 00110010 00110000 01011100 01111000 00110011 00110001 01011100 01111000 00110011 00110000 00100010 00111011 00001010 00100000 00100000 00100000 00100000 01110011 01110100 01110010 01101001 01101110 01100111 00100000 01101011 01100101 01111001 00100000 00111101 00100000 00100010 01100011 01100001 01110010 01110100 01101111 01101111 01101110 00100010 00111011 00001010 00100000 00100000 00100000 00100000 01110011 01110100 01110010 01101001 01101110 01100111 00100000 01100101 01101110 01100011 01110010 01111001 01110000 01110100 01100101 01100100 01011111 01110000 01110010 01101111 01101101 01110000 01110100 00100000 00111101 00100000 01100101 01101110 01100011 01110010 01111001 01110000 01110100 00101000 01110000 01110010 01101111 01101101 01110000 01110100 00101100 00100000 01101011 01100101 01111001 00101001 00111011 00001010 00100000 00100000 00100000 00100000 01110011 01110100 01110010 01101001 01101110 01100111 00100000 01101001 01101110 01110000 01110101 01110100 01011111 01101011 01100101 01111001 00111011 00001010 00100000 00100000 00100000 00100000 01100011 01101111 01110101 01110100 00100000 00111100 00111100 00100000 00100010 01000101 01101110 01110100 01100101 01110010 00100000 01110100 01101000 01100101 00100000 01101011 01100101 01111001 00111010 00100000 00100010 00111011 00001010 00100000 00100000 00100000 00100000 01100011 01101001 01101110 00100000 00111110 00111110 00100000 01101001 01101110 01110000 01110101 01110100 01011111 01101011 01100101 01111001 00111011 00001010 00100000 00100000 00100000 00100000 01110100 01110010 01100001 01101110 01110011 01100110 01101111 01110010 01101101 00101000 01101001 01101110 01110000 01110101 01110100 01011111 01101011 01100101 01111001 00101110 01100010 01100101 01100111 01101001 01101110 00101000 00101001 00101100 00100000 01101001 01101110 01110000 01110101 01110100 01011111 01101011 01100101 01111001 00101110 01100101 01101110 01100100 00101000 00101001 00101100 00100000 01101001 01101110 01110000 01110101 01110100 01011111 01101011 01100101 01111001 00101110 01100010 01100101 01100111 01101001 01101110 00101000 00101001 00101100 00100000 00111010 00111010 01110100 01101111 01101100 01101111 01110111 01100101 01110010 00101001 00111011 00001010 00100000 00100000 00100000 00100000 01101001 01100110 00100000 00101000 01101001 01101110 01110000 01110101 01110100 01011111 01101011 01100101 01111001 00100000 00111101 00111101 00100000 01101011 01100101 01111001 00101001 00100000 01111011 00001010 00100000 00100000 00100000 00100000 00100000 00100000 00100000 00100000 01110011 01110100 01110010 01101001 01101110 01100111 00100000 01100100 01100101 01100011 01110010 01111001 01110000 01110100 01100101 01100100 01011111 01110000 01110010 01101111 01101101 01110000 01110100 00100000 00111101 00100000 01100100 01100101 01100011 01110010 01111001 01110000 01110100 00101000 01100101 01101110 01100011 01110010 01111001 01110000 01110100 01100101 01100100 01011111 01110000 01110010 01101111 01101101 01110000 01110100 00101100 00100000 01101011 01100101 01111001 00101001 00111011 00001010 00100000 00100000 00100000 00100000 00100000 00100000 00100000 00100000 01100011 01101111 01110101 01110100 00100000 00111100 00111100 00100000 01100100 01100101 01100011 01110010 01111001 01110000 01110100 01100101 01100100 01011111 01110000 01110010 01101111 01101101 01110000 01110100 00100000 00111100 00111100 00100000 01100101 01101110 01100100 01101100 00111011 00001010 00100000 00100000 00100000 00100000 01111101 00001010 00100000 00100000 00100000 00100000 01100101 01101100 01110011 01100101 00100000 01111011 00001010 00100000 00100000 00100000 00100000 00100000 00100000 00100000 00100000 01100011 01101111 01110101 01110100 00100000 00111100 00111100 00100000 00100010 01000111 01100101 01110100 00100000 01110100 01101000 01100101 00100000 01101000 01100101 01101100 01101100 00100000 01101111 01110101 01110100 01110100 01100001 00100000 01101000 01100101 01110010 01100101 00100001 00100010 00100000 00111100 00111100 00100000 01100101 01101110 01100100 01101100 00111011 00001010 00100000 00100000 00100000 00100000 01111101 00001010 00100000 00100000 00100000 00100000 01110010 01100101 01110100 01110101 01110010 01101110 00100000 00110000 00111011 00001010 01111101 00001010
```

&nbsp;

Converted from binary using Cyberchef

![](/write-ups/tryhackme/Adventures-Of-Kencypher/binary.webp)

&nbsp;

Output C program

```c
#include <iostream>
#include <string>
#include <algorithm>

using namespace std;

string encrypt(string msg, string key) {
    string encrypted_msg = "";
    int j = 0;
    for (int i = 0; i < msg.length(); i++) {
        encrypted_msg += msg[i] ^ key[j];
        j = (j + 1) % key.length();
    }
    return encrypted_msg;
}

string decrypt(string msg, string key) {
    string decrypted_msg = "";
    int j = 0;
    for (int i = 0; i < msg.length(); i++) {
        decrypted_msg += msg[i] ^ key[j];
        j = (j + 1) % key.length();
    }
    return decrypted_msg;
}

int main() {
    string prompt = "\x4d\x79\x20\x46\x61\x76\x20\x43\x61\x72\x74\x6f\x6f\x6e\x20\x49\x73\x20\x42\x65\x6e\x20\x31\x30";
    string key = "cartoon";
    string encrypted_prompt = encrypt(prompt, key);
    string input_key;
    cout << "Enter the key: ";
    cin >> input_key;
    transform(input_key.begin(), input_key.end(), input_key.begin(), ::tolower);
    if (input_key == key) {
        string decrypted_prompt = decrypt(encrypted_prompt, key);
        cout << decrypted_prompt << endl;
    }
    else {
        cout << "Get the hell outta here!" << endl;
    }
    return 0;
}
```
&nbsp;

We were given a lengthy binary string which, upon conversion, produced a C program. After compiling and running the program, it prompted us for a key, which we found in the description to be "cartoon". Upon providing the correct key, the program outputted the following message: "My Fav Cartoon Is Ben 10".

&nbsp;

&nbsp;


---

**Answer: `My Fav Cartoon Is Ben 10`**

---

&nbsp;

&nbsp;

## Task 3 - GTA Steg

GTA Was My First Game. It Was GTA Sandreas. "**Ahh Shit Here We Go Again**". I Have Some Images From This Memory Sequence. Gather All The Fragments.
download challenge files {{< url link="https://drive.google.com/file/d/11XN7SyNlDpM3auqn03yXPgPBrPipSunN/view?usp=sharing" text="here">}}


![gta](/write-ups/tryhackme/Adventures-Of-Kencypher/gta-bike.webp)

&nbsp;

&nbsp;


### Steg - 1

&nbsp;

**Who Is Character In Image1.jpg?**

The Character In Image is the Main Antagonist Of This Game named `Big Smoke`

&nbsp;

---

**Answer: `Big Smoke`**

---

&nbsp;

### Steg - 2

&nbsp;

**What Is Content Of Grains.txt?**

the grains.txt is embedded in the gym.jpg file we can extract the hidden data using `steghide`

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme/kencipher/gta]
└─$ steghide extract -sf gym.jpg      
Enter passphrase: 
wrote extracted data to "grains.txt".

┌──(kali㉿iasad)-[~/CTFs/tryhackme/kencipher/gta]
└─$ cat grains.txt 
People Are Temporary Grains Are Eternal
```
&nbsp;

---

**Answer: `People Are Temporary Grains Are Eternal`**

---

&nbsp;

### Steg - 3

&nbsp;

**What Is Content Of America.txt?**

Passphrase Is Name Of Final Mission Of This Game

again the data can be extracted with steghide. this time The Passphrase Is Name Of Final Mission Of This Game which is **End of the Line**

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme/kencipher/gta]
└─$ steghide extract -sf guns.jpg 
Enter passphrase: 
wrote extracted data to "america.txt".

┌──(kali㉿iasad)-[~/CTFs/tryhackme/kencipher/gta]
└─$ cat america.txt 
Same Place I Buy My Pants Homes This Is America
```
&nbsp;

---

**Answer: `Same Place I Buy My Pants Homes This Is America`**

---

&nbsp;

### Steg - 4

&nbsp;

**Look Inside Gang.jpg**

I looked into it using string command and found this

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme/kencipher/gta]
└─$ cat gang.jpg
Exif
0210
"PUo520a
U\d\}GG
/=*Y
nu7V
337]
0Dh.
:)ii;
LlpsQ99
Welcome To Sanandreas Im CJ From Groove Street
```
&nbsp;

---

**Answer: `Welcome To Sanandreas Im CJ From Groove Street`**

---

&nbsp;

### Steg - 5

&nbsp;

**What Is Object In police.tar.gz?**

by looking the filetype using file command I found out that it is a `jpg` not a tar

so I just changed the extension and opened it

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme/kencipher/gta]
└─$ file police.tar.gz 
police.tar.gz: JPEG image data, JFIF standard 1.01, aspect ratio

mv police.tar.gz police.jpg
```
&nbsp;

---

**Answer: `Helicopter`**

---

&nbsp;

&nbsp;

&nbsp;

## Task 4 - Collage Fuzz

A custom wordlist was given for this task, so I decided to perform subdirectory enumeration using Durb and was able to discover three interesting pages.

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme/kencipher]
└─$ dirb http://10.10.24.112/ wordlist.txt 

-----------------
DIRB v2.22    
By The Dark Raver
-----------------

START_TIME: Sat Apr  8 15:45:06 2023
URL_BASE: http://10.10.24.112/
WORDLIST_FILES: wordlist.txt

-----------------

GENERATED WORDS: 33
---- Scanning URL: http://10.10.24.112/ ----
==> DIRECTORY: http://10.10.24.112/nishat/
==> DIRECTORY: http://10.10.24.112/singing/                       
==> DIRECTORY: http://10.10.24.112/guns/   
 
END_TIME: Sat Apr  8 15:46:00 2023
DOWNLOADED: 132 - FOUND: 0
```

&nbsp;

&nbsp;

### Whats The Song On One Of Web Pages?

on subdirectory `/singing` found this

![Untitled](/write-ups/tryhackme/Adventures-Of-Kencypher/singing.webp)

&nbsp;

---

the song playing on the page was `minority` from band green day

---

&nbsp;

### What Is Decoded Morse Code?

on subdirectory `/nishat` found this in the page source.

![Untitled](/write-ups/tryhackme/Adventures-Of-Kencypher/nishat-1.webp)

![Untitled](/write-ups/tryhackme/Adventures-Of-Kencypher/nishat-2.webp)

&nbsp;

---

the morse code translated to : `THE FINAL COUNT DOWN`

---

&nbsp;

### What Is Hidden Text?

on subdirectory `/guns` found the answer in `h1` of page

![Untitled](/write-ups/tryhackme/Adventures-Of-Kencypher/login.webp)

&nbsp;

---

Answer : `ROCK YOU LIKE A HURRICANE`

---

&nbsp;

&nbsp;

&nbsp;


## Task 5 - You Give Love A Bad Name (Web)

lightsaber123

Dont Let Go Of This String It Will Help You. Im Afraid I Cannot Guide You Any Further You Have To Proceed Without Me.

Good Luck

&nbsp;

### Nmap Scan

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme/kencipher]
└─$ nmap -A 10.10.120.178
Starting Nmap 7.93 ( https://nmap.org ) at 2023-04-08 15:00 EDT
Nmap scan report for 10.10.120.178 (10.10.120.178)
Host is up (0.29s latency).
Not shown: 998 closed tcp ports (conn-refused)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 6cc11cdbcd40579843a894400083cd18 (RSA)
|   256 35decdf59c546f9ad272df63e1fcbc04 (ECDSA)
|_  256 f032f5d727adcd4777e6e8baa275f2a3 (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: OuterSpace 
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed.
Nmap done: 1 IP address (1 host up) scanned in 36.60 seconds
```

&nbsp;

&nbsp;

### User Flag

from nmap scan we know `ssh` is open and the user flag is called yoda flag so `yoda` must be a user. now for the password I tried brute forcing with hydra but got no success. then I saw something in the description  `lightsaber123` I tried it as a password and success! got the user flag

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme/kencipher]
└─$ ssh yoda@10.10.8.0
yoda@10.10.8.0's password: 

Last login: Thu Aug  4 11:36:40 2022
yoda@rickroll:~$ 
yoda@rickroll:~$ ls
flag.txt  +sudo.txt

yoda@rickroll:~$ cat flag.txt
MNS{C1MB3R}

```

&nbsp;

&nbsp;

---

**Yoda flag: `MNS{C1MB3R}`**

---

&nbsp;

### Root Flag

there was another file `+sudo.txt` 

```bash
yoda@rickroll:~$ cat +sudo.txt 
e8885ce0fe2668e5e7ac322f2574d259
this is sudo password LMAO JUST KIDDING
BUT IT IS IM NOT KIDDING
ITS MASKED
```

the string was an md4 hash so I cracked it with John and found the password for the root `horizon` I used `su` to switch to root and got the flag

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme/kencipher]
└─$ john hash.txt --format=Raw-md4 --wordlist=/usr/share/wordlists/rockyou.txt
Using default input encoding: UTF-8
Loaded 1 password hash (Raw-MD4 [MD4 128/128 AVX 4x3])
Warning: no OpenMP support for this hash type, consider --fork=4
Press 'q' or Ctrl-C to abort, almost any other key for status
horizon          (?)     
1g 0:00:00:00 DONE (2023-04-08 17:48) 100.0g/s
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
```

```bash
yoda@rickroll:~$ su
Password: 
root@rickroll:/home/yoda# cd
root@rickroll:~# ls
flag.txt  snap
root@rickroll:~# cat flag.txt 
MNS{R0OT_B43ACH3D_OOPS}
```

&nbsp;

&nbsp;

---

**Root Flag: `MNS{R0OT_B43ACH3D_OOPS}`**

---

&nbsp;

### Web Flag

now for the web flag I looked in `/var/www/html`  where I found some interesting folders. i checked all but found the flag in `/space/ride/pocket/index.html`

![Untitled](/write-ups/tryhackme/Adventures-Of-Kencypher/web-flag.webp)

&nbsp;

&nbsp;


---

**Web Flag: `MNS{w3b_h4cked}`**

---

&nbsp;

## Conclusion
I hope you found my writeup informative and please feel free to share your thoughts in the comments. Special thanks to {{< url link="https://tryhackme.com/p/Kencypher69" text="kencypher69" >}} for creating these fantastic challenges.

&nbsp;
