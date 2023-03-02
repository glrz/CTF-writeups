---
description: >-
  This CTF was held from 1 Mar - 14 Mar 2023, hosted by MGCI and WLMAC. This
  contest was organized by WLMAC's Cybersecurity club and MGCI's CTF club.
---

# WxMCTF 2023

In this capture the flag (CTF) contest, teams of middle and high school students across Ontario battled it out with their skills in digital forensics, website and binary exploitation, reverse engineering, and cryptography!&#x20;

Intended for students of all experience types, the challenges are designed with a low barrier of entry to enable even first-time competitors to gain experience and knowledge in an enjoyable, cooperative way.

Although this Capture the Flag (CTF) event permitted teams of up to four individuals, I chose to compete independently to both relish and enhance my proficiency in tackling these challenges.

I participated as an individual with the username `glrz01` and placed

I spent some time tackling these challenges and found most of the challenges which I solved to be pretty easy and straightforward.

## Sanity Check

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Super straightforward, a challenge to get participants to familiarize with the flag format, just copy paste and submit the flag.

Flag: wxmctf{welcome\_2023}

## PROPRIETARY EOL

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

This challenge was under the forensics category, also a relatively simple challenge. I first-blooded this challenge within seconds.

First, we could check the file type by running the `file` command.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

This confirmed that it was a [`PCX` ](https://en.wikipedia.org/wiki/PCX)file. We could then open this file in `GIMP`.

```
┌──(kali㉿kali)-[~/Downloads]
└─$ gimp public.pcx  
```

Opening it in GIMP, we would be able to see the flag.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Alternatively, we could also open the file using `ImageMagick` as such:

```
┌──(kali㉿kali)-[~/Downloads]
└─$ display public.pcx  
```

Similarly, we would get the flag for the challenge.

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

Flag: CTF{digital\_archaeology\_42}

