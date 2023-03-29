---
author: "Asad Ullah"
title: Crack the Hash Level 2 - TryHackMe
description: The challenge involves decrypting different hash codes using various encryption cracking techniques. The writeup is likely to describe the methods used and the steps taken to successfully crack the hash.
summary: Advanced hash cracking challenges and wordlist generation

date: 2023-03-28T02:54:51+05:00

Section: "write-ups"

categories: ["writeup", "tryhackme","hash cracking"]

tags: ["hash cracking", "hashcat",  "John the Ripper", "rules based", "Mentalist", "CeWL","wordlistctl", "Freak mutation","pnwgen", "TTPassGen", "SecLists", "Haiti",]

draft: false

---


{{< 
boxinfo 
name="Crack the Hash Level 2" 
os="-" 
difficulty="Medium"  
points="600" 
creator_name="TryHackMe" creator_link="https://tryhackme.com/room/crackthehashlevel2" 
description="Advanced hash cracking challenges and wordlist generation"
>}}

---

> ***If you want to skip directly to the hash cracking section, click here [🔗](#its-time-to-crack-hashes---the-actual-challange)***


## Hash identification

When you come across a hash, the first step is usually to figure out what type of hash it is. There are many types of hashes, with some well-known ones like MD5 and SHA1,

To identify hashes, the challenge recommended installing Haiti, but I needed to install the gem package first. I did this by running the command

```bash
sudo apt-get install rubygems
```

 Once I had done this, I was able to install Haiti by running the command

```bash
sudo gem install haiti-hash
```

### Task 1 - Identify Hash Type

```bash
741ebf5166b9ece4cca88a3868c44871e8370707cf19af3ceaa4a6fba006f224ae03f39153492853
```

**Launch Haiti on hash**

![Untitled](/write-ups/tryhackme/crack-the-hash-level-2/(1).png)

---

### Task 2 - What is Keccak-256 Hashcat and John the Ripper code?

![Untitled](/write-ups/tryhackme/crack-the-hash-level-2/(2).png)

The blue section indicates the mode for Hashcat, while the pink section represents the hash code for John.

---

## Wordlists

To crack passwords, you'll need wordlists, which are collections of commonly used passwords or other strings. Two popular sources for wordlists are SecLists and Rawsec's CyberSecurity Inventory.

- [SecLists](https://github.com/danielmiessler/SecLists) is a comprehensive collection of various types of wordlists used in security assessments, such as passwords, usernames, and URLs.
- [wordlistctl](https://github.com/BlackArch/wordlistctl) is a script that can fetch, install, update, and search more than 6300 wordlist archives from websites that offer them.
- [Rawsec's CyberSecurity Inventory](https://inventory.raw.pm/overview.html) is a resource inventory for cybersecurity tools, including wordlist generator tools, which can help in the creation of custom wordlists.

---

**To use wordlistctl on Kali Linux, clone from {{< newtab link="https://github.com/BlackArch/wordlistctl" text="Github" >}}**

**`python3 wordlistctl/wordlistctl.py -h`**

**search for rockyou on your local archive with `wordlistctl search -l rockyou`**

![Untitled](/write-ups/tryhackme/crack-the-hash-level-2/(3).png)

**Q: what is the path where is stored the wordlist?**

```bash
/usr/share/wordlists/passwords/rockyou.txt
```

**Q: What is the name of the first wordlist in the usernames category?**

```bash
CommonAdminBase64
```

---

## Cracking tools, modes & rules

To crack passwords, you'll need a tool like • [Hashcat](https://hashcat.net/hashcat/) or [John the Ripper](http://www.openwall.com/john/). There are three ways to crack passwords:

- **Wordlist mode:** This method uses a list of common passwords, usernames, or other words to try and guess the password.
- **Incremental mode:** This method tries every possible combination of characters until it finds the password. This can take a long time, especially for long passwords.
- **Rule mode:** This method uses a wordlist but adds some patterns or modifies the words to try and guess the password.

There are two ways to perform a rule-based brute force:

- Generate a custom wordlist and use it with the classic wordlist mode.
- Use a common wordlist and apply custom mangling rules to it. This is more efficient as you don't have to store and generate multiple wordlists.

John the Ripper has various built-in rules to apply to wordlists, but you can also create your own. You can check the John the Ripper Wordlist rules syntax for guidance on creating custom rules.

John the Ripper already include various mangling rules but you can create your owns and apply them the wordlist when cracking:

```bash
$ john hash.txt --wordlist=/usr/share/wordlists/passwords/rockyou.txt rules=norajCommon02
```

﻿You can consult John the Ripper [Wordlist rules syntax](https://www.openwall.com/john/doc/RULES.shtml) for creating your own rules.

I'll give you the main ideas of mutation rules, of course several can be combined together.

- **Border mutation** - commonly used combinations of digits and special symbols can be added at the end or at the beginning, or both
- **Freak mutation** - letters are replaced with similarly looking special symbols
- **Case mutation** - the program checks all variations of uppercase/lowercase letters for any character
- **Order mutation** - character order is reversed
- **Repetition mutation** - the same group of characters are repeated several times
- **Vowels mutation** - vowels are omitted or capitalized
- **Strip mutation** - one or several characters are removed
- **Swap mutation** - some characters are swapped and change places
- **Duplicate mutation** - some characters are duplicated
- **Delimiter mutation** - delimiters are added between characters

Depending of your distribution, the John configuration may be located at `/etc/john/john.conf`
 and/or `/usr/share/john/john.conf`To locate the JtR install directory run locate `john.conf`then create `john-local.conf`in the same directory (in my case`/usr/share/john/john-local.conf` and create our rules in here.

Let’s use the top 10 000 most used password list from [SecLists](https://github.com/danielmiessler/SecLists#install) (`/usr/share/seclists/Passwords/Common-Credentials/10k-most-common.txt`) and generate a simple border mutation by appending all 2 digits combinations at the end of each password.Let's edit `/usr/share/john/john-local.conf` and add a new rule:,

![Untitled](/write-ups/tryhackme/crack-the-hash-level-2/(4).png#center)

&nbsp;
### let's crack the SHA1 hash

```bash
2d5c517a4f7a14dcb38329d228a7d18a3b78ce83
```

Now let’s crack the SHA1 hash  we just have to write the hash in a text file and to specify the hash type, the wordlist and our rule name.

```bash
john hash.txt --format=raw-sha1 --wordlist=/usr/share/seclists/Passwords/Common-Credentials/10k-most-common.txt --rules=THM01
```

![Untitled](/write-ups/tryhackme/crack-the-hash-level-2/(5).png)

&nbsp;
---

## Custom wordlist generation

Generating a custom wordlist may be a better option in some cases, even though using mangling rules can save storage space and time. Some reasons to generate a custom wordlist include:

- You plan to use the wordlist multiple times, and generating one upfront will save computation power compared to using a mangling rule each time.
- You want to use the same wordlist across different cracking tools.
- The tool you want to use supports wordlists but not mangling rules.
- You find the syntax for creating custom rules in John too complex.
&nbsp;
### Mentalist

Let's say we know the password we want to crack is about dogs. We can download a list of dog races `wordlistctl fetch -l dogs -d` (`/usr/share/wordlists/misc/dogs.txt`). Then we can use [Mentalist](https://github.com/sc0tfree/mentalist) to generate some mutations.

![Untitled](/write-ups/tryhackme/crack-the-hash-level-2/(6).png)

**Question 1** Crack the following md5 hash with the wordlist generated in the previous steps.

```bash
ed91365105bba79fdab20c376d83d752
```

![Untitled](/write-ups/tryhackme/crack-the-hash-level-2/(7).png)



&nbsp;
### CeWL

Now let’s use **[CeWL](https://github.com/digininja/CeWL)** to generate a wordlist from a website. It could be useful to retrieve a lot of words related to the password’s topic.

For example to download all words from example.org with a depth of 2, run:`cewl -d 2 -w $(pwd)/example.txt https://example.org`The depth is the number of link level the spider will follow.

**Question 2** What is the last word of the list?

![Untitled](/write-ups/tryhackme/crack-the-hash-level-2/(8).png)

&nbsp;
### TTPassGen

```
pip install ttpassgen
```

With **[TTPassGen](https://github.com/tp7309/TTPassGen)** we can craft wordlists from scratch. Create a first wordlist containing all 4 digits PIN code value.

```bash
ttpassgen --rule '[?d]{4:4:*}' pin.txt
```

Generate a list of all lowercase chars combinations of length 1 to 3.

```bash
ttpassgen --rule '[?l]{1:3:*}' abc.txt
```

![Untitled](/write-ups/tryhackme/crack-the-hash-level-2/(9).png)

Then we can create a new wordlist that is a combination of several wordlists. Eg. combine the PIN wordlist and the letter wordlist separated by a dash.

```bash
ttpassgen --dictlist 'pin.txt,abc.txt' --rule '$0[-]{1}$1' combination.txt
```

Be warned combining wordlists quickly generated huge files, here combination.txt is 1.64 GB.

```
$ wc pin.txt
10000 10000 50000 pin.txt

$ wc abc.txt
18278 18278 72384 abc.txt

$ wc combination.txt
 182780000  182780000 1637740000 combination.txt
```

**Question 3**
Crack this md5 hash with combination.txt.

`e5b47b7e8df2597077e703c76ee86aee`

![Untitled](/write-ups/tryhackme/crack-the-hash-level-2/(10).png)

&nbsp;

# It's time to crack hashes - the actual challange

You will have to crack several hashes. For each hash you will be given a short scenario that will help you to create a mangling rules, build a wordlist or finding some specialized data you'll need to crack the hash.

---

## Task 1

```bash
Advice n°1 = b16f211a8ad7f97778e5006c7cecdf31
```

> **Question Hint💡**
> 
> 
> English male name, MD5, Border mutation, custom rule
> 

```bash
echo 'b16f211a8ad7f97778e5006c7cecdf31' > hash1.txt
```

As the hint suggests the password is english male name with border mutation and custom rule and we also know that it is md5 hash.

**First,** we need to find wordlist of male names using wordlistctl `python3 [wordlistctl.py](http://wordlistctl.py/) search male`

download any wordlist I will use top_1000_usa_femalenames_english with the following commad

```bash
python3 wordlistctl.py fetch -l top_1000_usa_femalenames_english -d
```

**Secondly,** create a custom rule in `john-local.config`

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme]
└─$ cat /usr/share/john/john-local.conf 
[List.Rules:task01]
c$[0-9!@#$%^&*()_+]$[0-9!@#$%^&*()_+]$[0-9!@#$%^&*()_+]$[0-9!@#$%^&*()_+]$[0-9!@#$%^&*()_+]
c^[0-9!@#$%^&*()_+]^[0-9!@#$%^&*()_+]^[0-9!@#$%^&*()_+]^[0-9!@#$%^&*()_+]^[0-9!@#$%^&*()_+]
```

The border mutation rule adds a combination of digits and special symbols at the end or beginning, or both, and is commonly used.

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme]
└─$ john --format=Raw-MD5 hash1.txt --wordlist=malenames-usa-top1000.txt --rules=task01

Using default input encoding: UTF-8
Loaded 1 password hash (Raw-MD5 [MD5 256/256 AVX2 8x3])
Press 'q' or Ctrl-C to abort, almost any other key for status
0g 0:00:00:06 0.41% (ETA: 19:20:20) 0g/s 7024Kp/s 7024Kc/s 7024KC/s Lane03+4+..Curtis03+50
Za**********4*   (?)
1g 0:00:00:33 DONE (2021-04-23 18:56) 0.03018g/s 7760Kp/s 7760Kc/s 7760KC/s Alden1234*..Ivan1234(
Use the "--show --format=Raw-MD5" options to display all of the cracked passwords reliably
Session completed
```
&nbsp;

---

## Task 2

```bash
Advice n°2 = 7463fcb720de92803d179e7f83070f97
```

> **Question Hint💡**
> 
> 
> English female name, MD5, Border mutation, custom rule
> 

```bash
echo '7463fcb720de92803d179e7f83070f97' > hash2.txt
```

**First,** download common female namelist using `wordlistctl`

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme]
└─$ wordlistctl fetch -l femalenames-usa-top1000
```

Then create a rule in john-local.config according to the advice no 2 which suggests to use border mutation:

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme]
└─$ cat /usr/share/john/john-local.conf 
[List.Rules:task02]
c$[0-9!@#$%^&*()_+]$[0-9!@#$%^&*()_+]$[0-9!@#$%^&*()_+]
c^[0-9!@#$%^&*()_+]^[0-9!@#$%^&*()_+]^[0-9!@#$%^&*()_+]
```

Now run john on it

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme]
└─$ john --format=Raw-MD5 hash2.txt --wordlist=femalenames-usa-top1000.txt --rules=task02

┌──(kali㉿iasad)-[~/CTFs/tryhackme]
└─$ john --format=Raw-MD5 hash2.txt --show
?:*********5!
```
&nbsp;

---

## Task 3

```bash
Advice n°2 = 7463fcb720de92803d179e7f83070f97
```

> **Question Hint💡**
> 
> 
> Town name of Mexico, MD5, Freak mutation, mentalist tool
> 

```bash
echo '7463fcb720de92803d179e7f83070f97' > hash3.txt
```

**First,** download Mexico town namelist using `wordlistctl`

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme]
└─$ wordlistctl fetch -l towns_mx -d
```

Clean the wordlist. Remove spaces and change everything to lowercase.

```bash
cat cities.txt | sed -r 's/\s+//g' | tr '[:upper:]' '[:lower:]' > cities_final.txt
```

the advice suggests to use freak mutation. There is a default rule in john, “l33t”, which does the freak mutation by default.

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme]
└─$ john --format=Raw-MD5 hash3.txt --wordlist=cities_final.txt --rules=l33t

┌──(kali㉿iasad)-[~/CTFs/tryhackme]
└─$ john --format=Raw-MD5 hash2.txt --show
Tl@x******ng0
```
&nbsp;

---

## Task 4

```bash
Advice n°4 a3a321e1c246c773177363200a6c0466a5030afc
```

> **Question Hint💡**
> 
> 
> Own name, SHA1, Case mutation; existing rule
> 

```bash
echo 'a3a321e1c246c773177363200a6c0466a5030afc' > hash4.txt
```

**First,** we need to find the wordlist Since, wordlist consists of his name. We can add his first name, last name, combined name into the wordlist.

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme]
└─$ cat names.txt
david
gauttapan
davidguattapan
```

The "TN" rule in john is a default rule that toggles the case of each character in a password candidate.

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme]
└─$ john --format=Raw-SHA1 hash4.txt --wordlist=names.txt --rules=NT
Using default input encoding: UTF-8
Loaded 1 password hash (Raw-SHA1 [SHA1 256/256 AVX2 8x])
Press 'q' or Ctrl-C to abort, almost any other key for status
Dav******An   (?)
1g 0:00:00:00 DONE (2021-04-23 20:27) 8.333g/s 38333p/s 38333c/s 38333C/s DavIDgUEttapAn..DavIDgUEtTAPAn
Use the "--show --format=Raw-SHA1" options to display all of the cracked passwords reliably
Session completed
```
&nbsp;

---

## Task 5

```bash
Advice n°5 d5e085772469d544a447bc8250890949
```

> **Question Hint💡**
> 
> 
> Lyrics, MD5, Order mutation, lyricpass
> 

```bash
echo 'd5e085772469d544a447bc8250890949' > hash5.txt
```

**First,** we need to find the wordlist We can use ***[lyricpass](https://github.com/initstring/lyricpass)*** to download the lyrics of all the songs by Adele. Using the command:

`lyricpass.py -a "Adele"`

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme]
└─$ lyricpass.py -a Adele
[+] Looking up artist Adele
[+] Found 345 songs for artists Adele
[+] All done! 345/345...       

Raw lyrics: raw-lyrics-2021-04-23-20.30.50
Passphrases: wordlist-2021-04-23-20.30.50
```

The advice suggests "Order mutation - character order is reversed is used for that we have a default rule in john “r” we can use that

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme]
└─$ john --format=Raw-MD5 hash5.txt --wordlist=raw-lyrics-2021-04-23-20.30.50 --rules=r
Using default input encoding: UTF-8
Loaded 1 password hash (Raw-MD5 [MD5 256/256 AVX2 8x3])
Press 'q' or Ctrl-C to abort, almost any other key for status
uoy ot m**s ot em rof ***d oot ro **** oot si ***ir oN (?)
1g 0:00:00:00 DONE (2021-04-23 20:40) 16.66g/s 6400p/s 6400c/s 6400C/s tnew yrots eht woh si sihT..egdirb eht rednu retaw tnia evol ruo taht yaS
Use the "--show --format=Raw-MD5" options to display all of the cracked passwords reliably
Session completed
```
&nbsp;

---

## Task 6

```bash
Advice n°6 377081d69d23759c5946a95d1b757adc
```

> Question Hint💡
> 
> 
> Phone number, MD5, No mutation, pnwgen
> 

```bash
echo 'a3a321e1c246c773177363200a6c0466a5030afc' > hash6.txt
```

Clues from the given advice: ******Phone number from Sint Maarten. No Mutation.

**First,** we need to find the wordlist. for this we have to know what prefix Sint Maarten uses. here is a full list of country codes and prefixes on [wikipedia](https://en.wikipedia.org/wiki/List_of_mobile_telephone_prefixes_by_country)

Sint Maarten: `+1` and `721` prefix for mobile phone number

```
┌──(kali㉿iasad)-[~/CTFs/tryhackme]
└─$ python pnwgen.py +1721 '' 7
```

this will create a wordlist of all possible numbers in the given prefix and length is 7

```
┌──(kali㉿iasad)-[~/CTFs/tryhackme]
└─$ $ john hash6.txt --format=raw-md5 --wordlist=/tmp/pnwgen/wordlist.txt
Using default input encoding: UTF-8
Loaded 1 password hash (Raw-SHA1 [SHA1 256/256 AVX2 8x])
Press 'q' or Ctrl-C to abort, almost any other key for status
+1721****375   (?)
1g 0:00:00:00 DONE (2021-04-23 20:27) 8.333g/s 38333p/s 38333c/s 38333C/s DavIDgUEttapAn..DavIDgUEtTAPAn
Use the "--show --format=Raw-SHA1" options to display all of the cracked passwords reliably
Session completed
```
&nbsp;

---

## Task 7

```bash
Advice n°7 ba6e8f9cd4140ac8b8d2bf96c9acd2fb58c0827d556b78e331d1113fcbfe425ca9299fe917f6015978f7e1644382d1ea45fd581aed6298acde2fa01e7d83cdbd
```

> Question Hint💡
> 
> 
> Rockyou, SHA3-512, No mutation
> 

```bash
echo 'ba6e8f9cd4140ac8b8d2bf96c9acd2fb58c0827d556b78e331d1113fcbfe425ca9299fe917f6015978f7e1644382d1ea45fd581aed6298acde2fa01e7d83cdbd' > hash7.txt
```

Clues from the given advice: “ Last Competition Project of NIST” .Searching from the internet, I got to know that the hash is Raw-SHA3.

![Untitled](/write-ups/tryhackme/crack-the-hash-level-2/(12).png)

So we have to use sha3 hash

```
┌──(kali㉿iasad)-[~/CTFs/tryhackme]
└─$ $ john hash.txt --format=raw-sha3 --wordlist=rockyou.txt
Using default input encoding: UTF-8
Loaded 1 password hash (Raw-SHA1 [SHA1 256/256 AVX2 8x])
Press 'q' or Ctrl-C to abort, almost any other key for status
!@#******!@#   (?)
1g 0:00:00:00 DONE (2021-04-23 20:27) 8.333g/s 38333p/s 38333c/s 38333C/s DavIDgUEttapAn.
Use the "--show --format=Raw-SHA1" options to display all of the cracked passwords
Session completed
```
&nbsp;

---

## Task 8

```bash
Advice n°8 9f7376709d3fe09b389a27876834a13c6f275ed9a806d4c8df78f0ce1aad8fb343316133e810096e0999eaf1d2bca37c336e1b7726b213e001333d636e896617
```

> Question Hint💡
> 
> 
> Web scrapping, blake2, Repetition, CeWL
> 

```bash
echo 'ba6e8f9cd4140ac8b8d2bf96c9acd2fb58c0827d556b78e331d1113fcbfe425ca9299fe917f6015978f7e1644382d1ea45fd581aed6298acde2fa01e7d83cdbd' > hash8.txt
```

Clues from the given advice: All the words are form the webpage . Repetition of same word 2 or 3 or 5 or more than 5 times. Finalist of SHA-3 project. A simple internet search gives us the hash type.

![1_r233UogY](/write-ups/tryhackme/crack-the-hash-level-2/(13).webp)

Use CeWL to scrape the words from the website.

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme]
└─$  cewl -d 2 -w hash8_scrapped.txt http://<MACHINE_IP>/rtfm.re/en/sponsors/index.html
```

Generate the wordlist with 1,2,3,4 and 5 repetition of the words using python script.

```python
file1 = open('hash8_scrapped.txt', 'r')
file2 = open('hash8_final.txt', 'w')

while True:
  l = file1.readline()
  if not l:
      break
  l = l.strip()
  for i in range(1, 6):
      file2.write(l*i+'\n')

file1.close()
file2.close()
```

Use john with `Raw-Blake2`

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme]
└─$ john --format=Raw-Blake2 hash8 -wordlist=hash8_final.txt
Using default input encoding: UTF-8
Loaded 1 password hash (Raw-SHA1 [SHA1 256/256 AVX2 8x])
Press 'q' or Ctrl-C to abort, almost any other key for status
hacki************nghacking   (?)
1g 0:00:00:00 DONE (2021-04-23 20:27) 8.333g/s 38333p/s 38333c/s 38333C/s DavIDgUEttapAn..DavIDgUEtTAPAn
Use the "--show --format=Raw-SHA1" options to display all of the cracked passwords reliably
Session completed
```
&nbsp;

---

## Task 9

```
Advice n°9 $6$kI6VJ0a31.SNRsLR$Wk30X8w8iEC2FpasTo0Z5U7wke0TpfbDtSwayrNebqKjYWC4gjKoNEJxO/DkP.YFTLVFirQ5PEh4glQIHuKfA/
```

> Question Hint💡
> 
> 
> Rockyou, SHA512-crypt, No mutation
> 

```
echo '$6$kI6VJ0a31.SNRsLR$Wk30X8w8iEC2FpasTo0Z5U7wke0TpfbDtSwayrNebqKjYWC4gjKoNEJxO/DkP.YFTLVFirQ5PEh4glQIHuKfA/' > hash9.txt

```

**using sha512crypt format**

```
┌──(kali㉿iasad)-[~/CTFs/tryhackme]
└─$ $ john --format=sha512crypt hash9.txt --wordlist=/rockyou.txt
Using default input encoding: UTF-8
Loaded 1 password hash (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Press 'q' or Ctrl-C to abort, almost any other key for status
kakashi1         (?)
1g 0:00:00:17 DONE (2021-04-23 16:34) 0.05701g/s 1590p/s 1590c/s 1590C/s mothers..citlali
Use the "--show" option to display all of the cracked passwords reliably
Session completed

```
&nbsp;

---

# Conclusion

In summary, this room has a lot of valuable content and teachings about the rules in John. It may take some time to fully understand everything, but it is worth it. If you have any questions, don't hesitate to ask me.

&nbsp;

