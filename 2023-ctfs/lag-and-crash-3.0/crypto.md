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

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

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

