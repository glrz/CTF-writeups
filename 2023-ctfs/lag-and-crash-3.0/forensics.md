---
description: >-
  This was my favorite category where I first-blooded (first to solve) three
  challenges, and was in Top 3 solves for another two challenges.
---

# Forensics

## Embedment

<figure><img src="../../.gitbook/assets/image (6) (7).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `Flag.jpg` file and I was the first to solve it.

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

As the challenge name suggested, there could be files embedded within.

First, we could run `binwalk` to check

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ binwalk Flag.jpg 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
382           0x17E           Copyright string: "Copyright (c) 1998 Hewlett-Packard Company"
555091        0x87853         Zip archive data, at least v2.0 to extract, compressed size: 346, uncompressed size: 1312, name: [Content_Types].xml
556006        0x87BE6         Zip archive data, at least v2.0 to extract, compressed size: 239, uncompressed size: 590, name: _rels/.rels
556806        0x87F06         Zip archive data, at least v2.0 to extract, compressed size: 920, uncompressed size: 3453, name: word/document.xml
557773        0x882CD         Zip archive data, at least v2.0 to extract, compressed size: 244, uncompressed size: 817, name: word/_rels/document.xml.rels
558339        0x88503         Zip archive data, at least v2.0 to extract, compressed size: 1746, uncompressed size: 8393, name: word/theme/theme1.xml
560136        0x88C08         Zip archive data, at least v2.0 to extract, compressed size: 1052, uncompressed size: 3029, name: word/settings.xml
561235        0x89053         Zip archive data, at least v2.0 to extract, compressed size: 2986, uncompressed size: 29542, name: word/styles.xml
564266        0x89C2A         Zip archive data, at least v2.0 to extract, compressed size: 450, uncompressed size: 1310, name: word/webSettings.xml
564766        0x89E1E         Zip archive data, at least v2.0 to extract, compressed size: 634, uncompressed size: 2521, name: word/fontTable.xml
565448        0x8A0C8         Zip archive data, at least v2.0 to extract, compressed size: 370, uncompressed size: 757, name: docProps/core.xml
566129        0x8A371         Zip archive data, at least v2.0 to extract, compressed size: 369, uncompressed size: 711, name: docProps/app.xml
567513        0x8A8D9         End of Zip archive, footer length: 22
```

Indeed, there were some embedded files.

We could extract these as such                                                                                                              &#x20;

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ binwalk -D.* Flag.jpg                                          

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
382           0x17E           Copyright string: "Copyright (c) 1998 Hewlett-Packard Company"
555091        0x87853         Zip archive data, at least v2.0 to extract, compressed size: 346, uncompressed size: 1312, name: [Content_Types].xml
556006        0x87BE6         Zip archive data, at least v2.0 to extract, compressed size: 239, uncompressed size: 590, name: _rels/.rels
556806        0x87F06         Zip archive data, at least v2.0 to extract, compressed size: 920, uncompressed size: 3453, name: word/document.xml
557773        0x882CD         Zip archive data, at least v2.0 to extract, compressed size: 244, uncompressed size: 817, name: word/_rels/document.xml.rels
558339        0x88503         Zip archive data, at least v2.0 to extract, compressed size: 1746, uncompressed size: 8393, name: word/theme/theme1.xml
560136        0x88C08         Zip archive data, at least v2.0 to extract, compressed size: 1052, uncompressed size: 3029, name: word/settings.xml
561235        0x89053         Zip archive data, at least v2.0 to extract, compressed size: 2986, uncompressed size: 29542, name: word/styles.xml
564266        0x89C2A         Zip archive data, at least v2.0 to extract, compressed size: 450, uncompressed size: 1310, name: word/webSettings.xml
564766        0x89E1E         Zip archive data, at least v2.0 to extract, compressed size: 634, uncompressed size: 2521, name: word/fontTable.xml
565448        0x8A0C8         Zip archive data, at least v2.0 to extract, compressed size: 370, uncompressed size: 757, name: docProps/core.xml
566129        0x8A371         Zip archive data, at least v2.0 to extract, compressed size: 369, uncompressed size: 711, name: docProps/app.xml
567513        0x8A8D9         End of Zip archive, footer length: 22
```

If we go into the extracted directory and view these in hex editor, we would realize that one of the data is a zip file with the magic bytes `50 4B`.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cd _Flag.jpg.extracted                                          
                                                                                                                   
┌──(kali㉿kali)-[~/Downloads/_Flag.jpg.extracted]
└─$ ls
0	17E  87853  8A8D9

┌──(kali㉿kali)-[~/Downloads/_Flag.jpg.extracted]
└─$ ghex 87853
```

We could extract the zip file as such

```bash
┌──(kali㉿kali)-[~/Downloads/_Flag.jpg.extracted]
└─$ 7z x 87853 

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 12444 bytes (13 KiB)

Extracting archive: 87853
--
Path = 87853
Type = zip
Physical Size = 12444

Everything is Ok

Files: 11
Size:       52435
Compressed: 12444

┌──(kali㉿kali)-[~/Downloads/_Flag.jpg.extracted]
└─$ ls
 0   17E   87853   8A8D9  '[Content_Types].xml'   docProps   _rels   word
