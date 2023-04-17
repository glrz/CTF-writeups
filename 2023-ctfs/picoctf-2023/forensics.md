# Forensics

## hideme

<figure><img src="../../.gitbook/assets/image (3) (7).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.png` file. Viewing the file would show an image of `PicoCTF`.

<figure><img src="../../.gitbook/assets/image (4) (4).png" alt=""><figcaption></figcaption></figure>

I ran `exiftool` but could not find any useful information.

I then ran `binwalk` and found that there was a `flag.png` in this image.

```bash
┌──(kali㉿kali)-[~/Downloads/results]
└─$ binwalk trailing_data.bin   

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             Zip archive data, at least v1.0 to extract, name: secret/
65            0x41            Zip archive data, at least v2.0 to extract, compressed size: 2797, uncompressed size: 2947, name: secret/flag.png
3097          0xC19           End of Zip archive, footer length: 22
```

I used the `-e` option to extract the `flag.png` and opened the image.

```bash
┌──(kali㉿kali)-[~/Downloads/results]
└─$ binwalk -e trailing_data.bin

┌──(kali㉿kali)-[~/Downloads/results/_trailing_data.bin.extracted/secret]
└─$ eog flag.png
```

<figure><img src="../../.gitbook/assets/image (6) (4).png" alt=""><figcaption></figcaption></figure>

However, the top of the image looked slighly cut off. I checked the height and width in exiftool and it was the same in the hex editor.&#x20;

Running this script based on its `CRC32` value also showed the correct height and width.

```python
import binascii
import struct

crcbp = open("flag.png", "rb").read()
for i in range(3000):
    for j in range(3000):
        data = crcbp[12:16] + struct.pack('>i', i)+struct.pack('>i', j)+crcbp[24:29]
        crc32 = binascii.crc32(data) & 0xffffffff
        if(crc32 == 0xF56D2656):
            print(i, j)
            print('hex:', hex(i), hex(j))
```

<figure><img src="../../.gitbook/assets/image (2) (8).png" alt=""><figcaption></figcaption></figure>

Even though the top of the image was slightly cut off, I was still able to get the flag nonetheless.&#x20;

Flag: picoCTF{Hiddinng\_An\_imag3\_within\_@n\_ima9e\_6f0d0103}

## PcapPoisoning

<figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.pcap` file.

First, we could open it in `Wireshark` to analyze the packets.

There were quite a number of packets to analyze.

<figure><img src="../../.gitbook/assets/image (12) (1) (3).png" alt=""><figcaption></figcaption></figure>

So I thought.. why not let me try this quick "hack", where I can quickly search for the flag in these packet. By using `strings` on the pcap file and `grep` to search for the flag format, I was able to get the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ strings trace.pcap| grep pico
picoCTF{P64P_4N4L7S1S_SU55355FUL_b9e1bc54}=0
```

Flag: picoCTF{P64P\_4N4L7S1S\_SU55355FUL\_b9e1bc54}

## who is it

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

For this challenge, we can download the `.eml` email file.

{% file src="../../.gitbook/assets/email-export.eml" %}

If we read the contents of it, we will get the following

