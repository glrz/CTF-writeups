---
description: >-
  DownUnderCTF is the largest online Australian run Capture The Flag (CTF)
  competition with over 4000+ registered users and over 2100+ registered teams
  (2021). It was held from 23-25 Sept 2022.
---

# DownUnderCTF 2022

More information for this event can be found [here](https://ctftime.org/event/1625). For this event, I participated with team `Social Engineering Experts` with my initials `RZ`.&#x20;

<figure><img src=".gitbook/assets/image (595).png" alt=""><figcaption></figcaption></figure>

Some of my teammates were not able to commit and participate in this CTF due to other commitments. I did not really commit too much time on this CTF as well as it clashes with [Cyber League Major 2](https://gadiel-lau.gitbook.io/2022-writeups/sit-n0h4ts-cyber-league-2022/major-2) and I had some other plans. Nonetheless, I managed to solve a few challenges from categories such as MISC, DFIR and OSINT in this CTF.

<figure><img src=".gitbook/assets/image (501).png" alt=""><figcaption></figcaption></figure>

## Certificate of Participation

<figure><img src=".gitbook/assets/image (592).png" alt=""><figcaption></figcaption></figure>

It was pretty cool they had a certificate of participation for this CTF.

## discord

<figure><img src=".gitbook/assets/image (780).png" alt=""><figcaption></figcaption></figure>

Upon joining their discord channel, browse to the meme channel. It was an age restricted channel so I had to “verify” my age to be above 18.

In the channel, we can find the flag under pinned messages.

<figure><img src=".gitbook/assets/image (117).png" alt=""><figcaption></figcaption></figure>

Flag: DUCTF{G’day\_mates\_this’ll\_be\_a\_cracka}\


## doxme

<figure><img src=".gitbook/assets/image (277).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was under the DFIR category. We were given a doxme file.

Checking it using the `file` command reveals that it is a `Microsoft OOXML` file.

OOXML files are actually zip file containers, which means that one of the easiest ways to check for hidden data is to simply `unzip` the document:

<figure><img src=".gitbook/assets/image (715).png" alt=""><figcaption></figcaption></figure>

As I was scrolling through the contents that was extracted from `doxme`, what really caught my attention were the 2 `png` image files.

Navigating to the `media` directory and browsing the images using the `eog` command would give us 2 different parts of the flag.

<figure><img src=".gitbook/assets/image (703).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (588).png" alt=""><figcaption><p>Flag Part 1</p></figcaption></figure>

<figure><img src=".gitbook/assets/image (753).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (530).png" alt=""><figcaption><p>Flag Part 2</p></figcaption></figure>

Combining 2 parts of the flag gives us the flag to this challenge.

Flag: DUCTF{Word\_D0Cs\_Ar3\_R34L1Y\_W3ird}

## Rage!

<figure><img src=".gitbook/assets/image (541).png" alt=""><figcaption></figcaption></figure>

In this challenge, it was under the MISC category. We were given an audio `.wav` file.&#x20;

I played the audio and there was some REALLY NOISY music. I listened to it carefully and noticed there were beeping sounds in the background which indicated it could likely be `morse code`.

Opening the file in `Audacity`, we can see 2 different channels. Changing it to `Spectrogram mode`, we could see morse code at the bottom of each channel. This is indicated by the short and longer dashes.

<figure><img src=".gitbook/assets/image (129).png" alt=""><figcaption></figcaption></figure>

However, the morse code were not clear enough for us to deduce the message behind it. Playing around with the `Range` and `Gain` in `Spectrogram Settings` certainly helped to solve this challenge. I changed the `Range` to 1 and the `Gain` to 10.&#x20;

<figure><img src=".gitbook/assets/image (524).png" alt=""><figcaption></figcaption></figure>

Now we could see the morse code as indicated by the dots and dashes.

<figure><img src=".gitbook/assets/image (738).png" alt=""><figcaption></figcaption></figure>

Using an [online morse code translator](https://morsecode.world/international/translator.html), we can easily solve this challenge.

<figure><img src=".gitbook/assets/image (503).png" alt=""><figcaption><p>N</p></figcaption></figure>

Note that similar challenges which involve the use of `Audacity` / `Morse Code` could sometimes appear under `Forensics` category as well. This challenge which I just solved is similar to a previous challenge I solved in SIT's N0H4TS STANDCON CTF 2022. If you are interested in reading the writeup, its [here](https://gadiel-lau.gitbook.io/2022-writeups/sit-n0h4ts-standcon-ctf-2022#i-sea-you-part-1).

Flag : RAGINGTOWEIRDLIBIDO

## Bird's eye view!

<figure><img src=".gitbook/assets/image (520).png" alt=""><figcaption></figcaption></figure>



For this challenge, it was under the OSINT category. We were given a `.jpg` image file. We cannot really tell where this place is, the picture just shows a bunch of trees.

<figure><img src=".gitbook/assets/image (128).png" alt=""><figcaption></figcaption></figure>

To check for useful information about this image, we could use an [online exif tool ](https://exif.tools/upload.php)to find information about the image metadata. If we scroll down, we would see `GPS Position` which could be useful in helping us determine the location of this place.

<figure><img src=".gitbook/assets/image (539).png" alt=""><figcaption></figcaption></figure>

We could find the possible address by keying in the `Latitude` and `Longitude` [here](https://www.gps-coordinates.net/).

<figure><img src=".gitbook/assets/image (586).png" alt=""><figcaption></figcaption></figure>

If we click on `Get Address`, it would suggest that the place is likely to be in Australia.

<figure><img src=".gitbook/assets/image (505).png" alt=""><figcaption></figcaption></figure>

This place itself is not the flag. The challenge description mentioned `nice spot to have picnic`. However, there are many picnic spots around this place. We have to find the correct picnic spot where this image was taken.

A quick Google search on `sir samuel griffith drive bardon picnic` and we will get the following results.

<figure><img src=".gitbook/assets/image (518).png" alt=""><figcaption></figcaption></figure>

Clicking on the first link and looking around for nearby picnic spots, we will arrive at the flag under `Neaby Businesses`

<figure><img src=".gitbook/assets/image (113).png" alt=""><figcaption></figcaption></figure>

Note that similar challenges could be under the `forensics` category as it involves the use of exiftool to find metadata information. Check out other challenges where I used exiftool as part of  solving the challenges [here](https://gadiel-lau.gitbook.io/2021-writeups/csit-the-infosecurity-challenge-tisc-2021#scratching-the-surface-challenge-2), [here](https://gadiel-lau.gitbook.io/2022-writeups/sg-cyber-olympian-trials-2022#funny-monkey), [here](https://gadiel-lau.gitbook.io/2022-writeups/lagncrash-interpoly-ctf-2022#s3crethero) and [here](https://gadiel-lau.gitbook.io/2022-writeups/shell-ctf-2022#go-deep).

Flag: hooppine

## Honk Honk

<figure><img src=".gitbook/assets/image (565).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was under the OSINT category. The challenge description mentions about `car's CTP` and provides what seemed like the registration or plate number : `23HONK`. With these information, we could use Google to find our answers.

A quick search on Google on `car ctp status check` and we will get the following result

<figure><img src=".gitbook/assets/image (574).png" alt=""><figcaption></figcaption></figure>

I clicked into this [link](https://free-rego-check.service.nsw.gov.au/?isLoginRequired=true#.) to check the vehicle registration with the NSW plate number: `23HONK`.&#x20;

<figure><img src=".gitbook/assets/image (509).png" alt=""><figcaption></figcaption></figure>

This would give us more information about the vehicle including the vehicle type, colour etc. What we are interested in is the registration expiry date which can be found too.

<figure><img src=".gitbook/assets/image (131).png" alt=""><figcaption></figcaption></figure>

Flag: DUCTF{19/07/2023}

## twitter

<figure><img src=".gitbook/assets/image (528).png" alt=""><figcaption></figcaption></figure>

For this challenge, it is under the MISC category. A short description is given for this challenge.\
A quick Google search on the description and we would find the Twitter page for `DownUnderCTF`.

&#x20;

<figure><img src=".gitbook/assets/image (537).png" alt=""><figcaption></figcaption></figure>

We will find the flag under the description of the Twitter page.

<figure><img src=".gitbook/assets/image (553).png" alt=""><figcaption></figcaption></figure>

Flag: DUCTF{the-mascot-on-the-ductf-hoodie-is-named-ducky}

## Survey

<figure><img src=".gitbook/assets/image (794).png" alt=""><figcaption></figcaption></figure>

HAHA if you made it till the end of this writeup, Good Job! This however is not really a challenge, its just filling up a survey form with ratings and feedbacks about the CTF. At the end of it, the flag will be given :)

<figure><img src=".gitbook/assets/image (133).png" alt=""><figcaption></figcaption></figure>

Flag: DUCTF{thx\_4\_playing\_DUCTF\_2022}

Official writeups for this CTF can be found [here](https://github.com/DownUnderCTF/Challenges\_2022\_Public).
