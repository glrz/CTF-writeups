---
description: >-
  SG Cyber Olympian Trials 2022 is a trial to shortlist a batch for further
  training and sparring sessions in deep cyber security skills. The trial was
  conducted on the 26 Feb 2022 from 4.15 -6.15pm.
---

# SG Cyber Olympian Trials 2022

More information about this selection trial can be found below:

## About Cyber Olympian Trials 2022

![](<.gitbook/assets/image (314).png>)

## Rules of the Trials

![](<.gitbook/assets/image (261).png>)

For this 2 hours trial, we were given a series of challenges split into 3 different categories : Easy, Medium and Hard. The points for each category are as follow:

Easy challenge -> 50 points

Medium challenge -> 200 - 300 points&#x20;

Hard challenge -> 400 - 600 points

I solved 6 easy challenges and 2 Medium challenges, and came in 41/54 in position. If I am not wrong, they ended up selecting only around 20+ out of 54 candidates who participated. I did not get selected for **SG Cyber Olympians 2022** but I will continue to strive for excellence and build my skills so that I can excel further in the event that another selection period takes place.&#x20;

![](<.gitbook/assets/image (291).png>)

![](<.gitbook/assets/image (390).png>)

![](<.gitbook/assets/image (322).png>)

I felt that I could have done much better in this selection trials. Most importantly, there were a few key takeaways from this selection trial.

1. I should have made better preparations before this selection trial. During the selection trial, I realised my Kali Linux VM was in a mess. There were too many files and folders from the different CTFs I participated previously. This led to me having issues in locating some of the challenge files during the challenge. What I could have done is that I could better organize my files/folders prior to the event.
2. I went straight for the `Hard` category challenges right at the beginning. This caused me to lose quite a bit of time and confidence at the start. I think it would be better if I started solving the easy challenges first, then after I have warmed up, I could proceed to the Medium or Hard challenges.
3. Based on previous CTF experiences, there would always be a "format" to submit our flags, usually it is in this `flag{ }` format. However, for this selection trials, we only needed to submit the contents inside the `flag{ }`. I did not know about this and wasted quite some time at the beginning trying to figure out why my flag was wrong. I should read the challenge description more carefully next time..
4. I wasted too much time on a particular challenge. I spent at least 30 minutes trying different ways to brute force one of the challenges and ended up not solving it, which caused me to run out of time and I didn't have time to attempt some of the other challenges. I should have moved on to other challenges after 5-10 mins.

The challenges solved were

![](<.gitbook/assets/image (256) (1).png>)

The trials started at 4.15pm but I only got my first solve at 4.47pm.. That is more than 30mins later. Yes... I had wasted 30 mins(refer to point number 2 and 3 above if you would like to know why). My last solve was at 5.40pm and the trials ended at 6.15pm. If you are wondering what happened during the last 30+ mins... refer to point number 4 above.

## Exeggcute Me

![](<.gitbook/assets/image (222) (1).png>)

In this challenge, it attached a binary file and stated that there is a flag in it. For this we can run the following command `chmod 777` or `chmod + x` to enable execute permissions, then `./` to run the program.

![](<.gitbook/assets/image (271).png>)

Flag: c730f03e9fbf9fd58bf84a2028a0a21e

## Base 2^6

![](<.gitbook/assets/image (298).png>)

In this challenge, we are given a TXT file.&#x20;

{% file src=".gitbook/assets/base26.txt" %}

From the challenge title, we could tell that 2^6 results in 64, so the TXT file probably contains a Base64 encoded flag.

![](<.gitbook/assets/image (348).png>)

