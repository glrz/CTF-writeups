---
description: The competition took place on 3 Mar - 5 Mar 2023.
---

# KalmarCTF 2023

This year's competition featured a variety of categories including pwn, crypto, web, rev, forensics, and misc.

I participated with team `Social Engineering Expert` and we obtained

I was able to allocate some time to tackle a couple of challenges and successfully solved them.

## Sanity Check

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

This challenge was super straightfoward. If we navigate to the `Rules` section and scroll down, we would find the flag. Alternatively, we could search for `kalmar{` as well.

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Flag: kalmar{i\_have\_read\_the\_rules\_and\_each\_player\_has\_their\_own\_account}

## sewing-waste-and-agriculture-leftovers

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `swaal.pcap.gz` file.

{% file src="../.gitbook/assets/swaal.pcap.gz" %}

First, we could extract the `.pcap` file using the `gunzip` command.

Next, we can open this `.pcap` file in Wireshark. We will realize that all the packets are `UDP`.&#x20;

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

To further explore the data transmitted, we can select the first packet, right click and `Follow -> UDP stream`.&#x20;

This will show stream 0.

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

We can increment the stream at the bottom right.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

After going through a few streams, we should be able to see that the flag is hidden in each stream, with some alphanumeric characters appearing in some streams, while not in others. These alphanumeric characters will replace the `.` to form the final flag.

If we continue to browse through the `Streams`, we will be able to get more alphanumeric characters to form the flag.

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

By stream 12, we should be able to get the flag. Note that stream 12 also contains 2 lines, each line shows parts of the flag.

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

We could use a text editor like `Notepad` to replace each `.` with the alphanumeric character for every stream.

&#x20;

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

Alternatively, we could copy paste each stream on a new line on a text editor like `Sublime Text` to see the sequence better and form the flag eventually.

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

Of course, there are better ways to solve this, by using a simple script to extract the UDP stream and check if an alphanumeric character is present in the previous stream. If it is present, do nothing, else it will replace the `.` with an alphanumeric character found in the current stream. This check will loop through the UDP streams until the flag is eventually formed.

Flag: kalmar{if\_4t\_first\_you\_d0nt\_succeed\_maybe\_youre\_us1ng\_udp}