```

We could see that there's a `.xml` and 3 other directories extracted.

Finally, we could `grep` recursively on the directories with the flag format and we would get the flag.

```bash
┌──(kali㉿kali)-[~/Downloads/_Flag.jpg.extracted]
└─$ grep -r LNC
word/document.xml:<w:document xmlns:wpc="http://schemas.microsoft.com/office/word/2010/wordprocessingCanvas" xmlns:cx="http://schemas.microsoft.com/office/drawing/2014/chartex" xmlns:cx1="http://schemas.microsoft.com/office/drawing/2015/9/8/chartex" xmlns:cx2="http://schemas.microsoft.com/office/drawing/2015/10/21/chartex" xmlns:cx3="http://schemas.microsoft.com/office/drawing/2016/5/9/chartex" xmlns:cx4="http://schemas.microsoft.com/office/drawing/2016/5/10/chartex" xmlns:cx5="http://schemas.microsoft.com/office/drawing/2016/5/11/chartex" xmlns:cx6="http://schemas.microsoft.com/office/drawing/2016/5/12/chartex" xmlns:cx7="http://schemas.microsoft.com/office/drawing/2016/5/13/chartex" xmlns:cx8="http://schemas.microsoft.com/office/drawing/2016/5/14/chartex" xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" xmlns:aink="http://schemas.microsoft.com/office/drawing/2016/ink" xmlns:am3d="http://schemas.microsoft.com/office/drawing/2017/model3d" xmlns:o="urn:schemas-microsoft-com:office:office" xmlns:oel="http://schemas.microsoft.com/office/2019/extlst" xmlns:r="http://schemas.openxmlformats.org/officeDocument/2006/relationships" xmlns:m="http://schemas.openxmlformats.org/officeDocument/2006/math" xmlns:v="urn:schemas-microsoft-com:vml" xmlns:wp14="http://schemas.microsoft.com/office/word/2010/wordprocessingDrawing" xmlns:wp="http://schemas.openxmlformats.org/drawingml/2006/wordprocessingDrawing" xmlns:w10="urn:schemas-microsoft-com:office:word" xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main" xmlns:w14="http://schemas.microsoft.com/office/word/2010/wordml" xmlns:w15="http://schemas.microsoft.com/office/word/2012/wordml" xmlns:w16cex="http://schemas.microsoft.com/office/word/2018/wordml/cex" xmlns:w16cid="http://schemas.microsoft.com/office/word/2016/wordml/cid" xmlns:w16="http://schemas.microsoft.com/office/word/2018/wordml" xmlns:w16sdtdh="http://schemas.microsoft.com/office/word/2020/wordml/sdtdatahash" xmlns:w16se="http://schemas.microsoft.com/office/word/2015/wordml/symex" xmlns:wpg="http://schemas.microsoft.com/office/word/2010/wordprocessingGroup" xmlns:wpi="http://schemas.microsoft.com/office/word/2010/wordprocessingInk" xmlns:wne="http://schemas.microsoft.com/office/word/2006/wordml" xmlns:wps="http://schemas.microsoft.com/office/word/2010/wordprocessingShape" mc:Ignorable="w14 w15 w16se w16cid w16 w16cex w16sdtdh wp14"><w:body><w:p w14:paraId="26656AC9" w14:textId="77777777" w:rsidR="00E71DCA" w:rsidRDefault="00E71DCA" w:rsidP="00E71DCA"><w:pPr><w:shd w:val="clear" w:color="auto" w:fill="1E1E1E"/><w:spacing w:after="0" w:line="285" w:lineRule="atLeast"/><w:rPr><w:rFonts w:ascii="Consolas" w:eastAsia="Times New Roman" w:hAnsi="Consolas" w:cs="Times New Roman"/><w:color w:val="D4D4D4"/><w:sz w:val="21"/><w:szCs w:val="21"/></w:rPr></w:pPr><w:r><w:rPr><w:rFonts w:ascii="Consolas" w:eastAsia="Times New Roman" w:hAnsi="Consolas" w:cs="Times New Roman"/><w:color w:val="D4D4D4"/><w:sz w:val="21"/><w:szCs w:val="21"/></w:rPr><w:t>LNC2023{S3cr3tF1aG}</w:t></w:r></w:p><w:p w14:paraId="68B6E854" w14:textId="77777777" w:rsidR="00DD3231" w:rsidRDefault="00DD3231"/><w:sectPr w:rsidR="00DD3231"><w:pgSz w:w="11906" w:h="16838"/><w:pgMar w:top="1440" w:right="1440" w:bottom="1440" w:left="1440" w:header="708" w:footer="708" w:gutter="0"/><w:cols w:space="708"/><w:docGrid w:linePitch="360"/></w:sectPr></w:body></w:document>
```

Alternatively, an easier solution would be to extract the embedded zip content directly from the start using the `-e` option to extract or `-Me` to recursively extract files. After extracting, we can follow the same procedure and `grep` for the flag recursively.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ binwalk -Me Flag.jpg 

Scan Time:     2023-04-15 19:46:53
Target File:   /home/kali/Downloads/Flag.jpg
MD5 Checksum:  6d94d3ecadf1c2e359e2a6ca97082e35
Signatures:    391

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
382           0x17E           Copyright string: "Copyright (c) 1998 Hewlett-Packard Company"

WARNING: Extractor.execute failed to run external extractor 'jar xvf '%e'': [Errno 2] No such file or directory: 'jar', 'jar xvf '%e'' might not be installed correctly
555091        0x87853         Zip archive data, at least v2.0 to extract, compressed size: 346, uncompressed size: 1312, name: [Content_Types].xml
556006        0x87BE6         Zip archive data, at least v2.0 to extract, compressed size: 239, uncompressed size: 590, name: _rels/.rels
556806        0x87F06         Zip archive data, at least v2.0 to extract, compressed size: 920, uncompressed size: 3453, name: word/document.xml
557773        0x882CD         Zip archive data, at least v2.0 to extract, compressed size: 244, uncompressed size: 817, name: word/_rels/document.xml.rels
558339        0x88503         Zip archive data, at least v2.0 to extract, compressed size: 1746, uncompressed size: 8393, name: word/theme/theme1.xml
560136        0x88C08         Zip archive data, at least v2.0 to extract, compressed size: 1052, uncompressed size: 3029, name: word/settings.xml
561235        0x89053         Zip archive data, at least v2.0 to extract, compressed size: 2986, uncompressed size: 29542, name: word/styles.xml
564266        0x89C2A         Zip archive data, at least v2.0 to extract, compressed size: 450, uncompressed size: 1310, name: word/webSettings.xml
564766        0x89E1E         Zip archive data, at least v2.0 to extract, compressed size: 634, uncompressed size: 2521, name: word/fontTable.xml
565448        0x8A0C8         Zip archive data, at least v2.0 to extract, compressed size: 370, uncompressed size: 757, name: docProps/core.xml
566129        0x8A371         Zip archive data, at least v2.0 to extract, compressed size: 369, uncompressed size: 711, name: docProps/app.xml
567513        0x8A8D9         End of Zip archive, footer length: 22


Scan Time:     2023-04-15 19:46:53
Target File:   /home/kali/Downloads/_Flag.jpg.extracted/_rels/.rels
MD5 Checksum:  77bf61733a633ea617a4db76ef769a4d
Signatures:    391

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             XML document, version: "1.0"


Scan Time:     2023-04-15 19:46:53
Target File:   /home/kali/Downloads/_Flag.jpg.extracted/word/webSettings.xml
MD5 Checksum:  d4929875b042cd58fea3a8aac1099947
Signatures:    391

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             XML document, version: "1.0"


Scan Time:     2023-04-15 19:46:53
Target File:   /home/kali/Downloads/_Flag.jpg.extracted/word/document.xml
MD5 Checksum:  266e32db880a7646c27fe9a7b017819d
Signatures:    391

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             XML document, version: "1.0"


Scan Time:     2023-04-15 19:46:53
Target File:   /home/kali/Downloads/_Flag.jpg.extracted/word/settings.xml
MD5 Checksum:  0a4f50d1ca12a07a580b834c6d0a2a7d
Signatures:    391

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             XML document, version: "1.0"


Scan Time:     2023-04-15 19:46:53
Target File:   /home/kali/Downloads/_Flag.jpg.extracted/word/fontTable.xml
MD5 Checksum:  773aeb30c5670ef7d4cde1ee8b12b4f2
Signatures:    391

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             XML document, version: "1.0"


Scan Time:     2023-04-15 19:46:53
Target File:   /home/kali/Downloads/_Flag.jpg.extracted/word/styles.xml
MD5 Checksum:  e12dddbd8977ad7fce18c343f9e6075c
Signatures:    391

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             XML document, version: "1.0"


Scan Time:     2023-04-15 19:46:53
Target File:   /home/kali/Downloads/_Flag.jpg.extracted/word/theme/theme1.xml
MD5 Checksum:  fc5dd7a11f76159e8ac4ecd5e3e1b518
Signatures:    391

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             XML document, version: "1.0"


Scan Time:     2023-04-15 19:46:53
Target File:   /home/kali/Downloads/_Flag.jpg.extracted/word/_rels/document.xml.rels
MD5 Checksum:  7caaa99de7c709024bcfb5ae9c38352f
Signatures:    391

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             XML document, version: "1.0"


Scan Time:     2023-04-15 19:46:53
Target File:   /home/kali/Downloads/_Flag.jpg.extracted/[Content_Types].xml
MD5 Checksum:  8c71b2a6e8e97a96df3707e253a6fde5
Signatures:    391

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             XML document, version: "1.0"


Scan Time:     2023-04-15 19:46:53
Target File:   /home/kali/Downloads/_Flag.jpg.extracted/docProps/app.xml
MD5 Checksum:  c96e1c281781973c35b13e04ee659843
Signatures:    391

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             XML document, version: "1.0"


Scan Time:     2023-04-15 19:46:53
Target File:   /home/kali/Downloads/_Flag.jpg.extracted/docProps/core.xml
MD5 Checksum:  4b6678a1c4b9d2f623360202fe6f105e
Signatures:    391

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             XML document, version: "1.0"

                                                                                                                   
┌──(kali㉿kali)-[~/Downloads]
└─$ cd _Flag.jpg.extracted 
                                                                                                                   
┌──(kali㉿kali)-[~/Downloads/_Flag.jpg.extracted]
└─$ grep -r LNC    
word/document.xml:<w:document xmlns:wpc="http://schemas.microsoft.com/office/word/2010/wordprocessingCanvas" xmlns:cx="http://schemas.microsoft.com/office/drawing/2014/chartex" xmlns:cx1="http://schemas.microsoft.com/office/drawing/2015/9/8/chartex" xmlns:cx2="http://schemas.microsoft.com/office/drawing/2015/10/21/chartex" xmlns:cx3="http://schemas.microsoft.com/office/drawing/2016/5/9/chartex" xmlns:cx4="http://schemas.microsoft.com/office/drawing/2016/5/10/chartex" xmlns:cx5="http://schemas.microsoft.com/office/drawing/2016/5/11/chartex" xmlns:cx6="http://schemas.microsoft.com/office/drawing/2016/5/12/chartex" xmlns:cx7="http://schemas.microsoft.com/office/drawing/2016/5/13/chartex" xmlns:cx8="http://schemas.microsoft.com/office/drawing/2016/5/14/chartex" xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" xmlns:aink="http://schemas.microsoft.com/office/drawing/2016/ink" xmlns:am3d="http://schemas.microsoft.com/office/drawing/2017/model3d" xmlns:o="urn:schemas-microsoft-com:office:office" xmlns:oel="http://schemas.microsoft.com/office/2019/extlst" xmlns:r="http://schemas.openxmlformats.org/officeDocument/2006/relationships" xmlns:m="http://schemas.openxmlformats.org/officeDocument/2006/math" xmlns:v="urn:schemas-microsoft-com:vml" xmlns:wp14="http://schemas.microsoft.com/office/word/2010/wordprocessingDrawing" xmlns:wp="http://schemas.openxmlformats.org/drawingml/2006/wordprocessingDrawing" xmlns:w10="urn:schemas-microsoft-com:office:word" xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main" xmlns:w14="http://schemas.microsoft.com/office/word/2010/wordml" xmlns:w15="http://schemas.microsoft.com/office/word/2012/wordml" xmlns:w16cex="http://schemas.microsoft.com/office/word/2018/wordml/cex" xmlns:w16cid="http://schemas.microsoft.com/office/word/2016/wordml/cid" xmlns:w16="http://schemas.microsoft.com/office/word/2018/wordml" xmlns:w16sdtdh="http://schemas.microsoft.com/office/word/2020/wordml/sdtdatahash" xmlns:w16se="http://schemas.microsoft.com/office/word/2015/wordml/symex" xmlns:wpg="http://schemas.microsoft.com/office/word/2010/wordprocessingGroup" xmlns:wpi="http://schemas.microsoft.com/office/word/2010/wordprocessingInk" xmlns:wne="http://schemas.microsoft.com/office/word/2006/wordml" xmlns:wps="http://schemas.microsoft.com/office/word/2010/wordprocessingShape" mc:Ignorable="w14 w15 w16se w16cid w16 w16cex w16sdtdh wp14"><w:body><w:p w14:paraId="26656AC9" w14:textId="77777777" w:rsidR="00E71DCA" w:rsidRDefault="00E71DCA" w:rsidP="00E71DCA"><w:pPr><w:shd w:val="clear" w:color="auto" w:fill="1E1E1E"/><w:spacing w:after="0" w:line="285" w:lineRule="atLeast"/><w:rPr><w:rFonts w:ascii="Consolas" w:eastAsia="Times New Roman" w:hAnsi="Consolas" w:cs="Times New Roman"/><w:color w:val="D4D4D4"/><w:sz w:val="21"/><w:szCs w:val="21"/></w:rPr></w:pPr><w:r><w:rPr><w:rFonts w:ascii="Consolas" w:eastAsia="Times New Roman" w:hAnsi="Consolas" w:cs="Times New Roman"/><w:color w:val="D4D4D4"/><w:sz w:val="21"/><w:szCs w:val="21"/></w:rPr><w:t>LNC2023{S3cr3tF1aG}</w:t></w:r></w:p><w:p w14:paraId="68B6E854" w14:textId="77777777" w:rsidR="00DD3231" w:rsidRDefault="00DD3231"/><w:sectPr w:rsidR="00DD3231"><w:pgSz w:w="11906" w:h="16838"/><w:pgMar w:top="1440" w:right="1440" w:bottom="1440" w:left="1440" w:header="708" w:footer="708" w:gutter="0"/><w:cols w:space="708"/><w:docGrid w:linePitch="360"/></w:sectPr></w:body></w:document>
```

