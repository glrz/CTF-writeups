---
description: >-
  AIS3 EOF CTF 2022 is organized by Advanced Information Security - Summer
  School (AIS3). It is a Capture-The-Flag competition held from 12-13 Feb 2022.
---

# AIS3 EOF CTF 2022

I took part in the Global Cybersecurity Camp(GCC) 2022 Taiwan from 8-23 Jan 2022. Annually, the best 48 students (maximum) from member countries gather in one of the participating countries for a week to exchange experience, forge a life-long friendship, and learn from the best cybersecurity professionals. This year, 7 Singapore students were selected to attend GCC as Singapore delegates and I am one of them.

Participating countries and it’s organization of GCC includes: [Japan (Security Camp Committee)](https://www.security-camp.or.jp/event/gcc\_online2022.html), [Singapore (Division Zero)](https://www.div0.sg/gcc), [South Korea (KITRI BoB Programme)](https://www.kitribob.kr/), [Taiwan (Advanced Information Security Summer School)](https://ais3.org/), [Malaysia (Nanosec)](https://nanosec.asia/), [Thailand (2600 Thailand)](https://www.facebook.com/groups/2600Thailand), [Vietnam (VNSEC)](https://www.vnsecurity.net/) and [Australia (UQ Cyber Security)](https://www.itee.uq.edu.au/research/cyber-security).&#x20;

This year's GCC covered topics such as [Hand-on Post-exploitation Penetration and Investigation](https://gcc.ac/gcc\_2022/lecture1), [Reverse-Engineering and Exploitation Fundamentals](https://gcc.ac/gcc\_2022/lecture2), [Reverse Engineering Malware Written in C++ with IDA and Semi-Automated Scripts](https://gcc.ac/gcc\_2022/lecture3), [UEFI BIOS Security](https://gcc.ac/gcc\_2022/lecture4), [Computers within computers - a case study of emulation tech and potential pitfalls](https://gcc.ac/gcc\_2022/lecture5), [Robust Protocol Open Challenge](https://gcc.ac/gcc\_2022/lecture6), [Introduction to Homomorphic Encryption and Its Applications to Privacy Preserving Data/Signal Analysis](https://gcc.ac/gcc\_2022/lecture7), [Attacker behavior analysis base on attack vector analysis](https://gcc.ac/gcc\_2022/lecture8) and [Home IoT Device Security](https://gcc.ac/gcc\_2022/lecture9). For more information, visit GCC website [here](https://gcc.ac/gcc\_2022/).

The AIS3 EOF CTF 2022 was hosted by the same organization: AIS3. GCC students were then invited to participate in this CTF and up to 10 GCC students were allowed in a team. For this CTF, I participated with the team name: \[GCC]2, with 3 other teammates - Choo Chi Siang(Malaysia), Liu pin-tin(Taiwan) and Kota Fukushima(Japan). We had 2 solves, 1 was solved by me and the other solved by Liu pin-tin. In this writeup, I would only include the one I solved.

![](<.gitbook/assets/image (253).png>)

![](<.gitbook/assets/image (287).png>)

![](<.gitbook/assets/image (364).png>)

![Final scoreboard](<.gitbook/assets/image (296).png>)

## Capture the Flag™

In this challenge, we were given a .STL file.&#x20;

{% file src=".gitbook/assets/trademarked_flag.stl" %}

Spoiler : This challenge is kind of steganography related, where the flag is hidden in the 3D design.

STL is **a file format commonly used for 3D printing and computer-aided design (CAD)**. The name STL is an acronym that stands for stereolithography — a popular 3D printing technology.&#x20;

To view this file, I used an online viewer [here](https://www.viewstl.com/).&#x20;

At first glance, it just looks like a normal flag design.

I proceeded to check every part of the flag design: top view, bottom view, front view, back view..

![Front view](<.gitbook/assets/image (272) (1).png>)

![Back view](<.gitbook/assets/image (345).png>)

![Top view](<.gitbook/assets/image (361).png>)

![Bottom view](<.gitbook/assets/image (391).png>)

Zoomed in and out for a couple of minutes but could not find anything useful.

At this point, I tried tinkering with the other settings in the `Model selection mode`

I could click `Model selection mode` and then click on this model

&#x20;

![](<.gitbook/assets/image (332).png>)

On the left, I select `Wireframe`

![](<.gitbook/assets/image (238) (1).png>)

I realised there are some words at the base of the flag. I decided to zoom in to take a closer look

![](<.gitbook/assets/image (258).png>)

Now, we could change different settings such as decreasing the opacity, or try different rotating methods to read the words.

After doing this for some time, the text reads : `I heard that people have been stealing 3D printing without attributing the author Wonder if there is any way to add watermark to a 3d model?`

![](<.gitbook/assets/image (215) (1).png>)

Solving this challenge, I came across this online [site](https://www.watermark3d.com/) which allowed me to check the watermark.

I could upload the file, leave the password field as empty and click `check watermark`

![](<.gitbook/assets/image (283).png>)

As we can see, there is our flag in the results column

![](<.gitbook/assets/image (337).png>)

Flag: EOF{sT3gn0gr4phy\_0n-3d\_Fi1es-miGhT\_be-a\_vi4bl3-$trat\_lol}
