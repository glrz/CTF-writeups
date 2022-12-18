# Network

## ARP Spoofing

![](<../.gitbook/assets/image (68).png>)

For this challenge, we were given a `arp.pcapng` file in the zip file.

{% file src="../.gitbook/assets/arp.pcapng.zip" %}

I first blooded this challenge, which meant that I was the first to solve this challenge out of the many other teams.

This was a relatively easy challenge. From the challenge title, we know that this is [`ARP Spoofing` ](https://en.wikipedia.org/wiki/ARP\_spoofing)or `ARP poisoning`, which is a Man in the Middle (MitM) attack that allows attackers to intercept communication between network devices.

First, we could open this `.pcapng` file in [Wireshark ](https://www.wireshark.org/)to analyze the packets.

Next, we would notice in packet 3 that there is an indication of `Duplicate IP address detected for 192.160.0.100`. This is the `IP address` stated in the challenge, and if we look closer, we would see its `MAC address` beside.&#x20;

The flag is source MAC address `30:24:a9:81:04:90`.

![](<../.gitbook/assets/image (46).png>)

Flag: CDDC22{30:24:a9:81:04:90}

## Simple Shark

![](<../.gitbook/assets/image (72) (1).png>)

In this challenge, we were given a `Simple_Shark.pcap` file in the zip file.&#x20;

{% file src="../.gitbook/assets/Simple_Shark.pcap.zip" %}

If we use `strings` command and `grep` to filter out the flag format : `CDDC` from `.pcap` file, we would get the flag.

![](<../.gitbook/assets/image (70) (1).png>)

Flag: CDDC22{The\_s6@rK\_H@D\_@\_F1@99999!!!}

## Some Sharks

![](<../.gitbook/assets/image (36) (1).png>)

For this challenge, we were given a `.pcap` file in the zip file.&#x20;

{% file src="../.gitbook/assets/somesharks.pcap" %}

I had to use a hint here which helped me to solve the challenge.

![](<../.gitbook/assets/image (60) (1).png>)

Now if we search up how to filter `HTTP Authorization header`, we would find that we could use `http.authorization`. If we look at the `authorization`, we would see that it is in Base64 and the credentials is the decoded Base64. If this is not obvious to you, you could test it out and try to decode the Base64 using an [online Base64 decoder](https://www.base64decode.org/).

![](<../.gitbook/assets/image (52).png>)

If we go to the last packet: `packet 60732` , we would see the `admin` login credentials.

We could right click on the packet, `Follow > HTTP Stream`

![](<../.gitbook/assets/image (6) (1).png>)

Based on the packet information, we could tell that it uses [Basic access authentication](https://en.wikipedia.org/wiki/Basic\_access\_authentication), standard Base64 authorization. For example, the standard Base64 for client:password, “Aladdin:open sesame” is&#x20;

`Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==`

Based on this knowledge, we copy the Base64 Encoded string (as highlighted)

![](<../.gitbook/assets/image (18).png>)

Then decode the base64 using an [online Base64 decoder](https://www.base64decode.org/) and we get the credentials:

![](<../.gitbook/assets/image (8) (1).png>)

Alternatively, an easier solution could be to go to the last packet, right click on `Credentials`, `Copy > Value`. Then, we could paste this `value`, which is the admin credentials to a text editor first.

![](<../.gitbook/assets/image (19) (1).png>)

After we obtained the `admin` login credentials, we connect to the site as seen in `Referer`

![](<../.gitbook/assets/image (24) (1).png>)

Login to the website using the `admin` credentials obtained earlier.

![](<../.gitbook/assets/image (4) (1).png>)

After we logged in, we could see a `flag.txt` file.

![](<../.gitbook/assets/image (64) (1).png>)

Click on the file and we would be redirected to the `/flag.txt` path, which contains the flag.

![](<../.gitbook/assets/image (93).png>)

Flag: CDDC22{S0me\_Sh4rk5\_4r3\_k1nD\_ISNt\_1t?}

## SNMP

![](<../.gitbook/assets/image (20) (1).png>)

For this challenge, we were given a `.zip` file.

{% file src="../.gitbook/assets/printer_snmp.zip" %}

We needed to obtain the flag with an SNMP request. I decided to use a hint here which was quite helpful.&#x20;

![](<../.gitbook/assets/image (65) (1).png>)

Actually I did not really need the hint to solve this challenge, I was just missing the printer's ip address in my command.. So, after some tries I finally got the flag using this command

`snmpget -v1 -cpublic1 13.215.173.140 iso.3.6.1.2.1.1.1.0`

![](<../.gitbook/assets/image (80).png>)

Alternatively, we could also use this command to get the flag

`snmpwalk -v1 cpublic1 13.215.173.140 iso.3.6.1.2.1.1.1.0`

![](<../.gitbook/assets/image (161) (1).png>)

Note that I am not exactly sure if the `.pcapng` file provided would be helpful in solving this challenge as I have limited experience in analyzing SNMP packets.

Flag: CDDC22{L34king\_SNMP\_C0mmunity\_$}

## WEP

![](<../.gitbook/assets/image (156) (1).png>)

For this challenge, we were given `wep.zip` file.

{% file src="../.gitbook/assets/wep (1).zip" %}

First, we unzip the zip file using `unzip` command. We would extract a `dictionary.txt` and `wepcrack.cap` file from the zip file.

![](<../.gitbook/assets/image (188) (1).png>)

I went to check the SSID from `Wireless > VLAN Traffic`

![](<../.gitbook/assets/image (112).png>)

![](<../.gitbook/assets/image (101) (1).png>)

Then, I tried to use `-a` mode to set attack mode to `WEP`

![](<../.gitbook/assets/image (181) (1).png>)

With the command seen below

![](<../.gitbook/assets/image (195).png>)

However, I realised all these was not needed since there was only 1 SSID.

We could just use this simple command with the dictionary txt file provided to crack the password:

`aircrack-ng -w dictionary.txt wepcrack.cap`

![](<../.gitbook/assets/image (194).png>)

Flag: CDDC22{Dr0ne\_WEP\_Cr@cking!!!}

## WiFi

![](<../.gitbook/assets/image (132) (1).png>)

For this challenge, we were given a `wpa_crack.zip` file containing a `wpa_crack.cap` file.

{% file src="../.gitbook/assets/wpa_crack.zip" %}

I have never cracked a WiFi WPA password before, hence I needed to do a little bit of research on this challenge. Also, note that this challenge was not solved during the competition, I solved it after.

Some useful sites that helped me solve this challenge are

{% embed url="https://hashcat.net/wiki/doku.php?id=cracking_wpawpa2" %}

{% embed url="https://www.4armed.com/blog/perform-mask-attack-hashcat/" %}

{% embed url="https://hashcat.net/wiki/doku.php?id=mask_attack" %}

{% embed url="https://www.youtube.com/watch?v=Usw0IlGbkC4" %}

With the knowledge above, we first convert the `.cap` file into `hash.hc22000`. This format will be readable by [`hashcat`](https://hashcat.net/hashcat/) later.

![](<../.gitbook/assets/image (105).png>)

After that's done we would get the session summary that the cap file has been processed

![](<../.gitbook/assets/image (126).png>)

Finally, we could use this command to crack the password

`hashcat -m 22000 hash.hc22000 -a 3 2?d?d?d?d2?d?d`

`-m 22000` sets the mode to WPA-PBKDF2-PMKID+EAPOL

`-a 3` sets the attack mode to brute force attack

`2?d?d?d?d2?d?d` sets the 1st and 6th digit to `2` (we know this from challenge description) and `?d` represents digits

![](<../.gitbook/assets/image (171) (1).png>)

After we have executed the command, we could press `s` to view the status. In this case it estimated that this attack would take around 8 minutes.

![](<../.gitbook/assets/image (139) (1).png>)

After 6 minutes 33 seconds, we managed to crack the password: `23501268`.

![](<../.gitbook/assets/image (119).png>)

If you are interested in my other writeup using hashcat, click [here](broken-reference).

An alternative approach would be to use [`crunch`](https://www.kali.org/tools/crunch/) to generate our own wordlist, use [aircrack-ng](https://www.kali.org/tools/aircrack-ng/) to convert cap to hccap file, use [`hccap2john`](https://charlesreid1.com/wiki/John\_the\_Ripper/WPA) to convert it to hash and  finally use [John ](https://www.kali.org/tools/john/) to crack the WiFi Password.

The basic syntax for crunch is as follow:

For displaying password permutation on the terminal screen

`crunch[min len] [max len] [character set][options]`

To save crunch output into a specified file

`crunch[min len] [max len] [character set][options] –o file`

Since we already know that the password is 8-digit and the 1st and 6th digit is `2`, we could use the following command. `-t` option would specify a pattern to search . In this case, `%` is a wildcard for numeric. Other wildcard includes `@` which is for lower alphabetical characters, `,` which is wildcard for upper alphabetical characters and `^` for special characters.&#x20;

`-o` option will output it to a file `wifipass.txt`.

```
┌──(kali㉿kali)-[/]
└─$ sudo crunch 8 8 -t 2%%%%2%% -o wifipass.txt
[sudo] password for kali: 
Crunch will now generate the following amount of data: 9000000 bytes
8 MB
0 GB
0 TB
0 PB
Crunch will now generate the following number of lines: 1000000 

crunch: 100% completed generating output
```

Next, we use `aircrack-ng` to convert `.cap` file to `.hccap` file. Note that `-J` option will convert the `.cap` file to `.hccap` hashcat file.

```
┌──(root㉿kali)-[/]
└─# aircrack-ng wpa_crack.cap -J cap2hccap  
Reading packets, please wait...
Opening wpa_crack.cap
Read 2979 packets.

   #  BSSID              ESSID                     Encryption

   1  28:3B:82:7D:0F:8C  dlink-0F88                WPA (1 handshake)

Choosing first network as target.

Reading packets, please wait...
Opening wpa_crack.cap
Read 2979 packets.

1 potential targets



Building Hashcat file...

[*] ESSID (length: 10): dlink-0F88
[*] Key version: 2
[*] BSSID: 28:3B:82:7D:0F:8C
[*] STA: B2:A0:41:A2:90:88
[*] anonce:
    F5 D0 1E CD 1E 7E 15 A4 9E 14 26 6A 85 53 BF 17 
    55 B8 43 80 82 E9 9E 17 8E 8E 41 15 C7 DF 8B 2E 
[*] snonce:
    39 4B 6D D9 3D 40 00 3D 2B A3 5A 98 B7 56 00 5A 
    EF 3E 8B 8E E4 81 9F 12 C8 B2 20 E6 9F 65 9C 89 
[*] Key MIC:
    DB D0 8C 26 AB 7B 7A C2 7D 90 76 B9 6A 78 81 D3
[*] eapol:
    01 03 00 75 02 01 0A 00 00 00 00 00 00 00 00 00 
    02 39 4B 6D D9 3D 40 00 3D 2B A3 5A 98 B7 56 00 
    5A EF 3E 8B 8E E4 81 9F 12 C8 B2 20 E6 9F 65 9C 
    89 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
    00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
    00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
    00 00 16 30 14 01 00 00 0F AC 02 01 00 00 0F AC 
    04 01 00 00 0F AC 02 8C 00 

Successfully written to cap2hccap.hccap
```

Next, use `hccap2john` to convert the file to a format that `John` can read.

```
┌──(root㉿kali)-[/]
└─# hccap2john cap2hccap.hccap > crackwifi
```

Finally, we use `John` to crack the password using the wordlist we generated earlier.

```
┌──(root㉿kali)-[/]
└─# john -w=wifipass.txt -form=wpapsk crackwifi
Using default input encoding: UTF-8
Loaded 1 password hash (wpapsk, WPA/WPA2/PMF/PMKID PSK [PBKDF2-SHA1 256/256 AVX2 8x])
Will run 2 OpenMP threads
Note: Minimum length forced to 8 by format
Press 'q' or Ctrl-C to abort, almost any other key for status
0g 0:00:00:01 0.29% (ETA: 00:13:52) 0g/s 2823p/s 2823c/s 2823C/s 20028280..20029243

```

At 2 minutes 47 seconds, we get the password.

```
┌──(root㉿kali)-[/]
└─# john -w=wifipass.txt -form=wpapsk crackwifi
Using default input encoding: UTF-8
Loaded 1 password hash (wpapsk, WPA/WPA2/PMF/PMKID PSK [PBKDF2-SHA1 256/256 AVX2 8x])
Will run 2 OpenMP threads
Note: Minimum length forced to 8 by format
Press 'q' or Ctrl-C to abort, almost any other key for status
0g 0:00:00:01 0.29% (ETA: 00:13:52) 0g/s 2823p/s 2823c/s 2823C/s 20028280..20029243
23501268         (dlink-0F88)     
1g 0:00:02:47 DONE (2022-08-01 00:11) 0.005964g/s 2088p/s 2088c/s 2088C/s 23501244..23502207
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
```

We could use `--show` option to show the password.

```
┌──(root㉿kali)-[/]
└─# john --show crackwifi                      
dlink-0F88:23501268:b2a041a29088:283b827d0f8c:283b827d0f8c::WPA2:cap2hccap.hccap

1 password hash cracked, 0 left
```

Check out my other writeups using `John` [here](https://gadiel-lau.gitbook.io/2022-writeups/sg-cyber-olympian-trials-2022#password-attack), [here](https://gadiel-lau.gitbook.io/2022-writeups/lagncrash-interpoly-ctf-2022#riddle-me-this) and [here](https://gadiel-lau.gitbook.io/2022-writeups/lagncrash-interpoly-ctf-2022#nothing-here).

Another alternative solution which might be the easiest to execute is to use the wordlist generated using `crunch` earlier and use `aircrack-ng` (like how we used it to crack the previous WEP challenge) to crack the Wi-Fi password using the wordlist. This took 3 minutes 47 seconds to crack the password(My 2nd attempt). My first attempt to crack the password using `aircrack-ng` took 7 minutes 55 seconds. The longer cracking time was probably due to running Webex and other services in the background. Note that the cracking time depends on various factors such as the RAM allocated to the VM, the applications/programs running in the background and the device you are using to crack the password.&#x20;

```
┌──(kali㉿kali)-[~/Desktop]
└─$ sudo crunch 8 8 -t 2%%%%2%% -o wifipass.txt
[sudo] password for kali: 
Crunch will now generate the following amount of data: 9000000 bytes
8 MB
0 GB
0 TB
0 PB
Crunch will now generate the following number of lines: 1000000 

crunch: 100% completed generating output
                                                                                                                   
┌──(kali㉿kali)-[~/Desktop]
└─$ sudo aircrack-ng -w wifipass.txt wpa_crack.cap
[sudo] password for kali: 
Reading packets, please wait...
Opening wpa_crack.cap
Read 2979 packets.

   #  BSSID              ESSID                     Encryption

   1  28:3B:82:7D:0F:8C  dlink-0F88                WPA (1 handshake)

Choosing first network as target.

Reading packets, please wait...
Opening wpa_crack.cap
Read 2979 packets.

1 potential targets


                               Aircrack-ng 1.6 

      [00:03:46] 345120/1000000 keys tested (1549.12 k/s) 

      Time left: 7 minutes, 2 seconds                           34.51%

                           KEY FOUND! [ 23501268 ]


      Master Key     : A8 39 30 6E C3 CB 91 53 CE 31 FF 86 03 E4 F1 54 
                       7B 0E 8F 11 73 B1 1F A4 6C 0D 97 54 15 E8 4D C1 

      Transient Key  : 59 3F CD 0D CC 53 EF 00 00 00 00 00 00 00 00 00 
                       00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
                       00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
                       00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 

      EAPOL HMAC     : DB D0 8C 26 AB 7B 7A C2 7D 90 76 B9 6A 78 81 D3 


```

If you are interested in other Wi-Fi cracking tools, [Pyrit ](https://github.com/JPaulMora/Pyrit)and [Cowpatty ](https://github.com/joswr1ght/cowpatty)are good alternatives. Check out interesting read [here ](https://null-byte.wonderhowto.com/how-to/crack-wpa-wpa2-wi-fi-passwords-with-pyrit-0196782/)and [here](https://null-byte.wonderhowto.com/how-to/hack-wi-fi-cracking-wpa2-psk-passwords-with-cowpatty-0148423/).

Flag: CDDC22{23501268}
