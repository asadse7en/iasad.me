---
author: "Asad Ullah"
title: Cryptography - aupCTF
description: writeups for cryptographic challenges
summary: writeups for cryptographic challenges
date: 2023-07-01T19:33:32+05:00
tocopen: true

Section: "write-ups"

categories:
- aupctf
- cryptography

tags:
- enigma
- rsa
- transposition
- vigenere
- cipher
- ceaser
- aupctf


draft: False

---

&nbsp;

&nbsp;

{{< 
ctf 
name="Ancient Cipher" 
category="Cryptography" 
difficulty="Easy"
points="100"  
creator_name="aupCTF" creator_link="https://tryhackme.com/jr/aupctf" 
>}}

## **Ancient Cipher (100pts)**

### Description

Meet Bob, the world's worst cryptographer. His encryption skills are so bad that his messages are basically gibberish. One time, he tried to send a secret message to his friend Alice, but it was so poorly encrypted that his dog was able to decode it. Needless to say, Bob's not winning any cryptography awards anytime soon.

`rlgTKW{S0s'j_Sru_Tipgk0xirgyp_5b1ccj}`

### Approach

The name of the challenge implies an ancient cipher, which commonly refers to the Caesar cipher.

![Untitled](/write-ups/aupctf/crypto/1.webp)

&nbsp;

{{<flag "flag" "aupCTF{B0b's_Bad_Crypt0graphy_5k1lls}">}}


&nbsp;

&nbsp;


{{< 
ctf 
name="Rotation" 
category="Cryptography" 
difficulty="Easy"
points="100"  
creator_name="aupCTF" creator_link="https://tryhackme.com/jr/aupctf" 
>}}

## **Rotation (100pts)**

### Description

We've employed a unique technique to encode the message, one that goes beyond the traditional limits of the Caesar cipher. Keep your wits about you and explore every possible avenue - the answer may be closer than you think

`2FAr%uLJ_F\7_F?5\>bN`

### Approach

The challenge name suggests a rotation cipher, but it doesn't appear to be a simple rotation like ROT13. Since the ciphertext does not include the characters "{}" that would remain unchanged in ROT13, we can explore the possibility of using ROT47 as an alternative rotation cipher.

![Untitled](/write-ups/aupctf/crypto/2.webp)

Now the ciphertext appears to resemble ROT13, so it's worth attempting that ROT13.

![Untitled](/write-ups/aupctf/crypto/3.webp)

&nbsp;

&nbsp;

{{<flag "flag" "aupCTF{B0b's_Bad_Crypt0graphy_5k1lls}">}}


&nbsp;

{{< 
ctf 
name="Enigma" 
category="Cryptography" 
difficulty="Easy"
points="100"  
creator_name="aupCTF" creator_link="https://tryhackme.com/jr/aupctf" 
>}}


## **Enigma (100pts)**

### Description

I found an old enigma machine and was messing around with it. can you decipher it

```
MACHINE TYPE: `kriegsmarine 3 rotors`

REFLECTOR: `B`

ROTORS: `I, II, III`

INITIAL POSITIONS OF THE ROTORS: `X, Y, Z`

POSITION OF THE ALPHABET WHEEL: `A, B, C`

PLUGBOARD: `AT BS DE FM IR KN LZ OW PV XY`

CIPHER: `LXFUZLVHEJLEWZRIXIS`

remember to put the flag in format: `aupCTF{answer}` answer in UPPERCASE
```

### Approach

Since all the values are given we can simply put it in a decoder and get the answer

![Untitled](/write-ups/aupctf/crypto/4.webp)

&nbsp;

&nbsp;

{{<flag "flag" "aupCTF{ENIGMAISFASCINATING}">}}


&nbsp;

{{< 
ctf 
name="Disorder" 
category="Cryptography" 
difficulty="Medium"
points="200"  
creator_name="aupCTF" creator_link="https://tryhackme.com/jr/aupctf" 
>}}

## **Disorder (200pts)**

### Description

`utsa}Ts0aXa{1_eC1ngXph__XF_tmX`

### Approach

It seems that every letter of the flag format "aupCTF{}" is present in the ciphertext. A transposition cipher is a good assumption at this point, as it changes the order of the plaintext.

```plaintext
utsa}Ts0aXa{1_eC1ngXph__XF_tmX

By splitting the ciphertext after every 5 letters, 
we can extract the flag by selecting the letters according to the flag format.

utsa}  -- 2nd
Ts0aX  -- 5th
a{1_e  -- 1st
C1ngX  -- 4th
ph__X  -- 3rd
F_tmX  -- 6th

reconstructing the flag

aupCTF{th1s_1s_n0t_a_game}XXXX
```

&nbsp;

&nbsp;

