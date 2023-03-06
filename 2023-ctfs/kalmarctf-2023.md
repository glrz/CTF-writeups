---
description: The competition took place on 3 Mar - 5 Mar 2023.
---

# KalmarCTF 2023

This year's competition featured a variety of categories including pwn, crypto, web, rev, forensics, and misc.

I participated with team `Social Engineering Expert` and we obtained the position of 23/905 teams.

I was able to allocate some time to tackle a couple of challenges and successfully solved them.

## Sanity Check

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

This challenge was super straightfoward. If we navigate to the `Rules` section and scroll down, we would find the flag. Alternatively, we could search for `kalmar{` as well.

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Flag: kalmar{i\_have\_read\_the\_rules\_and\_each\_player\_has\_their\_own\_account}

## sewing-waste-and-agriculture-leftovers

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `swaal.pcap.gz` file.

{% file src="../.gitbook/assets/swaal.pcap.gz" %}

First, we could extract the `.pcap` file using the `gunzip` command.

Next, we can open this `.pcap` file in Wireshark. We will realize that all the packets are `UDP`.&#x20;

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

To further explore the data transmitted, we can select the first packet, right click and `Follow -> UDP stream`.&#x20;

This will show stream 0.

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

We can increment the stream at the bottom right.

<figure><img src="../.gitbook/assets/image (4) (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

After going through a few streams, we should be able to see that the flag is hidden in each stream, with some alphanumeric characters appearing in some streams, while not in others. These alphanumeric characters will replace the `.` to form the final flag.

If we continue to browse through the `Streams`, we will be able to get more alphanumeric characters to form the flag.

<figure><img src="../.gitbook/assets/image (10) (4).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (2) (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (7) (5).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

By stream 12, we should be able to get the flag. Note that stream 12 also contains 2 lines, each line shows parts of the flag.

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

We could use a text editor like `Notepad` to replace each `.` with the alphanumeric character for every stream.

&#x20;

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

Alternatively, we could copy paste each stream on a new line on a text editor like `Sublime Text` to see the sequence better and form the flag eventually.

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

Of course, there are better ways to solve this, by using a simple script to extract the UDP stream and check if an alphanumeric character is present in the previous stream. If it is present, do nothing, else it will replace the `.` with an alphanumeric character found in the current stream. This check will loop through the UDP streams until the flag is eventually formed.&#x20;

```python
from scapy.all import *

packets = rdpcap('swaal.pcap')
udp_data = b''.join(pkt.load for pkt in packets)
segments = udp_data.split(b'\n')

flag = {}
for s in segments:
    pattern = re.compile(rb'[a-z0-9}{_]')
    matches = pattern.finditer(s)

    for m in matches:
        flag[m.start()] = m.group()

flag = dict(sorted(flag.items())).values()
print(b''.join(flag).decode())
```

Flag: kalmar{if\_4t\_first\_you\_d0nt\_succeed\_maybe\_youre\_us1ng\_udp}

## cards

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `cards.pcap.gz` file.

{% file src="../.gitbook/assets/cards.pcap.gz" %}

Similar to the previous challenge, we can use the `gunzip` command to get the `cards.pcap` file.

Next, we'll use Wireshark to further inspect the packets.

In Wireshark, we can go to `Statistics > Protocol Hierarchy` to check the `Protocols` involved in this capture file.&#x20;

We will see that there are `TCP` and `FTP` protocols.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

For your information, `FTP` uses two `TCP` connections to transfer files from local machine to remote server.

1. Control connection (Port 21) - For sending control information like passwords
2. Data connection (Port 20) - For sending real data files

If we filter the packets by `ftp`, we will see that there is some transfer of data by right clicking the packet and `Follow > TCP Stream`.

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

If we go through the TCP Streams, we will notice that there is a CWD number which changes in each stream.

We will also notice that the flag starts to print out in a scrambled version from Stream 79 to Stream 158.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Basically, the flag is ordered by the `CWD` which we can find from the FTP stream. We will then need to correlate the FTP stream (port 21) with the binary data stream (some other TCP port). By using this Python script that uses `Scapy`, we can get the flag after some manual reordering.

```python
from scapy.all import *
import re

pcap = rdpcap("cards.pcap")
sPortToCwd = {}

cwdAndChar = []

for p in pcap:
    if p.haslayer(TCP) and p[TCP].payload:
        payload = p[TCP].payload.load.decode()
    
        if "CWD" in payload:
            cwdNum = int(payload.split(" ")[1])
            sPortToCwd[p[TCP].sport] = cwdNum

for p in pcap:
    if p.haslayer(TCP) and p[TCP].payload:
        payload = p[TCP].payload.load.decode()

        if "Switching to Binary" in payload:
            cwdNum = sPortToCwd[p[TCP].dport]

        if len(payload) == 1:
            cwdAndChar.append((cwdNum, payload))

print("".join(x[1] for x in sorted(cwdAndChar, key=lambda x: x[0])))python
```

Flag: kalmar{shuffle\_shuff1e\_can\_you\_k33p\_tr4ck\_of\_where\_th3\_cards\_are\_shuffl3d\_n0w}

## lleHSyniT!

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

This final challenge I solved was in the medium category but surprisingly I found it to be easier than the previous two challenges. I most likely solved it using an unintended approach.

In this challenge, we were given a `challenge.tar` file.

{% file src="../.gitbook/assets/challenge.tar" %}

We could extract the files as such

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ tar -xvf challenge.tar 
capture.pcap
proc.dmp
```

First, I opened the `pcap` file to analyze the packets. However, I did not find much information to be useful, so I moved on to do some static analysis on the `.dmp` file.

By running the `strings` command, I was able to roughly see what was going on in the process dump. As I scrolled through the `strings`, I found the flag which happened to be under the `password` portion.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Alternatively, I could have just `grep` for the flag as such

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ strings proc.dmp | grep kalmar
password:kalmar{My_F4v0r1t3_G4m3_1s_Cobalt_Strike:gL0b4l_0p3r4t0rs}
```

The intended solution was decrypting cobaltstrike traffic as such:

```bash
# Ref: https://blog.didierstevens.com/2021/04/26/quickpost-decrypting-cobalt-strike-traffic/
$ data=$(tshark -r capture.pcap -Y http.request.method==POST -Tfields -e data | tail -1)
$ cs-extract-key.py -c $data proc.dmp
$ cs-parse-traffic.py -k 24a0f5e701439f460d52ef4810f592f3:3c4267894c6fee7a5aaa4d13e0289051 capture.pcap -e
$ cat payload-61ca2f3dc9212781c983f9e13a99be08.vir
```

Basically, cobaltstrike memory to extract key then parse http beacon.

You can also read up more [here](https://isc.sans.edu/diary/Decrypting+Cobalt+Strike+Traffic+With+Keys+Extracted+From+Process+Memory/28006).

Flag: kalmar{My\_F4v0r1t3\_G4m3\_1s\_Cobalt\_Strike:gL0b4l\_0p3r4t0rs}