&#x20;Flag: LNC2023{S3cr3tF1aG}

## Slay The Robot

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.png` file. However, is it really a `.png` file?

Lets do a quick check by running the `file` command

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ file slaytherobot.png 
slaytherobot.png: ASCII text, with CRLF line terminators
```

This indicated that it was not an image file but rather an ASCII text file.

&#x20;If we read the contents of the file, we will get the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cat slaytherobot.png 
LNC2023{mah_mah_mah_theROBOT}
```

Flag: LNC2023{mah\_mah\_mah\_theROBOT}

## Wave

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.wav` file.&#x20;

We could simply load this file into an audio editor like `Audacity`.

If we change it to `spectrogram` mode, we will be able to see the flag.

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

Flag: LNC2023{annoyingwave}

## Survival's Message

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

For this challenge we were given a `flag.jpg` file and I was third  to solve the challenge.

<figure><img src="../../.gitbook/assets/image (15) (1).png" alt=""><figcaption></figcaption></figure>

First, if we run the `file` command, we would see that this is not a jpg image file but rather a ASCII text file, similar to the previous  `Slay The Robot` challenge.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ file flag.jpg 
flag.jpg: ASCII text, with CRLF line terminators
```

Similarly, we could read its contents.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cat flag.jpg                                     
Dear remaining warriors,

Many natural diaster has destroyed the world as we know it.

LNC2023{eX

The year is 3000, Many countries are in an icy place ruled by mutated huge insects.

1en

Our once glorious world, was once peaceful where all people live together.

SL0

But fret not remaining warriors, one day we will rise up to claim back what is ours.

N1sF8n}
```

