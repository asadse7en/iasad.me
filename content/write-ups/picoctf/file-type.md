---
author: "Asad Ullah"
title: File Types - PicoCTF
summary: forensics challenge with nested compressions and file types

date: 2023-03-30T02:54:51+05:00

Section: "write-ups"

categories: ["writeup", "picoctf", "forensics"]
tags: ["compression", "picoctf", "lzip", "lzop", "LZMA", "bzip2", "cpio", "forensics"]

draft: false

---


{{< 
picoinfo 
name="File Types" 
difficulty="Easy"  
points="100"
creator_name="PicoCTF" creator_link="https://play.picoctf.org/practice/challenge/268" 
category="Forensics"
>}}

## Description

This file was found among some files marked confidential but my pdf reader cannot read it, maybe yours can.

You can download the file from [here](https://artifacts.picoctf.net/c/80/Flag.pdf)

> **Hint💡**  
> Remember that some file types can contain and nest other files

First, download the file 

```bash
curl https://artifacts.picoctf.net/c/80/Flag.pdf
```

After downloading the file, the first step is to check its type by using the `file` command in Linux: `file Flag.pdf`. In this specific case, it turns out that the file is not a PDF but a shell archive.

let's change the extension from .pdf to .sh and give it executable permissions and execute it 

```bash
┌──(kali㉿iasad)-[~/CTFs/picoCTF]
└─$ mv flag.pdf flag.sh

┌──(kali㉿iasad)-[~/CTFs/picoCTF]
└─$ chmod +x flag.sh

┌──(kali㉿iasad)-[~/CTFs/picoCTF]
└─$ ./flag.sh
```

If you receive an error message saying `uudecode: command not found`, you need to install uudecode. This utility is part of sharutils, and can be installed with the command `sudo apt install sharutils`.

After installation, run `./flag.sh` to extract a flag file. Check the file type by running `file flag`. It is a current ar archive.

### Let's extract the flag from the nested Archives.

- `ar x flag` - **to extract ar archive use**
    - `file flag` - **cpio archive**
    - `mv flag flag.cpio` -  change file extension
- `cpio —file flag.cpio —extract`
    - `file flag` - **bzip2 compressed data**
    - `mv flag flag.bzip2` - change file extension
- `bzip2 flag`
    - `file flag.out` - **gzip compressed data**
    - `mv flag.out flag.gz` - change file extension
- `gunzip flag.gz`
    - `file flag` - **lzip compressed data**
- `lzip -d flag`
    - `file flag.out` - **LZ4 compressed data**
    - `mv flag.out flag.lz4` - change file extension
- `lz4 -d flag.lz4`
    - `file flag` - **LZMA compressed data**
    - `mv flag flag.lzma` - change file extension
- `unlzma -d flag.lzma`
    - `file flag` - **lzop compressed data**
    - `mv flag flag.lzop` - change file extension
- `lzop -x flag.lzop`
    - `file flag` - **lzip compressed data**
- `lzip -d flag`
    - `file flag` - **XZ compressed data**
    - `mv flag.out flag.xz` - change file extension
- `unxz flag.xz`
    - `file flag` - **ASCII Data**

**Finally** we got an ASCII text file containing the following hexadecimal string:

```bash
7069636f4354467b66316c656e406d335f6d406e3170756c407431306e5f
6630725f3062326375723137795f39353063346665657d0a
```

This is a hexadecimal representation of text. With a quick search on Google, you can find many tools that can convert it to text and ultimately reveal the flag. in Linux use this command`cat flag | xxd -r -p`

---

**Flag: `picoCTF{f1len@m3_m@n1pul@t10n_f0r_0b2cur17y_950c4fee}`**

---

## Conclusion

*The challenge "File Type" on PicoCTF involves analyzing a file that is not what it seems to be. The file appears to be a PDF, but it turns out to be a shell archive. The solution involves extracting the file using a series of commands, which reveal that the file is actually a compressed ASCII text file containing a hexadecimal representation of text. The final output is a flag that can be obtained by converting the hexadecimal string to text.*