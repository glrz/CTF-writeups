---
description: >-
  AISP Cyber Wellness CTF is a CTF organised by AISP and JUSTHACKING, held from
  28 May - 29 May 2022.
---

# AiSP Cyber Wellness CTF

![](<.gitbook/assets/image (485).png>)

I did not hear about this CTF, but I chanced upon it on AISP website, under `FOR YOUTHS` drop down list > `Mini-CTF`.&#x20;

![](<.gitbook/assets/image (456).png>)

If you are wondering why was I on AISP website, that is because I have been actively participating in events organised by AISP. Such events include Singapore Cyber Security Inter Association Cyber Day Quiz Competition 2021, Singapore Cyber Day Quiz 2021, AiSP Cyber Wellness March 2022 Quiz  and AiSP Cyber Wellness May 2022 Quiz.

The Singapore Cyber Security Inter Association (SCSIA) quiz competition is for primary, secondary and tertiary students (aged 35 years and below) in Singapore. This competition is supported by the Cyber Security Agency of Singapore. It aims to pique interest in students and equip with knowledge on Cyber Security. I completed all 29 weeks of questions from 25 March - 30 September 2021.

![](<.gitbook/assets/image (482).png>)

Singapore Cyber Day Quiz 2021 is for the students to take part in during the December school holidays. The 4 weeks online quiz competition is opened to primary, secondary and tertiary students (aged 25 years and below) in Singapore with the support from Cyber Security Agency of Singapore & Fortinet. This competition aims to pique interest in students and equip them with knowledge on Cyber Security.

