---
author: "Asad Ullah"
title: LazyAdmin - TryHackMe
description: Easy linux machine with multiple vulnerabilities in SweetRice CMS including backup disclosure, remote code execution, arbitrary file upload and arbitrary file download.
summary: Easy linux machine with multiple vulnerabilities in SweetRice CMS including backup disclosure, remote code execution, arbitrary file upload and arbitrary file download.

Section: "write-ups"

date: 2023-10-27T02:54:51+05:00
tags: 
- CMS
- RCE
- backup disclosure
categories:
- tryhackme
- writeup
draft: false

---

{{< 
tryhackme 
name="LazyAdmin" 
os="Linux" 
difficulty="Easy"  
creator_name="TryHackMe" creator_link="https://tryhackme.com/room/lazyadmin"
>}}

---

&nbsp;
&nbsp;


## Reconnaissance

### Nmap Scan

```bash
# nmap -Pn -sV -sC 10.10.24.59

Nmap scan report for 10.10.24.59
Host is up (0.18s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 49:7c:f7:41:10:43:73:da:2c:e6:38:95:86:f8:e0:f0 (RSA)
|   256 2f:d7:c4:4c:e8:1b:5a:90:44:df:c0:63:8c:72:ae:55 (ECDSA)
|_  256 61:84:62:27:c6:c3:29:17:dd:27:45:9e:29:cb:90:5e (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel 
```

Only two ports are open: 22 and 80. it's clear that the machine is web focused. Let's enumerate the web server.

### Directory Enumeration

```bash
# gobuster dir -u http://10.10.24.59/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt 

===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.24.59/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/content              (Status: 301) [Size: 312] [--> http://10.10.24.59/content/]
```

Gobuster discovered the path `/content`. which is using the SweetRice content management system (CMS). 

Further research revealed that SweetRice CMS is known to have multiple vulnerabilities.

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme/lazyadmin]
└─$ searchsploit sweetrice           
----------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                       |  Path
----------------------------------------------------------------------------------------------------- ---------------------------------
SweetRice 0.5.3 - Remote File Inclusion                                                              | php/webapps/10246.txt
SweetRice 0.6.7 - Multiple Vulnerabilities                                                           | php/webapps/15413.txt
SweetRice 1.5.1 - Arbitrary File Download                                                            | php/webapps/40698.py
SweetRice 1.5.1 - Arbitrary File Upload                                                              | php/webapps/40716.py
SweetRice 1.5.1 - Backup Disclosure                                                                  | php/webapps/40718.txt
SweetRice 1.5.1 - Cross-Site Request Forgery                                                         | php/webapps/40692.html
SweetRice 1.5.1 - Cross-Site Request Forgery / PHP Code Execution                                    | php/webapps/40700.html
SweetRice < 0.6.4 - 'FCKeditor' Arbitrary File Upload                                                | php/webapps/14184.txt
----------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results
```

We can access the backup file at `/inc/mysql_backup`

Exploiting the Backup Disclosure vulnerability, I came across a MySQL database containing a username and a hashed password. This hash could be decrypted using tools like CrackStation.

```bash
42f749ade7f9e195bf475f37a44cafcb:Password123
```

## Exploitation


I discovered that the ads page allows for the injection of PHP code, which can be executed by the system. This can give us initial access by submitting a PHP reverse shell payload from PentestMonkey through the ads page. The code can be accessed at the path: `inc/ads/filename`.

![Untitled](/write-ups/tryhackme/lazyadmin/1.webp)

Initiate netcat and execute the payload. We got a reverse shell as **`www-data`** user.

![Untitled](/write-ups/tryhackme/lazyadmin/2.webp)

&nbsp;
&nbsp;

---

**Flag`THM{63e5bce9271952aad1113b6f1ac28a07}`**

---

&nbsp;
&nbsp;


## Privilege Escalation

Using **`sudo -l`** we observed that we can run **`backup.pl`** without password. However,  we lack write permissions for this file.

![Untitled](/write-ups/tryhackme/lazyadmin/3.webp)
![Untitled](/write-ups/tryhackme/lazyadmin/4.webp)
we can see that **`backup.pl`** runs another file located at **`/etc/copy.sh`**. Fortunately, we have write permissions so we can inject our reverse shell payload into this file. We can then trigger its execution by using the following command: **`/usr/bin/perl /home/itguy/backup.pl`**

![Untitled](/write-ups/tryhackme/lazyadmin/5.webp)
![Untitled](/write-ups/tryhackme/lazyadmin/6.webp)

&nbsp;
&nbsp;


---

**Flag`THM{6637f41d0177b6f37cb20d775124699f}`**

---


&nbsp;
&nbsp;
