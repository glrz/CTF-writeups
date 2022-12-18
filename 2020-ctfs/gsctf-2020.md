---
description: >-
  GSCTF 2020 is a beginner-friendly 48 hours CTF competition for people in the
  community to test their skills and learn more about concepts in Cybersecurity.
  It was held on 21 Nov - 23 Nov 2020.
---

# GSCTF 2020



I participated with my initials "RZ". I am pretty satisfied with the results, obtained 6th/30 in this CTF.&#x20;

![](<../.gitbook/assets/image (211).png>)

Most of the challenges were beginner-friendly, so it was perfect for someone like me with little cybersecurity or CTF experience.

3/8 Stego Challenges were solved

![](<../.gitbook/assets/image (92).png>)

1/2 Forensics challenge was solved

![](<../.gitbook/assets/image (77).png>)

3/3 Web challenges were solved

![](<../.gitbook/assets/image (59).png>)

7/11 Crypto challenges were solved

![](<../.gitbook/assets/image (34).png>)

1/4 Programming challenge was solved

![](<../.gitbook/assets/image (70).png>)

1/7 MISC challenge was solved

![](<../.gitbook/assets/image (20).png>)

0/2 RE challenge was solved

![](<../.gitbook/assets/image (37).png>)

1/6 OSINT challenge was solved

![](<../.gitbook/assets/image (72).png>)

1/1 Best challenge was solved

![](../.gitbook/assets/image.png)

The best challenge was just a survey feedback form.

Special thanks to the challenge creator for granting me access to the platform long after the competition and providing the challenge files to make this writeup possible.

## Oh gif

In this challenge, we are given a gif file that plays an animated gif at a very fast speed.

![](<../.gitbook/assets/image (107).png>)