If we look closely, we would see 4 parts of the flag split up in the letter. By combining these parts, we will get the flag.

Flag: LNC2023{eX1enSL0N1sF8n}

## Base Madness

<figure><img src="../../.gitbook/assets/image (5) (7).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given two files, 1 `.txt` file and another `.zip` file.

I was third to solve this challenge.

<figure><img src="../../.gitbook/assets/image (7) (8).png" alt=""><figcaption></figcaption></figure>

First, lets read the contents of the `.txt` file. We can see that it is encoded and appended with `=`. This could suggest that it could be `Base64` encoded.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cat base_madness.txt      
dGhpc2lzdGhlcGFzc3dvcmR0b3VubG9ja3RoZWZpbGU=                                                                                                                   
```

We could decode the `Base64` as such

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ base64 -d base_madness.txt
thisisthepasswordtounlockthefile        
```

This would give us the password the unlock the zip file: `thisisthepasswordtounlockthefile`  &#x20;

Using the password, we can unzip the file and get a `.jpg` file.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ 7z x base_madness.zip     

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 52479 bytes (52 KiB)

Extracting archive: base_madness.zip
--
Path = base_madness.zip
Type = zip
Physical Size = 52479

    
Enter password (will not be echoed):
Everything is Ok

Size:       59002
Compressed: 52479

