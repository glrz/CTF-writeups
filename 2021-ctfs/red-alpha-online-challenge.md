---
description: >-
  Red Alpha Online Challenge is a cybersecurity challenge related to network
  forensics. It is the first stage of challenge for the Alpha Specialist
  Training Programme selection process.
---

# Red Alpha Online Challenge

We were given 5 days to complete this challenge. However, I think this challenge is beginner-friendly and it could be completed within an hour.

Even if you are someone from non-IT background, don't worry, you can always Google and find solutions online! In this challenge, you can actually just Google `How to extract pdf from Wireshark` and you will find a solution to solve this.

## First Stage

In this challenge, we are given a .pcap file which is a `Wireshark capture file`. _Wireshark_ is a packet sniffer and analysis tool.&#x20;

{% file src="../.gitbook/assets/red_alpha.pcap" %}

We were also given a separate `PDF` file on `Network Forensics Tutorial` which mentioned to extract from the file `red_alpha.pcap` a PDF file which contains the password.&#x20;

![](<../.gitbook/assets/image (85).png>)

Note: I am not allowed to share the PDF file due to copyright issues.

First, we can open this file in Wireshark to do further analysis.

I personally like to go `Statistics > Protocol Hierarchy` first to check out the different protocols in the network capture file.

![](<../.gitbook/assets/image (13).png>)

We can see visually what is the amount of traffic being sent or received per protocol, and identify the most common protocols in our capture.

![](<../.gitbook/assets/image (63).png>)

From the image, we could tell that there is File Transfer Protocol (FTP) involved. The File Transfer Protocol is a standard communication protocol used for the transfer of computer files from a server to a client on a computer network. In this case, the PDF file could be transferred via FTP.

Next, we can filter by `ftp-data` to review traffic from the FTP data channel. If you are new to "extracting objects" from Wireshark, I could suggest a good read [here](https://unit42.paloaltonetworks.com/using-wireshark-exporting-objects-from-a-pcap/).

![](<../.gitbook/assets/image (95).png>)

Then, we can go to the first network packet we see that contains `red_alpha.pdf`, that is packet 6051. We can right click on the packet, `follow > TCP stream`. `Follow TCP Stream` is a very useful feature in Wireshark which builds for us all of the TCP segments of a specific TCP connection that we choose, and shows us only the application data that was transmitted as a single stream.

![](<../.gitbook/assets/image (74).png>)

![](<../.gitbook/assets/image (12).png>)

Now, we can choose to save only the download side of the conversation, and change `Show data as` to Raw.

![](<../.gitbook/assets/image (71).png>)

Finally, we can `save as...` and save it as a .pdf file.

Opening the pdf file would give us the password to solve the challenge.

![I blurred out the password so that I don't spoil the challenge and I don't think I'm supposed to share it :)](<../.gitbook/assets/image (2).png>)

## Alternative solution

After we opened up the .pcap file in Wireshark, we can filter by `frame contains PDF-`. This will show us only packet 6051. From here, we could follow the same steps above to solve the challenge.

![](<../.gitbook/assets/image (35).png>)

## Out of scope

This is not part of the challenge, but it is something good to know.

If we filter by `ftp`, we could see personal information such as login credentials. In this case, we can see the `USER` and `PASS` from the network packets.

![](<../.gitbook/assets/image (11).png>)

We could also right click the packet, `follow > TCP stream` for more information.

![USER: anonymous   PASS: anonymous@example.com](<../.gitbook/assets/image (91).png>)
