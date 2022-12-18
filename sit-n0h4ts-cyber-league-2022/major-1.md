---
description: >-
  MAJOR 1 is part of The Cyber League, it is the first major that was held from
  30 Apr - 1 May 2022.
---

# MAJOR 1

![](<../.gitbook/assets/image (582).png>)

I solved 3 challenges, 2 trivia challenges and 1 forensics challenge. The trivia challenges answers can be found on Google and they are like free points giveaway, so I will only do the writeup for forensics challenge.

![](<../.gitbook/assets/image (588) (1).png>)

## Understand space politics

![](<../.gitbook/assets/image (552) (1).png>)

For this challenge, we were given a `hello_there.7z` file.

First, I unzip this file by using the `7z x` command.

![](<../.gitbook/assets/image (505) (1).png>)

After extracting, I would get a `hello_there.tar.gz` file.

Next, I used the `tar -xvf hello_there.tar.gz` command to extract.

![](<../.gitbook/assets/image (544) (1).png>)

Alternatively, we could use the `gunzip` command to unzip the `gz` file first.

![](<../.gitbook/assets/image (570).png>)

Then use the `tar-xvf hello_there.tar` command to get the `hello_there.zip` file.

![](<../.gitbook/assets/image (498).png>)

An easier alternative solution which I discovered later was to use the command

`tar xzvf hello_there.tar.gz`

This would extract the file, we specified an additional `z` option here because it is a .gz file&#x20;

<figure><img src="../.gitbook/assets/image (594).png" alt=""><figcaption></figcaption></figure>

After we extract this zip file, we could run `strings` to check for readable strings. We would notice that there could be a `hello_there.txt` inside the zip file.

![](<../.gitbook/assets/image (556).png>)

If we try to unzip the `hello_there.zip`, it would prompt us for password.

![](<../.gitbook/assets/image (499).png>)

This is when I could apply the skills learned from [CSIT InfoSecurity Challenge 2020](https://gadiel-lau.gitbook.io/2020-writeups-1/csit-infosecurity-challenge-2020)  and other CTF competitions to solve the challenge.

We run the `zip2john hello_there.zip > file` and `john file` commands to crack the password.

![](<../.gitbook/assets/image (592) (1).png>)

Now we can use the password cracked: 2hot4u to unzip the zip file.

![](<../.gitbook/assets/image (509) (1).png>)

After we extracted `hello_there.txt` from the zip file, we can use `cat` command to print out the contents of `hello_there.txt`. This would give us our flag.

![](<../.gitbook/assets/image (551).png>)

Flag: CYBERLEAGUE{Y0U\__Fo|\_|nD\_3e!}_