┌──(kali㉿kali)-[~/Downloads]
└─$ file ayaka.jpg 
ayaka.jpg: data
```

If we run `exiftool` to view its  metadata, we will be able to see the flag under the `XP Subject`

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ exiftool ayaka.jpg
ExifTool Version Number         : 12.44
File Name                       : ayaka.jpg
Directory                       : .
File Size                       : 59 kB
File Modification Date/Time     : 2022:10:03 14:14:02-04:00
File Access Date/Time           : 2023:04:14 05:06:24-04:00
File Inode Change Date/Time     : 2023:04:14 05:05:08-04:00
File Permissions                : -rw-r--r--
Warning                         : Processing TIFF-like data after unknown 30-byte header
Exif Byte Order                 : Big-endian (Motorola, MM)
XP Subject                      : C2023{ayaka_is_key}
Padding                         : (Binary data 2016 bytes, use -b option to extract)
```

However, if you noticed, there's `LN` missing from the flag. As the `Padding` suggested we could run it with the `-b` option. Here, we would find `LN` under the `HINT`.

Note that this part is actually unnecessary since we already know  the flag format is `LNC {}`

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ exiftool -b ayaka.jpg 
Warning: Processing TIFF-like data after unknown 30-byte header - ayaka.jpg
12.44ayaka.jpg.590022022:10:03 14:14:02-04:002023:04:14 05:06:24-04:002023:04:14 05:05:08-04:00100644Processing TIFF-like data after unknown 30-byte headerMMC2023{ayaka_is_key}HINT:jpegLN
```

Flag: LNC2023{ayaka\_is\_key}

## Incompetent

<figure><img src="../../.gitbook/assets/image (20) (2).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.zip` file and I was the first to solve it.

<figure><img src="../../.gitbook/assets/image (11) (3).png" alt=""><figcaption></figcaption></figure>

First,  lets unzip this file.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ 7z x secret.zip

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 19822 bytes (20 KiB)

Extracting archive: secret.zip
--
Path = secret.zip
Type = zip
Physical Size = 19822

Everything is Ok

Folders: 2
Files: 2
Size:       21969
Compressed: 19822
```

Next, if we navigate into the extracted directory, we would see  a `.7z` file and another directory.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cd Secret    
                                                                                                                   
┌──(kali㉿kali)-[~/Downloads/Secret]
└─$ ls
Secret
                                                                                                                   
┌──(kali㉿kali)-[~/Downloads/Secret]
└─$ cd Secret 
                                                                                                                   
┌──(kali㉿kali)-[~/Downloads/Secret/Secret]
└─$ ls
Homework.7z  Important
```

Lets check out what is in the `Important` directory first. From here, we can see that there's a `password.docx`  file.&#x20;

```
┌──(kali㉿kali)-[~/Downloads/Secret/Secret]
└─$ cd Important
┌──(kali㉿kali)-[~/Downloads/Secret/Secret/Important]
└─$ ls
password.docx
```

If we open it in hex editor, we would see a string that looks like a japanese phrase and likely could be the password for the `.7z` file we saw previously too.

```bash
┌──(kali㉿kali)-[~/Downloads/Secret/Secret/Important]
└─$ ghex password.docx
```

<figure><img src="../../.gitbook/assets/image (3) (1) (4).png" alt=""><figcaption></figcaption></figure>

We can use the Password: `kimiwadekinaiko` to unzip the `.7z` file and this will extract a new directory.

```bash
┌──(kali㉿kali)-[~/Downloads/Secret/Secret]
└─$ 7z x Homework.7z 

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 9781 bytes (10 KiB)

Extracting archive: Homework.7z
--
Path = Homework.7z
Type = 7z
Physical Size = 9781
Headers Size = 229
Method = LZMA2:12k 7zAES
Solid = -
Blocks = 1

    
Enter password (will not be echoed):
Everything is Ok                     

Folders: 2
Files: 1
Size:       12232
Compressed: 9781
```

From here, we could navigate into the new directories and find a `flag.docx` file.

```bash
┌──(kali㉿kali)-[~/Downloads/Secret/Secret]
└─$ ls
Homework  Homework.7z  Important
                                                                                                                   
┌──(kali㉿kali)-[~/Downloads/Secret/Secret]
└─$ cd Homework 
                                                                                                                   
┌──(kali㉿kali)-[~/Downloads/Secret/Secret/Homework]
└─$ ls
Materials
                                                                                                                   
┌──(kali㉿kali)-[~/Downloads/Secret/Secret/Homework]
└─$ cd Materials 
                                                                                                                   
┌──(kali㉿kali)-[~/…/Secret/Secret/Homework/Materials]
└─$ ls
flag.docx
```

