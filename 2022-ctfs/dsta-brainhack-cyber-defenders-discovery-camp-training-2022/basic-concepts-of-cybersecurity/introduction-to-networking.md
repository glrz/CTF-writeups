---
description: This topic consists of 4 challenges and I solved all of them.
---

# Introduction to Networking

## Do you understand network packets?

![](<../../../.gitbook/assets/image (750).png>)

For this challenge, we were given a `.pcapng` file.

{% file src="../../../.gitbook/assets/network_basic_3wayhandshake.pcapng" %}

We first had to find out the `IP address` of the destination performing the 3 way handshake. If we analyze this in [Wireshark](https://www.wireshark.org/), we could see that the 3 way handshake(SYN, SYN-ACK, ACK) was performed from packets 6 to 9.

![](<../../../.gitbook/assets/image (726).png>)

We could for example click on packet 9 to check the destination `IP address` and the `MAC address`.

![](<../../../.gitbook/assets/image (762).png>)

Finally, we generate the MD5 flag using an online [MD5 Hash Generator](https://www.md5hashgenerator.com/).

![](<../../../.gitbook/assets/image (753).png>)

## Who has...?

![](<../../../.gitbook/assets/image (724).png>)

For this challenge, we were given a `.pcapng` file.

{% file src="../../../.gitbook/assets/network_thirdARPresponse.pcapng" %}

First, we open this in Wireshark and we could see a bunch of ARP packets. Next, we key in `arp` into the filter box and filter by `arp`.

![](<../../../.gitbook/assets/image (781).png>)

Click on the `Destination` header twice, and we could locate the 3rd ARP response packet received by the broadcasting host.

![](<../../../.gitbook/assets/image (774).png>)

Alternatively, we could right click on packet 6’s destination, `Apply as Filter > Selected`

![](<../../../.gitbook/assets/image (707).png>)

![](<../../../.gitbook/assets/image (796).png>)

Then we add in `&& arp` into the filter box. From here, we could clearly see the 3rd ARP response packet - Packet 1339 received by the broadcasting host.

![](<../../../.gitbook/assets/image (782).png>)

Here we click on the 3rd ARP response packet – packet 1339 and we could see the Sender IP and MAC address!

![](<../../../.gitbook/assets/image (710).png>)

Generate the MD5 of `IP_MAC` using an online [MD5 Hash Generator](https://www.md5hashgenerator.com/) and we would get the flag.

## HTTP

![](<../../../.gitbook/assets/image (763).png>)

In this challenge, we were given a `.pcapng` file.&#x20;

{% file src="../../../.gitbook/assets/network_basic_http.pcapng" %}

We could analyze this file in Wireshark.&#x20;

As the challenge title is `HTTP`, we could first filter it by `http`. If we look closely, we would see the flag at packet 279, under the `Info` section.

![](<../../../.gitbook/assets/image (718).png>)

However, if we did not see this, we could right click on packet 39, `Follow > HTTP Stream`

![](<../../../.gitbook/assets/image (703).png>)

Scroll down a bit and we would see the flag.

![](<../../../.gitbook/assets/image (791).png>)

## My Precious Password

![](<../../../.gitbook/assets/image (730).png>)

For this challenge, we were given a `.pcapng` file.&#x20;

{% file src="../../../.gitbook/assets/network_basic_telnetpassword.pcapng" %}

We could analyze this file in Wireshark. First, we filter it by `tcp`

![](<../../../.gitbook/assets/image (743).png>)

Then right click on the packet, `Follow > TCP Steam`

![](<../../../.gitbook/assets/image (737).png>)

However, we would realise this is an incorrect password.

![](<../../../.gitbook/assets/image (701).png>)

We could go back and edit the filter to `tcp.stream eq 2` and then repeat the same process.

An easier alternative would be to increase the `Stream` here until we see the correct password.

![](<../../../.gitbook/assets/image (761).png>)

After increasing it to `Stream 4`, we will get the correct password : imth3k1ng

![](<../../../.gitbook/assets/image (744).png>)

Generate the MD5 of `imth3k1ng` using an online [MD5 Hash Generator](https://www.md5hashgenerator.com/) and we would get the flag.

![](<../../../.gitbook/assets/image (757).png>)
