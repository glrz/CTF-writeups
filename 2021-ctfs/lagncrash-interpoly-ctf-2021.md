---
description: >-
  LagNCrash Interpoly CTF 2021 is a CTF competition held from 10 Mar - 12 Mar
  2021.
---

# LagNCrash Interpoly CTF 2021

This competition allowed up to 4 members to form a team but I participated solo in this CTF. This CTF competition is mainly for polytechnic students to pit against other polytechnic students from the various polytechnics. I participated in the Open category as I was interested to broaden my knowledge in cybersecurity as well as gain more experience in CTF competitions.

I did not really care about the position I get in this CTF back then, and the organizers do not have access to the scoreboard anymore, hence there was no position recorded for this CTF.

Most of the challenges in this CTF are beginner-friendly and I managed to solve a few challenges in this competition. Through this experience, I learned more about concepts of cryptography and the different types of ciphers.&#x20;

## Pigs can write

I lost the challenge title and description for this one. Basically, the challenge gave us a TXT file which contained symbols. After searching on Google, I found out this is called `pigpen cipher`. This can be decoded into plaintext with an online tool[ here](https://www.boxentriq.com/code-breaking/pigpen-cipher).

After clicking on each symbol which matches the alphabet, we will get the flag.

![](<../.gitbook/assets/image (84).png>)

Flag: LNC{OINKOINKPIGISCUTE}

## tales from the past

![](<../.gitbook/assets/image (58).png>)

In this challenge, we are given a TXT file which looked like encrypted text when we opened it.

If we have no idea what cipher this is, we can always Google it. If we Google `old tale sky cipher`, we would find out that this is probably `scytale cipher`.&#x20;

We could decode the message [here.](https://www.dcode.fr/scytale-cipher)

Decoding the message would give us the flag.

![](<../.gitbook/assets/image (55).png>)

Flag: LNC{S3RP3NT1NE\__SN4K3_\_098f6bcd4621d373cade4e832627b4f6}

## weak n insecure

![](<../.gitbook/assets/image (66).png>)

In this challenge, we are given the value of `e`,`N` and `cipher`. We need to find the message which is 10 digit long.

First, I can use a modular inverse online tool [here](https://www.dcode.fr/modular-inverse) to find the modular multiplicative inverse. I will key in the information provided in the challenge description.

![](<../.gitbook/assets/image (89).png>)

This gives me the output 17935681591906784513, which will be the value of `d`

Now, I can just write a simple Python script to solve the challenge.

```python
d = 17935681591906784513
cipher = 10421600892944111639
N = 21805564595370162889
a = pow(cipher, d, N)
print(a)
# output: 5342585545
```

![](<../.gitbook/assets/image (19).png>)

Flag: LNC{5342585545}

## Broken keyboard

![](<../.gitbook/assets/image (32).png>)

This challenge shows a description which contained a bunch of text. It looked like a cat just stepped on the user's keyboard? If we google `keyboard cipher`, we would find out this is `keyboard shift cipher`.

We could decode the message [here](https://www.dcode.fr/keyboard-shift-cipher).

After we decode it, we get the result which looked like Base64 encoded.

![](<../.gitbook/assets/image (86).png>)

From here, we can go ahead to decrypt the Base64 encoded text [here](https://www.base64decode.org/).

![](<../.gitbook/assets/image (95).png>)

Here we get some hex values in the decoded output. We can proceed to convert this hex to text [here](http://www.unit-conversion.info/texttools/hexadecimal/).. and we will get the flag.

![](<../.gitbook/assets/image (14).png>)

Flag: LNC{IN33DAN3WK3YBOARD}

## Halmor

![](<../.gitbook/assets/image (68).png>)

In this challenge, we can see in the first line something that looked like `morse code`.

Based on the challenge title, if we google `half morse code`, we can find out that this is `fractionated morse cipher`. We can decrypt the ciphertext [here](https://www.dcode.fr/fractionated-morse).

![](<../.gitbook/assets/image (75).png>)

Flag: LNC{WOWMORS3C4NACTUALLYB3HALV3DCOOL}

## Romeo Shane Arthur

> Romeo, Shane and arthur are such talented students in my cryptography classes hope they would be able to make something that would improve the world of technology in the future submit the flag in the LNC{secret} format nc challenge1.lagncrash.com 16872

Looking at the challenge title, if we take the first letter of each words we will get `RSA`. This means it is related to `RSA.` When we netcat into the server, we are presented with two values "e" and "n". The server then tell us to find the value "d".

![](<../.gitbook/assets/image (90).png>)

After a quick google search, I found a Rsactftool which can calculate "e" and "n" to get "d". You can get this tool [here.](https://github.com/Ganapati/RsaCtfTool)

![](<../.gitbook/assets/image (26).png>)

![-h to show the options](<../.gitbook/assets/image (31).png>)

I git clone the tool into my kali and run the tool with argument `python3 RsaCtfTool.py -e (value) -n (value) --uncipher --dumpkey` as seen in the picture below

![](<../.gitbook/assets/image (27).png>)

Afterwards, I copy the `d` value and submit it to get the flag.

![](<../.gitbook/assets/image (8).png>)

Flag: LNC{L4rGe\_3Xp0N3nt\_15\_b4D\_L0L}

## BruteForce?

![](<../.gitbook/assets/image (62).png>)

For this challenge, we were given a zip file.

If we use the hint, it says it is encrypted with legacy encryption.

![](<../.gitbook/assets/image (64).png>)

This hint will be useful in solving the challenge later.

First, we open up the zip file to check its contents.

![](<../.gitbook/assets/image (49).png>)

It contains 2 files : `Desktop.zip` and `readme.txt`

If we open up the `readme.txt` file, it reads : `pleasedontseethis!!!`

Here, we can utilize the hint and search about legacy encryption of zip files.

To decrypt legacy encryption zip, we can use [pkcrack](https://github.com/keyunluo/pkcrack) or [bkcrack](https://github.com/kimci86/bkcrack).

In this case, we will be using pkcrack.

Refrencing the [Original Documentation](https://www.unix-ag.uni-kl.de/\~conrad/krypto/pkcrack/pkcrack-readme.html) of PKCrack, we can use

`./pkcrack -C /home/kali/Desktop/BruteForce/brute_force/Desktop.zip -c readme.txt -P /home/kali/Desktop/BruteForce/brute_force.zip -p readme.txt -d decrypted -a`

![](<../.gitbook/assets/image (61).png>)

After PKCrack cracked the zip, we can use `cat` to read flag.txt and get the flag

![](<../.gitbook/assets/image (65).png>)

Flag: LNC{plain\_t3xt\_BRO0T\_F0RCE}

## kidding

![](<../.gitbook/assets/image (74).png>)

For this challenge, we get some good hints and determined it to be `keyed caesar cipher`. We could use online tool [here](https://www.boxentriq.com/code-breaking/keyed-caesar-cipher) to solve it.

If we paste in the ciphertext, increase the key to `1` and enter the keyword as `interpoly`, we will get the flag.

![](<../.gitbook/assets/image (45).png>)

Flag: LNC{i\__w4snt_\_k1dd1ng!}

## Hidden Password

![](<../.gitbook/assets/image (23).png>)

For this challenge, we are given a zip file.

The zip file seems corrupted. To analyze this zip file further, lets open it in a hex editor like `HxD`. For the documentation of zip, we can read [here.](https://pkware.cachefly.net/webdocs/casestudies/APPNOTE.TXT)

If we change offset 06 and 63 from 09 to 00 and save it, we will get a string of text.

![](<../.gitbook/assets/image (17).png>)

![](<../.gitbook/assets/image (52).png>)

This was actually Base64 encoded, pretty tricky since it doesn't have any `=` behind the string of text. We could decode the Base64 [here](https://www.base64decode.org/).

![](<../.gitbook/assets/image (92).png>)

Finally, we get an output that is URL encoded and we can decode it [here](https://www.urldecoder.org/), giving us the flag.

![](<../.gitbook/assets/image (3).png>)

Flag: LNC{why\__%1s\_th3\_pa5sw0rd\_@f4ke}_