```
Delivered-To: francismanzi@gmail.com
Received: by 2002:ab0:638a:0:0:0:0:0 with SMTP id y10csp123720uao;
        Thu, 7 Jul 2022 23:19:48 -0700 (PDT)
X-Google-Smtp-Source: AGRyM1u8MgQ0wT0JmPs4nZbKyuwluXeP+mglR/hb66VElgQnwB8M2ofwYUFsHj+eMYBFAVDPITJc
X-Received: by 2002:a5d:6d06:0:b0:21b:c434:d99e with SMTP id e6-20020a5d6d06000000b0021bc434d99emr1524437wrq.148.1657261188086;
        Thu, 07 Jul 2022 23:19:48 -0700 (PDT)
ARC-Seal: i=1; a=rsa-sha256; t=1657261188; cv=none;
        d=google.com; s=arc-20160816;
        b=FJZQS4geDnyabQ7SUhA2v3roEqcufLmysXkLoRZd3yNXiNQFBFmwm5v5yANvDyyebA
         Jfjqv5X8Gujll585xj/MHlVhlEMg0edNWuwnLXj8SmNuPI1Jon9N+fokhSMxy2WxSACE
         4MruPo5QBlHdrFq8WNBAFgC1VtO0nR+BQYY18wqotLIQPvkXo3yOUUhx0D+ZjUwXvTKV
         yUFGdYulF58Lg7wAH/cLWROIHrraWTSsmaGWoYv577nztzueoG5RC5uUAGIAyzsJRqsV
         dCsapFxCUlbYbAgIVraylksCA+veFXfil6ocym8KKnls3j40Vojv0VLhHHZxXruG5x/K
         M5cQ==
ARC-Message-Signature: i=1; a=rsa-sha256; c=relaxed/relaxed; d=google.com; s=arc-20160816;
        h=mime-version:message-id:date:subject:to:from:dkim-signature;
        bh=RneTbuEOZUlwei4ZNPvzjmZpQE92irBmuzImA33zPEc=;
        b=RUd+ycq1YWbRNn9wB8UgJ8dZz0tHpvmqcEGQkWqzLy/6j3aFzaf7dwdoCtXjTTtrrE
         z9g498cmB55fs0x1CAjtzI+Nctb1cbPcnfMCrfsF3LwgYhCErFRnbBbOgqw4eeEB+hk0
         sKBN0QVpSLs1HlF8ZK3XiMKA2p3vSgHlbhMDPGnFTLHEQjlM63d/L30Rt8mpQsT77ni/
         f6X0TqTi4Y8ARIuEELMa6m5E5wQcfUxeUU5WAssz46tQyHKR6xg/g8K2zES+gSNymASk
         c5Eaq55k4Zi8dXWaPIwg4IdhVLVxe4llMx8c46GTdh8tvdMtmjME3wIaFR6Q2SLWRSZA
         o0hw==
ARC-Authentication-Results: i=1; mx.google.com;
       dkim=pass header.i=@onionmail.org header.s=jan2022 header.b=4sU2nk5Z;
       spf=pass (google.com: domain of lpage@onionmail.org designates 173.249.33.206 as permitted sender) smtp.mailfrom=lpage@onionmail.org;
       dmarc=pass (p=NONE sp=NONE dis=NONE) header.from=onionmail.org
Return-Path: <lpage@onionmail.org>
Received: from mail.onionmail.org (mail.onionmail.org. [173.249.33.206])
        by mx.google.com with ESMTPS id f16-20020a05600c4e9000b003a1947873d6si1882702wmq.224.2022.07.07.23.19.47
        for <francismanzi@gmail.com>
        (version=TLS1_3 cipher=TLS_AES_256_GCM_SHA384 bits=256/256);
        Thu, 07 Jul 2022 23:19:47 -0700 (PDT)
Received-SPF: pass (google.com: domain of lpage@onionmail.org designates 173.249.33.206 as permitted sender) client-ip=173.249.33.206;
Authentication-Results: mx.google.com;
       dkim=pass header.i=@onionmail.org header.s=jan2022 header.b=4sU2nk5Z;
       spf=pass (google.com: domain of lpage@onionmail.org designates 173.249.33.206 as permitted sender) smtp.mailfrom=lpage@onionmail.org;
       dmarc=pass (p=NONE sp=NONE dis=NONE) header.from=onionmail.org
DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/relaxed; d=onionmail.org;
 q=dns/txt; s=jan2022; bh=RneTbuEOZUlwei4ZNPvzjmZpQE92irBmuzImA33zPEc=;
 h=from:subject:date:message-id:to:mime-version:content-type;
 b=4sU2nk5ZG4F9+lCtCPU4nat6ovALqfOHOUM1/wTskeMdmMAa2yOMXy0GkqolIioL8nG0mRG45
 OD8b/nHZZEiA0aQppYHECSmXE7IFIFm/MP9wmXIlC/cDF1t9mEwumdDbes7hRhiO6q3A0wYWK+J
 C+qwHI99irsPhWZOptVVh0HV/HJPAtkzg7OBMX/oPDUSG3xo7dJvT5MCYUm2+4CBVjvLmEPUVTO
 uuVEU3HjVjumry5zw1H4s+o9jxCOwpT41uL94NM64Aki4+KIlS75W8Uo1YStqciHSHoEPLMvBhK
 OMfwhI02u5oLFbk6ZvmhyK5juc54lGbWgk277N0hB0Aw==
Received: from localhost
 by mail.onionmail.org (ZoneMTA) with API id 181dc76dff2000ccee.001
 for <francismanzi@gmail.com>;
 Fri, 08 Jul 2022 06:19:47 +0000
X-Zone-Loop: 83440723a48cf749c9e7702024ee772d7cb2fb7cab7a
Content-Type: multipart/mixed; boundary="--_NmP-426c22a2e0d8fc9a-Part_1"
From: Larry Page <lpage@onionmail.org>
To: francismanzi@gmail.com
Subject: One million Prize
Date: Fri, 08 Jul 2022 06:19:47 +0000
Message-ID: <03c11cd1-8fd9-584e-c9d7-e53df0faeccc@onionmail.org>
MIME-Version: 1.0

----_NmP-426c22a2e0d8fc9a-Part_1
Content-Type: multipart/alternative;
 boundary="--_NmP-426c22a2e0d8fc9a-Part_2"

----_NmP-426c22a2e0d8fc9a-Part_2
Content-Type: text/plain; charset=utf-8
Content-Transfer-Encoding: quoted-printable

Hello dear user, I am Larry Page and I am delighted to announce to you that=
 you
are the 99999999th GMAIL account and for that we want to reward you. =
You've
earned $1,000,000. To claim your prize open the attached file.
----_NmP-426c22a2e0d8fc9a-Part_2
Content-Type: text/html; charset=utf-8
Content-Transfer-Encoding: quoted-printable

<p>Hello dear user, I am Larry Page and I am delighted to announce to you =
that you are the 99999999th GMAIL account and for that we want to reward =
you. You've earned $1,000,000. To claim your prize open the attached file.=
<br></p>
----_NmP-426c22a2e0d8fc9a-Part_2--

----_NmP-426c22a2e0d8fc9a-Part_1
Content-Type: text/plain; name=attachment.txt
Content-Transfer-Encoding: base64
Content-Disposition: attachment; filename=attachment.txt

QW1vdW50OiAgJDEsMDAwLDAwMAo=
----_NmP-426c22a2e0d8fc9a-Part_1--
```

