# Misc

## go n c

![](<../.gitbook/assets/image (735).png>)

This should be the easiest challenge out of all the other challenges. We are given the netcat command in the challenge description and we just need to copy paste that in our terminal which would give us the flag.

![](<../.gitbook/assets/image (939).png>)

Flag: CDDC22{S1mple\_Ch4113ng3\_just\_G0\_4nd\_S33}

## Copy n Paste

![](<../.gitbook/assets/image (725).png>)

For this challenge, we were given a `.svg` file.

{% file src="../.gitbook/assets/copy_n_paste.svg" %}

The animation was playing too fast but we could tell that there was likely a `Base64` data from the `==` appended at the end as padding.

<figure><img src="../.gitbook/assets/image (879).png" alt=""><figcaption></figcaption></figure>

First, if we do not know how to copy and paste this data from `.svg` file, we could Google search `Copy paste svg`

![](<../.gitbook/assets/image (948).png>)

Then, we could simply follow the instructions, right click the `SVG` tag, select `Copy` then select `copy outerHTML`

![](<../.gitbook/assets/image (789).png>)

Next, I paste it on Notepad and realised there were a bunch of unnecessary text and we need to clean them up

![](<../.gitbook/assets/image (996).png>)

I was manually cleaning up those text but I think there should be an easier way to clean up these

![](<../.gitbook/assets/image (991).png>)

I realised I could `CTRL+H` and replace these text that I don't need

![](<../.gitbook/assets/image (998).png>)

Next, I searched for the End of base64 string and deleted everything below it.

![](<../.gitbook/assets/image (815).png>)

After these cleaning up, I saw another common pattern to delete.

