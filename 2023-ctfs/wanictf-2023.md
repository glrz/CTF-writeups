---
description: >-
  WaniCTF is a CTF event organized by Wani Hackase, the Osaka University CTF
  club. It was held from 4 May - 6 May 2023.
---

# WaniCTF 2023

I participated in this CTF with team `youtiaos` and we obtained the ranking: `10/840`. Scoreboard can be found on [CTFtime](https://ctftime.org/event/1988).

<figure><img src="../.gitbook/assets/image (25) (4) (1).png" alt=""><figcaption></figcaption></figure>

I managed to spend some time during the weekend to solve some beginner forensic challenges.

## whats\_happening

<figure><img src="../.gitbook/assets/image (1) (4) (2) (1).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.zip` file.

First, we can unzip this file.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ 7z x for-whats-happening.zip 

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 10499 bytes (11 KiB)

Extracting archive: for-whats-happening.zip
--
Path = for-whats-happening.zip
Type = zip
Physical Size = 10499

Everything is Ok

Folders: 1
Files: 1
Size:       382976
Compressed: 10499
```

Once we unzipped it, we will get a `updog` file. Lets check what file it is.

```bash
┌──(kali㉿kali)-[~/Downloads/for-whats-happening]
└─$ file updog    
updog: ISO 9660 CD-ROM filesystem data 'ISO Label'
```

We could also use `strings` to perform static analysis on the file.

```bash
┌──(kali㉿kali)-[~/Downloads/for-whats-happening]
└─$ strings updog              
CD001
Win32                           ISO Label                       
                                                                                                                                                                                                                                                                                                                                                                                                MKISOFS ISO9660/HFS/UDF FILESYSTEM BUILDER & CDRECORD CD/DVD/BluRay CREATOR (C) 1993 E.YOUNGDALE (C) 1997 J.PEARSON/J.SCHILLING                                                                                                                2022050814552092$2022050814552092$0000000000000000
2022050814552092$
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                
CD001
2022050814552092$2022050814552092$0000000000000000
2022050814552092$
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                
CD001
MKI Sun May  8 14:55:20 2022
3.02a06 -J -joliet-long -jcharset UTF-8 -l -r -V ISO Label -o C:\hack\mine\updog.iso C:\hack\mine\updog_1
FAKE_FLAG.TXT;1RR
FAKE_FLAG.txtPX,
FLAG.PNG;1
FLAG.pngPX,
RRIP_1991ATHE ROCK RIDGE INTERCHANGE PROTOCOL PROVIDES SUPPORT FOR POSIX FILE SYSTEM SEMANTICSPLEASE CONTACT DISC PUBLISHER FOR SPECIFICATION SOURCE.  SEE PUBLISHER IDENTIFIER IN PRIMARY VOLUME DESCRIPTOR FOR CONTACT INFORMATION.
FAKE{Never_gonna_let_you_down}
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
IHDR
        pHYs
tEXtSoftware
Celsys Studio Tool
IDATx
';#o
j       H?
b1 ,
b1 ,
b1 ,
b1 ,
a@X,
b@X,
b@X,
b@X,
b@X,
b1 ,
b1 ,
b1 ,
b1 ,
!;1f
b       vI
&QQU<|
o=}w!
/?ox
-FZ&;
RHgP8
XG~/
&^8f
/+p-
ZUC!
UlGc
j@*j
zvnOr
9XQ0
&J!]
Nf@zt
U5S
f@)#`TSL
a1 }
c0J`4{:
q6g8F
;dV?
geE2
FNt4
\v61
fE~7
b@X,
b@X,
b@X,
b@X,
WWg@.Q
;d'|
\QU|
b~/)J
k&jIFU
--&Y
0 Ci^
d(E-
U8o.[C
,fz"
$,6kC
R/7pZ
^)$W
R?jhL,}
`EiI
LwzKQQ
^Mf!0
F&n!
PBxs}
7fEU[
fRT(-
SE-7
\,6$ V
LYZ}h[
J%az
w"pH
j}5Ke
c;XQ
|>3kI
(~1>!a
v4fj
61 ,
b1 ,
b1 ,
b1 ,
b1 ,
b`@X]W
:W9d'
uf@X=
jZ=p5!5
9L;2
uk2R
tFtyj
&j0QW
d8Y>
3!54
12ah
&f'@
?z2T
{P^X
*,6[
|TQ.
BJKw
c6[K`.
L8d8!/
HE-7l
&1r]
b@X,
b@X,
b@X,
b@X,
IEND
FAKE_FLAG{
This is where this file is damaged haha
```

If we looked closely, we would see that there was `FLAG.png` in the strings, which could suggest there is an embedded flag image file.

Next, we could run `binwalk` to extract the `ISO Primary Volume`.

```bash
┌──(kali㉿kali)-[~/Downloads/for-whats-happening]
└─$ binwalk updog 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             ISO 9660 Primary Volume,

                                                                                                                   
┌──(kali㉿kali)-[~/Downloads/for-whats-happening]
└─$ binwalk -e updog 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             ISO 9660 Primary Volume,

```

If we go into the extracted directory and go into `iso-root` directory, we would see that there are 2 files. One is the `FAKE_FLAG.txt` and the other is `FLAG.png`.

If we view `FLAG.png` in image viewer, we would see the flag in image.

```bash
┌──(kali㉿kali)-[~/Downloads/for-whats-happening/_updog.extracted/iso-root]
└─$ eog FLAG.png
```

<figure><img src="../.gitbook/assets/image (80) (2).png" alt=""><figcaption></figcaption></figure>

Alternatively, we could load it into `Autopsy` and we will find the flag there as well.

<figure><img src="../.gitbook/assets/image (100) (1).png" alt=""><figcaption></figcaption></figure>

Note that when creating a new case in Autopsy, we will have to load it as `Unallocated Space Image File`

<figure><img src="../.gitbook/assets/image (4) (7) (1).png" alt=""><figcaption></figcaption></figure>

Interested in another challenge where I used `Autopsy` to solve? Check out my previous more detailed writeup [here](https://gadiel-lau.gitbook.io/2020-writeups-1/2020-ctfs/brixel-ctf-winter-edition-2020/forensics#lost-evidence).

Flag: FLAG{n0th1ng\_much}

## Just\_MP4

<figure><img src="../.gitbook/assets/image (26) (2).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.zip` file as well.

First, I tried to load it into `Audacity`. However, there were some error.

I noted that this audio was only 1 second long and it was unlikely that there could be hidden message under the spectrogram view.

Hence, I ran `exiftool` to check for its metadata.

```bash
┌──(kali㉿kali)-[~/Downloads/for-Just-mp4]
└─$ exiftool chall.mp4 
ExifTool Version Number         : 12.57
File Name                       : chall.mp4
Directory                       : .
File Size                       : 152 kB
File Modification Date/Time     : 2021:05:03 00:00:00-04:00
File Access Date/Time           : 2023:05:04 02:46:31-04:00
File Inode Change Date/Time     : 2023:05:04 02:46:14-04:00
File Permissions                : -rw-r--r--
File Type                       : MP4
File Type Extension             : mp4
MIME Type                       : video/mp4
Major Brand                     : MP4 v2 [ISO 14496-14]
Minor Version                   : 0.0.0
Compatible Brands               : mp41, isom
Media Data Size                 : 151250
Media Data Offset               : 71
Movie Header Version            : 0
Create Date                     : 2023:04:26 13:09:50
Modify Date                     : 2023:04:26 13:09:50
Time Scale                      : 30000
Duration                        : 1.00 s
Preferred Rate                  : 1
Preferred Volume                : 100.00%
Preview Time                    : 0 s
Preview Duration                : 0 s
Poster Time                     : 0 s
Selection Time                  : 0 s
Selection Duration              : 0 s
Current Time                    : 0 s
Next Track ID                   : 2
Track Header Version            : 0
Track Create Date               : 2023:04:26 13:09:50
Track Modify Date               : 2023:04:26 13:09:50
Track ID                        : 1
Track Duration                  : 1.00 s
Track Layer                     : 0
Track Volume                    : 0.00%
Matrix Structure                : 1 0 0 0 1 0 0 0 1
Image Width                     : 512
Image Height                    : 512
Media Header Version            : 0
Media Create Date               : 2023:04:26 13:09:50
Media Modify Date               : 2023:04:26 13:09:50
Media Time Scale                : 30000
Media Duration                  : 1.00 s
Media Language Code             : und
Handler Description             : VideoHandler
Graphics Mode                   : srcCopy
Op Color                        : 0 0 0
Compressor ID                   : avc1
Source Image Width              : 512
Source Image Height             : 512
X Resolution                    : 72
Y Resolution                    : 72
Compressor Name                 : AVC Coding
Bit Depth                       : 24
Video Frame Rate                : 30
Handler Type                    : Metadata
Publisher                       : flag_base64:RkxBR3tINHYxbl9mdW5fMW5uMXR9
Image Size                      : 512x512
Megapixels                      : 0.262
Avg Bitrate                     : 1.21 Mbps
Rotation                        : 0
```

&#x20;Under the `Publisher` information, we can see that the flag looked like its encoded in `Base64`.

We could decode it in our terminal and we would get the flag.

```bash
┌──(kali㉿kali)-[~/Downloads/for-Just-mp4]
└─$ echo RkxBR3tINHYxbl9mdW5fMW5uMXR9 | base64 -d
FLAG{H4v1n_fun_1nn1t}  
```

Flag: FLAG{H4v1n\_fun\_1nn1t}