Indeed, if we copy paste the text into [CyberChef](https://cyberchef.org/), we get the flag.

Flag: cbad9ba9c6c4e1788427ffde69fa9d35

## Word Search

![](<.gitbook/assets/image (232) (1).png>)

In this challenge, we can run the program using `./` and use `grep` to filter out the flag.

![](<.gitbook/assets/image (202).png>)

Flag: d39151bafaae1df6fc0ccde9817b0613

## Tallest Mountain

![](<.gitbook/assets/image (210) (1).png>)

For this challenge, we are given a JPG image which shows a picture of Mount Everest upon opening it. (Nothing interesting here for solving the challenge)

![](<.gitbook/assets/image (371).png>)

Since it was an image file, I suspected that it could be a steganography related challenge, that is hiding the flag in the image file.

Hence, I proceeded using `stegoveritas` command on the everest.jpg file.&#x20;

![](<.gitbook/assets/image (385).png>)

Here, I have found something interesting (i.e. steghide\_3ed88c801a82142ac875a300ba05115.bin) with StegHide and it was saved in the results folder.

I had to change the directory to results first to locate the file. Then, I run the `strings` command to find the pieces of readable information in binary file, followed by the pipe and `grep` command to search for flag in the file.&#x20;

![](<.gitbook/assets/image (333).png>)

For other steganography related challenges, you could check out my other writeups [here](https://gadiel-lau.gitbook.io/2021-writeups/csit-the-infosecurity-challenge-tisc-2021#scratching-the-surface-challenge-3), [here](https://gadiel-lau.gitbook.io/2020-writeups/gsctf-2020#wheres-the-file) and [here](https://gadiel-lau.gitbook.io/2020-writeups/brixel-ctf-winter-edition-2020/steganography#rufus-the-vampire-cat).

Flag: everestrocks!

## Test Result!

![](<.gitbook/assets/image (360).png>)

We could use the `file` command to check the file type. Checking the file type, I realised it is actually a PNG image file. Opening it up will give us the flag.

![](<.gitbook/assets/image (362).png>)

![](<.gitbook/assets/image (224) (1).png>)

Flag: Cnegative!

## Funny Monkey

![](<.gitbook/assets/image (320).png>)

In this challenge, we are given a JPG image of a `funny monkey`. My first thought is that this could be a steganography challenge.&#x20;

![](<.gitbook/assets/image (221) (1).png>)

I could use my good old friend `stegoveritas` to help me here.

![](<.gitbook/assets/image (324).png>)

![](<.gitbook/assets/image (297).png>)

The flag can be seen in the `value` column.

However, sometimes `stegoveritas` can take a while to run. I found an easier alternative solution after the selection trials, which is to use `exiftool` to solve this challenge.

![](<.gitbook/assets/image (370).png>)

Flag: funnymonkey$



## What did i send?

![](<.gitbook/assets/image (382).png>)

For this challenge, we were given a PCAPNG file.&#x20;



I opened the file in `Wireshark` to do further analysis.

![](<.gitbook/assets/image (279) (1).png>)

In Wireshark, I could see the packets captured. First, I applied `tcp` filter to filter out the other unnecessary information. TCP allows me to view the network conversation and data exchanged between the source and destination networks.

![](<.gitbook/assets/image (367).png>)

After that, I will follow TCP Stream by right clicking on the packet, `Follow > TCP Stream`.

![](<.gitbook/assets/image (306).png>)

From here, I could see the messages exchanged between the source and destination, and the flag.

![](<.gitbook/assets/image (268) (1).png>)

Flag: IknowHowToUseTelnet

## Identify Pepe

![](<.gitbook/assets/image (335).png>)

For this challenge, we were given a PCAPNG file as well (similar to challenge: `What did i send?` above).&#x20;

{% file src=".gitbook/assets/telnetLogin.pcapng" %}

I opened the file in Wireshark to do further analysis.

![](<.gitbook/assets/image (330).png>)

According to the challenge, I supposed I had to figure out the password to login to the telnet session, and the flag would be the password used for the telnet session.

Seeing that there are many different protocols, I had to filter them again. By applying the telnet filter, I was able to only view data that are relevant.

![](<.gitbook/assets/image (219) (1).png>)

I did a similar process like how I solved the previous challenge, that is to right click on the packet, `Follow > select TCP Stream`.

![](<.gitbook/assets/image (375).png>)

From here, I could see the messages exchanged between the source and destination.

Finally, I get the password used for the telnet session, which is also the flag.

![](<.gitbook/assets/image (326).png>)

Flag: pepeveryhandsome

## Hidden File

![](<.gitbook/assets/image (242).png>)

I solved this challenge after the selection trials as I did not have time to attempt this challenge.. This challenge was in the `Hard` Category at 400 points. After solving it, I think this should be considered as `Medium` challenge at most.

This challenge mentions a secret file is hidden in this binary. We could use `binwalk` to search for hidden files in the binary. Check out my other writeup [here](https://gadiel-lau.gitbook.io/2020-writeups/brixel-ctf-winter-edition-2020/steganography#doc-ception) where I used `binwalk` to solve.

![](<.gitbook/assets/image (212) (1).png>)

From the previous image, we could see a `flag.txt` file in it. Lets extract it with `-e` option

![](<.gitbook/assets/image (227) (1).png>)

Then, we could go to the directory storing `flag.txt`

![](<.gitbook/assets/image (396).png>)

&#x20;and open it to read its contents

![](<.gitbook/assets/image (225) (1).png>)

Alternatively, just use `cd` to change directory and `cat` command to read the contents

![](<.gitbook/assets/image (203) (1).png>)

Flag: 7236a313709df0184dd34f4c59685f7e

## Password attack

![](<.gitbook/assets/image (193).png>)

I solved this challenge after the competition. Also, this was the challenge which I spent 30mins trying to brute force but did not get the password because I missed out the format option when cracking the password using [John](https://en.wikipedia.org/wiki/John\_the\_Ripper).

For this challenge, we were given a `Passwd_Attack` file.

{% file src=".gitbook/assets/Passwd_Attack" %}

If we open up the `Passwd_Attack` file, we can see its contents as follow

> daemon:_:1:1:daemon:/usr/sbin:/usr/sbin/nologin bin:_:2:2:bin:/bin:/usr/sbin/nologin sys:_:3:3:sys:/dev:/usr/sbin/nologin sync:_:4:65534:sync:/bin:/bin/sync games:_:5:60:games:/usr/games:/usr/sbin/nologin man:_:6:12:man:/var/cache/man:/usr/sbin/nologin lp:_:7:7:lp:/var/spool/lpd:/usr/sbin/nologin mail:_:8:8:mail:/var/mail:/usr/sbin/nologin news:_:9:9:news:/var/spool/news:/usr/sbin/nologin uucp:_:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin proxy:_:13:13:proxy:/bin:/usr/sbin/nologin www-data:_:33:33:www-data:/var/www:/usr/sbin/nologin backup:_:34:34:backup:/var/backups:/usr/sbin/nologin list:_:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin irc:_:39:39:ircd:/var/run/ircd:/usr/sbin/nologin gnats:_:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin nobody:_:65534:65534:nobody:/nonexistent:/usr/sbin/nologin \_apt:_:100:65534::/nonexistent:/usr/sbin/nologin systemd-timesync:_:101:102:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin systemd-network:_:102:103:systemd Network Management,,,:/run/systemd:/usr/sbin/nologin systemd-resolve:_:103:104:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin mysql:!:104:109:MySQL Server,,,:/nonexistent:/bin/false Debian-exim:!:105:110::/var/spool/exim4:/usr/sbin/nologin uuidd:_:106:112::/run/uuidd:/usr/sbin/nologin rwhod:_:107:65534::/var/spool/rwho:/usr/sbin/nologin redsocks:!:108:113::/var/run/redsocks:/usr/sbin/nologin usbmux:_:109:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin miredo:_:110:65534::/var/run/miredo:/usr/sbin/nologin ntp:_:111:114::/nonexistent:/usr/sbin/nologin postgres:_:112:116:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash dnsmasq:_:113:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin messagebus:_:114:117::/nonexistent:/usr/sbin/nologin iodine:_:115:65534::/var/run/iodine:/usr/sbin/nologin arpwatch:!:116:119:ARP Watcher,,,:/var/lib/arpwatch:/bin/sh stunnel4:!:118:123::/var/run/stunnel4:/usr/sbin/nologin rtkit:_:119:124:RealtimeKit,,,:/proc:/usr/sbin/nologin sslh:!:120:126::/nonexistent:/usr/sbin/nologin inetsim:_:121:128::/var/lib/inetsim:/usr/sbin/nologin sshd:_:122:65534::/run/sshd:/usr/sbin/nologin speech-dispatcher:!:123:29:Speech Dispatcher,,,:/var/run/speech-dispatcher:/bin/false gluster:_:124:131::/var/lib/glusterd:/usr/sbin/nologin geoclue:_:125:133::/var/lib/geoclue:/usr/sbin/nologin colord:_:126:134:colord colour management daemon,,,:/var/lib/colord:/usr/sbin/nologin saned:_:127:135::/var/lib/saned:/usr/sbin/nologin avahi:_:128:136:Avahi mDNS daemon,,,:/var/run/avahi-daemon:/usr/sbin/nologin pulse:_:129:137:PulseAudio daemon,,,:/var/run/pulse:/usr/sbin/nologin dradis:_:130:139::/var/lib/dradis:/usr/sbin/nologin king-phisher:_:131:140::/var/lib/king-phisher:/usr/sbin/nologin beef-xss:_:132:141::/var/lib/beef-xss:/usr/sbin/nologin Debian-gdm:_:133:142:Gnome Display Manager:/var/lib/gdm3:/bin/false systemd-coredump:!!:998:998:systemd Core Dumper:/:/sbin/nologin Debian-snmp:!:117:122::/var/lib/snmp:/bin/false vboxadd:!:999:1::/var/run/vboxadd:/bin/false debian-tor:_:134:145::/var/lib/tor:/bin/false \_rpc:_:135:65534::/run/rpcbind:/usr/sbin/nologin statd:_:136:65534::/var/lib/nfs:/usr/sbin/nologin admin\_user:$6$7LYU9cUOW22Imt83$2thOaEfwnm5vjaxWgIFh2My4F//QdwmUB16BGTXz1S9rTc7x7tesUO0vu/dRkvVukAG5VhiuRS8flkzpEtO0p/:1003:1003::/home/admin\_user:/bin/sh

The general format for the passwd file is:

`Username:passwd:UID:GID:full_name:home directory:shell`

Username: Stores the username of whom the account belongs to.

Passwd: Stores the user's transformed password.&#x20;

– If shadow files are used, an x appears in this location

UID: The user ID or the user identification number, generally chosen by the system.

GID: The group ID or group identification number, which reflects the native group (base group of membership).

Full name: This field usually contains the user's full names but is not mandatory.

Home Directory: Stores the location of the user's home directory.

Shell: Stores the user's default shell, which is what runs when the user first logs onto the system.

In the challenge description, it says that we need to find the password of `admin_user`. We could see from the last line there is `admin_user`. Now if we look at the `Passwd` portion of `admin_user`, we could see that it starts with “$6$” which indicates that the password is hashed with the encryption algorithm [`sha512_crypt`](https://passlib.readthedocs.io/en/stable/lib/passlib.hash.sha512\_crypt.html#passlib.hash.sha512\_crypt). For more details on encryption algorithm formats, we could refer to the links [here](https://www.openwall.com/john/doc/OPTIONS.shtml), [here](https://passlib.readthedocs.io/en/stable/modular\_crypt\_format.html), [here](https://pentestmonkey.net/cheat-sheet/john-the-ripper-hash-formats) and [here](https://github.com/Shiva108/CTF-notes/blob/master/Notes%20VA/HashFormats\_JackTheRipper.txt).

Now that we know the format, we could proceed using john the ripper, using the crypt format and a password list to crack the password.

If I run the command

`john --format=crypt --wordlist=usr/share/john/password.lst ~/Desktop/Passwd_Attack`

I will get the password for `admin_user`.

![Password: cookie1](<.gitbook/assets/image (118) (1).png>)

I could also include the `--show` option to display the cracked password.

![](<.gitbook/assets/image (100) (1).png>)

Flag: cookie1

### Additional part that is similar but not related to any challenge:

We could crack our Kali Linux VM password following 2 simple steps.

First, we combine `/etc/passwd` and `etc/shadow` files. This process is called "unshadowing".

`/etc/passwd` stores a list of registered users in the system and `/etc/shadow` stores the hashes of the password.&#x20;

Note that previous version of UNIX systems' passwd file stored the hashes of the password.

We could achieve this by running the command

`unshadow /etc/passwd /etc/shadow > victims_pwd`

![](<.gitbook/assets/image (179) (1).png>)

If I were to `cat` and read the contents of `victims_pwd`, I would realise at the bottom there's this line of text.

`kali:$y$j9T$AB7f3WOFqXBj299UsTEOR0$ntPaAOtAgP55AQiBTCSr5R9zxN3E6RF0fBOHhFWXzf5:1000:1000:Kali,,,:/home/kali:/usr/bin/zsh`

Note that `$y$` indicates that the passwords are hashed with the encryption algorithm:`yescrypt`

Next, we could run John the Ripper, with the crypt format to perform dictionary attack against the unshadowed file using a word list and we would get the password : `kali`.

`john --format=crypt --wordlist=usr/share/john/password.lst victims_pwd`

![](<.gitbook/assets/image (143) (1).png>)

Additionally, we could simulate a process that is similar to some of the challenges here.&#x20;

First, create a user `steve` for testing on Kali:

`useradd –m steve –G sudo –s /bin/bash`

![](<.gitbook/assets/image (802).png>)

Next, set password for victim on Kali :

`passwd steve`

![Password set is test123](<.gitbook/assets/image (804).png>)

Next, combine entries of /etc/passwd and /etc/shadow by unshadowing:

`unshadow /etc/passwd /etc/shadow > steve_pwd`

![](<.gitbook/assets/image (806).png>)

Finally, run `John the Ripper` using the password list to crack the password:

Note that `-form` will specify the format and `-w` specifies the password list

`john –form=crypt -w=/usr/share/john/password.lst steve_pwd`

![Password: test123](<.gitbook/assets/image (807).png>)

Once `John the Ripper` has cracked the password, it will not do it again. It will save the cracked passwords. To view it, run `john --show steve_pwd.`

![](<.gitbook/assets/image (797).png>)

## Packetie

![](<.gitbook/assets/image (149) (1).png>)

Note that I solved this challenge after the competition. For this challenge, we were given a `packetie.pcapng` file.

{% file src=".gitbook/assets/packetie.pcapng" %}

&#x20;First, I open this file in Wireshark to analyze the packets.

If I go to `Statistics`, then `Protocol Hierarchy`. I would notice there is `ftp-data` in the protocol. This usually contains interesting information.

Next, I could apply the `ftp-data` filter in Wireshark. I would see that there is a `secret.txt` at packet 273.&#x20;

![](<.gitbook/assets/image (174).png>)

I can proceed to right click, `Follow > TCP Steam`. Here if I scroll down, I could see the encrypted password of `packetie`.  If you recalled, in the previous [additional notes](https://gadiel-lau.gitbook.io/2022-writeups/sg-cyber-olympian-trials-2022#additional-part-that-is-similar-but-not-related-to-any-challenge), we have seen the `$y$` encryption algorithm before, this is `yescrypt`. We can save this file as `packetie`.

![](<.gitbook/assets/image (173).png>)

The saved file is shown below

{% file src=".gitbook/assets/packetie.txt" %}

Finally, we proceed to use John the Ripper with the crypt format and `password.lst` to perform dictionary attack on `packetie`. We would get the password for packetie: `packer`.

![](<.gitbook/assets/image (141) (1).png>)

We could also use `--show` option to show the password.

![](<.gitbook/assets/image (104) (1).png>)

Flag: packer