We can copy paste this into [MxTOOLBOX email header analyzer](https://mxtoolbox.com/EmailHeaders.aspx).

<figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

This would give us the `IP address` of the mail server which was blacklisted.

Finally, we can run `whois` command and find the flag under `person`.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ whois 173.249.33.206                             

#
# ARIN WHOIS data and services are subject to the Terms of Use
# available at: https://www.arin.net/resources/registry/whois/tou/
#
# If you see inaccuracies in the results, please report at
# https://www.arin.net/resources/registry/whois/inaccuracy_reporting/
#
# Copyright 1997-2023, American Registry for Internet Numbers, Ltd.
#


NetRange:       173.249.0.0 - 173.249.63.255
CIDR:           173.249.0.0/18
NetName:        RIPE
NetHandle:      NET-173-249-0-0-1
Parent:         NET173 (NET-173-0-0-0-0)
NetType:        Early Registrations, Transferred to RIPE NCC
OriginAS:       
Organization:   RIPE Network Coordination Centre (RIPE)
RegDate:        2017-09-14
Updated:        2017-09-14
Ref:            https://rdap.arin.net/registry/ip/173.249.0.0

ResourceLink:  https://apps.db.ripe.net/search/query.html
ResourceLink:  whois://whois.ripe.net


OrgName:        RIPE Network Coordination Centre
OrgId:          RIPE
Address:        P.O. Box 10096
City:           Amsterdam
StateProv:      
PostalCode:     1001EB
Country:        NL
RegDate:        
Updated:        2013-07-29
Ref:            https://rdap.arin.net/registry/entity/RIPE

ReferralServer:  whois://whois.ripe.net
ResourceLink:  https://apps.db.ripe.net/search/query.html

OrgAbuseHandle: ABUSE3850-ARIN
OrgAbuseName:   Abuse Contact
OrgAbusePhone:  +31205354444 
OrgAbuseEmail:  abuse@ripe.net
OrgAbuseRef:    https://rdap.arin.net/registry/entity/ABUSE3850-ARIN

OrgTechHandle: RNO29-ARIN
OrgTechName:   RIPE NCC Operations
OrgTechPhone:  +31 20 535 4444 
OrgTechEmail:  hostmaster@ripe.net
OrgTechRef:    https://rdap.arin.net/registry/entity/RNO29-ARIN


#
# ARIN WHOIS data and services are subject to the Terms of Use
# available at: https://www.arin.net/resources/registry/whois/tou/
#
# If you see inaccuracies in the results, please report at
# https://www.arin.net/resources/registry/whois/inaccuracy_reporting/
#
# Copyright 1997-2023, American Registry for Internet Numbers, Ltd.
#



Found a referral to whois.ripe.net.

% This is the RIPE Database query service.
% The objects are in RPSL format.
%
% The RIPE Database is subject to Terms and Conditions.
% See http://www.ripe.net/db/support/db-terms-conditions.pdf

% Note: this output has been filtered.
%       To receive output for a database update, use the "-B" flag.

% Information related to '173.249.32.0 - 173.249.63.255'

% Abuse contact for '173.249.32.0 - 173.249.63.255' is 'abuse@contabo.de'

inetnum:        173.249.32.0 - 173.249.63.255
netname:        CONTABO
descr:          Contabo GmbH
country:        DE
org:            ORG-GG22-RIPE
admin-c:        MH7476-RIPE
tech-c:         MH7476-RIPE
status:         ASSIGNED PA
mnt-by:         MNT-CONTABO
created:        2018-08-22T07:28:02Z
last-modified:  2018-08-22T07:28:02Z
source:         RIPE

organisation:   ORG-GG22-RIPE
org-name:       Contabo GmbH
country:        DE
org-type:       LIR
remarks:        * Please direct all complaints about Internet abuse like Spam, hacking or scans *
remarks:        * to abuse@contabo.de . This will guarantee fastest processing possible. *
address:        Aschauer Strasse 32a
address:        81549
address:        Munchen
address:        GERMANY
phone:          +498921268372
fax-no:         +498921665862
abuse-c:        MH12453-RIPE
mnt-ref:        RIPE-NCC-HM-MNT
mnt-ref:        MNT-CONTABO
mnt-ref:        MNT-OCIRIS
mnt-by:         RIPE-NCC-HM-MNT
mnt-by:         MNT-CONTABO
created:        2009-12-09T13:41:08Z
last-modified:  2021-09-14T10:49:04Z
source:         RIPE # Filtered

person:         Wilhelm Zwalina
address:        Contabo GmbH
address:        Aschauer Str. 32a
address:        81549 Muenchen
phone:          +49 89 21268372
fax-no:         +49 89 21665862
nic-hdl:        MH7476-RIPE
mnt-by:         MNT-CONTABO
mnt-by:         MNT-GIGA-HOSTING
created:        2010-01-04T10:41:37Z
last-modified:  2020-04-24T16:09:30Z
source:         RIPE

% Information related to '173.249.32.0/23AS51167'

route:          173.249.32.0/23
descr:          CONTABO
origin:         AS51167
mnt-by:         MNT-CONTABO
created:        2018-02-01T09:50:10Z
last-modified:  2018-02-01T09:50:10Z
source:         RIPE

% This query was served by the RIPE Database Query Service version 1.106 (ABERDE
```

Flag: picoCTF{WilhelmZwalina}

## FindAndOpen

<figure><img src="../../.gitbook/assets/image (19) (1).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.pcap` file.

First, I opened it in `Wireshark` to further analyze what's going on.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ wireshark dump.pcap
```

At first glance, I noticed that the flag could have been splitted. Additionally, I also noticed some interesting strings which looked encoded.

<figure><img src="../../.gitbook/assets/image (17) (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (11) (1) (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

I copied those interesting strings down which gave the following

```
iBwaWNvQ1RGe1
AABBHHPJGTFRLKVGhpcyBpcyB0aGUgc2VjcmV0OiBwaWNvQ1RGe1IzNERJTkdfTE9LZF8=
PBwaWUvQ1RGesabababkjaASKBKSBACVVAVSDDSSSSDSKJBJS
PBwaWUvQ1RGe1
```

I copied these strings in `CyberChef` and used the following [recipe](https://cyberchef.org/#recipe=From\_Base64\('A-Za-z0-9%2B/%3D',true,false\)\&input=aUJ3YVdOdlExUkdlMQpBQUJCSEhQSkdURlJMS1ZHaHBjeUJwY3lCMGFHVWdjMlZqY21WME9pQndhV052UTFSR2UxSXpORVJKVGtkZlRFOUxaRjg9ClBCd2FXVXZRMVJHZXNhYmFiYWJramFBU0tCS1NCQUNWVkFWU0REU1NTU0RTS0pCSlMKUEJ3YVdVdlExUkdlMQoKaUJ3YVdOdlExUkdlMUFBQkJISFBKR1RGUkxLVkdocGN5QnBjeUIwYUdVZ2MyVmpjbVYwT2lCd2FXTnZRMVJHZTFJek5FUkpUa2RmVEU5TFpGOD0), which decodes using `Base64` by joining the first two strings.

This would give us what seemed like a partial flag.

<figure><img src="../../.gitbook/assets/image (14) (1).png" alt=""><figcaption></figcaption></figure>

I used this as the password to unlock the `.zip` file provided and managed to unzipped it.

Password: `picoCTF{R34DING_LOKd_`

Reading the contents in `flag` would give us the full flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ unzip flag.zip      
Archive:  flag.zip
[flag.zip] flag password: 
 extracting: flag          
┌──(kali㉿kali)-[~/Downloads]
└─$ cat flag     
picoCTF{R34DING_LOKd_fil56_succ3ss_1b40c358}
```

Flag: picoCTF{R34DING\_LOKd\_fil56\_succ3ss\_1b40c358}

## MSB

<figure><img src="../../.gitbook/assets/image (1) (7).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.png` image.

{% file src="../../.gitbook/assets/Ninja-and-Prince-Genji-Ukiyoe-Utagawa-Kunisada.flag (2).png" %}

As this was a `steganography` challenge, I ran `stegoveritas` once again.

It looked like it found something worth keeping!

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ stegoveritas Ninja-and-Prince-Genji-Ukiyoe-Utagawa-Kunisada.flag.png 
Running Module: SVImage
+---------------------------+------+
|        Image Format       | Mode |
+---------------------------+------+
| Portable network graphics | RGB  |
+---------------------------+------+
Found something worth keeping!
ASCII text
+--------+------------------+-----------------------------------------------------------------------------------------------+-----------+
| Offset | Carved/Extracted | Description                                                                                   | File Name |
+--------+------------------+-----------------------------------------------------------------------------------------------+-----------+
| 0x460d | Carved           | LZMA compressed data, properties: 0xBE, dictionary size: 0 bytes, uncompressed size: 64 bytes | 460D.7z   |
| 0x460d | Extracted        | LZMA compressed data, properties: 0xBE, dictionary size: 0 bytes, uncompressed size: 64 bytes | 460D      |
+--------+------------------+-----------------------------------------------------------------------------------------------+-----------+
Found something worth keeping!
Common Data Format (Version 2.5 or earlier) data
Found something worth keeping!
Matlab v4 mat-file (little endian) UUUUUUUU, numeric, rows 4294967295, columns 4294967295
Running Module: MultiHandler

Exif
====
+---------------------+------------------------------------------------------------------------------+
| key                 | value                                                                        |
+---------------------+------------------------------------------------------------------------------+
| SourceFile          | /home/kali/Downloads/Ninja-and-Prince-Genji-Ukiyoe-Utagawa-Kunisada.flag.png |
| ExifToolVersion     | 12.44                                                                        |
| FileName            | Ninja-and-Prince-Genji-Ukiyoe-Utagawa-Kunisada.flag.png                      |
| Directory           | /home/kali/Downloads                                                         |
| FileSize            | 3.4 MB                                                                       |
| FileModifyDate      | 2023:03:15 03:20:35-04:00                                                    |
| FileAccessDate      | 2023:03:15 03:20:41-04:00                                                    |
| FileInodeChangeDate | 2023:03:15 03:20:35-04:00                                                    |
| FilePermissions     | -rw-r--r--                                                                   |
| FileType            | PNG                                                                          |
| FileTypeExtension   | png                                                                          |
| MIMEType            | image/png                                                                    |
| ImageWidth          | 1074                                                                         |
| ImageHeight         | 1500                                                                         |
| BitDepth            | 8                                                                            |
| ColorType           | RGB                                                                          |
| Compression         | Deflate/Inflate                                                              |
| Filter              | Adaptive                                                                     |
| Interlace           | Noninterlaced                                                                |
| ImageSize           | 1074x1500                                                                    |
| Megapixels          | 1.6                                                                          |
+---------------------+------------------------------------------------------------------------------+
Found something worth keeping!
PNG image data, 1074 x 1500, 8-bit/color RGB, non-interlaced
+--------+------------------+-------------------------------------------+-----------+
| Offset | Carved/Extracted | Description                               | File Name |
+--------+------------------+-------------------------------------------+-----------+
| 0x29   | Carved           | Zlib compressed data, default compression | 29.zlib   |
| 0x29   | Extracted        | Zlib compressed data, default compression | 29        |
+--------+------------------+-------------------------------------------+-----------+
```

I found some interesting content once I navigated to the `keepers` directory and ran the `strings` command.

While I was scrolling through the long bunch of strings, I found the flag.

Alternatively, since the bunch of strings were too long to go through or paste here, we could run the `grep` command to search for the flag&#x20;

The `-r` option will search recursively in the `keepers` directory for a file which contained `pico` string.

```bash
┌──(kali㉿kali)-[~/Downloads/results/keepers]
└─$ grep -r pico   
1678926400.9391677-f14af6a3474944fc4a572c64585ce594:picoCTF{15_y0ur_que57_qu1x071c_0r_h3r01c_a02297a7}
```

We could also run `strings` directly on the file with `grep` as such

```
┌──(kali㉿kali)-[~/Downloads/results/keepers]
└─$ strings 1678926400.9391677-f14af6a3474944fc4a572c64585ce594 | grep pico
picoCTF{15_y0ur_que57_qu1x071c_0r_h3r01c_a02297a7}
```

Flag: picoCTF{15\_y0ur\_que57\_qu1x071c\_0r\_h3r01c\_a02297a7}

