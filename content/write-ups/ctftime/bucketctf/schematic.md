---
author: "Asad Ullah"
title: "Schematic - BucketCTF"
description: 
summary: Write-up on Misc challenge Schematic.
date: 2023-04-10T03:05:34+05:00
Section: write-ups
categories:
- writeup
tags:
- bucketctf
- misc
- minecraft
- schematic

draft: false

---

{{< 
ctftime 
name="Schematic" 
difficulty="Easy"  
points="284"
category="Misc"
>}}

&nbsp;

&nbsp;


## Description

I build a tnt cannon, how many dispensers am I using.

format: bucket{number_goes_here}

Download Attachments {{< url link="https://storage.ebucket.dev/Ricardo3s_60AP_100C_200SB.schematic" text="here" >}}

&nbsp;

## Approach

we are given a `.schematic` file and we have to count the number of dispensers used.

>
> **Schematic💡**  
> A schematic is a type of file format used to represent a 3D object or structure in Minecraft, It contains a blueprint or schematic of a Minecraft build.
> 
>


Tools such as **MCEdit** and **WorldEdit** can be used to analyze `.schematic` files, and there are also several online sites that offer the same functionality.

&nbsp;

I oped the file in {{< url link="https://cubical.xyz/" text="cubical.xyz" >}} but I had to manually count the dispensers, So I looked for alternatives and discovered {{< url link="https://www.mineprints.net/" text="Mineprints" >}} which conveniently displayed the number of dispensers used in the schematic.


![schematic](/write-ups/ctftime/bucket/schematic.webp)

&nbsp;

&nbsp;


---

**Flag `bucket{2238}`**

---

&nbsp;

&nbsp;
