---
description: LagNCrash Interpoly CTF 2022 is a CTF competition held from 23-25 March 2022
---

# LagNCrash Interpoly CTF 2022

This competition allowed up to 4 members to form a team but I participated solo in this CTF. This CTF competition is mainly for polytechnic students to pit against other polytechnic students from the various polytechnics. I participated in the Open category with the team name: Black Bolt as I was interested to broaden my knowledge in cybersecurity as well as gain more experience in CTF competitions.

![](<.gitbook/assets/image (344).png>)

Most of the challenges in this CTF are beginner-friendly and I managed to solve 9 challenges in this competition. Through this experience, I learned more about concepts of cryptography, forensics and cybersecurity in general.

Challenges I solved in the competition includes&#x20;

![](<.gitbook/assets/image (378).png>)

## CERTIFICATE OF PARTICIPATION

![](<.gitbook/assets/image (155).png>)

## Gold

![](<.gitbook/assets/image (358).png>)

For this challenge, we were given a `.txt` file

{% file src=".gitbook/assets/gold.txt" %}

A quick google search on "Golden bug cipher" and we will find `Gold Bug Cipher`.

We can decode it [here](https://www.dcode.fr/gold-bug-poe) to get the flag.

![](<.gitbook/assets/image (397).png>)

Flag: LNC2022{YAYGOLDCIPHERDECODED}

## Weak... R.essurection S.word A.ni-Mator

![](<.gitbook/assets/image (249).png>)

For this challenge, we were given a `values` file.

{% file src=".gitbook/assets/values" %}

This is quite similar to the [`Romeo Shane Arthur`](https://gadiel-lau.gitbook.io/2021-writeups/lagncrash-interpoly-ctf-2021#romeo-shane-arthur) challenge we did in the previous year's LagNCrash Interpoly CTF 2021.

First, we could download the RsaCtfTool. To download on Linux, we could follow the commands below

![](<.gitbook/assets/image (307).png>)

Then, we run the command `python3 RsaCtfTool.py -n (value) -e (value) --uncipher (value)`

And we will get the flag

![](<.gitbook/assets/image (275).png>)

Flag: LNC2022{D0u91As\_R4m5eyEARTH616}

## History is Important

![](<.gitbook/assets/image (329).png>)

The challenge mentioned about social media. Here, I guessed that it was Instagram and I was right.

I found his Instagram account [here](https://www.instagram.com/cyberxgunner/). If I go to his Instagram story/highlights, I would see that he posted a GitHub page.

![](<.gitbook/assets/image (302).png>)

![](<.gitbook/assets/image (207).png>)

Here we could see `https://github.com/cybe`

And in the final Instagram story, we could see his partial username `rxsaurus`.

![](<.gitbook/assets/image (305).png>)

If we combine both information, we would get [https://github.com/cyberxsaurus](https://github.com/cyberxsaurus), which is his GitHub.

Then, we click into his `superhero` repository, go to the [l0cation](https://github.com/cyberxsaurus/superhero/blob/main/l0cation) file and click on the history.

![](<.gitbook/assets/image (377).png>)

It will bring us to this page.

![](<.gitbook/assets/image (274).png>)

Clicking on [Update l0cation](https://github.com/cyberxsaurus/superhero/commit/8bb1bdb7ba2b11ed3e7f65c2dbb8246a0950db97) brings us to see the code where the flag was previously deleted.

![](<.gitbook/assets/image (237).png>)

Flag: LNC2022{Ih8HeR0E5}

## Plumber

![](<.gitbook/assets/image (308).png>)

For this challenge, using `grep` itself will not get us the flag.&#x20;

We need to add the `-a` option and specify the pattern(i.e. LNC)

![](<.gitbook/assets/image (273).png>)

Flag: LNC2022{w3lc0me\__t0\__th3\_aBy$s}

## Inverse Null

![](<.gitbook/assets/image (331).png>)

For this challenge, we are given a base64 encoded message in TXT file.&#x20;

{% file src=".gitbook/assets/inverse_null.txt" %}

We could decode the message [here](https://www.base64decode.org/). Decoding it would give us a conversation between John and Samuel. What looked really interesting was the portion I highlighted. It seemed to contain the flag with the `{ }` format.

![](<.gitbook/assets/image (304).png>)

If we refer back to the challenge title and search up null cipher, we would find that : in a null cipher, the [plaintext](https://en.wikipedia.org/wiki/Plaintext) is included within the [ciphertext](https://en.wikipedia.org/wiki/Ciphertext) and one needs to discard certain characters in order to decrypt the message (such as first letter, last letter, third letter of every second word, etc.)

This challenge is "Inverse Null", so could it be taking the last character of each word/digit?

If that is the case, then we shall take the last character of each word/digits from `Lol An Opportunistic 1222 1000 2212 4132 Person{ Is Solving This Easy Null Ctf Challenge}`

This would give us : `lnc2022{sgsylf}`. Take note the last part can be a little tricky, at first I thought it would take the last letter which is `e` but it's actually taking the last character `}`. Converting everything to caps will give us the flag.

Flag: LNC2022{SGSYLF}

## RiDdLe mE tHiS

![](<.gitbook/assets/image (251).png>)

In this challenge, we were given a .rar file.

We can use `binwalk` to extract a .txt file.

However, opening the .txt file would look like there is a shift in characters. We could decode that [here](https://rot13.com/).

![](<.gitbook/assets/image (250).png>)

I could not guess what this is. But it was actually `will`, the password to open the protected rar file. I had to brute force the password since I didn't get it from the decoded message.

Here, I used the command

`rar2john filename.rar > hash.txt` to save the hash output

`john filename.rar hashes.txt` to use John The Ripper to crack password

![Cracked password: will](<.gitbook/assets/image (292).png>)

Now, I used the password to `unrar e`, which would extract the rar file contents. However, the `are_u_the_night.rar` is password protected as well. Again, we follow the same steps above to crack the password.

![Cracked password: time](<.gitbook/assets/image (214).png>)

Now, for the last part, we had another rar file I\__AM\_BATMAN.rar which is password protected again. I tried to crack the password with similar steps above but after 4 hours + it was not able to crack. I decided to stop here. The intended solution was to perform dictionary attack I think._

![](<.gitbook/assets/image (387).png>)

Later, when I opened the hint, it became quite obvious for the 3rd password.

![](<.gitbook/assets/image (286).png>)

If we Google, we could find the Riddle [here](https://www.riddles.com/8026). The password was actually `question mark`.

![](<.gitbook/assets/image (338).png>)

This time if we extract the rar file and `cat` the contents of `REDACTED.txt`, we would get the flag.

![](<.gitbook/assets/image (239).png>)

Flag: LNC2022{GrEAteSt\_DeTecTiVe}

## fone

![](<.gitbook/assets/image (266).png>)

For this challenge, we are given a .wav file.&#x20;

{% file src=".gitbook/assets/Fone.wav" %}

If we listen to the audio, it plays an audio of the tones generated by a telephone when the numbers are pressed. I recognized this as DTMF tones as I had previously solved such challenges before. Previously I solved a challenge using Autopsy, Audacity and online DTMF decoder in this [writeup](https://gadiel-lau.gitbook.io/2020-writeups/brixel-ctf-winter-edition-2020/forensics#lost-evidence).&#x20;

Now, for this challenge, I would be trying a slightly different approach. I would download the DTMF decoder [here](https://github.com/ribt/dtmf-decoder) on my Linux and solve it there.

The command to run is very simple, just type `dtmf` followed by the wav file like this and we get the flag

![](<.gitbook/assets/image (318).png>)

Alternatively, we could use [multimon-ng](https://github.com/EliasOenal/multimon-ng)  to extract all the DTMF detected and get the corresponding numbers.

```
┌──(root㉿kali)-[/home/kali/Desktop]
└─# multimon-ng -a DTMF -t wav Fone.wav            
multimon-ng 1.1.9
  (C) 1996/1997 by Tom Sailer HB9JNX/AE4WA
  (C) 2012-2020 by Elias Oenal
Available demodulators: POCSAG512 POCSAG1200 POCSAG2400 FLEX EAS UFSK1200 CLIPFSK FMSFSK AFSK1200 AFSK2400 AFSK2400_2 AFSK2400_3 HAPN4800 FSK9600 DTMF ZVEI1 ZVEI2 ZVEI3 DZVEI PZVEI EEA EIA CCIR MORSE_CW DUMPCSV X10 SCOPE
Enabled demodulators: DTMF
DTMF: 7
DTMF: 6
DTMF: 3
DTMF: *
DTMF: 1
DTMF: 3
DTMF: 2
DTMF: A
DTMF: B
DTMF: D
DTMF: 3
DTMF: 2
DTMF: C
DTMF: 1
DTMF: 9
DTMF: 0
DTMF: #
DTMF: #
DTMF: 2
DTMF: 5
DTMF: 6
DTMF: 7
DTMF: 9
DTMF: 1
DTMF: A
```

If you run into some error when you try and start multimon-ng: _../unixinput.c: pa\_simple\_new() failed: Connection refused, m_ake sure you have the pulseaudio daemon started. Run the following command to start pulseaudio daemon

```
┌──(root㉿kali)-[/home/kali/Desktop]
└─# pulseaudio -D
```

Flag: LNC2022{763\*132ABD32C190##256791A}

## S3cretHERO

![](<.gitbook/assets/image (265) (1).png>)

In this challenge we are given a zip file. Inside the zip file is a JPG password protected file.

I ran `exiftool` and found the password here

![](<.gitbook/assets/image (254).png>)

If we use the password: i\__love_YUNOOOO, we would be able to extract the thor.jpg file.

![](<.gitbook/assets/image (240).png>)

We could extract the zip file now using `7z x` command. But there seems to be more hidden data in the jpg file extracted. We could use `binwalk` with `-e` option to extract the files. This would extract another empty file and zlib file from jpg file.

![](<.gitbook/assets/image (394).png>)

If we navigate to the extracted folder and use `strings` command on zlib file, it will give us the flag.

![](<.gitbook/assets/image (230).png>)

Check out my previous writeups [here](https://gadiel-lau.gitbook.io/2022-writeups/sg-cyber-olympian-trials-2022#hidden-file) and [here](https://gadiel-lau.gitbook.io/2020-writeups/brixel-ctf-winter-edition-2020/steganography#doc-ception), where I used `binwalk` to solve challenges.&#x20;

Flag: LNC2022{thor\_IShandsome}

## Around Singapore

![](<.gitbook/assets/image (349).png>)

For this challenge, we are giving a `.txt` file, an encoded message in binary.

{% file src=".gitbook/assets/message.txt" %}

First, we could convert the binary into Ascii text using an online converter tool [here](https://www.binaryhexconverter.com/binary-to-ascii-text-converter).

![](<.gitbook/assets/image (350).png>)

This would give us the encrypted flag. Looking at these "codes" in brackets, it looked really familiar and from the challenge title, could it be MRT stations code in Singapore?

If I search up the codes on Google, I would get

`Dakota Orchard Caldecott Tawas Oasis Redhill _ Fajar Xilin Tukang Expo Dover`

We apply our knowledge of null cipher, taking the first letter of each station, we get the flag.

Flag: LNC2022{doctor\_fxted}

## Lines, Lines, LINES

![](<.gitbook/assets/image (340).png>)

In this challenge, we were given a PNG image file.

![](<.gitbook/assets/image (284) (1).png>)

I am assuming this is some traditional cipher which I've never seen before. I searched [here](https://www.dcode.fr/symbols-ciphers) for ciphers using symbols and found that this is called `Ogham Alphabet`

![](<.gitbook/assets/image (276).png>)

I could decode that image [here](https://www.dcode.fr/ogham-alphabet) by just pressing the symbols which matches the symbol here. I decode every symbol from top to bottom.

![](<.gitbook/assets/image (270).png>)

I would get the output `NEERGNEGNaRO`. The text looks reversed and I could reverse it [here](https://www.textreverse.com/). This would give me the flag after converting all to lowercase.

Flag: LNC2022{orangengreen}

## Nothing Here

This challenge was not solved by any teams throughout the whole competition. I decided to include it in because I found it to be interesting.

![](<.gitbook/assets/image (290).png>)

In this challenge, we are given a .pcapng file. We could open `Wireshark` to analyze file.

![](<.gitbook/assets/image (205).png>)

We could go `File > Export Objects > HTTP`

![](<.gitbook/assets/image (355).png>)

Save this TXT file: `whodis.txt`

![](<.gitbook/assets/image (218) (1).png>)

Now, we go to `File > Export Objects > SMB`

![](<.gitbook/assets/image (368).png>)

And save these files as well

![](<.gitbook/assets/image (334).png>)

If we try to unzip the extracted `hidden.zip`, we cannot unzip the hidden.png contents, so maybe its password protected

![](<.gitbook/assets/image (373).png>)

Lets run `file` command to check, and indeed it is AES encrypted and requires password

![](<.gitbook/assets/image (282).png>)

We could try to brute force it using wordlist. The file `whodis.txt` extracted earlier might be useful.

Use `cat` just to check contents in `whodis.txt`

![](<.gitbook/assets/image (220).png>)

Here we use the commands to crack the zip file:

`zip2john filename.zip > file` to save the hashes into `file`

`john --wordlist=whodis.txt file` to use john the ripper to crack the password using `whodis.txt`

![](<.gitbook/assets/image (339).png>)

Now, we can see the password for hidden png file using `john --show file` command

![](<.gitbook/assets/image (351).png>)

We unzip the zip file using `7z x` and paste the password in

![](<.gitbook/assets/image (243).png>)

This would give us a `hidden.png` file. However, the file is corrupted.

Here, I used ghex - GNOME Hex editor for files, which can be downloaded [here](https://installati.one/kalilinux/ghex/) to analyze the data in the corrupted file.

We can see that it's starting with all 0s in the header data, which shouldn’t be the case

![](<.gitbook/assets/image (262).png>)

Let’s fix this by changing it to its correct values. The PNG file signature could be checked [here](https://www.w3.org/TR/PNG-Rationale.html#R.PNG-file-signature).

![](<.gitbook/assets/image (343).png>)

After fixing the data, we could press `CTRL+S` to save the data

![](<.gitbook/assets/image (233) (1).png>)

Now, if we open the PNG file, we get a fake flag in reverse base 64

![](<.gitbook/assets/image (228).png>)

Here, we could guess that the data in PNG could be reversed as well. If we use `hexdump` command on the `hidden.png` file , we can search for reverse order LNC (i.e. CNL)

![](<.gitbook/assets/image (363).png>)

Alternatively, we could run `strings` and `grep CNL`

![](<.gitbook/assets/image (325).png>)

This would give us the reverse order of flag

To reverse the flag, we go [here](https://www.textreverse.com/), paste the reversed flag in and click `Reverse Text` and we will get the flag.

![](<.gitbook/assets/image (327).png>)

Flag: LNC2022{y0u\__f0UnD\_m333\_50\_ea5iLy??$#!@}_

## _Extra_

_To recover 7z file, we could visit_ [_here_](https://www.7-zip.org/recover.html)_._

![Right side shows fixed file signature](<.gitbook/assets/image (389).png>)
