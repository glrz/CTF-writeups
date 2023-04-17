---
description: >-
  This mini challenge was posted on CSIT's LinkedIn page on the 19 Jan and was
  available for solving till 5 Feb 2023.
---

# CSIT CNY 2023 Challenge

Last year, CSIT also had a [`CNY 2022 Easter Egg Challenge`](https://www.linkedin.com/feed/update/urn:li:activity:6892384942458843136/). If I remembered correctly, that challenge was pretty easy and I solved it by using `Base64 decoder` after scanning a `QR Code`.

<figure><img src="../.gitbook/assets/image (4) (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

For this year's challenge, I found it to be more interesting and slightly more challenging. On CSIT LinkedIn page, we were presented with a short video of 7 seconds in the post. Taking a closer look, I saw that there was a QR Code that appeared in the video at around 2-3 seconds mark. Shortly after, it disappears at around 5 seconds mark.&#x20;

Can you spot it?

<figure><img src="../.gitbook/assets/image (33) (1).png" alt=""><figcaption></figcaption></figure>

However, if we tried to scan the QR code at around 2-3 seconds into the video, it probably won't work because the QR code is still blurred. I managed to scan the QR code at the 4 seconds mark by using my phone to scan it on my monitor screen, which leads me to the [challenge link](https://www.csit-events.sg/cny2023-easter-egg-challenge-huat-ah).

Upon reaching the challenge page, we were presented with the challenge description, some instructions and a challenge file.

<figure><img src="../.gitbook/assets/image (3) (3).png" alt=""><figcaption></figcaption></figure>

{% file src="../.gitbook/assets/special_hong_bao.7z" %}

We were also given some additional resources to understand more about Alternate Data Steams (ADS).

<figure><img src="../.gitbook/assets/image (2) (3).png" alt=""><figcaption></figcaption></figure>

Additional Resources

Overview of ADS:&#x20;

·     [https://blog.netwrix.com/2022/12/16/alternate\_data\_stream/](https://blog.netwrix.com/2022/12/16/alternate\_data\_stream/)&#x20;

Example usage of ADS:&#x20;

·    [https://textslashplain.com/2016/04/04/downloads-and-the-mark-of-the-web/](https://textslashplain.com/2016/04/04/downloads-and-the-mark-of-the-web/)&#x20;

If we scroll up, the challenge provided us with some instructions, that is, to download the file, on Windows, use 7zip to extract the file and find the flag within the file. However, for this challenge, I decided to try another approach by solving it on my Kali Linux VM instead. This is probably the unintended solution and I'll split my writeup into 2 parts for this challenge.

Note that solving this challenge is not sequential. This means that you could solve for `Part 1` first then  `Part 2` and  vice versa.

## Part 1

First, we could open this file in a simple text editor like Notepad to analyze its contents. Once we open the file in Notepad, we should notice that there are strings appended with `=` and `==`, which likely suggest that this could be `Base64 encoded.`

<figure><img src="../.gitbook/assets/image (17) (1) (1).png" alt=""><figcaption></figcaption></figure>

Alternatively, we could run `strings` command on UNIX and we would get these strings output as well.\
┌──(kali㉿kali)-\[\~/Downloads]

└─$ strings special\_hong\_bao.7z

MSWIM

root@csit:\~# ./future

Q1NJVCBpcyBhIHRlY2ggYWdlbmN5IHVuZGVyIE1JTkRFRiB0aGF0IGhhcm5lc3NlcyBjdXR0aW5nLWVkZ2UgZGlnaXRhbCB0ZWNobm9sb2dpZXMgdG8gbWVldCBTaW5nYXBvcmUncyBzZWN1cml0eSBuZWVkcy4=

Q1NJVCBzdXBwb3J0cyBuYXRpb25hbCBzZWN1cml0eSBtaXNzaW9ucyBzdWNoIGFzIGN5YmVyIGRlZmVuY2UsIGNvdW50ZXItdGVycm9yaXNtLCBhbmQgY291bnRlci1ob3N0aWxlIGluZm9ybWF0aW9uIG9wZXJhdGlvbnMu

Q1NJVHskODg4X2hBUHBZX1kzQFJfMGZfckA4YjFUfQ==

VGhlIG1lc3NhZ2VzIGFuZCBmbGFnIGFyZSBlbmNvZGVkIHVzaW5nIGJhc2U2NCE=

SHVhdCBBaCEgQ1NJVCB3aXNoZXMgeW91IGEgcHJvc3Blcm91cyB5ZWFyIG9mIHRoZSBSYWJiaXQh

Q1NJVCdzIHRlY2ggZm9jdXMgYXJlYXMgaW5jbHVkZSBDeWJlcnNlY3VyaXR5LCBTb2Z0d2FyZSBFbmdpbmVlcmluZywgRGF0YSBBbmFseXRpY3MgYW5kIENsb3VkIEluZnJhc3RydWN0dXJlIGFuZCBTZXJ2aWNlcy4=

aHR0cHM6Ly9lbi53aWtpcGVkaWEub3JnL3dpa2kvODgxXyhmaWxtKQ==

SHVhdCBBaCEgVW5mb3J0dW5hdGVseSB0aGUgZmxhZyBpcyBub3QgaGVyZS4gTWF5YmUgdGhlIGZsYWcgZm9ybWF0IHdpbGwgaGVscCB5b3Ugb3V0Pw==

4zr!

\#x7x

4zr!

\#x7x

We could paste this into [CyberChef](https://cyberchef.org/#recipe=From\_Base64\('A-Za-z0-9%2B/%3D',true,false\)\&input=UTFOSlZDQnBjeUJoSUhSbFkyZ2dZV2RsYm1ONUlIVnVaR1Z5SUUxSlRrUkZSaUIwYUdGMElHaGhjbTVsYzNObGN5QmpkWFIwYVc1bkxXVmtaMlVnWkdsbmFYUmhiQ0IwWldOb2JtOXNiMmRwWlhNZ2RHOGdiV1ZsZENCVGFXNW5ZWEJ2Y21VbmN5QnpaV04xY21sMGVTQnVaV1ZrY3k0PQpRMU5KVkNCemRYQndiM0owY3lCdVlYUnBiMjVoYkNCelpXTjFjbWwwZVNCdGFYTnphVzl1Y3lCemRXTm9JR0Z6SUdONVltVnlJR1JsWm1WdVkyVXNJR052ZFc1MFpYSXRkR1Z5Y205eWFYTnRMQ0JoYm1RZ1kyOTFiblJsY2kxb2IzTjBhV3hsSUdsdVptOXliV0YwYVc5dUlHOXdaWEpoZEdsdmJuTXUKUTFOSlZIc2tPRGc0WDJoQlVIQlpYMWt6UUZKZk1HWmZja0E0WWpGVWZRPT0KVkdobElHMWxjM05oWjJWeklHRnVaQ0JtYkdGbklHRnlaU0JsYm1OdlpHVmtJSFZ6YVc1bklHSmhjMlUyTkNFPQpTSFZoZENCQmFDRWdRMU5KVkNCM2FYTm9aWE1nZVc5MUlHRWdjSEp2YzNCbGNtOTFjeUI1WldGeUlHOW1JSFJvWlNCU1lXSmlhWFFoClExTkpWQ2R6SUhSbFkyZ2dabTlqZFhNZ1lYSmxZWE1nYVc1amJIVmtaU0JEZVdKbGNuTmxZM1Z5YVhSNUxDQlRiMlowZDJGeVpTQkZibWRwYm1WbGNtbHVaeXdnUkdGMFlTQkJibUZzZVhScFkzTWdZVzVrSUVOc2IzVmtJRWx1Wm5KaGMzUnlkV04wZFhKbElHRnVaQ0JUWlhKMmFXTmxjeTQ9CmFIUjBjSE02THk5bGJpNTNhV3RwY0dWa2FXRXViM0puTDNkcGEya3ZPRGd4WHlobWFXeHRLUT09ClNIVmhkQ0JCYUNFZ1ZXNW1iM0owZFc1aGRHVnNlU0IwYUdVZ1pteGhaeUJwY3lCdWIzUWdhR1Z5WlM0Z1RXRjVZbVVnZEdobElHWnNZV2NnWm05eWJXRjBJSGRwYkd3Z2FHVnNjQ0I1YjNVZ2IzVjBQdz09) and would get the following decoded output. If we look closely, we have found the flag in the bunch of decoded message. The flag is in `CSIT {...}` format as given by the hint in the challenge textbox placeholder.\


<figure><img src="../.gitbook/assets/image (13) (1) (2).png" alt=""><figcaption></figcaption></figure>

We could copy-paste the `Base64 encoded` string on `CyberChef` again to confirm the flag.\


<figure><img src="../.gitbook/assets/image (1) (3) (1).png" alt=""><figcaption><p>Q1NJVHskODg4X2hBUHBZX1kzQFJfMGZfckA4YjFUfQ==</p></figcaption></figure>

Flag: CSIT{$888\_hAPpY\_Y3@R\_0f\_r@8b1T}

## Part 2

Moving on, we will need to find out the stream name of the ADS. After reading through the additional resources provided, I understood how ADS is created and we could simply append a colon `:` to the file name or path, followed by the stream name. Since the colon is a reserved character not allowed in a filename, it doesn’t conflict with existing file names.

Knowing this, we would need to find the stream name which is after the colon `:`

On Linux, we could use the `7z x` command to extract the file. Although we should also note that this file is not a 7zip file, but rather a Windows imaging image when verified with the `file` command.

```
┌──(kali㉿kali)-[~/Downloads]
└─$ file special_hong_bao.7z 
special_hong_bao.7z: Windows imaging (WIM) image v1.13, reparse point fixup
```

We can still extract it as such&#x20;

```
┌──(kali㉿kali)-[~/Downloads]
└─$ 7z x special_hong_bao.7z 

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 66593 bytes (66 KiB)

Extracting archive: special_hong_bao.7z
WARNING: 
special_hong_bao.7z
Can not open the file as [7z] archive
The file is open as [wim] archive

--
Path = special_hong_bao.7z
Open WARNING: Can not open the file as [7z] archive
Type = wim
Physical Size = 66593
Size = 901
Packed Size = 901
Method = Copy:15
Cluster Size = 32768
Created = 2023-01-13 08:54:58
Modified = 2023-01-13 08:54:58
Comment = <WIM><TOTALBYTES>65899</TOTALBYTES><IMAGE INDEX="1"><NAME>1</NAME><DIRCOUNT>0</DIRCOUNT><FILECOUNT>1</FILECOUNT><TOTALBYTES>5</TOTALBYTES><CREATIONTIME><HIGHPART>0x01D92756</HIGHPART><LOWPART>0x9F961134</LOWPART></CREATIONTIME><LASTMODIFICATIONTIME><HIGHPART>0x01D92756</HIGHPART><LOWPART>0x9F961134</LOWPART></LASTMODIFICATIONTIME></IMAGE></WIM>
Version = 1.13
Multivolume = -
Volume = 1
Volumes = 1
Images = 1

Everything is Ok

Archives with Warnings: 1
Files: 1
Alternate Streams: 1000
Alternate Streams Size: 5851
Size:       5
Compressed: 66593

```

Now if we ran the `ls` command to check the files in the directory, we would see a bunch of ADS.\


<figure><img src="../.gitbook/assets/image (8) (2).png" alt=""><figcaption></figcaption></figure>

How could we look for the ADS which contains the flag? Going through and reading the contents of all 1000 of alternate streams manually in Linux would probably not be the best idea and would be too time-consuming.&#x20;

Since the secret message could be saved into the ADS using commands like `echo`,   we could try to `grep` for the flag. By using the `-r` option, we `grep` through all the files in the directory recursively and we are able to get the file name which contains the flag. Here's a pretty good [documentation](https://www.cyberciti.biz/faq/howto-search-find-file-for-text-string/) on Finding a File Containing a Particular Text String In Linux Server.&#x20;

Note that grep is a very powerful and useful tool. Some other instances where I used grep and specified different options such as `-a` or `-E` can be found [here](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/lagncrash-interpoly-ctf-2022#plumber) and [here](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/lagncrash-interpoly-ctf-2022#plumber).\


```
┌──(kali㉿kali)-[~/Downloads]
└─$ grep -r Q1NJVHs special_hong_bao.txt:*
special_hong_bao.txt:hidden588:Q1NJVHskODg4X2hBUHBZX1kzQFJfMGZfckA4YjFUfQ== 
```

Note that here I was trying to grep `Q1NJVHs` which is basically the `Base64 encoded` form of `CSIT{`

This would give us the stream name of the ADS where the flag can be found.\


<figure><img src="../.gitbook/assets/image (20) (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

Alternatively, we could also use a tool like [ADS Manager](https://dmitrybrant.com/adsmanager) to search through those with `size` greater than 5, since most of the ADS size were `5` and those that are greater likely suggest that there are hidden messages. From here, we could decode the `Base64` encoded string and get the flag as well.\


<figure><img src="../.gitbook/assets/image (3) (2) (1).png" alt=""><figcaption></figcaption></figure>

Stream name: hidden588

You might also be interested in this [blog](https://tmairi.github.io/posts/extracting-alternate-data-streams-with-linux/) which is about Extracting Alternate Data Streams with Linux.

Submitting the flag and stream name shows that it is the correct answer!\


<figure><img src="../.gitbook/assets/image (14) (2).png" alt=""><figcaption></figcaption></figure>

As a forensics enthusiast, I really enjoyed the process of solving this challenge. After attempting and solving this challenge, I learned more about ADS and how 7-zip could be vulnerable to hide malware. Malware within a 7-zip archive can be extracted without propagation of the MotW. 7-zip v15.14 _will_ add a MotW if we double-click an exe within an archive, but _not_ if we extract it first. The older 7-zip v9.2 _did not_ tag with MotW either way.

Although this was my first time attempting a challenge on NTFS and ADS which I had no prior knowledge, I am glad I managed to quickly pick up the concepts and solved it within the same day the challenge was released. In fact, I solved this challenge within 30 minutes at first attempt :)

<figure><img src="../.gitbook/assets/image (16) (2).png" alt=""><figcaption></figcaption></figure>

After solving it, I got a digital badge which looked awesome! Looking forward to more of such challenges in the coming years.

<figure><img src="../.gitbook/assets/image (12) (2).png" alt=""><figcaption></figcaption></figure>