Now, we can try to run `strings` on the file and `grep` for the flag. This would give us a part of the flag.

```bash
┌──(kali㉿kali)-[~/…/Secret/Secret/Homework/Materials]
└─$ strings flag.docx | grep LNC
LNC2023{konoyodei
```

We only have part of the flag now, how do we get the entire flag?

We could `grep` for anything ending with `}` as such

```bash
┌──(kali㉿kali)-[~/…/Secret/Secret/Homework/Materials]
└─$ strings flag.docx | grep '.*}'

5}nH"
chibandekinaiko}
}-;}PB
5}4Onb
c%%'b}
&}QR
N0i}~
```

On the second line, we would see what looked like another part of japanese phrase. Combining these two parts, we will get the flag.

Flag: LNC2023{konoyodeichibandekinaiko}

## Destroyed

<figure><img src="../../.gitbook/assets/image (10) (8).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.jpg` image file and I was the first to solve it.

<figure><img src="../../.gitbook/assets/image (16) (1).png" alt=""><figcaption></figcaption></figure>

First, lets open this image in image viewer.

<figure><img src="../../.gitbook/assets/image (4) (5).png" alt=""><figcaption></figcaption></figure>

This looked like any other ordinary images. Based on previous CTF experience, this could be a `steganography` challenge.&#x20;

I ran `stegoveritas` and found interesting information in the trailing data. This looked like it could likely be `Base64` encoded.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ stegoveritas Image.jpg    
Running Module: SVImage
+------------------+------+
|   Image Format   | Mode |
+------------------+------+
| JPEG (ISO 10918) | RGB  |
+------------------+------+
Trailing Data Discovered... Saving
b'TE5DMjAyM3tNM1RhREB0QSFAIX0='
+---------+------------------+------------------------------------------------------------------------------------------------+-----------+
| Offset  | Carved/Extracted | Description                                                                                    | File Name |
+---------+------------------+------------------------------------------------------------------------------------------------+-----------+
| 0x46e53 | Carved           | LZMA compressed data, properties: 0xB6, dictionary size: 0 bytes, uncompressed size: 121 bytes | 46E53.7z  |
| 0x46e53 | Extracted        | LZMA compressed data, properties: 0xB6, dictionary size: 0 bytes, uncompressed size: 121 bytes | 46E53     |
+---------+------------------+------------------------------------------------------------------------------------------------+-----------+
+---------+------------------+-------------------------------------------------------------------------------------------------------+-----------+
| Offset  | Carved/Extracted | Description                                                                                           | File Name |
+---------+------------------+-------------------------------------------------------------------------------------------------------+-----------+
| 0x1aebf | Carved           | LZMA compressed data, properties: 0xC0, dictionary size: 134217728 bytes, uncompressed size: 38 bytes | 1AEBF.7z  |
| 0x1aebf | Extracted        | LZMA compressed data, properties: 0xC0, dictionary size: 134217728 bytes, uncompressed size: 38 bytes | 1AEBF     |
| 0x1b09f | Carved           | LZMA compressed data, properties: 0xC0, dictionary size: 134217728 bytes, uncompressed size: 38 bytes | 1B09F.7z  |
| 0x1b09f | Extracted        | LZMA compressed data, properties: 0xC0, dictionary size: 134217728 bytes, uncompressed size: 38 bytes | 1B09F     |
| 0x1e7e0 | Carved           | LZMA compressed data, properties: 0xD0, dictionary size: 16777216 bytes, uncompressed size: 36 bytes  | 1E7E0.7z  |
| 0x1e7e0 | Extracted        | LZMA compressed data, properties: 0xD0, dictionary size: 16777216 bytes, uncompressed size: 36 bytes  | 1E7E0     |
+---------+------------------+-------------------------------------------------------------------------------------------------------+-----------+
+---------+------------------+-------------------------------------------------------------------------------------------------------+-----------+
| Offset  | Carved/Extracted | Description                                                                                           | File Name |
+---------+------------------+-------------------------------------------------------------------------------------------------------+-----------+
| 0x7fc8  | Carved           | LZMA compressed data, properties: 0x92, dictionary size: 0 bytes, uncompressed size: 32 bytes         | 7FC8.7z   |
| 0x7fc8  | Extracted        | LZMA compressed data, properties: 0x92, dictionary size: 0 bytes, uncompressed size: 32 bytes         | 7FC8      |
| 0x20e29 | Carved           | LZMA compressed data, properties: 0xD8, dictionary size: 0 bytes, uncompressed size: 32 bytes         | 20E29.7z  |
| 0x20e29 | Extracted        | LZMA compressed data, properties: 0xD8, dictionary size: 0 bytes, uncompressed size: 32 bytes         | 20E29     |
| 0x211e9 | Carved           | LZMA compressed data, properties: 0xC0, dictionary size: 16777216 bytes, uncompressed size: 128 bytes | 211E9.7z  |
| 0x211e9 | Extracted        | LZMA compressed data, properties: 0xC0, dictionary size: 16777216 bytes, uncompressed size: 128 bytes | 211E9     |
| 0x33131 | Carved           | LZMA compressed data, properties: 0xC0, dictionary size: 0 bytes, uncompressed size: 64 bytes         | 33131.7z  |
| 0x33131 | Extracted        | LZMA compressed data, properties: 0xC0, dictionary size: 0 bytes, uncompressed size: 64 bytes         | 33131     |
| 0x36f18 | Carved           | LZMA compressed data, properties: 0xD0, dictionary size: 0 bytes, uncompressed size: 36 bytes         | 36F18.7z  |
| 0x36f18 | Extracted        | LZMA compressed data, properties: 0xD0, dictionary size: 0 bytes, uncompressed size: 36 bytes         | 36F18     |
| 0x3cdf4 | Carved           | LZMA compressed data, properties: 0xB6, dictionary size: 0 bytes, uncompressed size: 72 bytes         | 3CDF4.7z  |
| 0x3cdf4 | Extracted        | LZMA compressed data, properties: 0xB6, dictionary size: 0 bytes, uncompressed size: 72 bytes         | 3CDF4     |
| 0x3cfd4 | Carved           | LZMA compressed data, properties: 0xB4, dictionary size: 0 bytes, uncompressed size: 96 bytes         | 3CFD4.7z  |
| 0x3cfd4 | Extracted        | LZMA compressed data, properties: 0xB4, dictionary size: 0 bytes, uncompressed size: 96 bytes         | 3CFD4     |
| 0x46a64 | Carved           | LZMA compressed data, properties: 0x90, dictionary size: 16777216 bytes, uncompressed size: 160 bytes | 46A64.7z  |
| 0x46a64 | Extracted        | LZMA compressed data, properties: 0x90, dictionary size: 16777216 bytes, uncompressed size: 160 bytes | 46A64     |
| 0x4ed0b | Carved           | LZMA compressed data, properties: 0x9A, dictionary size: 0 bytes, uncompressed size: 56 bytes         | 4ED0B.7z  |
| 0x4ed0b | Extracted        | LZMA compressed data, properties: 0x9A, dictionary size: 0 bytes, uncompressed size: 56 bytes         | 4ED0B     |
+---------+------------------+-------------------------------------------------------------------------------------------------------+-----------+
```

From here we could use an online tool like CyberChef to decode the `Base64` which gives us the flag`.`

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

Alternatively, we could decode it directly in the terminal (which is what I prefer and usually do).

```
┌──(kali㉿kali)-[~/Downloads/Secret/Secret/Important]
└─$ echo TE5DMjAyM3tNM1RhREB0QSFAIX0= | base64 -d
LNC2023{M3TaD@tA!@!}
```

Flag: LNC2023{M3TaD@tA!@!}

## Blind

<figure><img src="../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.gif` file. I was close to solving this challenge during the competition and solved it slightly after the competition.&#x20;

