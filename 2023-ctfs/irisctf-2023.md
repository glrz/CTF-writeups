---
description: >-
  IrisCTF is a 48-hour Capture The Flag competition organized by IrisSec.
  IrisCTF was held on 7 - 9 January.
---

# IrisCTF 2023

This CTF featured challenges in the disciplines of reverse engineering, binary exploitation, web exploitation, cryptography, radio frequency, networks, forensics, and more.&#x20;

I participated solo in this CTF as team `TheCross` even though this CTF allowed unlimited team  members to be in a team. I tried to use a new team name here which was different from the team name (i.e. T34M1) I used few years back.&#x20;

I wanted to try participating as solo because it has been quite some time since I participated as solo in a non-local CTF on [CTFtime](https://ctftime.org/event/1774). The last time I participated solo in non-local CTFs was in 2021. When I participated in these non-local CTFs: [TetCTF 2021](https://gadiel-lau.gitbook.io/2021-writeup/2021-ctfs/tetctf-2021), [justCTF \[\*\] 2020](https://gadiel-lau.gitbook.io/2021-writeup/2021-ctfs/justctf-2020), [LINE CTF 2021](https://gadiel-lau.gitbook.io/2021-writeup/2021-ctfs/line-ctf-2021) and [Securinets CTF Quals 2021](https://gadiel-lau.gitbook.io/2021-writeup/2021-ctfs/securinets-ctf-quals-2021), I remembered how I felt quite demoralized because I could only solve one challenge.

Fast forward one year, I started to participate more actively in CTFs in the year 2022 and gained more confidence and experience in tackling CTF challenges. This time I took courage to participate in non-local CTF as solo again after more than a year. Eventually, I got 227/730 placing which is still not too bad I guess.

<figure><img src="../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

I spent a few hours over the weekend trying out some of the challenges and managed to solve some challenges. I especially enjoyed the forensics challenge in this CTF  where I get to  learn  more about timezones and epochtime :) I solved a total of 5 challenges.

<figure><img src="../.gitbook/assets/image (23) (1).png" alt=""><figcaption></figcaption></figure>

## &#x20;Sanity Check

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Like most CTFs which had a sanity check or welcome challenge, this CTF had one as well. It's basically a freebie or giveaway and to introduce the flag format to  participants.

Flag: irisctf{w31c0m3\_t0\_1r15ctf\_2023}

## Discord

<figure><img src="../.gitbook/assets/image (16) (1).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a  discord link. Upon joining the discord server, the flag  can be found in one of  the channels, that is the `misc` channel. If we look closely beside the channel name at the top, we will see the flag displayed.

<figure><img src="../.gitbook/assets/image (12) (1) (1).png" alt=""><figcaption></figcaption></figure>

Flag: irisctf{d15c0rd\_c0nn3cts\_y0u\_t0\_0ur\_0rg4n1z3rs}

## babyshark

<figure><img src="../.gitbook/assets/image (30) (1).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were  given a `.pcapng` file embedded  in zip. This challenge was  relatively easy and was the easiest challenge under  the `Network` category. Most teams managed to solve it in 1 try.

<figure><img src="../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

I opened the extracted `.pcapng` file in Wireshark to inspect its packets and noticed there was a `babyshark.gif` file under the `HTTP`  protocol on  packet 133. This seemed interesting and so I proceeded to export this `HTTP` object. To extract this file, go to `File > Export Objects  >  HTTP ...`

<figure><img src="../.gitbook/assets/image (17) (1) (1).png" alt=""><figcaption></figcaption></figure>

Once the file is saved, we can open it and we  will  get the flag.

<figure><img src="../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>

Flag: irisctf{welc0m3\_t0\_n3tw0rks}

## babyforens

<figure><img src="../.gitbook/assets/image (20) (1).png" alt=""><figcaption></figcaption></figure>

This challenge was  under the `forensics` category and  I enjoyed solving it. This challenge took most teams multiple  tries to solve it and I solved it before the hint and subsequent hints were released.

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption><p>Hint: <a href="https://www.youtube.com/watch?v=rksaoaqt3JA">https://www.youtube.com/watch?v=rksaoaqt3JA</a></p></figcaption></figure>

I was the 7th to solve this challenge and was quite satisfied even though I think I could have first-blooded this challenge if I woke up earlier to attempt the challenges and if I attempted this challenge first before any other challenges.\


<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

For this challenge, I will split it up into 2 parts, but solving this challenge is not sequential. This means that you could solve `Part 1` first then  `Part 2` and  vice versa.

### Part 1

For this challenge, we were given a broken `.jpg` file.&#x20;

{% file src="../.gitbook/assets/IMG_0917.jpg" %}

First, I tried to open it on  `Mozzila Firefox` browser  on  my VM and it produced some error. If you try on other browser like `Google Chrome`, you may see a small white square instead.

<figure><img src="../.gitbook/assets/image (9) (1) (1).png" alt=""><figcaption></figcaption></figure>

