---
author: "Asad Ullah"
title: "Impossible - ångstromCTF"
description: 
summary: Write-up on cryptography challenge Impossible.
date: 2023-04-27T01:00:24+05:00
Section: write-ups
categories:
- writeup
- ctftime.org
tags:
- angstormctf
- crypto

draft: false

---

{{< 
ctftime 
name="Impossible" 
difficulty="Medium"  
points="50"
category="Cryptography"
>}}

&nbsp;

&nbsp;

## Description

Is this challenge impossible?

`nc challs.actf.co 32200`

[impossible.py](https://files.actf.co/fbb3d3649ac3408c393acd75d08d59c1c52ce87715845251ee34fa212b3dd991/impossible.py)

## Approach

**source code**

```bash
def fake_psi(a, b):
    return [i for i in a if i in b]

def zero_encoding(x, n):
    ret = []
    for i in range(n):
        if (x & 1) == 0:
            ret.append(x | 1)
        x >>= 1
    return ret

def one_encoding(x, n):
    ret = []
    for i in range(n):
        if x & 1:
            ret.append(x)
        x >>= 1
    return ret

print("Supply positive x and y such that x < y and x > y.")
x = int(input("x: "))
y = int(input("y: "))

if len(fake_psi(one_encoding(x, 64), zero_encoding(y, 64))) == 0 and x > y and x > 0 and y > 0:
    print(open("flag.txt").read())
```

&nbsp;

we need to satisfy 3 conditions to get the flag

1. **`x`** must be greater than **`y`**.
2. Both **`x`** and **`y`** must be positive
3. The length of the list returned by fake_psi should be 0.  
**`fake_psi(one_encoding(x, 64), zero_encoding(y, 64))`**  

&nbsp;

We can set **`y`** to 1, which means that **`zero_encoding(y, 64)`** returns a list of 64 ones, where there are 64 ones in total.

To satisfy the condition that **`fake_psi`** should return an empty list, we need to find a value of **`x`** such that **`one_encoding(x, 64)`** returns an empty list. The **`one_encoding`** function only appends to the list if the least significant bit of **`x`** is 1, so we need to set the 64 least significant bits of **`x`** to 0.

We can set **`x`** to **`1 << 64`**, which means shifting the binary representation of **`1`** 64 bits to the left, effectively adding 64 zeros to the end. Therefore, **`x`** is equal to **`18446744073709551616`**.

So, to obtain the flag, you should enter **`x`** as **`18446744073709551616`** and **`y`** as **`1`**.

&nbsp;


```bash
┌──(kali㉿iasad)-[~/CTFs/angstorm]
└─$ nc challs.actf.co 32200
Supply positive x and y such that x < y and x > y.
x: 18446744073709551616
y: 1

actf{se3ms_pretty_p0ssible_t0_m3_7623fb7e33577b8a}
```

&nbsp;

---

**Flag: `actf{se3ms_pretty_p0ssible_t0_m3_7623fb7e33577b8a}`**

---

&nbsp;

&nbsp;
