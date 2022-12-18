---
description: >-
  The SG Cyber Olympians Selection Trial is back. The trial took place virtually
  on 29 Oct 2022 from 4.20 - 6.20 pm.
---

# SG Cyber Olympian 2nd Trial 2022



<figure><img src="../.gitbook/assets/image (92).png" alt=""><figcaption></figcaption></figure>

I took part in the 1st Trial previously [here](https://gadiel-lau.gitbook.io/2022-writeups/sg-cyber-olympian-trials-2022). The rules of this trial was similar to the first trial. In my previous trial, I placed 41/54. This time, I placed 19/52 and was generally satisfied with the results. Not only did I improve my rank placement, I also managed to apply my knowledge to solve more challenges in this trial.

Note : I did not get selected to be part of SG Cyber Olympians Programme after this trial. They selected around 15 people only for this selection. Nonetheless, I will continue to build my skills and hopefully participate in the next selection.

<figure><img src="../.gitbook/assets/image (210).png" alt=""><figcaption></figcaption></figure>

The scoreboard for this trial can be found below.

<figure><img src="../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (226).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (188).png" alt=""><figcaption></figcaption></figure>

For this 2 hours trial, we were given a series of challenges split into 3 different categories : Easy, Medium and Hard. The points for each category are as follow:

Easy challenge -> 50 points

Medium challenge -> 100 - 200 points&#x20;

Hard challenge -> 500 - 700 points

In this trial, I solved 12 challenges, 10 Easy challenges and 2 Intermediate challenges.

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (192).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (219).png" alt=""><figcaption></figcaption></figure>

There were quite a number of challenges that were similar to the ones in the 1st Trial. As such, I will  only be doing writeups for challenges that were not included in my previous writeup for 1st Trial and challenges that I solved after this trial.&#x20;

## Bestpinger

<figure><img src="../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a link to connect to. Above the description of this challenge, we could also see this is a `Command Injection` related challenge.

Browsing to the webpage, we can see the following

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

Here, we can start to perform `Command Injection` due to the lack of input sanitization. If we add `;` in front of the command we want to execute, we are essentially performing `command injection`.

The `;` will signify the end of the first command and the beginning of another.

For example, to see the current working directory, we can issue `;pwd` and press `submit`.

<figure><img src="../.gitbook/assets/image (203).png" alt=""><figcaption></figcaption></figure>

Now, we can also try to list the files in the current working directory, by issuing `;ls` command. Here we can see that there is a `secret.txt` file which could possibly contain the flag we are looking for.

<figure><img src="../.gitbook/assets/image (208).png" alt=""><figcaption></figcaption></figure>

To view the contents of `secret.txt,` issue the command `;cat secret.txt.` This will give us the flag.

<figure><img src="../.gitbook/assets/image (224).png" alt=""><figcaption></figcaption></figure>

Note that we could also join multiple UNIX commands together with the delimiter `;` as follows:

`;whoami;pwd;ls -la;cat secret.txt`

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

Flag: 6a15741987d67efb8ee9b9d2c30a0982

## Search Warrant

<figure><img src="../.gitbook/assets/image (212).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a link to connect to. If we browse to the webpage, we would see the following

<figure><img src="../.gitbook/assets/image (223).png" alt=""><figcaption></figcaption></figure>

Above the challenge description, we could see that this challenge is related to `SQL Injection`. We could try the usual `'or 1=1` query which will always return True. However, trying this would give us an error in the SQL syntax. This is somewhat like a `Error-Based SQL injection` where we could find out information of the structure of the database based on the error message thrown by the database server. In this case, we know that it is using `MYSQL Server`.

<figure><img src="../.gitbook/assets/image (231).png" alt=""><figcaption></figcaption></figure>

MYSQL Server supports three comment styles which can be found [here](https://dev.mysql.com/doc/refman/8.0/en/comments.html). Trying `--` to comment will not work, but trying `#` to comment at the end of this query worked.

<figure><img src="../.gitbook/assets/image (227).png" alt=""><figcaption></figcaption></figure>

Once we press `Submit Query`, we will see the flag appearing below under `Admin`.

<figure><img src="../.gitbook/assets/image (179).png" alt=""><figcaption></figcaption></figure>

Flag : 1e2f826948bafe445735a9fe9376407d

## Zoo Message

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `elephant.txt` file, with the description to `find the English message inside this animal file`. My initial thought was that the English message could be hidden as a string in the text file. Hence, I proceeded to use `strings` command to look through the file manually, hoping to find an English message. However, this process of searching through all the strings in the text file was too slow. To solve this issue, I used the `grep` command to specifically look for characters a-z or A-Z in the text file, essentially providing a suitable regular expression that could help me to find the English message. After minutes of searching, I still could not find the flag.&#x20;

This was when I decided to use the `file` command to determine the type of file and its data (I probably should have done this earlier as my first step). After running the command, I realised I am dealing with a `.jpg` image file, not a `.txt` file.

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

I proceeded to use the `eog` command to view the image file.

<figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

Opening the file would show an image of an elephant. I tried to look for possible English message that could be hidden near the elephant or at other places around the image but could not find any.

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

At this moment, I thought that this could be a Steganography related challenge, where the message is hidden in the image. I proceeded to use a Steganography tool : `StegoVeritas` to help me solve this challenge. Running the `stegoveritas` command shows that it found something with StegHide.

<figure><img src="../.gitbook/assets/image (221).png" alt=""><figcaption></figcaption></figure>

If I use the `cat` command to view its contents, I will see a string that looked like there’s a shift of characters.

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

I could easily tell that this message had been encoded by ROT-13 (based on previous CTF experience [here](https://gadiel-lau.gitbook.io/2022-writeups/aisp-cyber-wellness-ctf#rot13)). ROT-13 is a simple Caesar cipher used for obscuring text by replacing each letter with the letter thirteen places down the alphabet. To decode it, I simply used an [online ROT-13 decoder ](https://rot13.com/)which gives me the flag.

<figure><img src="../.gitbook/assets/image (216).png" alt=""><figcaption></figcaption></figure>

Flag : asdJuieoAPlefdjAujefdiqqOpnM

## Hardcrack

<figure><img src="../.gitbook/assets/image (209).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `Dict_Crack.zip` file which was password protected. The description clearly specified to crack the zip file’s password to open the flag file inside. Above the description, we could also see that this challenge is `Dictionary Password Cracking` related, which highly suggest to perform a dictionary attack to get the password.

First, I used `zip2john` command to convert the zip file into a hash format that is readable by `John The Ripper`.

<figure><img src="../.gitbook/assets/image (230).png" alt=""><figcaption></figcaption></figure>

Now that we have this `hash` file, we could crack the password by specifying zip format and performing a dictionary attack using the wordlist : `rockyou.txt`. This could be done by executing the following command:

`john --form=zip -w=/usr/share/wordlists/rockyou.txt hash`

After around 13 seconds, we will get the password : `likeavirgin`

<figure><img src="../.gitbook/assets/image (198).png" alt=""><figcaption></figcaption></figure>

I proceeded to use `7z x` command to extract the zip file contents using the password above.

<figure><img src="../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

This would give us `flag1.txt`, which is the extracted file. Using the `cat` command, the flag is revealed.

<figure><img src="../.gitbook/assets/image (200).png" alt=""><figcaption></figcaption></figure>

Flag: P@ssw0rdCracker

## Port Up!

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given 2 files `portup3.bin` and `portup_linux_64.bin`. I was very close to solve this challenge during the trial, but solved it after the trial.&#x20;

This challenge is similar to a challenge which I had solved before [here](https://gadiel-lau.gitbook.io/2022-writeups/dsta-brainhack-cyber-defenders-discovery-camp-training-2022/ctf-topics/reverse-engineering#weird-section).&#x20;

First, I execute the first program : `portup3.bin`. This program seemed like it was taking in commands but not executing them.

<figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

Next, I used `strings command` to check the `head` and `tail` of the program. The program looked normal.

<figure><img src="../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

Next, I proceeded to run the second file : `portup_linux_64.bin`. I ran the program as well and the program looked kind of similar to the first program.

Just like what I did previously, I ran `strings`  command and checked the `tail` of the program. This time I found that there was `UPX UPX UPX` at the bottom, which likely suggest that this program was packed by [UPX](https://upx.github.io/). Note that the following image shown below was not the original program packed by UPX, I lost the original program and had to pack it with UPX (reverse the process) after solving this challenge. To pack the program with `UPX`, I used the `-1` or `-9` option.

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

Next, we could use `UPX` to unpack the `.bin` file.

`-d` option will decompress the file

<figure><img src="../.gitbook/assets/image (205).png" alt=""><figcaption></figcaption></figure>

I made it up till this point during the trial. The next part to solve this challenge is actually quite easy and straightforward. Instead of loading this program into software like [IDA Freeware](https://hex-rays.com/ida-free/) or [Ghidra](https://ghidra-sre.org/), we could simply use `strings` command and `grep` for flag.

<figure><img src="../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

Note that we have to unpack this file first before performing this step, else we would not be able to see the flag because the strings in the program was obfuscated.

Flag: b30363fab42cf3a08fdfc45b3472c5ee

## Shark Chat

<figure><img src="../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `sharkchat.pcapng` file. I solved this challenge after the trial. After solving the challenge, I realised I had previously solved a similar challenge [here](https://gadiel-lau.gitbook.io/2021-writeups/red-alpha-online-challenge).

First, we could open the file in `Wireshark`.&#x20;

If we go to `Statistics > Protocol Hierarchy` to check out the different protocols in the network capture file, we would see that all the packets are transferred using `TCP`.

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

Since all the packets are using `TCP`, we could right click on the 1st packet and go to `Follow > TCP Steam`. From here, we could see that there is a `secret.pdf` being transferred.

<figure><img src="../.gitbook/assets/image (201).png" alt=""><figcaption></figcaption></figure>

There are a few ways to locate this `secret.pdf` file in Wireshark. Two possible ways are:

1. Increase the `Stream` number at the bottom right.
2. Filter by `frame contains PDF-`

For `1.` it is the easier solution for this challenge. We simply increase `Stream` to `Stream : 1` and we can export the PDF.

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

However, if we just directly export and save the file like this, we would just get a blank PDF. To see the contents in the PDF, we have to change Show data as : `ASCII` to Show data as : `Raw` before saving the file as PDF.

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

For `2.` we could also arrive at this step by applying the filter : `frame contains PDF-`. This will look for packet that contains the string `PDF-`, which is the header for PDF files.

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

Now, we can `Follow > TCP Stream` and we would get to the same step above. After this, simply change to Show data as : `Raw` and save the file with .pdf extension.

Opening the PDF file would give us the flag.

<figure><img src="../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

An alternative solution would be to use another tool like [NetworkMiner](https://www.netresec.com/?page=NetworkMiner). NetworkMiner can be downloaded on [Windows](https://www.netresec.com/?page=NetworkMiner) or [Linux](https://www.netresec.com/?page=Blog\&month=2014-02\&post=HowTo-install-NetworkMiner-in-Ubuntu-Fedora-and-Arch-Linux).

If we want to use NetworkMiner, note that the NetworkMiner Free Edition currently only supports `.pcap` files, not `.pcapng` files.

As such, we will need to convert the `.pcapng` file to`.pcap` file first by running the following `tshark` command

`tshark -F pcap -r sharkchat.pcapng -w sharkchat.pcaptshark -F pcap -r sharkchat.pcapng -w sharkchat.pcap`

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

Since I downloaded NetworkMiner on Linux, I could open it by executing the program with&#x20;

`./NetworkMiner`

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

If I open up the `pcap` file in NetworkMiner, and go to `Files` section, I would see the `secret.pdf` file. Now we just have to right click and open the file to view the flag.

<figure><img src="../.gitbook/assets/image (189).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (225).png" alt=""><figcaption></figcaption></figure>

Flag: 271e5f5f44a0406305507ac4344ca24a