We can use an online tool [here](https://ezgif.com/split/ezgif-1-b62335cd75.gif) to split it into frames.

After we split the frames, we can see that one of the frames contain the flag

![](<../.gitbook/assets/image (106).png>)

Alternatively, we could use [ffmpeg](https://ffmpeg.org/) to extract each frame from the gif file using the following command:

`ffmpeg -i flag.gif file%03d.png`

![](<../.gitbook/assets/image (126).png>)

`ffmpeg` is a very useful tool and can be used to convert audio files from `.mp4` to `.wav` as well.

If we run `ls` to check the contents extracted, we will see 28 frames extracted.

![](<../.gitbook/assets/image (134).png>)

To view the images, we could use the `eog` command to start the image viewer.

![](<../.gitbook/assets/image (148).png>)

To view the next image, click `->`

&#x20;

![](<../.gitbook/assets/image (166).png>)

We would find the flag in `file016.png`.

![](<../.gitbook/assets/image (164).png>)

We could also notice some blue words in the image and clicking to view the image would give us the flag.

![](<../.gitbook/assets/image (116).png>)

Another alternative is to use `stegoveritas` with the `-extract_frames` option to extract frames from `gif` and get the flag.

```
┌──(kali㉿kali)-[~/Desktop]
└─$ stegoveritas -extract_frames flag.gif 
Running Module: SVImage
+----------------+----------+
|  Image Format  |   Mode   |
+----------------+----------+
| Compuserve GIF | ColorMap |
+----------------+----------+
Running Module: MultiHandler
```

We could change directory to `results` and find the flag there.

![](<../.gitbook/assets/image (153).png>)

![](<../.gitbook/assets/image (140).png>)

Flag: FLAG{g1f\_3xpAnD3d}

## LSB 2

![](<../.gitbook/assets/image (258).png>)

For this challenge, we were given a picture of Marina Bay Sands.&#x20;

![](<../.gitbook/assets/image (168).png>)

Initially, I had no clue on how to find the flag with only an image given. But I recalled reading a book which talked about the concept of Steganography, that is concealing a message within another message or a physical object. In this case, the flag is probably hidden in this image.

I went on to do some research on tools that can solve steganography related challenges and I came across this tool called StegoVeritas which can be found[ here](https://github.com/bannsec/stegoVeritas). I proceeded to install it on my Kali Linux VM. If you are new to Linux, an installation video guide can be found[ here](https://www.youtube.com/watch?v=HLdEdU7qZ5M).

This tool is very easy to use. I just had to run the `stegoveritas` command with the PNG file

&#x20;  &#x20;

![](<../.gitbook/assets/image (202).png>)

![](<../.gitbook/assets/image (210).png>)

If we browse to the results directory, we can see one image with the flag

![](<../.gitbook/assets/image (170).png>)

![](<../.gitbook/assets/image (181).png>)

Alternatively, we could upload the image on [Aperi'Solve ](https://www.aperisolve.com/2a75f99358094d2c27604649750c3394)and we would get the flag.

![](<../.gitbook/assets/image (157).png>)

Flag : FLAG{1M4GE\_ST4CK}

## Where's the file

This challenge looks similar to the previous one, we were given an image only. Could it be steganography again?&#x20;

![](<../.gitbook/assets/image (231).png>)

_We are given this image of a dog_

![](<../.gitbook/assets/image (144).png>)

Let's see if StegoVeritas will work again

![Notice we found something with StegHide here](<../.gitbook/assets/image (213).png>)

![](<../.gitbook/assets/image (177).png>)

Indeed, stegoveritas worke_d_ again. Going to the directory, we can see the flag

![](<../.gitbook/assets/image (201).png>)

Flag : FLAG{f0und\__th3\_f1le_\__1n\_th3\_1mg}_

## _Imaging_

![](<../.gitbook/assets/image (204).png>)

What type of image could this be? I had no idea at first. Downloading the image file gives us a .ad1 file.&#x20;

{% file src="../.gitbook/assets/topsecretdisk (1).ad1" %}

This is my first time seeing such file format, so I went on to Google `how to open ad1 file` .  &#x20;

I found out that ad1 files are logical images, which contains the Forensic Toolkit Image data. To open this file, I downloaded FTK Imager from its official website [here](https://accessdata.com/product-download/ftk-imager-version-4-5).

After that, I opened up FTK Imager, go to File > Add Evidence Item

![](<../.gitbook/assets/image (154).png>)

_Select image file_

![](<../.gitbook/assets/image (111).png>)

_Open the file and press finish_

![](<../.gitbook/assets/image (232).png>)

_Here in the Evidence Tree section, we can expand it and see 3 different documents in it_

![](<../.gitbook/assets/image (261).png>)

_We navigate to the first file secret.txt and there's nothing there_

![](<../.gitbook/assets/image (251).png>)

_Next, we move on to the super\_secret.docx file and it looks like it's empty and has no readable data_

![](<../.gitbook/assets/image (205).png>)

_Finally, we go to the top\_secret.txt file and we get the flag._

![](<../.gitbook/assets/image (253).png>)

_Flag: FLAG{sT0r4gE\_f0r3nS1cs}_

## Directions

This challenge provided us with a link.

![](<../.gitbook/assets/image (124).png>)

If we go to the link, we can see this page.

![](<../.gitbook/assets/image (151).png>)

Lets change index to home and check the page

![](<../.gitbook/assets/image (169).png>)

Well, at this point I just change the path to /secret/flag.txt and got the flag. I guess I was lucky to find this one.

![](<../.gitbook/assets/image (173).png>)

Flag: FLAG{f0und\_th3\_d1r3ct0ry}

## _What a bot_

_In this challenge, we are given a link to join a discord server._

![](<../.gitbook/assets/image (265).png>)

After I joined the server, I noticed a Infosec Bot in the server. Reading the challenge description, it asked what functions does my bot have, followed by a new line and a `~` symbol.&#x20;

At this moment, I thought `~` could be the prefix for issuing commands to the bot.

So I ran the `~help` command in the server chat, and true enough the Infosec Bot responded with the possible commands.

![](<../.gitbook/assets/image (102).png>)

I ran the `~gimmetheflag` command on the server chat and after a few seconds the bot DM-ed me the flag.

![](<../.gitbook/assets/image (224).png>)

Flag: NYP{y0u\__b34t\_th3\__b0t}

## Crypto War

This challenge presents us with a flag in the challenge description which looks "encrypted" ?

![](<../.gitbook/assets/image (122).png>)

It mentioned something about Germans using cool machines. After a quick google search, we will find what is known as `Enigma Machine`.

Since it has 4 rotors, it is most probably using the `Enigma M4 "Shark"` Model. Putting the information into Cryptii [here](https://cryptii.com/pipes/enigma-machine), and we select `include` foreign character option, we get the flag.

![](<../.gitbook/assets/image (273).png>)

Flag: FLAG{w0rld\_w4r\_en1gma\_crypt0}

## Takeover

In this challenge we were given a link.

![](<../.gitbook/assets/image (269).png>)

Clicking into the link shows a page which tells us to `Look around!`, with the background changing color.

![](<../.gitbook/assets/image (278).png>)

Going to the `/robots.txt` path will show us something interesting. The _robots_._txt_ file tells search engine crawlers which URLs the crawler can access on your site. Here, we can see `/flag.html/` being disallowed.

![](<../.gitbook/assets/image (55).png>)

If we go to `/flag.html`, we get a pop up message which can be seen here

![](<../.gitbook/assets/image (49).png>)

After the page finish loading, we could see a bunch of text on the screen

![](<../.gitbook/assets/image (30).png>)

If I search for `NYP{`, there would be 520 possibilities for the flag which is completely insane.

![](<../.gitbook/assets/image (131).png>)

Looking again at the previous hint, it mentioned something about robot. If I search for `r0b0t`, I will easily find the flag.&#x20;

![](<../.gitbook/assets/image (43).png>)

Flag: NYP{r0b0ts\_ar3\_sc4ry}

## Consoling

In this challenge we are given a link.

![](<../.gitbook/assets/image (147).png>)

Clicking on the link brings us to this webpage&#x20;

![](<../.gitbook/assets/image (277).png>)

If we click on `Page with the fake flag`, it redirects us to a YouTube [site](https://www.youtube.com/watch?v=6n3pFFPSlW4).&#x20;

If we click on `Page with the flag`, it redirects us to another YouTube [site](https://www.youtube.com/watch?v=dQw4w9WgXcQ).

Finally, if we click on `Page with the real flag`, we see this webpage.

![](<../.gitbook/assets/image (66).png>)

Here I tried to inspect the code and found something interesting in `trash.js`

![](<../.gitbook/assets/image (62).png>)

I was stuck on this challenge for awhile and decided to use the hint.

![](<../.gitbook/assets/image (50).png>)

Taking a closer look on the javascript function in `trash.js`, I noticed there were 2 interesting functions here `getKey()` and `getFlag(passkey)`

![](<../.gitbook/assets/image (123).png>)

What if I could just call the javascript function getFlag(98D2B27) in the console?

![](<../.gitbook/assets/image (81).png>)

Indeed, that was it. Calling the function in the console gives us the flag.

![](<../.gitbook/assets/image (63).png>)

Flag: NYP{PC\_0r\_c0ns0le}

## Just Dance

In this challenge we were given a PNG image file.&#x20;

![](<../.gitbook/assets/image (91).png>)

For this challenge, we were given a `.png` file.

{% file src="../.gitbook/assets/flag.png" %}

![](<../.gitbook/assets/image (215).png>)

This looked like some traditional encryption method using dancing stickmen. A quick google search and I found out this is called `dancing men cipher`. To decode the message, we could go to google images to decode it manually.

![Dancing men cipher](<../.gitbook/assets/image (160).png>)

Alternatively, we could search for online tools to solve this.

Flag: FLAG{l3ts\__d4nc3\__m4n\_:)}

## 2x2x2x2x2x2

This challenge provided us to a TXT file.

![](<../.gitbook/assets/image (84).png>)

For this challenge, we were given a `.txt` file.

{% file src="../.gitbook/assets/flag (1).txt" %}

The challenge title is 2x2x2x2x2x2, which gives the result of 64. If I look at the challenge title, my initial thought would be that this txt file contains some text that is Base64 encoded.

Lets see if I am right

![](<../.gitbook/assets/image (61).png>)

Indeed, it looks like it is encoded in Base64. We can easily decode this [here ](https://cyberchef.org/#input=VTNWd1pYSWdZbUZ6YVdNZ09pa2dSa3hCUjN0aU5ITXhZMTlpTkhNelh6WTBmUT09)

![Click on the "magic tool button"](<../.gitbook/assets/image (280).png>)

And we will get the flag

![](<../.gitbook/assets/image (39).png>)

Flag: FLAG{b4s1c\_b4s3\_64}

## +13

This challenge provides us with a TXT file

![](<../.gitbook/assets/image (40).png>)

For this challenge, we were given a `.txt` file.

{% file src="../.gitbook/assets/flag.txt" %}

Based on the challenge description, it looks like there is a shift of 13 character, A will become N. This is ROT13. We can decode this[ here](https://cyberchef.org/#recipe=ROT13\(true,true,false,13\)\&input=U1lOVHtlMGc0Z3YwYV8xM30).

![](<../.gitbook/assets/image (270).png>)

Flag: FLAG{r0t4ti0n\_13}

## Lock and Key

![](<../.gitbook/assets/image (64).png>)

We are given a TXT file in the zip file. However, the TXT file is password protected.

{% file src="../.gitbook/assets/flag.zip" %}

![](<../.gitbook/assets/image (14).png>)

The challenge description mentioned something about ezkey. Could that be the password? lets try

![](<../.gitbook/assets/image (89).png>)

Indeed, that is the password. Opening up the txt file gives us the flag.

Flag: FLAG{f1le\_unl0ck3d}

## Hash Browns

![](<../.gitbook/assets/image (83).png>)

Looking at the challenge title, could it be hash? What are the common hash used? My first thought would be md5, and looking at the length of it, it makes sense. We could google md5 hash decrypt or decode and use an online tool to solve this

For me, I prefer to use this[ site](https://hashes.com/en/tools/hash\_identifier). This site determines the hash for me and gives the output.

![Output: ilovecats123](<../.gitbook/assets/image (10).png>)

Flag: FLAG{ilovecats123}

## Beeps

This challenge provided us with a .wav audio file.

![](<../.gitbook/assets/image (3).png>)

For this challenge, we were given a `.wav` file.

{% file src="../.gitbook/assets/audio.wav" %}

If I listen to the audio, it is just beeping sounds with slight pauses in between. What do these beeping mean? Well, after a quick google search, I found out this could be `morse code`.

Let's upload the file use this tool [here](https://morsecode.world/international/decoder/audio-decoder-adaptive.html) to analyze the morse code.

If I press the play button, it will start playing the audio and analyzing the morse code sounds

I realised this site is not accurate 100% of the time

![](<../.gitbook/assets/image (19).png>)

As we can see, it did not give the correct flag. But we could clear the message and try again.

Finally, we get the correct flag.

![](<../.gitbook/assets/image (33).png>)

Flag: NYP{MoRSECoD3}

## What file is this?

We are given a file with no file extension.

![](<../.gitbook/assets/image (52).png>)

For this challenge, we were given a `flag` file, with no file extension.

{% file src="../.gitbook/assets/flag" %}

If we open up the file in notepad or hex editor, we can see that it should be a PNG file

![](<../.gitbook/assets/image (44).png>)

Adding in the file extension .png will give us the flag

![](<../.gitbook/assets/image (5).png>)

Flag: FLAG{F1LE\_S1GN4TUR3S}

## Dictionary

Note: This challenge was not solved during the competition, I solved it after.

We are given a rockyou.txt.bz2 file from the link : [https://drive.google.com/file/d/1RG5oqrrMgWSp0VWuq61UU2H0ekyEIjrS/view?usp=sharing](https://drive.google.com/file/d/1RG5oqrrMgWSp0VWuq61UU2H0ekyEIjrS/view?usp=sharing)

and what seemed to look like hash value : `91d9ab9d5b731edebb5c1315bdee6e68` in the challenge description.

![](<../.gitbook/assets/image (26).png>)

First, let us save this hash value to a file

We could use a simple editor like vim.

Type the command `vi hash` in the terminal, press `i` to go into insert mode and paste the hash value in.

Next, we can press `esc` followed by `:wq` to write the changes and quit.

Now we can check the contents of the file using `cat` command

![](<../.gitbook/assets/image (80).png>)

We use the `file` command to check the file type of rockyou.txt.bz2

![](<../.gitbook/assets/image (73).png>)

We can use `--help` to see the options. To decompress the bzip2 file, we can use `-d` option.

![](<../.gitbook/assets/image (75).png>)

Now, the file is decompressed. We can try to use John The Ripper to crack the hash based on the wordlist provided.

If we analyze the hash [here](https://hashes.com/en/tools/hash\_identifier), it is MD5.

We can use the `--wordlist=rockyou.txt` option to perform a dictionary attack and `--format=Raw-MD5` to specify that the hash is MD5 format.

Within a few seconds, we get the flag.

![](<../.gitbook/assets/image (47).png>)

![](<../.gitbook/assets/image (8).png>)

Flag: FLAG{d1ct1on4ry\_4tt4ck}

## APK

![](<../.gitbook/assets/image (45).png>)

For this challenge, we were given an .apk file

{% file src="../.gitbook/assets/Infosec.apk" %}

&#x20;we can use an online tool [here ](http://www.javadecompilers.com/)to decompile the apk.&#x20;

If we check the files and go to `assets>www>img`, and go to the banner.png file, we can find the flag.

![](<../.gitbook/assets/image (97).png>)

Flag: NYP{Op3n\_th3\_aPk}
