---
author: "Asad Ullah"
title: "TBDLCG - BucketCTF"
description: 
summary: Write-up on cryptography challenge TBDLCG.
date: 2023-04-10T04:04:24+05:00
Section: write-ups
categories:
- writeup
- cryptography
tags:
- bucketctf
- bot

draft: false

---

{{< 
ctftime 
name="TBDLCG" 
difficulty="Easy"  
points="200"
category="cryptography"
>}}

&nbsp;

&nbsp;


## Description

I created a tennis game. BLAHFALJFAJDFLBLAHAOIFLJFDA - is that random enough for you?

&nbsp;

## Approach

we are given a container that we can connect to using `netcat`

```bash
┌──(kali㉿iasad)-[~/CTFs/BucketCTF/crypto/TBDLCG]
└─$ nc 213.133.103.186 5766
You are playing a game of table tennis against Cogsworth64 AI bot.
The bot is only able to serve the ball, because Cogsworth64 disabled .
The bot will send a certain spin (represented by a number 0-8)
and location (represented by a number 0-8) at each point.
If you can guess the spin and location, you win the point.
If you can not, the bot wins the point.
The first player to win 20 points wins the game. Try not to lose.

Your score: 0
Bot's score: 0
What is your guess for location?
```
&nbsp;

Initially, I spent some time experimenting with the game to understand its workings. then I assigned a very large negative value to both the location and spin variables. After executing two turns, I noticed that the bot position and spin values remained fixed at 3. Based on this observation, I deduced that inputting 3 as the values for both variables would result in a win every time. and hence I got the flag

```bash
What is your guess for location?-999999
What is your guess for spin?-999999
You lose the point!
The bot's spin was 3 and location was 3
Your score: 0
Bot's score: 1
What is your guess for location?3
What is your guess for spin?3
You win the point!
Your score: 1
Bot's score: 1
What is your guess for location?3
3What is your guess for spin?
You win the point!
Your score: 2
Bot's score: 1
What is your guess for location?3
3What is your guess for spin?
3You win the point!
Your score: 3
Bot's score: 1
What is your guess for location?3
What is your guess for spin?3
You lose the point!
The bot's spin was 3 and location was 3
Your score: 3
Bot's score: 2
What is your guess for location?33
What is your guess for spin?3
You lose the point!
The bot's spin was 3 and location was 3
Your score: 3
Bot's score: 3
What is your guess for location?3
3What is your guess for spin?
You win the point!
Your score: 4
Bot's score: 3
What is your guess for location?3
What is your guess for spin?3
You win the point!
You win the game!
b'bucket{#1_victory_royale_86f2b88341d8d}\n'
```

&nbsp;

---

**Flag: `bucket{#1_victory_royale_86f2b88341d8d}`**

---

&nbsp;

&nbsp;
