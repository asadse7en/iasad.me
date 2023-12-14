---
author: "Asad Ullah"
title: CyberEvilCorp - CyberHackathon
description: Easy OSINT challenge.
summary: Easy OSINT challenge.

Section: "write-ups"

date: 2023-11-12T02:54:51+05:00
tags: 
- archive.org
- exiftool
categories:
- CyberHackathon
- writeup
draft: false

---

{{< 
ctf 
name="CyberEvilCorp"
category="OSINT" 
difficulty="Easy"
points="50"  
creator_name="CyberHackathon" creator_link="https://patch.com.pk/competitions/digital-cyber-security-hackathon-2023-onlinequalifier/challenges" 
>}}


&nbsp;
&nbsp;


## Description

Hi agent, welcome to the cyberevilcorp. We have recovered this picture of one of the agents of cyberevilcorp. They call him Seeker. Hunt him down and uncover their next move.

## Approach

we are given the following image

![seeker.jpg](/write-ups/cyberhackathon/cyberevilcorp/1.webp)

&nbsp;

The only thing that looks interesting is the text in background so i extracted it but didn't find any leads.

![seeker.jpg](/write-ups/cyberhackathon/cyberevilcorp/2.webp)

&nbsp;

Next, I looked at metadata of the image and found a username `@evilseeker`

&nbsp;

```bash
┌──(n4ruto㉿iasad.me)-[~/CTFs/CyberHackathon/cyberevilcorp]
└─$ exiftool seeker.jpg
File Name                       : seeker.jpg
XP Title                        : Seeker
XP Comment                      : @evilseeker
XP Author                       : cyberevilcorp
XP Keywords                     : hacking
XP Subject                      : Hardware
```

&nbsp;

I attempted a manual search for the username on various search engines but found nothing. Then, I utilized a tool called [Sharlock](https://github.com/sherlock-project/sherlock) to locate the social account.

&nbsp;

```bash
┌──(n4ruto㉿iasad.me)-[~/CTFs/CyberHackathon/cyberevilcorp]
└─$ python /opt/sherlock/sherlock/sherlock.py evilseeker -b # Used -b to open every link in default browser
[*] Checking username evilseeker on:

[+] AllMyLinks: https://allmylinks.com/evilseeker
[+] Asciinema: https://asciinema.org/~evilseeker
[+] AskFM: https://ask.fm/evilseeker
[+] Blogger: https://evilseeker.blogspot.com
[+] Duolingo: https://www.duolingo.com/profile/evilseeker
[+] Fiverr: https://www.fiverr.com/evilseeker
[+] Flipboard: https://flipboard.com/@evilseeker
[+] G2G: https://www.g2g.com/evilseeker
[+] GaiaOnline: https://www.gaiaonline.com/profiles/evilseeker
[+] Gamespot: https://www.gamespot.com/profile/evilseeker/
[+] Kongregate: https://www.kongregate.com/accounts/evilseeker
[+] Lolchess: https://lolchess.gg/profile/na/evilseeker
[+] Reddit: https://www.reddit.com/user/evilseeker
[+] Roblox: https://www.roblox.com/user.aspx?username=evilseeker
[+] Smule: https://www.smule.com/evilseeker
[+] Snapchat: https://www.snapchat.com/add/evilseeker
[+] Telegram: https://t.me/evilseeker
[+] TikTok: https://tiktok.com/@evilseeker
[+] Twitch: https://www.twitch.tv/evilseeker
[+] Twitter: https://twitter.com/evilseeker
[+] Virgool: https://virgool.io/@evilseeker
[+] Whonix Forum: https://forums.whonix.org/u/evilseeker/summary
[+] YandexMusic: https://music.yandex/users/evilseeker/playlists
[+] interpals: https://www.interpals.net/evilseeker
[+] metacritic: https://www.metacritic.com/user/evilseeker

[*] Search completed with 25 results
```

&nbsp;

Found the intended user on [Aciinema](https://asciinema.org/~evilseeker).

&nbsp;

![seeker.jpg](/write-ups/cyberhackathon/cyberevilcorp/3.webp)

&nbsp;

```bash
┌──(wolf㉿predator)-[~]                                                          
└─$ python3 SecretServer.py                                                     
                                                                                
Secret server started! Waiting for connections...                               
Hey Seeker!!!                                                                   
There is a disaster!!!                                                           
Our C2 password has been leaked publicly on https://asciinema.org/a/610542      
Delete it ASAP
```

&nbsp;

Opening the message we are directed to another page but that page doesn’t exist. so we have to use [archive.org](http://archive.org) to view a past version of the page 

&nbsp;

![seeker.jpg](/write-ups/cyberhackathon/cyberevilcorp/4.webp)

&nbsp;

Looking at the snapshot from Sept 26 we got the flag

&nbsp;

```bash
┌──(wolf㉿predator)-[~]                                                          
└─$ python3 SecretServer.py                                                     
                                                                                
Secret server started! Waiting for connections...                               
Greetings Seeker,                                                               
Good news, we have got a new foothold at the cybergoodcorp infrastructure       
You may access our C2 server using the following password:                      
flag{Wh4t_a_H4rdP@55}
```

&nbsp;

{{< flag "flag" "flag{Wh4t_a_H4rdP@55}">}}

&nbsp;

&nbsp;