I went to [CyberChef ](https://cyberchef.org/)and selected `find and replace` operation:

![](<../.gitbook/assets/image (742).png>)

After some final clean up, I got the flag.

![](<../.gitbook/assets/image (750).png>)

Flag: CDDC22{S4V4G3\_LOVE}

## Invisible morse

![](<../.gitbook/assets/image (817).png>)

For this challenge, we are given a `blind_for_.-.txt` file in the zip file.

First, I opened this on [HxD](https://mh-nexus.de/en/hxd/). This seemed like a similar challenge that we had attempted before [here](https://gadiel-lau.gitbook.io/2022-writeups/nus-greyhats-grey-cat-the-flag-2022#ghost). However, its a little different.

![](<../.gitbook/assets/image (814).png>)

Next, I tried [stegsnow](https://manpages.ubuntu.com/manpages/bionic/man1/stegsnow.1.html) - whitespace steganography program. But as you can see, it didn't work as well or produce any useful output.

![](<../.gitbook/assets/image (918).png>)

There are a few steps we could take to solve this in [CyberChef](https://cyberchef.org/)&#x20;

1. Find `20` and replace with `.`
2. Find `09` and replace with `-`
3. Find `0A` and replace with `\n`
4. Find `` and replace with&#x20;
5. From Morse Code
6. Find `` and replace with&#x20;

4\. and 6. are replacing the space, basically deleting the space in between. Following these steps, we would get the flag from this [recipe](https://cyberchef.org/#recipe=Find\_/\_Replace\(%7B'option':'Regex','string':'20'%7D,'.',true,false,true,false\)Find\_/\_Replace\(%7B'option':'Regex','string':'09'%7D,'-',true,false,true,false\)Find\_/\_Replace\(%7B'option':'Regex','string':'0A'%7D,'%5C%5Cn',true,false,true,false\)Find\_/\_Replace\(%7B'option':'Regex','string':'%20'%7D,'',true,false,true,false\)From\_Morse\_Code\('Space','Line%20feed'\)Find\_/\_Replace\(%7B'option':'Regex','string':'%20'%7D,'',true,false,true,false\)\&input=MjAgMDkgMjAgMjAgMEEgMjAgMDkgMDkgMDkgMDkgMEEgMjAgMjAgMjAgMEEgMDkgMEEgMjAgMEEgMDkgMjAgMEEgMDkgMjAgMjAgMjAgMjAgMDkgMEEgMDkgMEEgMDkgMDkgMDkgMDkgMDkgMEEgMDkgMjAgMjAgMjAgMjAgMDkgMEEgMDkgMEEgMjAgMjAgMjAgMjAgMEEgMjAgMEEgMDkgMjAgMjAgMjAgMjAgMDkgMEEgMDkgMDkgMEEgMDkgMDkgMDkgMDkgMDkgMEEgMjAgMDkgMjAgMEEgMjAgMjAgMjAgMEEgMjAgMEEgMDkgMjAgMjAgMjAgMjAgMDkgMEEgMDkgMjAgMDkgMjAgMEEgMDkgMDkgMDkgMDkgMDkgMEEgMDkgMjAgMjAgMEEgMjAgMjAgMjAgMDkgMDkgMEEgMDkgMjAgMjAgMjAgMjAgMDkgMEEgMjAgMDkgMDkgMjAgMEEgMjAgMDkgMjAgMjAgMEEgMjAgMEEgMjAgMjAgMjAgMjAgMDkgMEEgMjAgMjAgMjAgMEEgMjAgMEE).

![](<../.gitbook/assets/image (728).png>)

CDDC22{L1STEN-T0-THE-M0RSE-C0D3-PLE4SE}

## PPS

![](<../.gitbook/assets/image (961).png>)

For this challenge, we were given a `dtmf.wav` file in the zip file.

We know what DTMF is from previous challenge solved [here ](https://gadiel-lau.gitbook.io/2022-writeups/lagncrash-interpoly-ctf-2022#fone)and [here](https://gadiel-lau.gitbook.io/2020-writeups/brixel-ctf-winter-edition-2020/forensics#lost-evidence).&#x20;

We could try to use [dtmf decoder](https://github.com/ribt/dtmf-decoder). However, the decoder I was using does not support mp3 format.

Thus I need to convert it to `.wav` file using `ffmpeg` command.

`ffmpeg -i DTMF.mp3 DTMP.wav`

![](<../.gitbook/assets/image (911).png>)

After it has converted to `DTMF.wav`, I proceed to run `dtmf` on the file

![](<../.gitbook/assets/image (787).png>)

At this point, I noticed there could be an extra `*` in front. We could also run with the `-v` option to analyze further.

![](<../.gitbook/assets/image (928).png>)

If we remove the extra `*` in front, we would get the 8 digit access password : `*38492751#`

Alternatively, we could use multimon-ng to get the flag.

```
┌──(root㉿kali)-[/home/kali/Desktop]
└─# multimon-ng -a DTMF -t wav DTMF.wav 
multimon-ng 1.1.9
  (C) 1996/1997 by Tom Sailer HB9JNX/AE4WA
  (C) 2012-2020 by Elias Oenal
Available demodulators: POCSAG512 POCSAG1200 POCSAG2400 FLEX EAS UFSK1200 CLIPFSK FMSFSK AFSK1200 AFSK2400 AFSK2400_2 AFSK2400_3 HAPN4800 FSK9600 DTMF ZVEI1 ZVEI2 ZVEI3 DZVEI PZVEI EEA EIA CCIR MORSE_CW DUMPCSV X10 SCOPE
Enabled demodulators: DTMF
DTMF: *
DTMF: 3
DTMF: 8
DTMF: 4
DTMF: 9
DTMF: 2
DTMF: 7
DTMF: 5
DTMF: 1
DTMF: #
```

Flag: CDDC22{\*38492751#}

## Hash Attack

![](<../.gitbook/assets/image (967).png>)

For this challenge, we were given a `hash.txt` in the zip file.

If we open the `hash.txt` file, we could see a bunch of hex data that looks hashed.&#x20;

At this point, I used a hint that helped me solve the challenge.

![](<../.gitbook/assets/image (806).png>)

I searched up and found that I could use the `fold` command to divide these characters.

Using the command

`fold -b64 input hash.txt`

I was able to divide these into 64 characters on each line. Then I copied the results.

I proceeded to my favourite website for [hash identifier](https://hashes.com/en/tools/hash\_identifier), pasted the results in and click `SUBMIT & IDENTIFY`

![](<../.gitbook/assets/image (983).png>)

Here we can see the flag.

![](<../.gitbook/assets/image (927).png>)

Flag: CDDC22{1\_Love\_you\_more\_than\_ever!}
