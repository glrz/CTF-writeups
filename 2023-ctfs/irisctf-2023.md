---
description: >-
  IrisCTF is a 48-hour Capture The Flag competition organized by IrisSec.
  IrisCTF was held on 7 - 9 January.
---

# IrisCTF 2023

This CTF featured challenges in the disciplines of reverse engineering, binary exploitation, web exploitation, cryptography, radio frequency, networks, forensics, and more.&#x20;

I participated solo in this CTF as team `TheCross` even though this CTF allowed unlimited team  members to be in a team. I wanted to try participating as solo because it has been quite some time since I participated as solo in a non-local CTF on [CTFtime](https://ctftime.org/event/1774). The last time I participated solo in non-local CTFs was in 2021. When I participated in these non-local CTFs: [TetCTF 2021](https://gadiel-lau.gitbook.io/2021-writeup/2021-ctfs/tetctf-2021), [justCTF \[\*\] 2020](https://gadiel-lau.gitbook.io/2021-writeup/2021-ctfs/justctf-2020), [LINE CTF 2021](https://gadiel-lau.gitbook.io/2021-writeup/2021-ctfs/line-ctf-2021) and [Securinets CTF Quals 2021](https://gadiel-lau.gitbook.io/2021-writeup/2021-ctfs/securinets-ctf-quals-2021), I remembered how I felt quite demoralized because I could only solve one challenge.

Fast forward one year, I started to participate more actively in CTFs in the year 2022 and gained more confidence and experience in tackling CTF challenges. This time I took courage to participate in non-local CTF as solo again after more than a year. Eventually, I got 227/730 placing which is still not too bad I guess.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

I spent a few hours over the weekend trying out some of the challenges and managed to solve some challenges. I especially enjoyed the forensics challenge in this CTF  where I get to  learn  more about timezones and epochtime :) I solved a total of 5 challenges.

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

## &#x20;Sanity Check

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Like most CTFs which had a sanity check or welcome challenge, this CTF had one as well. It's basically a freebie or giveaway and to introduce the flag format to  participants.

Flag: irisctf{w31c0m3\_t0\_1r15ctf\_2023}

## Discord

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a  discord link. Upon joining the discord server, the flag  can be found in one of  the channels, that is the `misc` channel. If we look closely beside the channel name at the top, we will see the flag displayed.

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Flag: irisctf{d15c0rd\_c0nn3cts\_y0u\_t0\_0ur\_0rg4n1z3rs}

## babyshark

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were  given a `.pcapng` file embedded  in zip. This challenge was  relatively easy and was the easiest challenge under  the `Network` category. Most teams managed to solve it in 1 try.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

I opened the extracted `.pcapng` file in Wireshark to inspect its packets and noticed there was a `babyshark.gif` file under the `HTTP`  protocol on  packet 133. This seemed interesting and so I proceeded to export this `HTTP` object. To extract this file, go to `File > Export Objects  >  HTTP ...`

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

Once the file is saved, we can open it and we  will  get the flag.

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

Flag: irisctf{welc0m3\_t0\_n3tw0rks}

## babyforens

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

This challenge was  under the `forensics` category and  I enjoyed solving it. This challenge was took most teams multiple  tries to solve it and I solved it before the hint and subsequent hints were released.

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption><p>Hint: <a href="https://www.youtube.com/watch?v=rksaoaqt3JA">https://www.youtube.com/watch?v=rksaoaqt3JA</a></p></figcaption></figure>

I was the 7th to solve this challenge and was quite satisfied even though I think I could have first-blooded this challenge if I woke up earlier to attempt the challenges and if I attempted this challenge first before any other  challenges.\


<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

For this challenge, I will split it up into 2 parts, but solving this challenge is not sequential. This means that you could solve `Part 1` first then  `Part 2` and  vice versa.

### Part 1

For this challenge, we were given a broken `.jpg` file. First, I tried to open it on  `Mozzila Firefox` browser  on  my VM and it produced some error.

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

To save this broken file, I will need to right click on the file and `Save Link As…`

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