To save this broken file, I had to right click on the file and `Save Link As…`

<figure><img src="../.gitbook/assets/image (27) (1).png" alt=""><figcaption></figcaption></figure>

Next, I proceeded to open up this  file on my hex editor : GHex. You could use any hex editor you prefer. If you want, you could also find an online hex editor [here](https://hexed.it/).

Opening the file in  hex  editor showed that the first few bytes are null bytes.&#x20;

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

If we scroll down till the end, we will see `FF D9`. Based on previous CTF experiences, we know that this is the trailer bytes for `.jpg` files. This gives us the idea that we are probably dealing with a `.jpg`  file.

<figure><img src="../.gitbook/assets/image (29) (1).png" alt=""><figcaption></figcaption></figure>

If you do not have any experiences dealing with  `.jpg` files, you could also find useful resources online [here ](https://en.wikipedia.org/wiki/List\_of\_file\_signatures)and [here ](https://www.file-recovery.com/jpg-signature-format.htm)which covers the concepts  of file signatures. After understanding  the concept of  file signature, we can fix this broken file  easily.

To fix this broken file, we simply change the first 2 bytes from `00 00` to `FF D8`

<figure><img src="../.gitbook/assets/image (13) (1) (1).png" alt=""><figcaption></figcaption></figure>

Once we have successfully modified the starting bytes, we can save this file and open it in image viewer using the `eog` command. We will be greeted by this lovely image of a coyote, with the `secret` part of the flag shown above.

<figure><img src="../.gitbook/assets/image (24) (1).png" alt=""><figcaption><p>Secret : exif_data_can_leak_a_lot_of_info</p></figcaption></figure>

For other forensics challenges writeups that involved fixing of broken files, you may refer to my other writeups [here](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/csit-challenge-of-wits-2022), [here](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/sit-n0h4ts-standcon-ctf-2022#warmup-forensics) and [here](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/dsta-brainhack-cyber-defenders-discovery-camp-training-2022/ctf-topics/cyber-forensics#png-file-is-corrupted).

### Part 2

Now that we  have  the `secret` part of the flag, we are left with the `latitude`,`longitude`, `epochtime` and `serial`. If we had solved `Part 1` first, we would  get the hint  that `exiftool` can leak a lot of info. Alternatively, if we choose to do this part first, then we should already know that `exiftool` is a very useful tool that contains the metadata of the file.

First, we can  find the `latitude` and `longitude` by  running `exiftool`.

<figure><img src="../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>

We can simply copy paste these values in Google and get the latitude and  longitude in decimal form: `37.74_-119.59`. We can also see the  location where this image was taken.&#x20;

<figure><img src="../.gitbook/assets/image (21) (1).png" alt=""><figcaption></figcaption></figure>

Next, we can proceed to find the  `epochtime`.  The `epochtime` is the number of seconds since 01/01/1970 UTC 00:00:00, also known as `unix time`. It is `UTC` which  is also `GMT +0.`

To find out more about unix time, read [here](https://en.wikipedia.org/wiki/Unix\_time).

To find the time this picture was taken,  we can use `exiftool` again.

<figure><img src="../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

There is a tricky part here. This picture was taken in `USA California` and we will need to take the timezones into consideration to find the `epochtime`. Another thing to note is that in some area like `USA California` have timezone changes due to [Daylight Saving Time](https://www.timeanddate.com/time/zone/usa/los-angeles?year=2022).  At that point when the picture was taken, the timezone was  UTC/GMT -7.

<figure><img src="../.gitbook/assets/image (8) (1) (1).png" alt=""><figcaption></figcaption></figure>

To get  the `epochtime`, we need to add 7 hours to the original time seen in `exiftool`. Then, we could use an  [online epoch converter ](https://www.epochconverter.com/) to get the `epochtime` or use [CyberChef](https://cyberchef.org/#recipe=To\_UNIX\_Timestamp\('Seconds%20\(s\)',true,true\)\&input=U2F0IDI3IEF1Z3VzdCAyMDIyIDE3OjA0OjU2IEdNVAo) to achieve the same result.

<figure><img src="../.gitbook/assets/image (6) (1) (1).png" alt=""><figcaption><p>epochtime: 1661619896</p></figcaption></figure>

Finally, we can find the `serial number` using `exiftool` as well.

&#x20;However, this part tricked me a bit because I overthinked. I thought it was referring to the `Internal Serial Number` initially.&#x20;

<figure><img src="../.gitbook/assets/image (1) (2) (1).png" alt=""><figcaption></figcaption></figure>

After reading the challenge description again, I discovered the  serial number can be found at the bottom of the camera and we could check the format of serial  number  [here](https://www.canon-europe.com/support/consumer\_products/where\_to\_find\_your\_serial\_number/).

As I searched through the fields in `exiftool`, I found the  serial number.

<figure><img src="../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption><p>392075057288</p></figcaption></figure>

Piecing up all  parts of the flag will give us the flag.

Flag: irisctf{37.74\_-119.59\_1661619896\_392075057288\_exif\_data\_can\_leak\_a\_lot\_of\_info}

## Exit Survey

<figure><img src="../.gitbook/assets/image (15) (1).png" alt=""><figcaption></figcaption></figure>

This challenge is a survey form which mainly questioned our experience on  this CTF.  After the survey is submitted, the flag is encodded in `Base64`.

<figure><img src="../.gitbook/assets/image (19) (1).png" alt=""><figcaption></figcaption></figure>

We can easily solve this by copy pasting into CyberChef and will get the flag from the output after decoding the `Base64`.

<figure><img src="../.gitbook/assets/image (22) (1).png" alt=""><figcaption></figcaption></figure>

Flag: irisctf{struggling\_means\_youre\_learning\_thank\_you\_and\_happy\_hacking}

## wi-the-fi

<figure><img src="../.gitbook/assets/image (24) (2).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.cap` file embedded in the `capture.zip`.

{% file src="../.gitbook/assets/BobertsonNet.cap" %}

I solved this challenge after the competition. Still decided to document it since I was very close to solve it during the CTF.

First, lets open this file in Wireshark to analyze the packets.

In wireshark, we can see that the packets were all transmitted in layer 2, also known as the the data-link layer. This included 802.11 protocol packets which are part of the IEEE 802.1 set of LAN standards.

We can apply the filter `eapol` to see the WiFi handshake. To read up more about the 4-way handshake, you can check out [here](https://www.wifi-professionals.com/2019/01/4-way-handshake). You could also check out this [detailed blog writeup](https://praneethwifi.in/2019/11/09/4-way-hand-shake-keys-generation-and-mic-verification/) on the 4-way handshake or this [CTF example ](https://ctf-wiki.mahaloz.re/misc/traffic/protocols/WIFI/)on how to crack the password  and decrypt the traffic.

<figure><img src="../.gitbook/assets/image (5) (2).png" alt=""><figcaption></figcaption></figure>

We can crack the password by using `Aircrack-ng` to perform dictionary attack.

```
$ aircrack-ng BobertsonNet.cap -w /usr/share/wordlists/rockyou.txt
```

After a few seconds, the password will be found : billybob1.&#x20;

<figure><img src="../.gitbook/assets/image (17) (2).png" alt=""><figcaption></figcaption></figure>

We can use this key to decrypt the packets. To decrypt, we can follow the documentation [here](https://wiki.wireshark.org/HowToDecrypt802.11). Note  that we do not need all 4 eapol packets to be captured to crack the password as shown above, we could still crack the password with 3 out of 4 eapol packets.

We can navigate `File > Edit > Preferences`

&#x20;&#x20;

<figure><img src="../.gitbook/assets/image (7) (1) (2).png" alt=""><figcaption></figcaption></figure>

Next, we go to IEEE 802.11 and edit the decryption key.

<figure><img src="../.gitbook/assets/image (32) (1).png" alt=""><figcaption></figcaption></figure>

Once the key is entered, we will get the decrypted traffic in Wireshark.

After the packets are decrypted, we can analyze these packets again. We would see various packets  under the `TCP` protocol.&#x20;

We can filter it by `tcp.len > 0` to view the packets that contains payload or  data. From here, we will get the filtered `packet 20422`.

<figure><img src="../.gitbook/assets/image (4) (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

Finally, we can inspect the packet data which will give us the flag.

<figure><img src="../.gitbook/assets/image (2) (2) (1).png" alt=""><figcaption></figcaption></figure>

Alternatively, we could use  [`airdecap-ng`](https://www.aircrack-ng.org/doku.php?id=airdecap-ng) to decrypt the WPA/WPA2 capture file. We can do so by running the following command:

```
┌──(kali㉿kali)-[~/Downloads]
└─$ airdecap-ng -e BobertsonNet -p billybob1 BobertsonNet.cap
Total number of stations seen            5
Total number of packets read         20980
Total number of WEP data packets         0
Total number of WPA data packets      2657
Number of plaintext data packets         0
Number of decrypted WEP  packets         0
Number of corrupted WEP  packets         0
Number of decrypted WPA  packets      1964
Number of bad TKIP (WPA) packets         0
Number of bad CCMP (WPA) packets         0
```

This will produce a `-dec.cap` file which is the decrypted/stripped version of the input file.

Finally, running `strings` on the `-dec.cap`  file, and `grep` for iris would give us the flag

<figure><img src="../.gitbook/assets/image (3) (2) (1).png" alt=""><figcaption></figcaption></figure>

Check out my previous challenge writeup on WiFi [here](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/dsta-brainhack-cyber-defenders-discovery-camp-ctf-2022/network#wifi). It was a challenge which involved the use of `aircrack-ng` to perform dictionary attack as well, after I used `crunch` to create my own wordlist.

Flag: irisctf{4ircr4ck\_g0\_brrrrrrrrrrrrrrr}
