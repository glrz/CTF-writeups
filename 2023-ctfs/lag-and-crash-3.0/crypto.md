# Crypto

## Noise

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given two `.wav` files.

Upon initial analysis in `Audacity`, it seemed like it was `morse code` and it sounded like `morse code` too.

However, if we tried to run `multimon-ng` on it, we would get  gibberish.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ multimon-ng -a MORSE_CW -t wav message.wav     
multimon-ng 1.1.9
  (C) 1996/1997 by Tom Sailer HB9JNX/AE4WA
  (C) 2012-2020 by Elias Oenal
Available demodulators: POCSAG512 POCSAG1200 POCSAG2400 FLEX EAS UFSK1200 CLIPFSK FMSFSK AFSK1200 AFSK2400 AFSK2400_2 AFSK2400_3 HAPN4800 FSK9600 DTMF ZVEI1 ZVEI2 ZVEI3 DZVEI PZVEI EEA EIA CCIR MORSE_CW DUMPCSV X10 SCOPE
Enabled demodulators: MORSE_CW
BHEE I ITI<..._..>IST E IEST IEIISI IIISIN EIER E ET I II 4U5 T& EE EA NINEEE IEIIE EEET LEII E ESEEE LHE EEISHE EE <_......>TIEU XETSMEEHETH S E E IIEE NH I I E EI TE E EE EE IIE EUI IE<SN>EE EHE EA IIEEEM <SN>N E JETES S ET TNE T V5E E E EEI H ES IEI IIAAIER NI EE EE ET ET S U E IE EE I ETI EE EE EEE
```

This is because there was noise added to  the message and  the message could not be captured properly.

In audacity, I simply adjusted some of the `Stetrogram settings` to get a clearer view  of  the morse code.

<figure><img src="../../.gitbook/assets/image (95).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

As we already know, the short dashes represent `.` and longer dashes represents `-` in morse code. I then decoded it manually using [CyberChef](https://cyberchef.org/#recipe=From\_Morse\_Code\('Space','Line%20feed'\)\&input=Li0uLiAtLiAtLi0uIC4uLS0tIC0tLS0tIC4uLS0tIC4uLi0tIC4tLiAuLSAtLi4gLi4gLS0tIC4tLSAuLSAuLi4tIC4gLi4gLS4gLSAuIC4tLiAuLi0uIC4gLi0uIC4gLS4gLS4tLiAu).

The intended solution was probably to minus out the noise with the `noise.wav` file given. The solution would be something like [this](https://jason-kool.github.io/LNC2023/noise/).

Flag: LNC2023{RADIOWAVEINTERFERENCE}

## 2030

<figure><img src="../../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>

This was probably one of the harder crypto challenges (as compared to other challenges) which I solved.

For this challenge, we were given a `.jpg.enc` file.

{% file src="../../.gitbook/assets/flag.jpg.enc" %}

If we run `strings` on it and view the starting few lines, we would see a phrase : `thisiskeylol`

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ strings flag.jpg.enc | head             
ic!#0*omuhirirke
                o/tmjwmwh`}hkiqmote{lb~k`g
                                          aebfaytv}~
                                                    bt~`}i~thtNtnutlvlxr[HMrPtwlw
                                                                                 e:mjiqootg{ckgx~xjvwmwmu{grqrjvwmwmu{grqrjvwmwmu{grqrjvwmwmu{grqrjv
                                ibcaAk
                                      ouJiqxrhtx
                                                lohiphrjdxlolthisiskd{okiro
                                                                           idjdxmnlthisiskeylolujj
                                                                                                  sgfxlm|wxish
```

As I continued to view more parts of the strings in the file, I realized that this file  could be `xor` encrypted. I previously had the experience of solving a pretty similar challenge in [CSIT Challenge of Wits 2022](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/csit-challenge-of-wits-2022).

Alternatively, if we didnt catch the phrase using `strings`, we could also use an [online xor cracker](https://wiremask.eu/tools/xor-cracker/) which would suggest the possible key.

<figure><img src="../../.gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>

Using the key, we can decrypt it in [CyberChef](https://cyberchef.org/#recipe=XOR\(%7B'option':'UTF8','string':'thisiskeylol'%7D,'Standard',false\)). In the output, we can see `JFIF` which likely suggest that its a `.jpg` file obtained from the decrypted output.

<figure><img src="../../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>

We can save this file as `flag.jpg` and view it.

<figure><img src="../../.gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>

Nothing too interesting to see in the image. Although I did notice a word `PANDA` in the picture, that is not the flag.

If we looked up this image in hex editor, we would notice some trailing bytes `AAAA`. Alternatively, if we ran `stegoveritas`, it would discover the trailing bytes as well.

```
┌──(kali㉿kali)-[~/Downloads]
└─$ stegoveritas flag.jpg        
Running Module: SVImage
                       +------------------+------+
                                                  |   Image Format   | Mode |
                                                                             +------------------+------+
                                                                                                        | JPEG (ISO 10918) | RGB  |
               +------------------+------+
                                          Trailing Data Discovered... Saving
                                                                            b'\xaa\xaa\xaa\xaa'
```

<figure><img src="../../.gitbook/assets/image (6) (2).png" alt=""><figcaption></figcaption></figure>

However, this was just a red herring. To get the flag, we simply run `strings` and `grep` for the flag format.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ strings flag.jpg | grep LNC
6\6LNC2023{w45_x0r_fun?}
```

Flag: LNC2023{w45\_x0r\_fun?}

## Hope

<figure><img src="../../.gitbook/assets/image (97).png" alt=""><figcaption></figcaption></figure>

For this challenge, we are given a `.txt` file.

First, we can read the contents of the file.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ file message.txt 
message.txt: ASCII text, with CRLF line terminators
                                                                                                                   
┌──(kali㉿kali)-[~/Downloads]
└─$ cat message.txt     
.egassem detpyrcne eht eb ot smees txet dedocne noitacinummocelet .detcepxenu eht loof ot detpyrced ylisae eb nac ti taht os mhtirogla noitpyrcne kaew a gnisu eb ot demees yek ehT .rehpic noitutitsbus citebahplaylop fo tros emos gnisu si dna gnorts yrev ton si dohtem noitpyrcne eht taht smees tI

Encoded Key: 36f9a5900a637b0248cf7c8fe3af44ca
Encoded Message: ...- -.-- .. .. .. .-- -- .-.. .-- -..-
```

At first glance, the contents in the first line seemed to be reversed. The following line looked like some kind of hash and the final line looked like morse code.

We could reverse the text in the first line using [online text reverse](https://www.textreverse.com/).

This would produce the following message

```bash
It seems that the encryption method is not very strong and is using some sort of polyalphabetic substitution cipher. The key seemed to be using a weak encryption algorithm so that it can be easily decrypted to fool the unexpected. telecommunication encoded text seems to be the encrypted message
```

For the next one, we can crack the hash [here](https://crackstation.net/), which would give us the password: `SUPERKEY`.

<figure><img src="../../.gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>

For the final line, we could decode the morse code which gives us the output: `VYIIIWMLWX`.

Finally, since the message suggested that the encryption method is not very strong and is using some sort of polyalphabetic substituition cipher, we can try to decode the morse code output: `VYIIIWMLWX` using `Vigenere cipher` with the key obtained earlier on [CyberChef](https://cyberchef.org/#recipe=From\_Morse\_Code\('Space','Line%20feed'\)Vigen%C3%A8re\_Decode\('SUPERKEY'\)\&input=Li4uLSAtLi0tIC4uIC4uIC4uIC4tLSAtLSAuLS4uIC4tLSAtLi4t).

Flag: LNC2023{DETERMINED}

## Zig Zag

<figure><img src="../../.gitbook/assets/image (4) (1) (5).png" alt=""><figcaption></figcaption></figure>

As the challenge name suggested, this is Rail fence (zigzag) Cipher.

We can decode the encoded string given on [CyberChef](https://cyberchef.org/#recipe=Rail\_Fence\_Cipher\_Decode\(3,3\)\&input=TjJJU1RWU0xDMDNIU0FRSUVCSVUyVFdVT08).

Flag: LNC2023{thiswasquiteobvious}

## Ancient Pokémon

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.png` image file.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ file Ancient_Pokemon.png 
Ancient_Pokemon.png: PNG image data, 600 x 531, 8-bit/color RGBA, non-interlaced
```

First, I opened this image in image viewer.

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

This looked like some kind of symbol cipher. We could search it up on [dcode](https://www.dcode.fr/symbols-ciphers) and we would find that this is `Pokemon unown alphabet`. We could also infer from the challenge description which mentioned `Unown`.

We could then decode these characters manually [here](https://www.dcode.fr/pokemon-unown-alphabet), which gives us the following output

```bash
PVBRHVRTSG LUUHVGRHHRCGVVM SHOULD I JUMP OVER THIS RAIL FENCE? IT HAS VEEIHRWTYAEBNBETOSTT WRITTEN ALL OVER IT
```

Here, I noticed two pieces of key information. First, it mentioned about rail fence, which likely suggested that this could be rail fence cipher encoded. Second, It mentioned that it has `VEEIHRWTYAEBNBETOSTT` written all over it.

&#x20;For the first part of the string: `PVBRHVRTSG LUUHVGRHHRCGVVM`, I'm not too sure what that was, maybe that was just a red herring and I guess the `JUMP OVER THIS` implied that we could ignore that.

Hence, I copied pasted `VEEIHRWTYAEBNBETOSTT` into [CyberChef](https://cyberchef.org/#recipe=Rail\_Fence\_Cipher\_Decode\(8,2\)\&input=dmVlaWhyd3R5YWVibmJldG9zdHQ) and decoded the rail fence cipher with key: `8`, offset: `2`, which gave me the flag.

Flag: LNC2023{iwanttobetheverybest}

## You Don't Know About Us

<figure><img src="../../.gitbook/assets/image (7) (6).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given this encoded string in the challenge description.

> JZUWGZJAORZHSIDIOVWWC3RBEBKGQ2LTEBUXGIDUNBSSAYLDOR2WC3BAMVXGG33EMVSCA3LFONZWC43HMU5AUQSEKMZDAMRTPN2GWY3SORVWG4T5

We can copy paste this into CyberChef which would suggest that it's `Base32` encoded.

<figure><img src="../../.gitbook/assets/image (5) (2).png" alt=""><figcaption></figcaption></figure>

We can decode it as `Base32` on [CyberChef ](https://cyberchef.org/#recipe=From\_Base32\('A-Z2-7%3D',false\)\&input=SlpVV0daSkFPUlpIU0lESU9WV1dDM1JCRUJLR1EyTFRFQlVYR0lEVU5CU1NBWUxET1IyV0MzQkFNVlhHRzMzRU1WU0NBM0xGT05aV0M0M0hNVTVBVVFTRUtNWkRBTVJUUE4yR1dZM1NPUlZXRzRUNQ)and we would get what seemed like the flag, but with a shift of characters.

<figure><img src="../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

Finally, we could add `ROT13 Brute Force` to the [CyberChef recipe](https://cyberchef.org/#recipe=From\_Base32\('A-Z2-7%3D',false\)ROT13\_Brute\_Force\(true,true,false,100,0,true,''\)\&input=SlpVV0daSkFPUlpIU0lESU9WV1dDM1JCRUJLR1EyTFRFQlVYR0lEVU5CU1NBWUxET1IyV0MzQkFNVlhHRzMzRU1WU0NBM0xGT05aV0M0M0hNVTVBVVFTRUtNWkRBTVJUUE4yR1dZM1NPUlZXRzRUNQ), which will give us the flag.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Flag: LNC2023{dumbdumb}

## Multilinguistic

<figure><img src="../../.gitbook/assets/image (29) (3).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.zip` file. Note that I solved this shortly after the competition.

First, we could verify the zip file and unzip it to see its contents.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ file Secret.zip 
Secret.zip: Zip archive data, at least v2.0 to extract, compression method=deflate
                                                                                                                   
┌──(kali㉿kali)-[~/Downloads]
└─$ 7z x Secret.zip 

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 95533 bytes (94 KiB)

Extracting archive: Secret.zip
--
Path = Secret.zip
Type = zip
Physical Size = 95533

Everything is Ok

Files: 2
Size:       95388
Compressed: 95533
```

Once we unzipped it, we have a new directory: `zomb-phish`. Lets go into the directory and check its contents.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cd zomb-phish 
                                                                                                                   
┌──(kali㉿kali)-[~/Downloads/zomb-phish]
└─$ ls
blublub.txt
```

We can see a `.txt` file, lets read its contents.

```bash
┌──(kali㉿kali)-[~/Downloads/zomb-phish]
└─$ cat blublub.txt 
iisiiiisiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiioddddddddoiiiiiiiiiiiiioddddddoiiioddddddddddddoiiiioiiiiiiiiodddddddddddddoiiiiiiiiiioiiiiiiiiiodddddddddddddddddddo                     
```

We are presented with a string, but what could this be? If we refer back to the challenge description and directory name, it mentioned Zomb-phish. This is actually referring to the `Deadfish language`.

We could decode this in [dCode](https://www.dcode.fr/deadfish-language).

This gives us the output: merlocgoblub which is also the password for the next zip file.

<figure><img src="../../.gitbook/assets/image (80) (2).png" alt=""><figcaption></figcaption></figure>

If we run `ls` with the `-la` option we can see the zip file `.-.7z`

We could unzip it using the password obtained earlier

```bash
┌──(kali㉿kali)-[~/Downloads/zomb-phish]
└─$ ls -la
total 176
drwx------ 2 kali kali  4096 Apr 26 06:17 .
drwxr-xr-x 6 kali kali 69632 Apr 26 06:17 ..
-rw-r--r-- 1 kali kali 95218 Nov  1 12:38 .-.7z
-rw-r--r-- 1 kali kali   170 Nov  1 12:35 blublub.txt
                                                                                                                   
┌──(kali㉿kali)-[~/Downloads/zomb-phish]
└─$ 7z x .-.7z     

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 95218 bytes (93 KiB)

Extracting archive: .-.7z
--
Path = .-.7z
Type = 7z
Physical Size = 95218
Headers Size = 226
Method = LZMA2:17 7zAES
Solid = +
Blocks = 1

    
Enter password (will not be echoed):
Everything is Ok    

Folders: 1
Files: 2
Size:       100962
Compressed: 95218
```

Now we could navigate into the new directory `.-` and see its contents. We would find a `.txt` and `.7z` file in there.

```bash
┌──(kali㉿kali)-[~/Downloads/zomb-phish]
└─$ ls -la
total 180
drwx------ 3 kali kali  4096 Apr 26 06:19 .
drwx------ 2 kali kali  4096 Nov  1 00:37 .-
drwxr-xr-x 6 kali kali 69632 Apr 26 06:17 ..
-rw-r--r-- 1 kali kali 95218 Nov  1 12:38 .-.7z
-rw-r--r-- 1 kali kali   170 Nov  1 12:35 blublub.txt
                                                                                                                   
┌──(kali㉿kali)-[~/Downloads/zomb-phish]
└─$ cd .-          
                                                                                                                   
┌──(kali㉿kali)-[~/Downloads/zomb-phish/.-]
└─$ ls    
 dido.txt  'd@n(e.7z'
```

Lets check out the `.txt` content

```bash
┌──(kali㉿kali)-[~/Downloads/zomb-phish/.-]
└─$ cat dido.txt   
- .... . / ... -.-.{ .-. --- .-.. .-.. / --- ..-. / --- .-. .. --. .. -. / -- --- .-. ... . / -.-. --- -.. . / .. ... / .- / -- . - .... --- -.. / ..- ... . -.. / .. -. / - . .-.. . -.-. --- -- -- ..- -. .. -.-. .- - .. --- -. / - --- / . -. -.-. --- -.{. . / - . -..- - / -.-. .... .- .-. .- -.-. - . .-. ... / .- ... / ... - .- -. -.. .- .-. -.. .. --.. . -.. / ... . –{.- ..- . -. -.-. . ... / --- ..-. / - .-- --- / -.. .. ..-. ..-. . .-. . -. - / ... .. --. -. .- .-.. / -.. ..- .-. .- - .. --- -. ... --..-- / -.-. .- .-.. .-.. . -.. / -.. --- - ... / .- -. -.. / -.. .- ..{. .... . ... --..-- / --- .-. / -.. .. - ... / .- -. -.. {/ -.. .- .... ... .-.-.- / -- --- .-. ... . / -.-. --- -.. . / .. ... / -. .- -- . -.. / .- ..-. - .] .-. / ... .- -- ..- . .-.. / -- --- .-. ... .] --..-- / --- -. ]{. / --- ..-. / -] .... . / .. -]. ...- . -. - --- .-. ... / -]-- ..-. / - .]... . / - . .]-.. . --. .-. .]- .--. ...]. .-.-.- / .. -. - . .-. -. .]- - .. --- -. .- .-.. / -- --- .-. ... . / -.-. -]-- -.. . / . -. -.-. ---{ -].. . ...] / - .... . / ..--- -.]... / -... .- ... .. -.-. / .-..] .- - .. -. / .-.. . - - . .-]. ... / .- / - .... .{-. --- ..- --. ].... / --.. --..-- / --- -. . / .- ]-.-. -.-. . -.] - . -.. / .-.. {.- - .]. -. / .-.. . - - . .-. / -.--. . -.--.- ]--..-- / - .... . / .- .-. ].- -... .. -.-. / -. ..-] -- . .-. .- .-.. ... -]-..-- / .- -. -.. / .- / ... -- ].- .-.. .-.. / ... . - / --- ..-.] / .—{. ..- -. -.-. - ..- .- - .. --- -. / .- {-. -.. / .--. .-. --- -.-. . -.. ..- .-. .- .-.. /] ...{ .. --. -. .- .-.. ... / -.--. .--. .-. --]- ... .. --. -. ... -.--.- .-.-.- / - .... . .-. .{ / .. ..]. / -. --- / -.. .. ... - .. -. -.-. - .. --- -. / -..]. . - .-- .{ . -. / ..- .--. .--. . .-. / .- -. -.. / .-..] --- .-- . .-. / -.-. .{- ... . / .]-.. . - - . .-. ... .-.-.- / . ].- -.-. .... / -- --{- .-. ... . / -.-. --- ]-.. . / ... -.-- -- -... --- .-.. / .. ... / ..-. --- ].-. -- . {-.. / -... -.-- / .- / ... . --.- ..- . -. -.-. . / --{- ..-. ]/ -.. .. - ... / .- -. -.. / -.. .- .... ]... .-.-.- / - .... . / -.. .. - / {-.. ..- .-]. .- - .. --- -. / .. ... / - .... . / -... .- ... .. -.-. / ..- -. .]. - / --- ..-. / - .. -- . / -- . .- ..{]. ..- .-. . -- . -. - / .. -. / -- -]-- .-. ... . / -.-. --- -.. . / - .-. .- -. ...{ -- .. ... ... .. --- -. .-.-].- / - .... . / -.. ..- .-. .- - .. –- -. / --- ..-. / .- / -.. .- .... / .. ... / - .... .-. . . / - ].. -- . ... / - .... . / -.. ..- .-. .- {- .. --- -. / --- ..-. / .- / -.. .. - .-.-.- / . .- -.-]. .... / -{.. .. - / --- .-. / -.. .- .... / .-- .. - .... .. -. / .- -. / . -. -.-. --- -.. . -..] / -.-. .... .{- .-. .- -.-. - . .-. / .. ... / ..-. --- .-.{. .-.. --- .-- . -.. / -... -.-- / .- / .--. . .-. .. --- -.. / {-]-- ..-. / ... .. --. -. .- .-.. / .- -... ... . -. -.-. . --..-- / -.-. .- .-.. .-.. . -.. / .- / ... .—{. ].- -.-. . --..-- / . --.- ..- .- .-.. / - --- / - .... . / -.. .. - / -.. ..- .-. .- - {.. --- -. .-.-.- / - .... . / .-.. . - ]- . .-. ... / --- ..-.{ / .- / .-- --- .-. -.. / .- .-. . / ... . ].--. .- .-. .- - . -.. / -.{.. -.-- / .- / ... .--. .- -.-. . / --- ..-. / -.. ..- .-. .- - .. --- -. / . --.- ..- .- .-.. / - --- / - .]... .-. . . / -.. .. {- ... --..-- / .- -. -.. / .-- --- .-. -.. ... / .- .-. .] / ... {. .--. .- .-. .- - . -.. / -... -.-- / .- / ... .--. .- -.-. . / . --.- .].- .- .-.. / - --- /{ ... . ...- . -. / -.. .. - ... .-.-.- / ..- -. - .. .-.. /{ .---- ----. ....- ----.] --..-- / .-- --- .-. -.. ... / .-- . .-. . / ...{ . .--. .- .-. .- - . -.. / -... -.-- / .- / ... .-{-. .- -.-. . / . --.- ]..- .- .-.. / - --- / ..-. .. ...- . / -.. .. - ... .-.-.- / -- --- {.-. ... . / -.-. --- -.. . / -.-. .- -. / -... . / -- ].{ -- --- .-. .. --.. . -.. / .- -. -.. / ... . -. - / .. -. / .- / ..-. --- .-]. -- / .--. . .-{. -.-. . .--. - ..] -... .-.. . / - --- / - {.... . / .... ..- -- .- -. / ... . -. ... . ... --..-- / . .-.-.- --. .-.-.]- / ...- .. .- / ... --- ..- -. -.. /{ .-- .- ...- . ... / --- .-. / ...{- .. ... .. -... .-.. . / .-.. .. --. ].... - --..-- / ... ..- -.-. .... / - .... .- - / .. - / -.-. .- {-. / -... . / -.. .. .-. . -.-. - .-.. -.-- / .. -. - . .-. .--. .]-. . –{ . -.. / -... -.-- / .--. . .-. ... --- -. ... / - .-. .- .. -. . -.. / .. -. / - .... . / ... -.- .. .{-.. ].-.. .-.-.- / -- --- .-. ... . / -.-{. -]-- -.. . / .. ... / ..- ... ..- .- .-.. .-.. ]-.-- / - .-. .- -. ... -- .. - - . -.. / -... -.-- / ]--- -. {-....- --- ..-. ..-. / -.- . -.-- .. -. --. / --- ..-. / .- -. /{ .. -. ..-. --- .-. -- .- - .. --- -. -...].- -.-. .- .-. .-. -.-- .. -. --. / -- . -.. .. ..- -- / ... ..{- -.-. .... / .- ... / . .-.. . -.-. - .-. .. -.-. /{ -.-. ..- .-. .-. . -. - --]..-- / .-. .- -.. .. --- / .-- .- ...- . ... --..{-- / ...- .. ... .. -... .-.. . / .-.. .. --. .... - --..-- / --- .-. / ... --- ..- -. -.. /] .-- .- ...- . ... .-.-.- / - .... . / -.-.{ ..- .-. .-. . -. - / --- .-. / .-- .- ...- . / .. ... / {.--. .-. . ... . -.] - / -.. ..- .-. .. -. --. / - .... . / - .. -- . / .--. . .-. .. --- -.. / ---{ ..-. / - .... . / -.. .. - / --- .-. / -.. .- ..{.. / .- -. -.. / .- -... ]... . -. - / -.. ..- .-. .. -. --. / - .... . / - .. –{- . / -... . - .-- . . -. / -.. .. - ... / .- -. -.. / -.. .- {.... ... .-.-.- / ... .. -. -.-. . / -- .- -. -.-- / -. .- - ..- .-. .- .-.. / .-.. .- -. --. ..- .- --. . ]..{. / ..- ... . / -- --- .-. . / - .... .- -. / - .... . / ..{--- -.... / .-.. . - - .] .-. ... / --- ..-. / - .... . / .-.{. .- - .. -. / .- .-.. .--. .... .- -... . - --{..-- / -- --- .-. .].. . / .- .-.. .--. .... .- -... . - ... / .... .- ...- . / -... . . -. / -.. . ...- . .-.. --- .--. {. -.. / ..-. --- .-. / - .... –{-- ... . / .-].. .- -. --. ..- .- --. . ... --..-- / .-.. .- .-. --. . .-.. -.-- / -... -.-- / - .-. .-{ -. ... .-.. .. - . .-. .- - .. ---{ -. / --- ..-. / . -..]- .. ... - .. -. --. / -.-. --- -.. . ... .-.-.- / - --- / .. -. -.-. .-. . .- ... . / - .... . / . ..-. .{.-. .. -.-. .. . -. -.-. -.-- /] --- ..-. / . -.[ -.-. --- -.. .. -. --. --..-- / -- --- .-. ... . / -.-. --- -.. . / .-- .- ... / -.. . ... .. --. -. .] -.. / ... –{- / - .... .- - / - .... . / .-.. . -. --. - ....{ / --- ..-. / . .- -.-. ...]. / ... -.-- -- -... --- .-.. / .. ... / .- .--. .--. .-. --- -..- .. –{ .- - . .-.. -.-- / .. -. ...- . .-.{ ... . / - --- / - .... . / ..-. ].-. . --.- ..- . -. -.-. -.-- / --- ..-. / --- -.-. -.-. ..{- .-. .-. . ]-. -.-. . / --- ..-. / - .... . / -.-{. .... .- .-. .- -.-. - . .-. / - .... .- - / .. - / .-. . .--. .-. . ... . {-. - ... / .. -. / - ]. -..- - / --- ..-. / - .... . / . -. --. .-.. .. ... .... / .-.. .- -{. --. ..- .- --. . .-.-.- / - .... ..- ...] / - .... . / -- --- ... - / -.-. --- -- -- --- -. / .-.. . - - . .-. / .. -. / {. -. --. .-.. .. ... .... --..-- /] - .... . / .-.. . - - . .-. / . --..-- / .... .- ... / - ....{ . / ... .... --- .-. - . ... - / -.-. --- -.. . ---... / .- / ... .. -. --. .{-.. . /] -.. .. - .-.-.- / -... . -.-. .- ..- ... . / - .... . / -- --- .-. ... . / -.-. {--- -.. . / . .-.. . -- . -. - ... / .- .-. . ]/ ... .--. . -.-. {.. ..-. .. . -.. / -... -.-- / .--. .-. --- .--. --- .-. - .. --- -. / .-. .- - .... . .-{. / ]- .... .- -. / ... .--. . -.-. .. ..-. .. -.-. / - .. -- . / -.. ..- .-. .- - .. --- -. ... --..-- / - .... . / -.-. --- -.]. . / .. ... / ..- ... ..- {.- .-.. .-.. -.-- / - .-. .- -. ... -- .. - - . -.. / .- - / - .... . / .... .. –{-. .... . ... - / .-. .- - . / - .... .- - / - ].... . / .-. . -.-. . {.. ...- . .-. / .. ... / -.-. .- .--. .- -... .-.. . / ---{ ..-. / -.. . -.-. ---] -.. .. -. --. .-.-.- / -- --- .-. ... . / -.-. {--- -.. . / - .-. .- -. ... -- .. ... ... .. --- -. / .-. .- - . / -.--. ... .--. . . -.. -.--.- / .. ... / ... .--. .{ -.-. .. ..-. .. . -.. / .. -. / -]-. .-. --- ..- .--. ... /{ .--. . .-. / -- .. -. ..- - . --..-- / -.-. --- -- -- --- -. .-.. -.-- / .-. . ..-. . .-. .]-. . -.. / - --- / .- ... / .-- --- .-. -.. .{.. / .--. . .-. / -- .. -. ..- - . .-.-.- / - .... . ... . / .. -. ..-. --- .-. -- .- - ..] --- -. / .- .-. . / -. --- - / ..- ..{. . ..-. ..- .-.. .-.. .-.-.- / - .... . / .--. .- ... ...[ .-- --- .-. -.. / .. ... ---... ]/ -.. .. -.. .- .... -.. .. -.. .. -.. .- .... -.. .. -.. .- .... -.. .. -.. .- .... -.. ..           
```

This looked like `Morse Code` and we could decode it using CyberChef which would give us the password if we scroll down to the bottom of the decoded output

<figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption><p>Password: DIDAHDIDIDAHDIDAHDIDAHDI</p></figcaption></figure>

Lets use this password to unzip the `d@n(e.7z`

```bash
┌──(kali㉿kali)-[~/Downloads/zomb-phish/.-]
└─$ 7z x d@n\(e.7z 

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 92743 bytes (91 KiB)

Extracting archive: d@n(e.7z
--
Path = d@n(e.7z
Type = 7z
Physical Size = 92743
Headers Size = 231
Method = LZMA2:96k 7zAES
Solid = +
Blocks = 1

    
Enter password (will not be echoed):
Everything is Ok        

Folders: 1
Files: 2
Size:       93501
Compressed: 92743
```

Similarly, we would go into the new directory extracted, and check its contents.

```bash
┌──(kali㉿kali)-[~/Downloads/zomb-phish/.-]
└─$ cd d@n\(e 
                                                                                                                   
┌──(kali㉿kali)-[~/Downloads/zomb-phish/.-/d@n(e]
└─$ ls    
colour.7z  Runes.png
```

We could see a `.png` file so lets try to view it in image viewer.

```bash
┌──(kali㉿kali)-[~/Downloads/zomb-phish/.-/d@n(e]
└─$ eog Runes.png
```

<figure><img src="../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

Of course, I quickly recognised this as `dancing men cipher` because I've solved a challenge on this in [GSCTF 2020](https://gadiel-lau.gitbook.io/2020-writeups-1/2020-ctfs/gsctf-2020#just-dance).

I decoded it manually in dCode which gave me the following output

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

Removed the new line to get the whole passphrase

<figure><img src="../../.gitbook/assets/image (25) (4) (1).png" alt=""><figcaption></figcaption></figure>

The password is : `wewillmakethemgetschwifty` and we can use this to unzip our next zip file.

Similarly, I'll check its contents. We can find a `.7z` and `.docx` file in the directory.

```bash
┌──(kali㉿kali)-[~/Downloads/zomb-phish/.-/d@n(e]
└─$ 7z x colour.7z 

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 17854 bytes (18 KiB)

Extracting archive: colour.7z
--
Path = colour.7z
Type = 7z
Physical Size = 17854
Headers Size = 238
Method = LZMA2:24k 7zAES
Solid = +
Blocks = 1

    
Enter password (will not be echoed):
Everything is Ok        

Folders: 1
Files: 2
Size:       22372
Compressed: 17854
┌──(kali㉿kali)-[~/Downloads/zomb-phish/.-/d@n(e]
└─$ cd colour 
                                                                                                                   
┌──(kali㉿kali)-[~/…/zomb-phish/.-/d@n(e/colour]
└─$ ls 
final.7z  RGB.docx
```

A `.docx` file is like a zip file, so we could unzip it and check its contents.

```bash
┌──(kali㉿kali)-[~/…/zomb-phish/.-/d@n(e/colour]
└─$ 7z x RGB.docx 

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 22046 bytes (22 KiB)

Extracting archive: RGB.docx
--
Path = RGB.docx
Type = zip
Physical Size = 22046

Everything is Ok

Files: 24
Size:       88346
Compressed: 22046

┌──(kali㉿kali)-[~/…/.-/d@n(e/colour/word]
└─$ ls
document.xml  fontTable.xml  media  _rels  settings.xml  styles.xml  theme  webSettings.xml
```

If we explored the `/word/media` directory, we would find a bunch of `.png` images.

```bash
┌──(kali㉿kali)-[~/…/.-/d@n(e/colour/word]
└─$ cd media 
                                                                                                                   
┌──(kali㉿kali)-[~/…/d@n(e/colour/word/media]
└─$ ls
image10.png  image12.png  image1.png  image3.png  image5.png  image7.png  image9.png
image11.png  image13.png  image2.png  image4.png  image6.png  image8.png
```

If we open up one of these images, we would see this

<figure><img src="../../.gitbook/assets/image (27) (3) (2).png" alt=""><figcaption></figcaption></figure>

The other images are similar and they are actually `hexahue`

We could decode the `hexahue` in [dCode](https://www.dcode.fr/hexahue-cipher), which will give us the password for the final zip file.

However, I'm not too sure why for some reason there was only 13 png images found in `/word/media`. By right, there should be 21 images.

If we just open it as a Word document, we will be able to see the full hexahue.

<figure><img src="../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

We could decode this manually, but an easier way would be to copy and paste it into the decoder, that is, to `CTRL+A` on the word documents and `CTRL+C` to copy and `CTRL+V` to paste on [dCode](https://www.dcode.fr/hexahue-cipher).

<figure><img src="../../.gitbook/assets/image (65) (2).png" alt=""><figcaption></figcaption></figure>

The  password is : `W3WILL7URN7H3MR4INB0W`.

Finally, we could use this password to go into the extracted directory and read the flag.

```bash
┌──(kali㉿kali)-[~/…/zomb-phish/.-/d@n(e/colour]
└─$ 7z x final.7z

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 326 bytes (1 KiB)

Extracting archive: final.7z
--
Path = final.7z
Type = 7z
Physical Size = 326
Headers Size = 198
Method = LZMA2:12 7zAES
Solid = -
Blocks = 1

    
Enter password (will not be echoed):
Everything is Ok       

Folders: 1
Files: 1
Size:       123
Compressed: 326
                                                                                                                   
┌──(kali㉿kali)-[~/…/zomb-phish/.-/d@n(e/colour]
└─$ ls
'[Content_Types].xml'   docProps   final   final.7z   _rels   RGB.docx   word
                                                                                                                   
┌──(kali㉿kali)-[~/…/zomb-phish/.-/d@n(e/colour]
└─$ cd final 
                                                                                                                   
┌──(kali㉿kali)-[~/…/.-/d@n(e/colour/final]
└─$ ls
flag.txt
                                                                                                                   
┌──(kali㉿kali)-[~/…/.-/d@n(e/colour/final]
└─$ cat flag.txt 
Secret meeting at ksahbmwnasd for plans on human testing at 1.2868° N, 103.8545° E. Entry code is LNC2023{h0m4N_m0t471oN}                
```

Flag: LNC2023{h0m4N\_m0t471oN} &#x20;