Next, I proceeded to open up this  file on my hex editor : GHex. You could use any hex editor you prefer. If you want, you can find an online hex editor [here](https://hexed.it/).

Opening the file in  hex  editor showed that the first few bytes are null bytes.&#x20;

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

If we scroll down till the end, we will see `FF D9`. Based on previous CTF experiences, we know that this is the trailer bytes for `.jpg` files. This gives us the idea that we are probably dealing with a `.jpg`  file.

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

If you do not have any experiences dealing with  `.jpg` files, you could also find useful resources online [here ](https://en.wikipedia.org/wiki/List\_of\_file\_signatures)and [here ](https://www.file-recovery.com/jpg-signature-format.htm)which covers the concepts  of file signatures. After understanding  the concept of  file signature, we can fix this broken file  easily.

To fix this broken file, we simply change the first 2 bytes from `00 00` to `FF D8` as such

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

Once we have successfully modified the starting bytes, we can save this file and open it in image viewer using the `eog` command. We will be greeted by this lovely image of a coyote, with the `secret` part of the flag shown above.

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption><p>Secret : exif_data_can_leak_a_lot_of_info</p></figcaption></figure>

For other forensics challenge writeups that involved fixing of broken files, you may refer [here](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/csit-challenge-of-wits-2022), [here](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/sit-n0h4ts-standcon-ctf-2022#warmup-forensics) and [here](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/dsta-brainhack-cyber-defenders-discovery-camp-training-2022/ctf-topics/cyber-forensics#png-file-is-corrupted).

### Part 2

Now that we  have  the `secret` part of the flag, we are left with the `latitude`,`longitude`, `epochtime` and `serial`. If we had solved `Part 1` first, we would  get the hint  that `exiftool` can leak a lot of info. Alternatively, if we choose to do this part first, then we know that `exiftool` is a very useful tool that contains the metadata of the file.

First, we can  find the `latitude` and `longitude` by  running `exiftool`.

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

We can simply copy paste these values in Google and get the latitude and  longitude in decimal form: `37.74_-119.59`. We can also see the  location where this image was taken.

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

Next, we can proceed to find the  `epochtime`.  The `epochtime` is the number of seconds since 01/01/1970 UTC 00:00:00, also known as `unix time`. It is `UTC` which  is also `GMT +0.`

To find out more about unix time, read [here](https://en.wikipedia.org/wiki/Unix\_time).

To find the time this picture was taken,  we can use `exiftool` again.

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

There is a tricky part here. This picture was taken in `USA California` and we will need to take the timezones into consideration to find the `epochtime`. Another thing to note is that in  some area like `USA  California`, the  timezone changes due to [Daylight Saving Time](https://www.timeanddate.com/time/zone/usa/los-angeles?year=2022).  At that point when the picture was taken, the timezone was  UTC/GMT -7.

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

To get  the `epochtime`, we need to add 7 hours to the original time seen in `exiftool`. Then, we could use an  [online epoch converter ](https://www.epochconverter.com/) to get the `epochtime` or use [CyberChef](https://cyberchef.org/#recipe=To\_UNIX\_Timestamp\('Seconds%20\(s\)',true,true\)\&input=U2F0IDI3IEF1Z3VzdCAyMDIyIDE3OjA0OjU2IEdNVAo) to achieve the same  result.

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption><p>epochtime: 1661619896</p></figcaption></figure>

Finally, we can find the `serial number` using `exiftool` as well.

&#x20;However, this  part tricked me a  bit because I overthinked. I  thought it was referring to the `Internal Serial Number` initially.&#x20;

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

After reading the challenge description again, I discovered the  serial number can be found at the bottom of the camera and we could check the format of serial  number  [here](https://www.canon-europe.com/support/consumer\_products/where\_to\_find\_your\_serial\_number/).

As I searched through the fields in `exiftool`, I found the  serial number.

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption><p>392075057288</p></figcaption></figure>

Piecing up all  parts of the flag will give us the flag.

Flag: irisctf{37.74\_-119.59\_1661619896\_392075057288\_exif\_data\_can\_leak\_a\_lot\_of\_info}

## Exit Survey

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

This challenge is a survey form which mainly questioned our experience on  this CTF.  After the survey is submitted, the flag is encodded in `Base64`.

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

We can easily solve this by copy pasting into CyberChef and will get the flag from the output after decoding the `Base64`.

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

Flag: irisctf{struggling\_means\_youre\_learning\_thank\_you\_and\_happy\_hacking}