{{<flag "flag" "aupCTF{th1s_1s_n0t_a_game}">}}
&nbsp;

{{< 
ctf 
name="Really Secure Algorithm" 
category="Cryptography" 
difficulty="Medium"
points="200"  
creator_name="aupCTF" creator_link="https://tryhackme.com/jr/aupctf" 
>}}

## **Really Secure Algorithm (200pts)**

### Description

Just remember, the key to success is staying calm, cool, and collected. Oh, and maybe a little bit of math.

**Challenge Files:** [output.txt](https://aupctf.s3.eu-north-1.amazonaws.com/output.txt)  [rsa.py](https://aupctf.s3.eu-north-1.amazonaws.com/rsa.py)

### Approach

**rsa.py**

```python
from Crypto.Util.number import getStrongPrime, bytes_to_long
f = open("flag.txt").read()
m = bytes_to_long(f.encode())
p = getStrongPrime(512)
q = getStrongPrime(512)
n = p*q
e = 0x10001
c = pow(m,e,n)

print("n =",n)
print("e =",e)
print("c =",c)
print("p + q = ",p + q)
print("p - q = ",p - q)
```

**output**

```
n = 114451512782061350994183549689132403225242966062482357218929786202609314635625168402975465116960672539381904935689924074978793017604108838426275397024126351435336388859375577638687615733448645699186377194544704879027804400841223407182597828299190404980916587708863068950664207317360099871904794302327240026597
e = 0x10001
c = 77973874950946982309998238055233832655056168217930252243355819182449120246116674359138553216317477143768434108918799869104308920311195408379262816485377057853246446992573203590942762693635615621774057306679349618708293741847308966437868706668452083656318895155238523224237514077565164105837790895618179891869
p + q =  21400959789031198835597502268226110838410793429486235013163818172148759394109297013195530163943463063090162742198192075506990494863858727035693527345539878
p - q =  441620610348849769847261104024471204541391170160225757260110727514761526074769013762749528928112909396341014808517549368576708910310103233373547986477636
```

We can find $p$ and $q$ using python

```python
from sympy import symbols, Eq, solve

p, q = symbols('p q')

eq1 = Eq((p+q), 21400959789031198835597502268226110838410793429486235013163818172148759394109297013195530163943463063090162742198192075506990494863858727035693527345539878)
eq2 = Eq((p-q), 441620610348849769847261104024471204541391170160225757260110727514761526074769013762749528928112909396341014808517549368576708910310103233373547986477636)

solution = solve((eq1, eq2), (p, q))
print(solution)
```

&nbsp;

**output**

```python
{p: 10921290199690024302722381686125291021476092299823230385211964449831760460092033013479139846435787986243251878503354812437783601887084415134533537666008757, 
 q: 10479669589341174532875120582100819816934701129663004627951853722316998934017263999716390317507675076846910863694837263069206892976774311901159989679531121}
```

&nbsp;

{{< toggle title="Decryption Process" >}}
  
&nbsp;

1. Compute \\(\phi(n) = (p-1)(q-1)\\).
2. Calculate the modular multiplicative inverse of \\(e\\) modulo \\(\phi(n)\\), denoted as \\(d\\), such that \\((d \cdot e) \bmod \phi(n) = 1\\).   
In python we can use `inverse` function from `Crypto.Util.number`
3. Compute \\(m = c^d \bmod n\\). In python `pow(c, d, n)`.  
The plaintext message, denoted as \\(m\\), can then be obtained by converting the resulting integer value to its corresponding character representation.

{{< /toggle >}}

```python
from Crypto.Util.number import long_to_bytes, inverse

p = 10921290199690024302722381686125291021476092299823230385211964449831760460092033013479139846435787986243251878503354812437783601887084415134533537666008757
q = 10479669589341174532875120582100819816934701129663004627951853722316998934017263999716390317507675076846910863694837263069206892976774311901159989679531121

n = p * q
e = 65537  # Converted hex 0x10001 to decimal
phi = (p - 1) * (q - 1)
d = inverse(e, phi)

c = 77973874950946982309998238055233832655056168217930252243355819182449120246116674359138553216317477143768434108918799869104308920311195408379262816485377057853246446992573203590942762693635615621774057306679349618708293741847308966437868706668452083656318895155238523224237514077565164105837790895618179891869
m = pow(c, d, n)

plaintext = long_to_bytes(m)
print(plaintext.decode())

```

&nbsp;

&nbsp;

{{<flag "flag" "aupCTF{3a5y_tw0_3quat10n5_and_hax3d_3}">}}

&nbsp;

{{< 
ctf 
name="Swiss Army Knife" 
category="Cryptography" 
difficulty="Medium"
points="200"  
creator_name="aupCTF" creator_link="https://tryhackme.com/jr/aupctf" 
>}}

## **Swiss Army Knife (200pts)**

### Description

[decode.txt](https://aupctf.s3.eu-north-1.amazonaws.com/decode.txt)

### Approach

The contents of the file consist solely of 'X' and 'Y' characters, resembling a binary format. 'X' is replaced with '0', and 'Y' is replaced with '1'.

when we can decode multiple encodings one by one, here is the [complete racipe](https://gchq.github.io/CyberChef/#recipe=Find_/_Replace(%7B'option':'Regex','string':'X'%7D,'0',true,false,true,false)Find_/_Replace(%7B'option':'Regex','string':'Y'%7D,'1',true,false,true,false)From_Binary('Space',8)From_Base64('A-Za-z0-9%2B/%3D',true,false)From_Morse_Code('Space','Line%20feed')From_Base32('A-Z2-7%3D',true)ROT13(true,true,false,7)&input=WFlYWFlZWFggWFlYWVhYWVkgWFhZWVhYWFggWFlZWVhZWFggWFlYWFlYWFkgWFlYWFhYWVkgWFhZWVhZWFggWFlZWVhZWFggWFlYWFlZWFggWFlZWFlYWFkgWFlYWFhYWFkgWFlZWVhZWFggWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWVhZWFggWFlYWFlYWFkgWFlYWFhYWVkgWFhZWVhYWFggWFlZWVhZWFggWFlYWFlZWFggWFlZWFlYWFkgWFlYWFhYWFkgWFlZWVhZWFkgWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWFhZWVkgWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWVhZWFkgWFlYWFlZWFggWFlYWVhYWVkgWFlYWFhYWFkgWFlZWVhZWFkgWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWFhZWVkgWFlYWFlZWFggWFlYWVhYWVkgWFhZWVhZWFggWFlZWFhZWVkgWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhYWFggWFlZWVhZWFkgWFlYWFlZWFggWFlZWFlYWFkgWFlYWFhYWFkgWFlZWVhZWFkgWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhYWFggWFlZWVhZWFkgWFlYWFlYWFkgWFlYWFhYWVkgWFhZWVhZWFggWFlZWVhZWFkgWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWVhZWFkgWFlYWFlYWFkgWFlYWFhYWVkgWFhZWVhZWFggWFlZWVhZWFggWFlYWFlZWFggWFlYWVhYWVkgWFlYWFhYWFkgWFlZWVhZWFggWFlYWFlZWFggWFlYWVhYWVkgWFlYWFhYWFkgWFlZWVhZWFkgWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWVhZWFggWFlYWFlZWFggWFlYWVhYWVkgWFlYWFhYWFkgWFlZWVhZWFkgWFlYWFlZWFggWFlYWVhYWVkgWFhZWVhZWFggWFlZWFhZWVkgWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhYWFggWFlZWVhZWFkgWFlYWFlYWFkgWFlYWFhYWVkgWFhZWVhYWFggWFlZWVhZWFkgWFlYWFlYWFkgWFlYWFhYWVkgWFhZWVhZWFggWFlZWVhZWFkgWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhYWFggWFlZWFhZWVkgWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhYWFggWFlZWVhZWFkgWFlYWFlYWFkgWFlYWFhYWVkgWFhZWVhYWFggWFlZWVhZWFggWFlYWFlZWFggWFlZWFlYWFkgWFlYWFhYWFkgWFlZWVhZWFkgWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWFhZWVkgWFlYWFlZWFggWFlYWVhYWVkgWFhZWVhYWFggWFlZWFhZWVkgWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhYWFggWFlZWVhZWFggWFlYWFlZWFggWFlYWVhYWVkgWFlYWFhYWFkgWFlZWVhZWFggWFlYWFlYWFkgWFlYWFhYWVkgWFhZWVhZWFggWFlZWVhZWFkgWFlYWFlZWFggWFlYWVhYWVkgWFhZWVhZWFggWFlZWFhZWVkgWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWVhZWFggWFlYWFlYWFkgWFlYWFhYWVkgWFhZWVhYWFggWFlZWVhZWFggWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWFhZWVkgWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhYWFggWFlZWVhZWFggWFlYWFlYWFkgWFlYWFhYWVkgWFhZWVhYWFggWFlZWVhZWFggWFlYWFlZWFggWFlYWVhYWVkgWFlYWFhYWFkgWFlZWVhZWFkgWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWVhZWFkgWFlYWFlZWFggWFlZWFlYWFkgWFlYWFhYWFkgWFlZWVhZWFkgWFlYWFlZWFggWFlYWVhYWVkgWFhZWVhZWFggWFlZWFhZWVkgWFlYWFlZWFggWFlYWVhYWVkgWFhZWVhYWFggWFlZWVhZWFkgWFlYWFlZWFggWFlYWVhYWVkgWFlYWFhYWFkgWFlZWVhZWFggWFlYWFlZWFggWFlYWVhYWVkgWFhZWVhYWFggWFlZWFhZWVkgWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWVhZWFkgWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhYWFggWFlZWFhZWVkgWFlYWFlZWFggWFlYWVhYWVkgWFhZWVhZWFggWFlZWVhZWFggWFlYWFlZWFggWFlYWVhYWVkgWFlYWFhYWFkgWFlZWVhZWFkgWFlYWFlZWFggWFlYWVhYWVkgWFhZWVhYWFggWFlZWFhZWVkgWFlYWFlZWFggWFlYWVhYWVkgWFhZWVhYWFggWFlZWVhZWFggWFlYWFlYWFkgWFlYWFhYWVkgWFhZWVhYWFggWFlZWVhZWFkgWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWVhZWFkgWFlYWFlYWFkgWFlYWFhYWVkgWFhZWVhZWFggWFlZWVhZWFggWFlYWFlZWFggWFlZWFlYWFkgWFlYWFhYWFkgWFlZWVhZWFkgWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWVhZWFggWFlYWFlYWFkgWFlYWFhYWVkgWFhZWVhZWFggWFlZWVhZWFkgWFlYWFlZWFggWFlYWVhYWVkgWFhZWVhZWFggWFlZWFhZWVkgWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWVhZWFkgWFlYWFlZWFggWFlYWVhYWVkgWFlYWFhYWFkgWFlZWVhZWFggWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWVhZWFggWFlYWFlYWFkgWFlYWFhYWVkgWFhZWVhYWFggWFlZWVhZWFkgWFlYWFlZWFggWFlZWFlYWFkgWFlYWFhYWFkgWFlZWVhZWFggWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhYWFggWFlZWFhZWVkgWFlYWFlZWFggWFlYWVhYWVkgWFhZWVhYWFggWFlZWFhZWVkgWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWVhZWFkgWFlYWFlZWFggWFlYWVhYWVkgWFhZWVhYWFggWFlZWFhZWVkgWFlYWFlZWFggWFlYWVhYWVkgWFhZWVhZWFggWFlZWVhZWFkgWFlYWFlZWFggWFlYWVhYWVkgWFlYWFhYWFkgWFlZWVhZWFkgWFlYWFlZWFggWFlYWVhYWVkgWFhZWVhYWFggWFlZWVhZWFkgWFlYWFlYWFkgWFlYWFhYWVkgWFhZWVhZWFggWFlZWVhZWFkgWFlYWFlZWFggWFlYWVhYWVkgWFlYWFhYWFkgWFlZWVhZWFggWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWVhZWFkgWFlYWFlZWFggWFlYWVhYWVkgWFlYWFhYWFkgWFlZWVhZWFggWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWVhZWFkgWFlYWFlZWFggWFlYWVhYWVkgWFlYWFhYWFkgWFlZWVhZWFggWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWVhZWFkgWFlYWFlZWFggWFlYWVhYWVkgWFlYWFhYWFkgWFlZWVhZWFggWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWVhZWFkgWFlYWFlZWFggWFlYWVhYWVkgWFlYWFhYWFkgWFlZWVhZWFggWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWVhZWFkgWFlYWFlZWFggWFlYWVhYWVkgWFlYWFhYWFkgWFlZWVhZWFggWFlYWFlZWFggWFlZWFlYWFkgWFhZWVhZWFggWFlZWVhZWFkgWFlYWFlZWFggWFlYWVhYWFkgWFhZWVlZWFkgWFhZWVlZWFk)

**Binary —> Base64 —> Morse Code —> Base32 —> Rot13**

![Untitled](/write-ups/aupctf/crypto/5.webp)

&nbsp;

&nbsp;

{{<flag "flag" "aupCTF{mu1tip13-3nc0d1ng5-u53d}">}}

&nbsp;

{{< 
ctf 
name="Battista Bet" 
category="Cryptography" 
difficulty="Medium"
points="200"  
creator_name="aupCTF" creator_link="https://tryhackme.com/jr/aupctf" 
>}}


## **Battista Bet (200pts)**

### Description

My friend is a big fan of the famous Italian cryptographer **Giovan Battista Bellaso**, he has challenged me to crack this ciphertext. I have been struggling to decode it, Can you help me out

**`syrTXY{T3pnr50A0ndhD3Gv0nv}`**

Hint💡: The key to decode the message is a **SECRET**

### Approach

from the description its clear that vigenere cipher is used and the key is secret

![Untitled](/write-ups/aupctf/crypto/6.webp)


&nbsp;

&nbsp;

{{<flag "flag" "aupCTF{B3lla50W0uldB3Pr0ud}">}}

&nbsp;

&nbsp;
