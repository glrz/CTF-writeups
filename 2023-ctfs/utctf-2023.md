---
description: UTCTF 2023 was held from 11 Mar - 13 Mar 2023.
---

# UTCTF 2023

More information about the event can be found [here](https://ctftime.org/event/1919).

For this CTF competition, I dedicated a few hours to solve some challenges. I managed to quickly pick up new tools like `smbclient` and `smbmap` to solve a network challenge.&#x20;

I participated solo with team name: `T34M1`. The last time I participated solo with this same team name was in 2020/2021.&#x20;

The scoreboard is shown below.

<figure><img src="../.gitbook/assets/image (12) (1) (2).png" alt=""><figcaption></figcaption></figure>

A total of 5 challenges were solved.

<figure><img src="../.gitbook/assets/image (6) (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (7) (4).png" alt=""><figcaption></figcaption></figure>

I was pretty satisfied with the results in general because I managed to solve more challenges as compared to when I first started out playing most of the non-local CTFs in 2020 and 2021.

## Dry Run

<figure><img src="../.gitbook/assets/image (7) (2).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was pretty easy and straightforward.

To join the Discord server, we will first need to go back to the main page to find the link.

<figure><img src="../.gitbook/assets/image (17) (3).png" alt=""><figcaption></figcaption></figure>

Upon clicking the `Discord`, we will get the invite link which will allow us access to the server.

Once we enter the server, we will need to press the `tick` icon to indicate that we have read the rules and to have access to other channels.

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

After the access to other channels is granted, we can navigate to the `announcements` channel and look under `Pinned Messages` to get the flag.

<figure><img src="../.gitbook/assets/image (9) (2).png" alt=""><figcaption></figcaption></figure>

Flag: utflag{welc0me\_to\_utctf!}

## Reading List

<figure><img src="../.gitbook/assets/image (21) (2).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `readingList` file.

First, we can run the `file` command to determine the file type.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ file readingList 
readingList: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, BuildID[sha1]=89c121972d4f9072c7f516e7ac405833e73f2934, not stripped
```

We can see that the ELF execitable is `not stripped`, which could make solving this easier.&#x20;

Strip can remove this debugging information and other data included in the executable which is not necessary for execution in order to reduce the size of the executable. This could complicate things and make it harder to obtain the flag.

Since it is `not stripped`, we could try to `grep` the flag format from the file and we would get the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ strings readingList | grep utflag
utflag{string_theory_is_a_cosmological_theory_based_on_the_existence_of_cosmic_strings}
```

Alternatively, we could load this file into a software like `IDA Freeware`.

Once we have loaded the file, we could use the keyboard shortcut `SHIFT+F12` to search for the strings in this executable. Then, we can use `CTRL+F` to find the flag.

<figure><img src="../.gitbook/assets/image (6) (3) (1).png" alt=""><figcaption></figcaption></figure>

Flag: utflag{string\_theory\_is\_a\_cosmological\_theory\_based\_on\_the\_existence\_of\_cosmic\_strings}

## A Network Problem - Part 1

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

This challenge was very easy and can be solved in no time.

Once, we use `netcat` to connect to the server and port number, we will get the flag.

netcat (often abbreviated to nc) is a computer networking utility for reading from and writing to network connections using TCP or UDP. The command is designed to be a dependable back-end that can be used directly or easily driven by other programs and scripts.

<figure><img src="../.gitbook/assets/image (4) (3).png" alt=""><figcaption></figcaption></figure>

Flag: utflag{meh-netcats-cooler}

## A Network Problem - Part 2

<figure><img src="../.gitbook/assets/image (2) (1) (4).png" alt=""><figcaption></figcaption></figure>

For this challenge, it took me an hour or so to solve it because I did not realize that there was an update where the smb port was moved. Additionally, I was also not familiar with solving challenges related to `SMB`.&#x20;

I am glab I managed to pick up new tools like `smbclient` and `smbmap` to solve this challenge.

First, if we tried `nc` like the previous challenge, it would not give any output.

Next, I proceeded to use `nmap` to get the ip address of the server.

```bash
┌──(kali㉿kali)-[~]
└─$ nmap -Pn betta.utctf.live                                   

Starting Nmap 7.92 ( https://nmap.org ) at 2023-03-11 02:32 EST
Nmap scan report for betta.utctf.live (44.201.8.3)
Host is up (0.29s latency).
rDNS record for 44.201.8.3: ec2-44-201-8-3.compute-1.amazonaws.com
Not shown: 997 filtered tcp ports (no-response)
PORT     STATE SERVICE
22/tcp   open  ssh
139/tcp  open  netbios-ssn
8080/tcp open  http-proxy

Nmap done: 1 IP address (1 host up) scanned in 23.83 seconds
```

Next, we can use `smbmap`.

SMBMap allows users to enumerate samba share drives across an entire domain. List share drives, drive permissions, share contents, upload/download functionality, file name auto-download pattern matching, and even execute remote commands.

```bash
┌──(kali㉿kali)-[~]
└─$ smbmap -H 44.201.8.3 -P 8445      
[+] IP: 44.201.8.3:8445 Name: ec2-44-201-8-3.compute-1.amazonaws.com            
        Disk                                                    Permissions     Comment
        ----                                                    -----------     -------
        WorkShares                                              READ ONLY       Sharing of work files
        BackUps                                                 NO ACCESS       File Backups.
        IPC$                                                    NO ACCESS       IPC Service (Samba Server)
```

From here, we could see that there is `WorkShares` with `READ ONLY` permissions.

To view the sharing of work files, we can use `smbclient` to connect to `WorkShares` . When prompted for password, the password is the default kali password: `kali`.

```bash
┌──(kali㉿kali)-[~]
└─$ smbclient //44.201.8.3/WorkShares
Password for [WORKGROUP\kali]:
Try "help" to get a list of possible commands.
smb: \> help
?              allinfo        altname        archive        backup         
blocksize      cancel         case_sensitive cd             chmod          
chown          close          del            deltree        dir            
du             echo           exit           get            getfacl        
geteas         hardlink       help           history        iosize         
lcd            link           lock           lowercase      ls             
l              mask           md             mget           mkdir          
more           mput           newer          notify         open           
posix          posix_encrypt  posix_open     posix_mkdir    posix_rmdir    
posix_unlink   posix_whoami   print          prompt         put            
pwd            q              queue          quit           readlink       
rd             recurse        reget          rename         reput          
rm             rmdir          showacls       setea          setmode        
scopy          stat           symlink        tar            tarmode        
timeout        translate      unlock         volume         vuid           
wdel           logon          listconnect    showconnect    tcon           
tdis           tid            utimes         logoff         ..             
!              
```

At this point, I also found some documentations and blog [here ](https://www.samba.org/samba/docs/current/man-html/smbclient.1.html)and [here ](https://svch0st.medium.com/ctf-methods-and-tool-92febcac2ff4)which was quite helpful.&#x20;

Once we have connected to the server, we can run `ls` to list the files in the current directory.

```bash
smb: \> ls
  .                                   D        0  Wed Mar  8 14:45:05 2023
  ..                                  D        0  Wed Mar  8 14:45:05 2023
  shares                              D        0  Wed Mar  8 14:45:05 2023

                9974088 blocks of size 1024. 6139912 blocks available
```

We can then go into the `shares` directory using the `cd` command

```bash
smb: \> cd shares\
smb: \shares\> ls
  .                                   D        0  Wed Mar  8 14:45:05 2023
  ..                                  D        0  Wed Mar  8 14:45:05 2023
  Advertising                         D        0  Wed Mar  8 14:45:05 2023
  OfficeFun                           D        0  Wed Mar  8 14:45:05 2023
  IT                                  D        0  Wed Mar  8 14:45:05 2023

                9974088 blocks of size 1024. 6139912 blocks available
```

As we can see, there are three different directories `Advertising`, `OfficeFun` and `IT`.

If we go into `Adveritising`, we can see some other files.

```bash
smb: \shares\Advertising\> ls
  .                                   D        0  Wed Mar  8 14:45:05 2023
  ..                                  D        0  Wed Mar  8 14:45:05 2023
  Advertising Plan                    N       33  Wed Mar  8 14:45:05 2023
  Logos                               D        0  Wed Mar  8 14:45:05 2023
```

However, these files does not look like it would contain the flag. Hence, lets go to  other directories to check out.

We can go into `OfficeFun` and see that there's a `.jpg` file.

```bash
smb: \shares\> cd OfficeFun\
smb: \shares\OfficeFun\> ls
  .                                   D        0  Wed Mar  8 14:45:05 2023
  ..                                  D        0  Wed Mar  8 14:45:05 2023
  JaysCats                            D        0  Wed Mar  8 14:45:05 2023

                9974088 blocks of size 1024. 6123916 blocks available

smb: \shares\OfficeFun\> cd JaysCats\
smb: \shares\OfficeFun\JaysCats\> ls
  .                                   D        0  Wed Mar  8 14:45:05 2023
  ..                                  D        0  Wed Mar  8 14:45:05 2023
  Meowfoy.jpg                         N   215821  Wed Mar  8 14:45:05 2023

                9974088 blocks of size 1024. 6123964 blocks available
```

Sometimes the flag could be in an image, so let's try to view this image.

To do that, we will need to use the `get` command to copy the file to our local system. We can  then `exit` to view the file.

```bash
smb: \shares\OfficeFun\JaysCats\> get Meowfoy.jpg 
getting file \shares\OfficeFun\JaysCats\Meowfoy.jpg of size 215821 as Meowfoy.jpg (86.6 KiloBytes/sec) (average 86.6 KiloBytes/sec)
smb: \shares\OfficeFun\JaysCats\> exit
```

However, it was just a cat image with no flag given upon viewing it.

<figure><img src="../.gitbook/assets/image (3) (1) (3).png" alt=""><figcaption></figcaption></figure>

At first, I thought.. could it be some kind of steganography challenge where the flag is hidden in this image? However, after noting that this was a network category challenge, I thought that I might be overthinking it.

Therefore, I went on to check out the final folder first, which is the `IT` directory.

Once I'm in the `IT` directory, I will see a `notetoIT` file which looked interesting.

I copied this file to my local system in the similar way and read the file which gave me the flag.

```bash
smb: \shares\IT\Itstuff\> get notetoIT
getting file \shares\IT\Itstuff\notetoIT of size 380 as notetoIT (0.4 KiloBytes/sec) (average 0.4 KiloBytes/sec)
smb: \shares\IT\Itstuff\> exit
┌──(kali㉿kali)-[~]
└─$ cat notetoIT 
I don't understand the fasination with the magic phrase "abracadabra", but too many people are using them as passwords. Crystal Ball, Wade Coldwater, Jay Walker, and Holly Wood all basically have the same password. Can you please reach out to them and get them to change thier passwords or at least get them append a special character? 

-- Arty F.

utflag{out-of-c0ntrol-access}
```

Flag: utflag{out-of-c0ntrol-access}

## Half-time Survey

<figure><img src="../.gitbook/assets/image (16) (4).png" alt=""><figcaption></figcaption></figure>

If we click on the Google Forms link, we will be able to access the survey.

Upon completion of the survey, the flag will be presented.

<figure><img src="../.gitbook/assets/image (7) (1) (4).png" alt=""><figcaption></figcaption></figure>

Flag: utctf{h4ck\_h4ck\_h4ck}

## Insanity Check Redux

<figure><img src="../.gitbook/assets/image (19) (1).png" alt=""><figcaption></figcaption></figure>

This challenge was under the forensics category and I solved it after the competition.

I thought it was quite interesting so I decided to do a short writeup on it.&#x20;

First, if we navigated to the Discord server - `General` channel, we would realize that there was an admin who posted some message with an image before the competition started.

This image might just look like a Discord sticker to many and if we did not click on it, we would not have known that it was a `.jpg` image.

<figure><img src="../.gitbook/assets/image (3) (6) (1).png" alt=""><figcaption></figcaption></figure>

There was another similar image posted in the `memes` channel as well.

<figure><img src="../.gitbook/assets/image (2) (6).png" alt=""><figcaption></figcaption></figure>

However, even though this image was similar, with the same filename, it did not contain the flag.

If we ran `StegoVeritas` and try to read the contents found in `StegHide`, we would  realize it's not the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ stegoveritas notlikeduck.jpg
Running Module: SVImage
+------------------+------+
|   Image Format   | Mode |
+------------------+------+
| JPEG (ISO 10918) | RGB  |
+------------------+------+
Found something with StegHide: /home/kali/Downloads/results/steghide_38229acdc709a52e42f90b841e640675.bin
Running Module: MultiHandler

Exif
====
+---------------------+--------------------------------------+
| key                 | value                                |
+---------------------+--------------------------------------+
| SourceFile          | /home/kali/Downloads/notlikeduck.jpg |
| ExifToolVersion     | 12.44                                |
| FileName            | notlikeduck.jpg                      |
| Directory           | /home/kali/Downloads                 |
| FileSize            | 7.3 kB                               |
| FileModifyDate      | 2023:03:12 23:52:26-04:00            |
| FileAccessDate      | 2023:03:12 23:52:43-04:00            |
| FileInodeChangeDate | 2023:03:12 23:52:26-04:00            |
| FilePermissions     | -rw-r--r--                           |
| FileType            | JPEG                                 |
| FileTypeExtension   | jpg                                  |
| MIMEType            | image/jpeg                           |
| ExifByteOrder       | Big-endian (Motorola, MM)            |
| ImageWidth          | 112                                  |
| ImageHeight         | 112                                  |
| EncodingProcess     | Baseline DCT, Huffman coding         |
| BitsPerSample       | 8                                    |
| ColorComponents     | 3                                    |
| YCbCrSubSampling    | YCbCr4:4:4 (1 1)                     |
| ImageSize           | 112x112                              |
| Megapixels          | 0.013                                |
+---------------------+--------------------------------------+
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
Found something worth keeping!
JPEG image data, Exif standard: [TIFF image data, big-endian, direntries=0], baseline, precision 8, 112x112, components 3
                                                                                                                    
┌──(kali㉿kali)-[~/Downloads]
└─$ cat /home/kali/Downloads/results/steghide_38229acdc709a52e42f90b841e640675.bin

This is not the flag  
```

An easier way to find the image would be to search for the challenge creator username on Discord to find the messages posted by him.

<figure><img src="../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

Note: Only two images were `.jpg` files. There were several other `psyduck` that looked like image files but they were just Discord stickers.

<figure><img src="../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

We can download the psyduck image in the `general` channel that contained the flag and run `StegoVeritas` which would find something in `StegHide`.

Reading the contents found in `StegHide` would give us the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ file notlikeduck.jpg 
notlikeduck.jpg: JPEG image data, Exif standard: [TIFF image data, big-endian, direntries=0], baseline, precision 8, 112x112, components 3
                                                                                                                  
┌──(kali㉿kali)-[~/Downloads]
└─$ stegoveritas notlikeduck.jpg 
Running Module: SVImage
+------------------+------+
|   Image Format   | Mode |
+------------------+------+
| JPEG (ISO 10918) | RGB  |
+------------------+------+
Found something with StegHide: /home/kali/Downloads/results/steghide_06a52537dafef525f0ce60cbd19ad078.bin
Running Module: MultiHandler

Exif
====
+---------------------+--------------------------------------+
| key                 | value                                |
+---------------------+--------------------------------------+
| SourceFile          | /home/kali/Downloads/notlikeduck.jpg |
| ExifToolVersion     | 12.44                                |
| FileName            | notlikeduck.jpg                      |
| Directory           | /home/kali/Downloads                 |
| FileSize            | 7.3 kB                               |
| FileModifyDate      | 2023:03:12 21:53:16-04:00            |
| FileAccessDate      | 2023:03:12 21:53:24-04:00            |
| FileInodeChangeDate | 2023:03:12 21:53:16-04:00            |
| FilePermissions     | -rw-r--r--                           |
| FileType            | JPEG                                 |
| FileTypeExtension   | jpg                                  |
| MIMEType            | image/jpeg                           |
| ExifByteOrder       | Big-endian (Motorola, MM)            |
| ImageWidth          | 112                                  |
| ImageHeight         | 112                                  |
| EncodingProcess     | Baseline DCT, Huffman coding         |
| BitsPerSample       | 8                                    |
| ColorComponents     | 3                                    |
| YCbCrSubSampling    | YCbCr4:4:4 (1 1)                     |
| ImageSize           | 112x112                              |
| Megapixels          | 0.013                                |
+---------------------+--------------------------------------+
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
Found something worth keeping!
JPEG image data, Exif standard: [TIFF image data, big-endian, direntries=0], baseline, precision 8, 112x112, components 3
                                                                                                                  
┌──(kali㉿kali)-[~/Downloads]
└─$ cat /home/kali/Downloads/results/steghide_06a52537dafef525f0ce60cbd19ad078.bin

utflag{again_and_again_and_again}                                                         
```

Flag: utflag{again\_and\_again\_and\_again} &#x20;
