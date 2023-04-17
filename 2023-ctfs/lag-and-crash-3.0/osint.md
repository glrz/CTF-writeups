# Osint

## Container

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.zip` file. We could extract the contents from the zip file which would give us an image of container.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ file container.zip      
container.zip: Zip archive data, at least v2.0 to extract, compression method=deflate
                                                                                                                   
┌──(kali㉿kali)-[~/Downloads]
└─$ 7z x container.zip   

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 155869 bytes (153 KiB)

Extracting archive: container.zip
--
Path = container.zip
Type = zip
Physical Size = 155869

Everything is Ok

Size:       155721
Compressed: 155869
                                                                                                                   
┌──(kali㉿kali)-[~/Downloads]
└─$ eog Container.jpg 
```

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

If we look at the container in the middle, we can see its `Prefix + Container number + Check digit`

We can use that information: `LGEU4513799` to get the more information [here](https://alltrack.org/container/CARU-caru-containers-tracking?Company%5Bcontainer%5D=CARU4835855\&yt0=).

If we scroll down, we would see an [attachment](https://portal.carucontainers.com/scripts/caruweb02.wsc/WService=caru/system/web/sp-web-stream\_attachment.r?attachmentnr=4481682\&attseqnr=3\&companycode=CS\&accesstoken=ccbdfjbabEakddhQ).

In the attachment, we can find the CSC number: `NL-LR 70003-03/07` and control number: `RET42976`.

Flag: LNC2023{NL-LR 70003-03/07\_RET42976}

## The Man With No Name

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a website link.

We can browse to the website and see many different pages and posts content.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

There's a page which prompts us for password to enter. I guess the flag could be in here. But what is the password?

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

If we notice in previous pages, there is one thing in common. That is the postal code number appears on every page at the bottom.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Could that be the password? Lets try it out!

Indeed, the password is `596303`. Upon entering the password, we are redirected to this site where we could `CTRL+F` to search for the flag.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Flag: LNC2023{Wh@ts\_My\_N@m3}
