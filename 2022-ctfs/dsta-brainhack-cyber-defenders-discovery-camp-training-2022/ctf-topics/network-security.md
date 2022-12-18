---
description: This topic consists of 8 challenges and I solved all of them.
---

# Network Security

## Port Scan

![](<../../../.gitbook/assets/image (644).png>)

For this challenge, we were given a `.pcapng` file.

{% file src="../../../.gitbook/assets/network_ctf_synfinscan.pcapng" %}

have to find out the 2`MAC address` since we know that the person changed the `MAC address` and again performed port scanning.&#x20;

But, what type of scans did he perform? Here I unlocked a hint that was pretty useful.

![](<../../../.gitbook/assets/image (689).png>)

First, we could filter out the SYN scan by applying this filter

`tcp.flags.syn==1 && tcp.flags.ack==0`

![](<../../../.gitbook/assets/image (659).png>)

If we scroll down we would see packet 4118 with the IP address `192.168.171.129`, clicking into the packet would give us more information such as its `MAC address.`

![](<../../../.gitbook/assets/image (665).png>)

Next, we could filter out FIN scan by applying this filter

`tcp.flags==0x001`

![](<../../../.gitbook/assets/image (668).png>)

Again, we could click into the packet which would give us more information such as its `MAC address.`

![](<../../../.gitbook/assets/image (664).png>)

Notice the `MAC address` changed but `IP address` remained the same : `192.168.171.129`

An alternative solution which is easier is to filter by port number 8080 (Tomcat default port uses HTTP)

`tcp.port == 8080`

![](<../../../.gitbook/assets/image (619).png>)

From here, we could get the same results by comparing the `MAC address` in `packet 4126` and `packet 17386`.

Finally, we generate the MD5 of the 2 `MAC address` using an online [MD5 Hash Generator](https://www.md5hashgenerator.com/).

![](<../../../.gitbook/assets/image (661).png>)

## Follow the Attacker

![](<../../../.gitbook/assets/image (652).png>)

For this challenge, we were given a `.pcapng` file.

{% file src="../../../.gitbook/assets/followtheattacker (1).pcapng" %}

If we open this file in Wireshark, we could see that there are 2 IP address with the same MAC address. This is very suspicious. To find out what tampered HTTP response the attacker is making, we could apply this filter

`ip.src==192.168.171.129 && http`

![](<../../../.gitbook/assets/image (672).png>)

Right click on the first packet, `Follow > HTTP Stream`

![](<../../../.gitbook/assets/image (605).png>)

If we scroll down a bit, we would find the flag.

![](<../../../.gitbook/assets/image (627).png>)

## Recover My Flag

![](<../../../.gitbook/assets/image (679).png>)

For this challenge, we were given a `.pcapng` file.

{% file src="../../../.gitbook/assets/network_ctf_flagimage.pcapng" %}

We need to recover an image that was downloaded. First, we open this `.pcapng` file in Wireshark.&#x20;

Next, we go to File, `Export Objects > HTTP`.

![](<../../../.gitbook/assets/image (629).png>)

We would notice a `network-flag.png` file in the HTTP object list.

![](<../../../.gitbook/assets/image (616).png>)

If we save `network-flag.png and open the file`, we could generate the MD5 of the string in `network-flag.png` using an online [MD5 Hash Generator](https://www.md5hashgenerator.com/) to get the flag.

## Am I Bot?

![](<../../../.gitbook/assets/image (615).png>)

For this challenge, we were given a `.pcapng` file.

{% file src="../../../.gitbook/assets/aesdecrypt.pcapng" %}

First, we open this `.pcapng` file in Wireshark.&#x20;

Next, we Filter by `http`. We can see that `packet 3682` has `Info` of `/flag` which looks very interesting.

![](<../../../.gitbook/assets/image (617).png>)

We could right click on `packet 3682`, `Follow > TCP Stream`. Here we would get some hex data which looks encrypted.

![](<../../../.gitbook/assets/image (638).png>)

If we go back to the packets to check, we could see that `packet 3635` has the AES key and IV.

Similarly, we right click on the packet, `Follow > TCP Stream`.

![](<../../../.gitbook/assets/image (667).png>)

Finally, we could get the flag by decrypting this on CyberChef with this [recipe](https://cyberchef.org/#recipe=AES\_Decrypt\(%7B'option':'UTF8','string':'c0mm4nd\_4nd\_ctr1'%7D,%7B'option':'Hex','string':'0xCDDC202200000000d761bd823c9d792c'%7D,'CBC','Hex','Raw',%7B'option':'Hex','string':''%7D,%7B'option':'Hex','string':''%7D\)\&input=NGVjZDJlNzM3OGMyMGQxZDgyMTNjMjBjY2Q2MjdiNzRmMWNjYjNhMGJiOGM0OThjMzUxNTM2ZWYxMTE4MjgwMjYyYzZjN2ExZGMzMDNjMTk0ZmUzZTkyNWRlN2E1YmI1).

![](<../../../.gitbook/assets/image (680).png>)

## CLI HTTP

![](<../../../.gitbook/assets/image (610).png>)

For this challenge, we were presented with 5 stages of challenges before we could get the flag.

It tests on the knowledge of different HTTP methods, how to write cookies, forms etc. The solutions could be searched online through Google.

![Tutorial/ Demo](<../../../.gitbook/assets/image (604).png>)

![Stage 1](<../../../.gitbook/assets/image (660).png>)

![Stage 2](<../../../.gitbook/assets/image (690).png>)

![Stage 3](<../../../.gitbook/assets/image (688).png>)

![Stage 4](<../../../.gitbook/assets/image (641).png>)

![Stage 5](<../../../.gitbook/assets/image (637).png>)

## Safe Password

![](<../../../.gitbook/assets/image (647).png>)

For this challenge, we were given a `.pcapng` file.

{% file src="../../../.gitbook/assets/safety_password.pcapng" %}

This challenge was an easy one. If you managed to solve the previous challenges, this challenge is rather straightforward.

First, we open the `.pcapng` file given in Wireshark. Next, we right click on the first packet, `Follow > TCP Stream` and that's it. We get the password/flag.

![](<../../../.gitbook/assets/image (628).png>)

![](<../../../.gitbook/assets/image (675).png>)

## Network Divider&#x20;

![](<../../../.gitbook/assets/image (640).png>)

For this challenge, we had to complete 10 stages before we could get the flag.&#x20;

We could use [IP Subnet Calculator](https://www.calculator.net/ip-subnet-calculator.html) to help us get through these stages.

![](<../../../.gitbook/assets/image (656).png>)

![](<../../../.gitbook/assets/image (621).png>)

## Spam

![](<../../../.gitbook/assets/image (686).png>)

We are given a `spam.pcapng` file for this challenge.&#x20;

First, lets analyze the packets in Wireshark.&#x20;

![](<../../../.gitbook/assets/image (603).png>)

If we scroll down and continue to analyze further, we would see what looks like UDP flooding attack from the `IP address` : 192.168.2.1

![](<../../../.gitbook/assets/image (682).png>)

We could confirm this by going to `Statistics > conversations`. Take note of the packets and bytes sent. At this point, we know the attacker IP is 192.168.2.1

![](<../../../.gitbook/assets/image (678).png>)

We also know that this is UDP flooding

If we generate the SHA1 of the string using an [online SHA1 generator](http://www.sha1-online.com/), we would get the flag.

![](<../../../.gitbook/assets/image (658).png>)
