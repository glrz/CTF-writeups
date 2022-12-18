---
description: >-
  SHELLCTF 2022 is a beginner-friendly CTF, Hosted By S.H.E.L.L : Cybersecurity
  Club of VNIT. It was held from 12 Aug to 14 Aug 2022.
---

# SHELL CTF 2022

The challenges range from Easy to Hard in difficulty and was segregated into topics :

* Cryptography
* Reverse Engineering
* Web Security
* Forensics
* Miscellaneous

More information for this event can be found [here](https://ctftime.org/event/1604). For this event, I participated with team `Social Engineering Experts` with my initials `RZ`. This is also my first time participating in CTF with them. I recently joined the team after solving the [Social Engineering Experts (Crypto challenge)](https://gadiel-lau.gitbook.io/2022-writeups/social-engineering-experts-crypto-challenge).

We achieved 2nd position for this CTF out of 1000+ teams! I managed to solve a few challenges in this CTF, as well as learn new techniques from awesome teammates.&#x20;

&#x20;

![](<.gitbook/assets/image (70).png>)

The team solved all the challenges.

![](<.gitbook/assets/image (90).png>)

I solved 3 of the challenges. There were some other challenges which I solved too, but my teammates were faster at solving them.

![](<.gitbook/assets/image (122).png>)

I will be including writeups of challenges I solved and some other writeups of challenges which was not solved by me during the CTF for documentation purposes.

## Sanity Check

![](<.gitbook/assets/image (143).png>)

This should be the easiest challenge out of all the other challenges. Usually in CTF, there would be such a challenge probably for participants to get familiar with the flag format.&#x20;

Joining their discord server, and browsing to the announcement channel would give us the flag. I am not exactly sure why I could not copy the flag from the discord server, so I had to type it out manually and submit the flag.

![](<.gitbook/assets/image (99).png>)

Flag: SHELLCTF{W3lc0me\_2\_SHELLCTF2022}

## Alien Communications

![](<.gitbook/assets/image (157).png>)

This challenge was under the forensics category. This challenge was relatively easy but I actually got 6 wrong attempts before getting the correct flag due to the flag format. When I submitted it, I  then realised my teammate zeyu already submitted the correct flag few seconds earlier.&#x20;

For this challenge, we were given an audio file. First, I put this file in `Audacity` for further analysis. If I change it to spectrogram mode, I would see the flag. However, the flag is not exactly as seen in the spectrogram. `shell` needs to be in CAPS in order to be correct.

Note that this kind of challenge is rather simple and common in CTF, I have previously solved similar challenges here.

![](<.gitbook/assets/image (165).png>)

Flag: SHELL{y0u\_g07\_7h3\_f1ag}

## World's Greatest Detective

![](<.gitbook/assets/image (241).png>)

This challenge was under the MISC category. For this challenge, we were given an image file. If we download this image, we would notice that this is a screenshot image and at the end of the image name, it mentions `Wakandan_Translator`.

![](<.gitbook/assets/image (118).png>)

If we open the image, we would see an image with weird characters that look like our flag. We could tell this from the `{ }` in the image.

![](<.gitbook/assets/image (91).png>)

A quick Google search and we would find that we could decode this [here](https://www.dcode.fr/wakanda-alphabet). If we manually match each character, we would get the decoded flag.

![](<.gitbook/assets/image (279).png>)

Flag: SHELLCTF{w4kandA\_F0rev3r}

## Tweet

![](<.gitbook/assets/image (272).png>)

This challenge is under the cryptography category. For this challenge, we were given a `.jpeg` image file. If we open the file, we could see this image.

![](<.gitbook/assets/image (107).png>)

What could this be? Normally, for cryptography challenge, participants would need to write a script or decode messages that are encoded or encrypted with commonly used encryptions or encoding such as `XOR`, `Base64` etc. I would seldom see image in Cryptography related challenges.

First, I opened this image in hex editor like `HxD` but could not find anything useful. At this point, I thought ... what if this challenge could be similar to the previous challenge `World's Greatest Detective` that I just solved.

A quick Google search on `bird cryptography` and we could find `Birds on a Wire Cipher`.

![](<.gitbook/assets/image (104).png>)

Now, we just need to match each bird image/position to get the decoded flag [here](https://www.dcode.fr/birds-on-a-wire-cipher).

![](<.gitbook/assets/image (76).png>)

Flag: SHELLCTF{WELOVESINGING}

## MALBORNE

![](<.gitbook/assets/image (131).png>)

This challenge was in the cryptography category as well. I solved this challenge few seconds after my teammate solved it. For this challenge, we were given a bunch of text which looked like some kind of [Esoteric programming language](https://en.wikipedia.org/wiki/Esoteric\_programming\_language) or esolang in short.

We could go to the [esolang language list](https://esolangs.org/wiki/Language\_list) and search for `malbo`. This would give us an indication that this could be [Malbolge](https://en.wikipedia.org/wiki/Malbolge).

We could then copy the entire code in the challenge description, paste it [here](https://malbolge.doleczek.pl/), run the program and we would get the flag in the terminal output.

![](<.gitbook/assets/image (259).png>)

Flag: SHELL{m41b01g3\_15\_my\_n3w\_l4ngu4g3}

## GO Deep!

![](<.gitbook/assets/image (268).png>)

This challenge was under the forensics category. For this challenge, my teammate solved it but I managed to solve part of the challenge.

We were given a [Google Drive link](https://drive.google.com/drive/folders/1uypoKVmafoPHn9AfgrAR0IuF1EHIhziG). If we open the link, we can download a `agent.zip` file.  In the zip file, there is a `.wav` audio file.

After we extract the audio file, we can run a simple `strings` or `exiftool` command. It would indicate `Password:shell`.

I got to this part and got stuck for awhile, then my teammate managed to solve the other part of the challenge, which is to download [DeepSound](http://jpinsoft.net/deepsound/download.aspx). We could probably infer this from the challenge title which says `Deep`.&#x20;

After we have downloaded `DeepSound`, simply drag and drop the audio file and key in the Password: `shell`.

This would give us a `Deep Flag.txt` file at the bottom. We could extract this file by pressing `F5` or clicking the `Extract secret files` button.

![](<.gitbook/assets/image (82).png>)

&#x20;Opening up the file would give us the flag.

![](<.gitbook/assets/image (113).png>)

SHELL{y0u\_w3r3\_7h1nk1ng\_R3ally\_D33p}

The official writeups for all the challenges can be found [here](https://github.com/S-H-E-L-L/S.H.E.L.L-CTF-2022).
