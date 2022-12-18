---
description: >-
  SIT N0H4TS STANDCON 2022 was held from 17 - 19 June 2022. The 24 hours CTF
  competition was held from 18 - 19 June 2022.
---

# SIT N0H4TS STANDCON CTF 2022

![](<.gitbook/assets/image (562).png>)

I attended the Conference as well as Reverse Engineering workshop on Day 1. On Day 1, I also searched for fishes around the GatherTown platform. See if you can spot my name in one of the images on [Twitter](https://twitter.com/N0H4TS/status/1538869529828372480?s=20\&t=YCTTiPrZtgn55kqQZnKjuQ), [Instagram ](https://www.instagram.com/p/CfBy8Lrsltb/)and [LinkedIn](https://www.linkedin.com/posts/n0h4ts\_student-conference-standcon-activity-6944635001439170560-Z4u\_/).&#x20;

On Day 2 and 3 is when STANDCON CTF 2022 happens. STANDCON CTF 2022 is an InfoSec competition that puts cyber defenders across all backgrounds and ages to test with specially curated challenges.

This event was quite a unique one. Normally in CTF competitions, the challenges would be unlocked in batches by the organizers or all the challenges would be available from the start.

This CTF is a little different. Participants were required to find `key` objects in GatherTown platform just like how we found `fishes` on Day1 to participate in lucky draw and exchange for vouchers.

This competition allowed up to 3 members to form a team but I participated solo in this CTF with the team name: Mekdonal. I managed to solve 3 challenges - 1 MISC, 1 OSINT and 1 Forensics challenge. Honestly, the searching of keys got quite tiring at some point. Searching for a bunch of keys alone throughout the whole GatherTown map was not an easy task.

![](<.gitbook/assets/image (580).png>)

![](<.gitbook/assets/image (553).png>)

## CERTIFICATE OF PARTICIPATION

![](<.gitbook/assets/image (177).png>)

## A New Gateway

![](<.gitbook/assets/image (510).png>)

In this challenge, we were given a .pcapng file.

We could open up this file on [Wireshark](https://www.wireshark.org/) to analyze the packets.

If you have no idea what Wireshark is or never heard of it before, you could probably get the hint from the challenge description `(Wire)Shark` and then Google it.

Once the `Challenge3.pcapng` file is opened in Wireshark, we can select file, `Export Objects > HTTP`

Here we can see there is a file in packet 16957 transferred by HTTP. Lets save this file!

![](<.gitbook/assets/image (520).png>)

I opened up the file and saw some `HTML` code. But notice this string which I highlighted. Does this look familiar? If not, I suggest you could check out my previous [writeup](https://gadiel-lau.gitbook.io/2022-writeups/nus-greyhats-grey-cat-the-flag-2022#ghost) and get familiar with different encoding methods.

![](<.gitbook/assets/image (597).png>)

The `=` appended at the end of the string likely suggest that this is Base64 encoded. To decode this, we could use an [online Base64 decoder](https://www.base64decode.org/). If you would like to try an alternative tool to solve this, check out my other [writeup](https://gadiel-lau.gitbook.io/2022-writeups/aisp-cyber-wellness-ctf#mix-and-match).

Once it is decoded, we get the output which is the flag.

![](<.gitbook/assets/image (577).png>)

Flag: STANDCON2022{cfc-y0u2\_d3f4u17\_9473w4y\_70\_4\_cy832\_c42332}

## I Sea You (Part 1)

![](<.gitbook/assets/image (521).png>)

For this challenge, we were given a `.wav` audio file. I compressed to zip file (because file upload limit size here is 100MB only)

{% file src=".gitbook/assets/intercepted-audio-sea-waves.zip" %}

I listened to the audio and heard `Morse code` from `1:00` to `1:30`.

I opened the `.wav` file in [Audacity](https://www.audacityteam.org/download/) to analyze the audio.

&#x20;I moved to the 1 min mark because I know that's when the morse code starts playing. Next, I could right click on the drop down list and select `Spectrogram`

![](<.gitbook/assets/image (507).png>)

This would give us the Spectrogram view

![](<.gitbook/assets/image (546).png>)

There were 8 different channels for this audio file. But I saw something interesting at Channels 7 and 8.

![](<.gitbook/assets/image (533).png>)

It looked like these 2 channels contained the morse code we are looking for. We could click `Solo` here just to listen to the specific channel. I realised channel 7 and 8 are probably the same audio.

I proceeded to click on the drop down list again and select `Spectrogram settings`. I changed the `range` to `1` . This time the morse code appeared much clearer. We could take the longer dash as `-` and the shorter dash as `.`&#x20;

![](<.gitbook/assets/image (567).png>)

I decoded this using this [online morse code translator](https://morsecode.world/international/translator.html). I input the morse code which I saw on Audacity into the input (can be quite time consuming) and saw the message in the output. For an alternative solution, refer to my previous writeup [here](https://gadiel-lau.gitbook.io/2020-writeups/brixel-ctf-winter-edition-2020/forensics#lost-evidence) where I used Audacity to copy paste the audio section into a new file and export it. After that, we could upload the audio on [online morse code decoder](https://morsecode.world/international/decoder/audio-decoder-adaptive.html) to get the message. I wanted to try to "manually" decode this time as the morse code decoder doesn't work 100% of the time for me (i.e. sometimes it decodes a wrong output)

![](<.gitbook/assets/image (593).png>)

Alternative solution output (after a few tries.. had to clear message and play again)

![](<.gitbook/assets/image (536).png>)

In both output above, we would get the same message.

`CHANNELCOMPROMISED.EMAILORCA.ATLANTIS@GMAIL.COM.`

Alternatively, the easier solution could be to use multimon-ng to get the decoded morse code message.

`-a` option will add the demodulator and `MORSE_CW` specify that it is morse code `-t` will specify the `wav` format

```
┌──(root㉿kali)-[/home/kali/Desktop]
└─# multimon-ng -a MORSE_CW -t wav flag.wav 
multimon-ng 1.1.9
  (C) 1996/1997 by Tom Sailer HB9JNX/AE4WA
  (C) 2012-2020 by Elias Oenal
Available demodulators: POCSAG512 POCSAG1200 POCSAG2400 FLEX EAS UFSK1200 CLIPFSK FMSFSK AFSK1200 AFSK2400 AFSK2400_2 AFSK2400_3 HAPN4800 FSK9600 DTMF ZVEI1 ZVEI2 ZVEI3 DZVEI PZVEI EEA EIA CCIR MORSE_CW DUMPCSV X10 SCOPE
Enabled demodulators: MORSE_CW
CHANNEL COMPROMISED. EMAIL ORCA.ATLANTIS@GMAIL.COM. 
```

After getting the message, I proceeded to email `ORCA` for the flag.

![](<.gitbook/assets/image (561).png>)

After a few seconds, I get back a response which contained a Partial Flag for Part 1.

![Part 1 flag: STANDCON22{Y0u\_F0uNd\_0r](<.gitbook/assets/image (590).png>)

If I click on `Show original`, I would see more details about this email. Now I know that `Content-Transfer-Encoding` used Base64 and I could see a chunk of Base64 encoded text at the bottom.

![](<.gitbook/assets/image (581).png>)

I copied the whole chunk and paste into [online Base64 decoder](https://www.base64decode.org/), which gave me an interesting output. Right at the bottom, I could see a message that was not shown in the email previously.

![](<.gitbook/assets/image (596).png>)

This is likely to be "`Digital invisible ink`".  If we press `CTRL+A` on the email message, we could see the hidden message appear at the bottom as well.

![](<.gitbook/assets/image (573).png>)

Now that we got the first part of the flag, where is the second part? We know that `ORCA` left us a hint from the hidden message which reads `I loved the food so much that I left a review!`

This could likely be a food review left by `ORCA`. From these information, We have ORCA's gmail and we know ORCA left a food review.

After some searching online, I found a pretty good read [here](https://webintmaster.com/blog/how-to/how-to-find-the-google-id-gaia-id-of-an-email-and-the-users-google-maps-reviews-and-public-albums/). We could use [EPIEOS](https://epieos.com/?q=orca.atlantis%40gmail.com) and search up ORCA's gmail.

Sometimes you would get this "annoying" pop up to verify that you are human. It is totally normal. If you are unable to verify for some reason and cannot proceed to the next step, continue reading.. I have another solution to solve this challenge.

![](<.gitbook/assets/image (508).png>)

After verified, we will see a `Google maps` link at the bottom.

![](<.gitbook/assets/image (540).png>)

If we go to the [link](https://www.google.com/maps/contrib/115760377201113977336), and click on `Reviews`, we will get the 2nd part of the flag.

An alternative solution to find the 2nd part of the flag would be to use [GHunt](https://github.com/mxrch/GHunt).&#x20;

After installation, I could simply run the command `python ghunt.py email orca.atlantis@gmail.com` on my Command Prompt and I would get the [Google Maps link](https://www.google.com/maps/contrib/115760377201113977336/reviews) where Orca left a review.&#x20;

![](<.gitbook/assets/image (504) (1).png>)

Clicking on the link would give us the 2nd part of the flag.

![](<.gitbook/assets/image (576).png>)

Combining both parts of the flag would give us the flag for this challenge.

Flag: STANDCON22{Y0u\_F0uNd\_0r C@'s\_SEA\_cR3t!}

## Warmup Forensics

![](<.gitbook/assets/image (565).png>)

We are given a `broken` file with no file extensions.

{% file src=".gitbook/assets/broken" %}

First, I used `file` command to check the type of file data. Next, I used a hex editor like[ GHex](https://wiki.gnome.org/Apps/Ghex) to analyse the file data.

![](<.gitbook/assets/image (539).png>)

We could see that the decoded [file signature](https://en.wikipedia.org/wiki/List\_of\_file\_signatures) shows `STANDCON2022`. This is an invalid file signature, so we have to change this. But what file signature should we change? or what type of file should this  be?&#x20;

If we continue inspecting the data, we would see `IHDR`,`IDAT` and `IEND`. Hence, this is most likely a [PNG](https://en.wikipedia.org/wiki/Portable\_Network\_Graphics#File\_format) file.&#x20;

We could change the file signature and the following 2 bytes to `00 00` as well. If we take a closer look, we would realise that the width(4 bytes) and height(4 bytes) are all set to 0.&#x20;

![](<.gitbook/assets/image (531).png>)

We need to find out the correct width and height of this image. To do this, we could check its[ CRC value(4 bytes)](https://www.w3.org/TR/PNG-Structure.html) as highlighted

![CRC value: E8 D3 C1 43](<.gitbook/assets/image (555).png>)

Now, we could write a simple Python script on a text editor like Vim or Sublime Text.

```python
import binascii
import struct

crcbp = open("broken", "rb").read()
for i in range(3000):
    for j in range(3000):
        data = crcbp[12:16] + struct.pack('>i', i)+struct.pack('>i', j)+crcbp[24:29]
        crc32 = binascii.crc32(data) & 0xffffffff
        if(crc32 == 0xE8D3C143):
            print(i, j)
            print('hex:', hex(i), hex(j))
```

If we run the python script, we would get the correct values for width and height. In this case, we should set the width to 0x780 and height to 0x438.

![](<.gitbook/assets/image (563).png>)

Now that everything is set, we will save this data in GHex.

![](<.gitbook/assets/image (584).png>)

If we go to the directory and open up `broken`, we can now see the flag at the bottom of the image!

![](<.gitbook/assets/image (501).png>)

Flag: STANDCON22{W@RMUP\_lia00000}

## MemeDump

![](<.gitbook/assets/image (158).png>)

For this challenge, we were given a [google drive link](https://drive.google.com/file/d/1oR2iV5kub75hfSya91xjPiXs7cCBNbao/view) which contained a `memedump.raw` file. Note that I solved this challenge after the competition. Nevertheless, I thought this was quite an interesting challenge and decided to do a writeup.

I will be using [Volatility 2](https://en.wikipedia.org/wiki/Volatility\_\(software\)) for this challenge. Volatility is an open-source memory forensics framework for incident response and malware analysis. The CheatSheet can be found [here](https://downloads.volatilityfoundation.org/releases/2.4/CheatSheet\_v2.4.pdf)

First, we run `imageinfo` to determine the profile of `memedump`.

![](<.gitbook/assets/image (808).png>)

Next, we could take the first profile that we see: `Win7SP1x86_23418` to perform other commands below. We could run `pslist` to check the list of processes.

```
┌──(kali㉿kali)-[~/Desktop/tools/volatility]
└─$ python2 vol.py -f ~/Desktop/memedump.raw --profile=Win7SP1x86_23418 pslist
Volatility Foundation Volatility Framework 2.6.1
Offset(V)  Name                    PID   PPID   Thds     Hnds   Sess  Wow64 Start                          Exit                          
---------- -------------------- ------ ------ ------ -------- ------ ------ ------------------------------ ------------------------------
0x84e4ac78 System                    4      0     54      367 ------      0 2022-05-15 04:13:25 UTC+0000                                 
0x85cffd40 smss.exe                204      4      2       29 ------      0 2022-05-15 04:13:25 UTC+0000                                 
0x864e1d40 csrss.exe               288    272      8      209      0      0 2022-05-15 04:13:25 UTC+0000                                 
0x86510290 wininit.exe             336    272      3       75      0      0 2022-05-15 04:13:25 UTC+0000                                 
0x86512d40 csrss.exe               344    328      7      202      1      0 2022-05-15 04:13:25 UTC+0000                                 
0x865194e8 winlogon.exe            384    328      3      108      1      0 2022-05-15 04:13:25 UTC+0000                                 
0x8654e290 services.exe            428    336      8      161      0      0 2022-05-15 04:13:25 UTC+0000                                 
0x86556030 lsass.exe               436    336      6      467      0      0 2022-05-15 04:13:25 UTC+0000                                 
0x86558030 lsm.exe                 444    336      9      134      0      0 2022-05-15 04:13:25 UTC+0000                                 
0x865a2990 svchost.exe             556    428     10      333      0      0 2022-05-15 04:13:26 UTC+0000                                 
0x85da7030 svchost.exe             620    428      7      220      0      0 2022-05-15 04:13:26 UTC+0000                                 
0x865cb630 svchost.exe             672    428     16      347      0      0 2022-05-15 04:13:26 UTC+0000                                 
0x874a6588 svchost.exe             752    428     11      282      0      0 2022-05-15 04:13:26 UTC+0000                                 
0x8658d188 svchost.exe             828    428     30      704      0      0 2022-05-15 04:13:26 UTC+0000                                 
0x86626860 svchost.exe             948    428      8      154      0      0 2022-05-15 04:13:26 UTC+0000                                 
0x865fb8e8 svchost.exe            1076    428      5       93      0      0 2022-05-15 04:13:26 UTC+0000                                 
0x86691880 svchost.exe            1120    428      9      293      0      0 2022-05-15 04:13:26 UTC+0000                                 
0x86728030 dwm.exe                1404    752      3       70      1      0 2022-05-15 04:13:27 UTC+0000                                 
0x8672b530 explorer.exe           1416   1380     32      762      1      0 2022-05-15 04:13:27 UTC+0000                                 
0x8674d6e8 taskhost.exe           1480    428      8      145      1      0 2022-05-15 04:13:27 UTC+0000                                 
0x8678b530 Everything.exe         1600   1416      2       59      1      0 2022-05-15 04:13:28 UTC+0000                                 
0x867bd030 dllhost.exe            1936    556     28      537      1      0 2022-05-15 04:14:07 UTC+0000                                 
0x86800a58 WmiPrvSE.exe           1104    556      6      113      0      0 2022-05-15 04:14:27 UTC+0000                                 
0x86787d40 mspaint.exe            1464   1416     12      297      1      0 2022-05-15 04:14:31 UTC+0000                                 
0x84f66d40 svchost.exe             544    428      9      118      0      0 2022-05-15 04:15:26 UTC+0000                                 
0x867ef030 DumpIt.exe             1784   1416      2       39      1      0 2022-05-15 04:18:37 UTC+0000                                 
0x8660b030 conhost.exe            1816    344      2       52      1      0 2022-05-15 04:18:37 UTC+0000           
```

If we used the hint, it would tell us that MEMES are made in `Microsoft Paint`. Notice previously when we ran `pslist`, there was a `mspaint.exe` with the Process ID - PID: `1464`. This process could have our flag.

![](<.gitbook/assets/image (801).png>)

Another possibility could be the flag is in the filesystem. We could run `filescan` and `grep` for `Users.*` to check the list of files and limit to only search for users files. We would see that there are a few files with `.png` files.

```
┌──(kali㉿kali)-[~/Desktop/tools/volatility]
└─$ python2 vol.py -f ~/Desktop/memedump.raw --profile=Win7SP1x86_23418 filescan | grep Users.*  
Volatility Foundation Volatility Framework 2.6.1
0x000000001d309928      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Searches\desktop.ini
0x000000001d309a70      8      0 R--rwd \Device\HarddiskVolume2\Users\Public\Music\desktop.ini
0x000000001d309d40      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Libraries\Videos.library-ms
0x000000001d3ea750      5      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PIFCD5.tmp
0x000000001d3eadc8      9      1 RW-rw- \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\History\History.IE5\index.dat
0x0000000024c20dc8      6      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PIF146.tmp
0x00000000272af790      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Music\desktop.ini
0x000000003e001c20      9      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PIF10.tmp
0x000000003e0086b8      7      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes\realFlag.png
0x000000003e008770      7      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes\flag.png
0x000000003e00c708      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Recent\desktop.ini
0x000000003e00cd30      1      1 RW-rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Explorer\thumbcache_idx.db
0x000000003e00e550      9      1 RW-rw- \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Cookies\index.dat
0x000000003e00ef80      9      1 RW-rw- \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Temporary Internet Files\Content.IE5\index.dat
0x000000003e0128b8      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Links\RecentPlaces.lnk
0x000000003e01bc30      1      1 R--rw- \Device\HarddiskVolume2\Users\Administrator\Desktop
0x000000003e01c4a0      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Links\Downloads.lnk
0x000000003e50e850      1      1 RW-rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Explorer\thumbcache_idx.db
0x000000003e5622f0      1      1 R--rw- \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes
0x000000003e562b08      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Links\Desktop.lnk
0x000000003e5907c0      5      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes\genius.png
0x000000003e5f40c8      2      1 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Printer Shortcuts
0x000000003e5f6840      2      1 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Printer Shortcuts
0x000000003e5f7c90      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Videos\desktop.ini
0x000000003e601f80      6      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes\dank.png
0x000000003e642198      1      1 RW---- \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\UsrClass.dat.LOG2
0x000000003e645d40      1      1 RW---- \Device\HarddiskVolume2\Users\Administrator\ntuser.dat.LOG2
0x000000003e647580      1      1 RW---- \Device\HarddiskVolume2\Users\Administrator\NTUSER.DAT
0x000000003e647c00      2      1 RW-rw- \Device\clfs\Device\HarddiskVolume2\Users\Administrator\NTUSER.DAT{6cced2f1-6e01-11de-8bed-001e0bcd1824}.TM
0x000000003e647cb8      2      1 RW-r-- \Device\HarddiskVolume2\Users\Administrator\NTUSER.DAT{6cced2f1-6e01-11de-8bed-001e0bcd1824}.TMContainer00000000000000000002.regtrans-ms
0x000000003e648698      1      1 RW-rwd \Device\clfs\Device\HarddiskVolume2\Users\Administrator\NTUSER.DAT{6cced2f1-6e01-11de-8bed-001e0bcd1824}.TM
0x000000003e6b16e0      8      0 R--r-- \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Recent\CustomDestinations\5afe4de1b92fc382.customDestinations-ms
0x000000003e6b7bd0      6      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PIF792.tmp
0x000000003e6ba800      7      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes\redflag.png
0x000000003e707b30      1      1 RW---- \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\UsrClass.dat
0x000000003e707be8      2      1 RW-r-- \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\UsrClass.dat{724b16f7-d404-11ec-b6e5-40ec99f065a8}.TMContainer00000000000000000001.regtrans-ms
0x000000003e70d7f8      1      1 RW---- \Device\HarddiskVolume2\Users\Administrator\ntuser.dat.LOG1
0x000000003e70da50      2      1 RW-r-- \Device\HarddiskVolume2\Users\Administrator\NTUSER.DAT{6cced2f1-6e01-11de-8bed-001e0bcd1824}.TMContainer00000000000000000001.regtrans-ms
0x000000003e70ef80      2      1 RW-r-- \Device\HarddiskVolume2\Users\Administrator\NTUSER.DAT{6cced2f1-6e01-11de-8bed-001e0bcd1824}.TM.blf
0x000000003e710940      2      1 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Credentials
0x000000003e7116c8      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Libraries\Music.library-ms
0x000000003e713830      2      1 RW-r-- \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\UsrClass.dat{724b16f7-d404-11ec-b6e5-40ec99f065a8}.TMContainer00000000000000000002.regtrans-ms
0x000000003e7138f0      1      1 RW-rwd \Device\clfs\Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\UsrClass.dat{724b16f7-d404-11ec-b6e5-40ec99f065a8}.TM
0x000000003e713d20      2      1 RW-r-- \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\UsrClass.dat{724b16f7-d404-11ec-b6e5-40ec99f065a8}.TM.blf
0x000000003e71ab58      8      0 R--rw- \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Accessories\System Tools\Private Character Editor.lnk
0x000000003e720390      8      0 R--rw- \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Accessories\Windows Explorer.lnk
0x000000003e720500      8      0 R--rw- \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Accessories\System Tools\Control Panel.lnk
0x000000003e720d58      2      0 R--rw- \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Foxit Reader\Uninstall.lnk
0x000000003e722eb8      2      0 R--rw- \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Accessories\System Tools\computer.lnk
0x000000003e7237f0      2      0 R--rw- \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Accessories\System Tools\Internet Explorer (No Add-ons).lnk
0x000000003e72c278      3      0 R--r-- \Device\HarddiskVolume2\Users\Administrator\AppData\Local\IconCache.db
0x000000003e73eaa0      2      0 R--rw- \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\WinRAR\WinRAR help.lnk
0x000000003e73ece8      8      0 R--rwd \Device\HarddiskVolume2\Users\desktop.ini
0x000000003e73f5f8      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Accessories\System Tools\Desktop.ini
0x000000003e740378      2      0 R--rw- \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Accessories\Run.lnk
0x000000003e741f80      2      0 R--rw- \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Foxit Reader\Foxit Reader.lnk
0x000000003e7448a8      1      1 RW-rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Explorer\thumbcache_1024.db
0x000000003e74e5a0      1      1 RW-rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Explorer\thumbcache_32.db
0x000000003e74e6c8      2      1 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes
0x000000003e750688      5      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes\croppedMEME.png
0x000000003e7524e0      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\desktop.ini
0x000000003e753db8      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\desktop.ini
0x000000003e7581c0      2      0 R--rw- \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Accessories\Notepad.lnk
0x000000003e759348      8      0 R--rwd \Device\HarddiskVolume2\Users\Public\desktop.ini
0x000000003e7598f8      2      0 R--rw- \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\WinRAR\Console RAR manual.lnk
0x000000003e75a428      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Accessories\Desktop.ini
0x000000003e75b230      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Maintenance\Desktop.ini
0x000000003e75b510      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Administrative Tools\desktop.ini
0x000000003e75bf80      8      0 R--rw- \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Accessories\Command Prompt.lnk
0x000000003e75c7e0      2      0 R--rw- \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Internet Explorer.lnk
0x000000003e75cc70      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\desktop.ini
0x000000003e75de20      2      0 R--rw- \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\WinRAR\WinRAR.lnk
0x000000003e76fcc0      8      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PI4A5F.tmp
0x000000003e7701e8      1      1 -W-rw- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\FXSAPIDebugLogFile.txt
0x000000003e774cc0      8      0 R--rwd \Device\HarddiskVolume2\Users\Public\Videos\desktop.ini
0x000000003e777220      7      0 RW-rw- \Device\HarddiskVolume2\Users\Administrator\AppData\Local\GDIPFONTCACHEV1.DAT
0x000000003e777590      2      1 R--rwd \Device\HarddiskVolume2\Users\Public\Desktop
0x000000003e777830      6      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PIE3C4.tmp
0x000000003e77a830      6      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PIE3C5.tmp
0x000000003e77ad40      1      1 RW-rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Explorer\thumbcache_96.db
0x000000003e77aef0      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Links\desktop.ini
0x000000003e77fcb8      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Favorites\desktop.ini
0x000000003e77fe28      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Downloads\desktop.ini
0x000000003e781928      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Contacts\desktop.ini
0x000000003e783388      6      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PIEA9C.tmp
0x000000003e7834d0      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Libraries\Documents.library-ms
0x000000003e7836b8      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Libraries\desktop.ini
0x000000003e783770      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Documents\desktop.ini
0x000000003e784d58      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Saved Games\desktop.ini
0x000000003e787600      8      0 R--rwd \Device\HarddiskVolume2\Users\Public\Documents\desktop.ini
0x000000003e78aa98      8      0 R--rwd \Device\HarddiskVolume2\Users\Public\Libraries\desktop.ini
0x000000003e78c038      5      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes\grassFlag.png
0x000000003e78d9a0      1      1 RW-rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Explorer\thumbcache_32.db
0x000000003e790488      2      1 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop
0x000000003e790ac8      4      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PICAC1.tmp
0x000000003e7928c0      6      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PICA22.tmp
0x000000003e793448      2      1 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop
0x000000003e793500      2      1 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu
0x000000003e794038      4      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PID9B4.tmp
0x000000003e794488      2      1 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu
0x000000003e7945e8      2      1 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Libraries
0x000000003e7954d8      2      1 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Burn
0x000000003e795590      2      1 R--rwd \Device\HarddiskVolume2\Users\Public\Desktop
0x000000003e797770      2      1 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Burn
0x000000003e79b260      4      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes\mylife.png
0x000000003e79f708      8      0 RW-rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Explorer\thumbcache_idx.db
0x000000003e7a14d8      4      0 RW-rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Explorer\thumbcache_96.db
0x000000003e7a1770      8      0 RW-rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Explorer\thumbcache_32.db
0x000000003e7a19b0      4      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PICA33.tmp
0x000000003e7a24e0      8      0 RW-rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Explorer\thumbcache_sr.db
0x000000003e7a2628      8      0 RW-rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Explorer\thumbcache_1024.db
0x000000003e7a2770      7      0 RW-rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Explorer\thumbcache_256.db
0x000000003e7a46b8      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Libraries\Pictures.library-ms
0x000000003e7a4770      2      1 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Windows\Libraries
0x000000003e7a9828      6      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PID2FD.tmp
0x000000003e7ab110      3      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes\MONEYYYY.png
0x000000003e7ab950      4      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PID30E.tmp
0x000000003e7ac548      8      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Pictures\desktop.ini
0x000000003e7ad610      8      0 R--rwd \Device\HarddiskVolume2\Users\Public\Pictures\desktop.ini
0x000000003e7af110      7      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes\REDREDFLAG.png
0x000000003e7b0168      8      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PIEAAD.tmp
0x000000003e7b0b70      8      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PIF1E5.tmp
0x000000003e7b8c40      7      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PIE463.tmp
0x000000003e7be9b0      7      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PIEB4B.tmp
0x000000003e7cbc40      1      1 RW-rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Explorer\thumbcache_sr.db
0x000000003e7d48d0      1      1 RW-rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Explorer\thumbcache_256.db
0x000000003e7d9ca8      6      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PIF840.tmp
0x000000003e7dfbe0      8      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PIF7A2.tmp
0x000000003e7e9830      6      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PIFCC5.tmp
0x000000003e7ed488      4      0 R--r-d \Device\HarddiskVolume2\Users\Administrator\Desktop\DumpIt.exe
0x000000003e7ef770      8      0 R--r-- \Device\HarddiskVolume2\Users\Administrator\Desktop\DumpIt.exe
0x000000003e7f8bf0      6      0 R--rw- \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\1033\StructuredQuerySchema.bin
0x000000003ec7c038      1      1 RW-rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Explorer\thumbcache_96.db
0x000000003ecd3038      1      1 RW---- \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\UsrClass.dat.LOG1
0x000000003ecd3518      2      1 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Roaming\Microsoft\Credentials
0x000000003ecd3690      2      1 RW-rw- \Device\clfs\Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\UsrClass.dat{724b16f7-d404-11ec-b6e5-40ec99f065a8}.TM
0x000000003ed83960      1      1 RW-rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Explorer\thumbcache_1024.db
0x000000003edeaed8      2      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Burn\Burn\desktop.ini
0x000000003ff2a6f0      4      1 RWD--- \Device\HarddiskVolume2\Users\ADMINI~1\AppData\Local\Temp\~PIC936.tmp
0x000000003ff2e940      1      1 RW-rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Explorer\thumbcache_256.db
0x000000003ff3d550      1      1 RW-rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Explorer\thumbcache_idx.db
0x000000003ff3d6f0      2      1 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes
0x000000003ff6b858      1      1 RW-rw- \Device\HarddiskVolume2\Users\Administrator\Desktop\WIN-BICD439RGQO-20220515-041837.raw
0x000000003ff6f5c8      1      1 RW-rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Explorer\thumbcache_idx.db
0x000000003ff734f8      1      1 RW-rwd \Device\HarddiskVolume2\Users\Administrator\AppData\Local\Microsoft\Windows\Explorer\thumbcache_sr.db
```

If we want to search for all the `.png` files only, we could `grep png`. However, if we extract any of these images such as `realFlag.png`, we would only get memes and not the flag.

```
┌──(kali㉿kali)-[~/Desktop/tools/volatility]
└─$ python2 vol.py -f ~/Desktop/memedump.raw --profile=Win7SP1x86_23418 filescan | grep png  
Volatility Foundation Volatility Framework 2.6.1
0x000000003e0086b8      7      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes\realFlag.png
0x000000003e008770      7      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes\flag.png
0x000000003e5907c0      5      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes\genius.png
0x000000003e601f80      6      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes\dank.png
0x000000003e6ba800      7      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes\redflag.png
0x000000003e750688      5      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes\croppedMEME.png
0x000000003e78c038      5      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes\grassFlag.png
0x000000003e79b260      4      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes\mylife.png
0x000000003e7ab110      3      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes\MONEYYYY.png
0x000000003e7af110      7      0 R--rwd \Device\HarddiskVolume2\Users\Administrator\Desktop\Memes\REDREDFLAG.png
```

As such, we proceed to extract the `mspaint.exe` memory.&#x20;

```
┌──(kali㉿kali)-[~/Desktop/tools/volatility]
└─$ python2 vol.py -f ~/Desktop/memedump.raw --profile=Win7SP1x86_23418 memdump -p 1464 --dump-dir=.
Volatility Foundation Volatility Framework 2.6.1
************************************************************************
Writing mspaint.exe [  1464] to 1464.dmp
```

Once it's extracted, we will get a `1464.dmp` file. We change this to `.data` file.

![](<.gitbook/assets/image (799).png>)

Open the `1464.data` in [`GIMP`](https://www.gimp.org/).&#x20;

![](<.gitbook/assets/image (803).png>)

After some trial and error, if we change the Image settings to `Offset: 192115874` `Width: 953` `Height: 910`, we will get the flag.

![](<.gitbook/assets/image (120) (1).png>)

![](<.gitbook/assets/image (121) (1).png>)

Flag: STANDCON22{meme\_mem\_dump}



Official writeups of the challenges in STANDCON2022 CTF can be found [here](https://github.com/div0-n0h4ts/STANDCON-CTF-2022-Writeups).

## Reflections

Overall, I think this CTF was an interesting one. I enjoyed the forensics challenge where I get to fix the broken file. Of course, the other challenges were great too. After the competition, I enjoyed the other forensics challenge as well where I used volatility to extract the `mspaint` process and eventually get the flag from the image in GIMP.

I would like to thank the organiser N0H4TS for the giftpack which contained pen, diary, thumb drive and more. I would also like to thank the sponsor - Offensive Security for the lucky draw prize as well.

## Gift pack & Lucky Draw Winner

![Gift pack](<.gitbook/assets/image (566) (1).png>)

![Lucky Draw prize](<.gitbook/assets/image (537).png>)

![Lucky Draw Prize Giving Ceremony](<.gitbook/assets/image (111).png>)

![Venue was changed 1 day before...](<.gitbook/assets/image (128) (1).png>)

Pictures taken for this Prize Giving Ceremony can be found on [Instagram ](https://www.instagram.com/p/Cg1YSaTpt5o/?hl=en)and [LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:6960904737680486400/?updateEntityUrn=urn%3Ali%3Afs\_feedUpdate%3A%28V2%2Curn%3Ali%3Aactivity%3A6960904737680486400%29).
