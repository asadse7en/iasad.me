---
author: "Asad Ullah"
title: Pickle Rick - TryHackMe
description: Easy linux machine with pretty straight remote code execution vulnerability.
summary: Easy linux machine with pretty straight remote code execution vulnerability.

Section: "write-ups"

date: 2023-11-06T02:54:51+05:00
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
name="Pickle Rick" 
os="Linux" 
difficulty="Easy"  
creator_name="TryHackMe" creator_link="https://tryhackme.com/room/picklerick"
>}}

---

&nbsp;
&nbsp;

## Reconnaissance

### Nmap Scan

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme/pickle-rick]
└─$ cat ports.txt 
# Nmap 7.94 scan initiated Sun Nov  5 04:34:08 2023 as: nmap -p- -T4 -oN ports.txt 10.10.181.53
Warning: 10.10.181.53 giving up on port because retransmission cap hit (6).
Nmap scan report for 10.10.181.53 (10.10.181.53)
Host is up (0.21s latency).
Not shown: 65371 closed tcp ports (conn-refused), 162 filtered tcp ports (no-response)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

# Nmap done at Sun Nov  5 05:21:15 2023 -- 1 IP address (1 host up) scanned in 2827.06 seconds
```

Port 80 and 22 are the only open ports so it looks like a web-focused machine

![Untitled](/write-ups/tryhackme/pickle-rick/1.webp)

![Untitled](/write-ups/tryhackme/pickle-rick/2.webp)

Looking at the source code we find a username. let's further enumerate port 80

### Gobuster Scan

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme/pickle-rick]
└─$ cat gobuster.txt 
#gobuster dir -u http://10.10.10.10 -w path/to/wordlist
/.hta                 (Status: 403) [Size: 291]
/.htaccess            (Status: 403) [Size: 296]
/.htpasswd            (Status: 403) [Size: 296]
/assets               (Status: 301) [Size: 313] [--> http://10.10.181.53/assets/]
/index.html           (Status: 200) [Size: 1062]
/robots.txt           (Status: 200) [Size: 17]
/server-status        (Status: 403) [Size: 300]
```

In robots.txt we found a password

![Untitled](/write-ups/tryhackme/pickle-rick/3.webp)

Now we have a username and a password but there's no login portal. let’s scan for vulnerabilities with Nikto

### Nikto Scan

```bash
┌──(kali㉿iasad)-[~/CTFs/tryhackme/pickle-rick]
└─$ cat nikto.txt   
# nikto -h 10.10.10.10
- Nikto v2.5.0/
+ Target Host: 10.10.181.53
+ Target Port: 80
+ GET /: The anti-clickjacking X-Frame-Options header is not present. See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options: 
+ GET /: The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type. See: https://www.netsparker.com/web-vulnerability-scanner/vulnerabilities/missing-content-type-header/: 
+ HEAD Apache/2.4.18 appears to be outdated (current is at least Apache/2.4.54). Apache 2.2.34 is the EOL for the 2.x branch.
+ GET /: Server may leak inodes via ETags, header found with file /, inode: 426, size: 5818ccf125686, mtime: gzip. See: CVE-2003-1418: 
+ GET /login.php: Cookie PHPSESSID created without the httponly flag. See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies: 
+ OPTIONS OPTIONS: Allowed HTTP Methods: POST, OPTIONS, GET, HEAD .
+ GET /icons/README: Apache default file found. See: https://www.vntweb.co.uk/apache-restricting-access-to-iconsreadme/: 
+ GET /login.php: Admin login page/section found.
```

Nikto found a `/login.php`

## Exploitation

Let’s login with the username and password that we found in the initial enumeration

![Untitled](/write-ups/tryhackme/pickle-rick/4.webp)

We can tell that the command panel is vulnerable to command injections, but there are some limits. For example, we're not allowed to use the `cat`, `more`, `head`, or `tail` commands. but luckily `less` is working. we can use that to get the flags.

listing files in the current directory we got our first flag

![Untitled](/write-ups/tryhackme/pickle-rick/5.webp)

![Untitled](/write-ups/tryhackme/pickle-rick/6.webp)


&nbsp;

---

**Flag `mr. meeseek hair`**

---

&nbsp;


In the same directory, there's another file `clue.txt` which give us hint that other flags are in the file system

![Untitled](/write-ups/tryhackme/pickle-rick/7.webp)

Got the second flag at `home/rick`

![Untitled](/write-ups/tryhackme/pickle-rick/8.webp)

![Untitled](/write-ups/tryhackme/pickle-rick/9.webp)


&nbsp;

---

**Flag `1 jerry tear`**

---


&nbsp;


## Privilege Escalation

For the 3rd flag, we need root privileges. on the system user www-data had the privilege to run sudo on anything that means we can access `/root` without password

![Untitled](/write-ups/tryhackme/pickle-rick/10.webp)

![Untitled](/write-ups/tryhackme/pickle-rick/11.webp)

and we got our 3rd flag

&nbsp;

---

**Flag `fleeb juice`**

---

&nbsp;

&nbsp;