If we run the `file` command, it would indicate that its a GIF image data.

```
┌──(kali㉿kali)-[~/Downloads]
└─$ file blind.gif  
blind.gif: GIF image data, version 87a, 2586 x
```

However, somethings quite off here. This file seemed to be corrupted or broken and cannot be opened.

If we analyze it in a hex editor, we would see that the magic bytes are correct, but the bytes after it are not bytes that we should see in a GIF image data file.

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

`IHDR`, `sRGB`, `pHYs`, `IDAT` indicates that it could likely be a `.png` file instead. Checking the trailing bytes also showed that it matched with what a `.png` file would have.

We could download a sample PNG file [here](https://file-examples.com/index.php/sample-images-download/sample-png-download/) to compare the magic bytes and replace it with the correct values.

Alternatively, we could search up the magic bytes for file signature as well.

Note that we should NOT just change it on the right side of hex editor i.e. Add in .PNG on the right like this.

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

The above will not work. We will need to fix the bytes to the correct values like this

<figure><img src="../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

Now that we have the magic bytes fixed, we can save it as a `.png` file and view the image.

<figure><img src="../../.gitbook/assets/image (35).png" alt=""><figcaption><p>Part 1 : LNC2023{       Part 3 : wrong}</p></figcaption></figure>

However, in this image, it looked like we had part 1 and part 3 of the flag, but not part 2 of the flag.

This was where I stopped during the competition. After the competition, I realized that part 2 of the flag could actually be seen after I ran `stegoveritas`.

If we navigate to the `results` directory, we will see various images with different colour, contrast etc.

```
┌──(kali㉿kali)-[~/Downloads/results]
└─$ ls
exif                                 flag.png_enhance_sharpness_50.png   flag.png_Median.png
flag.png_autocontrast.png            flag.png_enhance_sharpness_-75.png  flag.png_Min.png
flag.png_Blue_0.png                  flag.png_enhance_sharpness_75.png   flag.png_Mode.png
flag.png_Blue_1.png                  flag.png_equalize.png               flag.png_Red_0.png
flag.png_Blue_2.png                  flag.png_Find_Edges.png             flag.png_Red_1.png
flag.png_Blue_3.png                  flag.png_GaussianBlur.png           flag.png_Red_2.png
flag.png_Blue_4.png                  flag.png_grayscale.png              flag.png_Red_3.png
flag.png_Blue_5.png                  flag.png_Green_0.png                flag.png_Red_4.png
flag.png_Blue_6.png                  flag.png_Green_1.png                flag.png_Red_5.png
flag.png_Blue_7.png                  flag.png_Green_2.png                flag.png_Red_6.png
flag.png_blue_plane.png              flag.png_Green_3.png                flag.png_Red_7.png
flag.png_Edge-enhance_More.png       flag.png_Green_4.png                flag.png_red_plane.png
flag.png_Edge-enhance.png            flag.png_Green_5.png                flag.png_Sharpen.png
flag.png_enhance_sharpness_-100.png  flag.png_Green_6.png                flag.png_Smooth.png
flag.png_enhance_sharpness_100.png   flag.png_Green_7.png                flag.png_solarized.png
flag.png_enhance_sharpness_-25.png   flag.png_green_plane.png            keepers
flag.png_enhance_sharpness_25.png    flag.png_inverted.png
flag.png_enhance_sharpness_-50.png   flag.png_Max.png
```

In one of them, we could slightly see part 2 of the flag at the bottom.

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

Alternatively, we could open the original image that we fixed earlier in an image editing software like `gimp` and change its hue / brightness settings.

<figure><img src="../../.gitbook/assets/image (29) (3) (1).png" alt=""><figcaption><p>Part 2 : guessiwas</p></figcaption></figure>

By combining the three parts of the flag we obtained earlier, we will get the flag.

Flag: LNC2023{guessiwaswrong}

## Licensed Forensics

<figure><img src="../../.gitbook/assets/image (25) (3) (2).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a[ GDrive Link](https://drive.google.com/file/d/12dN8gxb653xAJsEzXQp3eZMXxIWkhMjI/view?usp=sharing) which leads us to download a Suspect\_Image.E01 file. Note that I solved this challenge shortly after the competition.

Since it was an `EO1` file, which is an EnCase image file, we could load it into a tool like EnCase Forensic Tool. However, the tool is a paid software. Hence, we will be using another tool, `FTK Imager` to solve this challenge.

First, we could load this disk image file into FTK imager.&#x20;

Next, we further analyze the different partitions. There are a few partitions and only one of them is of our interest, that is, the basic data partition \[2439MB].

<figure><img src="../../.gitbook/assets/image (29) (3).png" alt=""><figcaption></figcaption></figure>

As we further analyze and expand the partition in the evidence tree, we will find an interesting `Secret_Documents` folder.

In this folder, we will see a total of six files. Of which, only `Note.txt` and `flag.zip` looked like it contained useful information to solve this challenge.

<figure><img src="../../.gitbook/assets/image (1) (6).png" alt=""><figcaption></figcaption></figure>

If we read the `Note.txt`, it will give us some information about the password to the secret folder, most likely referring to `flag.zip`.

It also mentioned that the password is backed up somewhere else and the virtual machine LICENSE is the KEY.

> Note to self, do not let the authorities look in the contents of my secret folder.
>
> &#x20;
>
> The password for the secret folder is:
>
> &#x20;
>
> 32\*\*\*9\*\*\*\*\*\*\*\*\*9\*\*\*
>
> &#x20;
>
> Whoops, spilled my digital tea on the password! I can't remember my password...
>
> &#x20;
>
> Eh, no worries, I keep my password backed up somewhere else. Gotta remember that my
>
> virtual machine LICENSE is the KEY. It's important..!
>
> &#x20;
>
> Yes... The KEY...

Now, if we looked further into `Windows > System32 > Config`, which is where the registry files are usually located in, we would find some information about `VMware.inc` if we do a quick search in FTK Imager on the file `SOFTWARE.FileSlack` using the `CTRL+F` shortcut.

<figure><img src="../../.gitbook/assets/image (27) (4) (2).png" alt=""><figcaption></figcaption></figure>

If we manually searched through and scroll down near the bottom, we would see a `pastebin` link.

Alternatively, in this file, if we searched for `pastebin`, we would find a unique pastebin link. We should always keep in mind that information could be hidden in any files(including text files, image files etc.) or any links(including GDrive link, pastebin link etc.)

<figure><img src="../../.gitbook/assets/image (24) (4) (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

If you are interested in other forensics challenges which implemented the use of pastebin into the challenge, check out my previous writeup where I solved [GovTech STACK the Flags CTF 2020 - Voices in the head](https://gadiel-lau.gitbook.io/2020-writeups-1/2020-ctfs/govtech-stack-the-flags-ctf-2020/forensics#voices-in-the-head).

Back to this challenge, once we obtain the unique pastebin link: [https://pastebin.com/F6j80vMC](https://pastebin.com/F6j80vMC), we will be redirected to this site upon visiting the link.

<figure><img src="../../.gitbook/assets/image (2) (6).png" alt=""><figcaption></figcaption></figure>

>
>
> 1. Good thing that I kept a backup!
> 2. &#x20;
> 3. AGH I SPILT THE DIGITAL TEA™ AGAIN
> 4. &#x20;
> 5. \*\*983\*432689537\*123

This looked like its the second part of the password, where those denoted as `*` are the missing digits. We could combine this with what we obtained earlier in `Note.txt` and we would get thte following password: `3298394326895379123`.

Using this password, we will be able to view the PDF content that was password protected previously in `flag.zip`.

<figure><img src="../../.gitbook/assets/image (3) (2).png" alt=""><figcaption></figcaption></figure>

Once we open the password protected PDF file, we are presented with the flag.

<figure><img src="../../.gitbook/assets/image (30) (4).png" alt=""><figcaption></figcaption></figure>

You might want to check out a very detailed writeup by a friend [here](https://flagthecapture.blogspot.com/2023/04/ctf-writeup-lnc-2023-licensed-forensics.html) where he used another tool: `Autopsy` to solve it.

For simpler and more detailed forensics challenges which I solved using FTK Imager, you might want to check out my previous writeups in [GSCTF 2020](https://gadiel-lau.gitbook.io/2020-writeups-1/2020-ctfs/gsctf-2020#imaging) and [CDDC 2022 training](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/dsta-brainhack-cyber-defenders-discovery-camp-training-2022/ctf-topics/cyber-forensics#my-secret-folder).

Flag: LNC2023{ou7of51ght\_outofm1nd}