For this competition I was in `Top 3` and was invited to a Prize Presentation at Fortinet Office in Jan 2022. Pictures taken during prize presentation could be found [here](https://www.facebook.com/media/set/?set=a.4858764924212028\&type=3). You can also search for my name in [AiSP's newsletter](https://www.aisp.sg/document/newsletter/AiSP\_Newsletter\_2022%20February.pdf).

Thanks once again to AISP and Fortinet for sponsoring amazing gifts such as wireless mouse, wireless phone charger, wireless earpiece, portable charger, Starbucks gift card and more.

![](<.gitbook/assets/image (455).png>)

I completed 5 weeks of Quiz (launched on 1 Mar, 8 Mar, 15 Mar, 22 Mar & 30 Mar). This quiz aims to pique interest in Youths and equip them with knowledge on Cyber Security. It is supported by the Digital for Life Fund, an initiative by the Infocomm Media Development Authority (IMDA), that supports digital inclusion projects and activities to help all Singaporeans embrace digital, to enrich lives.

![](<.gitbook/assets/image (418).png>)

I completed 3 weeks of Quiz (launched on 5 May, 12 May, 19 May). This quiz aims to pique interest in Youths and equip them with knowledge on Cyber Security. It is supported by the Digital for Life Fund, an initiative by the Infocomm Media Development Authority (IMDA), that supports digital inclusion projects and activities to help all Singaporeans embrace digital, to enrich lives.

![](<.gitbook/assets/image (464).png>)

There were 8 Challenges in Cyber Wellness CTF - 2 Warmup and 6 Cryptography challenges. I participated solo in this CTF with my initials `glrz` and managed to solve all challenges. I got 1st place for this CTF, and first blooded all challenges. Later I realised I was the only one who participated in this CTF, which explains the position: 1/1.

![](<.gitbook/assets/image (449).png>)

![](<.gitbook/assets/image (495).png>)

The 2 fails in submitting the flag was due to copy pasting error.. If you realised I submitted the all the flags within 3 minutes and I accidentally submitted some flags to a different challenge.

![](<.gitbook/assets/image (416).png>)

Overall, this CTF was a good practice to refresh on basic concepts in cryptography and good practice for me to solve challenges faster.

## Scan It

![](<.gitbook/assets/image (447).png>)

This challenge includes a QR code in `flag.png` file.

![](<.gitbook/assets/image (470).png>)

We could just scan this QR code using a QR scanner application and we will get the flag

Alternatively, we could use a QR code/barcode scanner like `zbarimg` on Linux to get the flag. Check out [here](https://linuxgui.com/scan-barcode-qr-code-from-webcam-linux/) to install `zbarimg`.

![](<.gitbook/assets/image (426).png>)

Flag: flag{514c5c6bb335e4bb357e0e20d7554f58}

## Welcome!

![](<.gitbook/assets/image (414).png>)

This challenge basically describes what a CTF is and then gives us a "free" flag at the bottom

Flag: flag{ea85a6ae37d91a96b231932cfa3a0613}

## Mix & Match

![](<.gitbook/assets/image (413).png>)

For this challenge, we were given an encrypted flag as seen in the challenge description.

We could use an [online Base32 decode tool](https://emn178.github.io/online-tools/base32\_decode.html) to decrypt the encrypted flag. I assumed that it was Base32 from the challenge description and usually Base64 would have `=` or `==` at the end of the string, but this has `====`.

`JV5GW5KNGNTGUTCHK52UYSSEGFGEUQL2JQZFEMCNI5CXQTKROBVU2SS2NNGHUSBUJVKFMNCBNVJXUQKVGBMA====`

![](<.gitbook/assets/image (430).png>)

Then we get this string which looked like a shift of characters. I assumed it was ROT13 and we could decode it [here](https://rot13.com/)

`MzkuM3fjLGWuLJD1LJAzL2R0MGExMQpkMJZkLzH4MTV4AmSzAU0X`

![](<.gitbook/assets/image (454).png>)

Finally, we could Base64 decode this [here](https://www.base64decode.org/), which will give us the flag.

`ZmxhZ3swYTJhYWQ1YWNmY2E0ZTRkZDcxZWMxYmU4ZGI4NzFmNH0K`

![](<.gitbook/assets/image (461).png>)

Alternatively, I tried using a new tool [basecrack](https://github.com/mufeedvh/basecrack). This tool can help to determine the encoded base, so we do not need to guess what base its encoded in.

`-b` to decode a single encoded base from argument

![](<.gitbook/assets/image (494).png>)

After that, we could decode ROT13 [here](https://rot13.com/) and finally use `basecrack` again to decode the base64.

![](<.gitbook/assets/image (445).png>)

However, I think the above 2 solutions could be a bit time consuming. An easier alternative would be to just use [CyberChef](https://cyberchef.org/) . CyberChef is effective as it has this `magic wand` icon which will suggest to us what encryption it could be.

![](<.gitbook/assets/image (479).png>)

We could simply click this `magic wand` icon twice and we would get this  [recipe](https://cyberchef.org/#recipe=From\_Base32\('A-Z2-7%3D',false\)From\_Base64\('N-ZA-Mn-za-m0-9%2B/%3D',true,false\)\&input=SlY1R1c1S05HTlRHVVRDSEs1MlVZU1NFR0ZHRVVRTDJKUVpGRU1DTkk1Q1hRVEtST0JWVTJTUzJOTkdIVVNCVUpWS0ZNTkNCTlZKWFVRS1ZHQk1BPT09PQ), which gives us the flag in output.

![](<.gitbook/assets/image (457).png>)

Alternatively, you could also try out a tool like [Ciphey](https://github.com/Ciphey/Ciphey) which is easy to use.

Flag: flag{0a2aad5acfca4e4dd71ec1be8db871f4}

## Morse

![](<.gitbook/assets/image (420).png>)

In this challenge, we were given the encrypted flag with `- . /` symbols. I recognised this, this is morse code. The challenge also mentioned morse code which is a plain giveaway.

If you are interested in my other writeup on morse code challenge, check out [here](https://gadiel-lau.gitbook.io/2020-writeups/gsctf-2020#beeps).

Similar to other morse code challenges I solved, I used an online tool [here](https://morsecode.world/international/decoder/audio-decoder-adaptive.html) to analyze the morse code.

![](<.gitbook/assets/image (483).png>)

However, note that as mentioned before, this tool isn't accurate 100% of the time.

In this case we replace the `#`s with `{` and `}` respectively and we will get the flag.

Flag: flag{6a3e3b740bbb2f2cfc299a7bedb56b13}

## ROT13

![](<.gitbook/assets/image (434).png>)

In this challenge, we are given a flag encrypted in ROT13. We could decode it [here](https://rot13.com/) and get the flag.

Flag: flag{b0069821700f01de6685f7fc14440258}

## Base32

![](<.gitbook/assets/image (474).png>)

In this challenge, we are given a flag encoded in Base32. We could decode it using [CyberChef](https://cyberchef.org/).

![](<.gitbook/assets/image (486).png>)

Flag: flag{1399249f949585c7c6d3a6b59f9376e9}

## Base64

![](<.gitbook/assets/image (444).png>)

In this challenge, we are given a flag encoded in Base64. We could decode it using [CyberChef](https://cyberchef.org/).

Press this `magic wand` icon

![](<.gitbook/assets/image (439).png>)

We can now see the flag in output.

![](<.gitbook/assets/image (554) (1).png>)

Flag: flag{69cc4294c4986c901f053d364d822acb}

## Vigenère

![](<.gitbook/assets/image (575).png>)

This challenge mentions `Vigenère cipher` in the description, so we already know how it's encrypted. We have solved similar challenge before [here](https://gadiel-lau.gitbook.io/2020-writeups/brixel-ctf-winter-edition-2020/cryptography#merde).

We could use [CyberChef](https://cyberchef.org/) to decrypt this and get the flag.

![Vigenère cipher Key: key](<.gitbook/assets/image (538) (1).png>)

Flag: flag{357256db26aa89137e14fc6c46128031}
