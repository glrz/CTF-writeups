---
description: >-
  CSIT Challenge of Wits 2022 is a cybersecurity challenge held from 1-8 April
  2022.
---

# CSIT Challenge of Wits 2022

Challenge of Wits 2022 series had 4 different challenges. I completed Challenge 1: Simulation & Training and Challenge 3: Cyber Forensics and Cryptography. I am glad I won the grand prize for Challenge 3: Cyber Forensics and Cryptography. The grand prize includes Logitech Pro X Keyboard, Logitech Pro Wireless Gaming Mouse and a Razer Barracuda X – Black Headphones. More information could be found [here.](https://www.dtcareers.gov.sg/terms-conditions-and-frequently-asked-questions)

![](<.gitbook/assets/WhatsApp Image 2022-07-29 at 8.38.02 AM.jpeg>)

You could also find picture taken for the prize presentation on the social media platforms below:

Instagram - [DSTA](https://www.instagram.com/p/CdXMgXMtYTt/?hl=en), [DSO](https://www.instagram.com/p/CdXB0MWldfd/?hl=en)

Facebook - [DSTA](https://www.facebook.com/watch/?v=976745656328895\&ref=sharing), [DSO](https://www.facebook.com/watch/?v=425901772698199\&ref=sharing)

LinkedIn - [CSIT](https://www.linkedin.com/posts/csitsg\_congrats-to-csit-challenge-winner-activity-6929613335273369600-Yita/), [DSTA](https://www.linkedin.com/posts/dsta\_designdevelopdefend-challengeofwits-dtcareers-activity-6929768428375334912-xRqn/), [DSO](https://www.linkedin.com/posts/dso-national-laboratories\_dtc-challenge-of-wits-challenge-3-grand-activity-6929611066968563712-Wb2Q/)

I would only be doing the writeup for Challenge 3, which is cybersecurity related.

This challenge mirrors real-life situation faced against defense engineers in their work against cybersecurity threats of uncovering malware hidden in seemingly harmless files. We are given 2 JPG files for this challenge. The hint given for this challenge is that both file sizes are different.

![](<.gitbook/assets/image (484).png>)

More information about the challenge could be found on [YouTube](https://www.youtube.com/watch?v=meMMPPDgFOI).

For this challenge, I split my solving process into 3 stages.

## STAGE 1

Given the 2 JPG files [_Original.jpg_](https://drive.google.com/file/d/1gpaN92F8eZr\_Skj5cPq67oxLEcGZDdna) and [_Challenge.jpg_](https://drive.google.com/file/d/1v1Y18gaKJuifvf5fLR6OFZypNbUUEoCq), I proceeded to download the files first.

From the hint given, we know that the file sizes of the files are different. This led me to think that there could be additional bytes appended at the end of `Challenge.jpg` file. Note that we could add additional bytes to the end of the JPG file and the image would still look the same.

To do further analysis on the data, I opened it on a hex editor like [HxD](https://mh-nexus.de/en/hxd/) on Windows.&#x20;

![](<.gitbook/assets/image (480).png>)

If you are on Linux, you could download any hex editor like GHex which can be downloaded [here](https://installati.one/kalilinux/ghex/) to analyze the data. Whichever hex editor you use, you would see a chunk of data at the bottom.

![](<.gitbook/assets/image (468).png>)

Alternatively, we could use the `strings` command in Kali Linux and see the same text

![](<.gitbook/assets/image (408).png>)

![](<.gitbook/assets/image (450).png>)

The highlighted text `aHR0cHM6Ly9kcml2ZS5nb29nbGUuY29tL2ZpbGUvZC8xeDA1NjY0MjkyaFozZWRaOXhRNWcwUk9rQWJMNTBkUjkvdmlldz91c3A9c2hhcmluZw==` is Base64 encoded. We know this from previous CTF experience.&#x20;

We could use an online tool [here](https://www.base64decode.org/) to help us decode this string. Once its decoded, we will see a [Google Drive link](https://drive.google.com/file/d/1x05664292hZ3edZ9xQ5g0ROkAbL50dR9/view?usp=sharing).&#x20;

Alternatively, we could use this command to decode Base64 strings on Kali Linux terminal

echo `string` | base64 -d

`-d` option stands for decode

![](<.gitbook/assets/image (478).png>)

Then `CTRL+ click` on the link.

After we click on the link, we could download the zip file `learn_more_about_CSIT.zip`.&#x20;

If we open the zip file, we will see 3 PDF and a secret file. However, these files are all password protected.

![](<.gitbook/assets/image (417).png>)

![](<.gitbook/assets/image (467).png>)

If we recall, we saw a string of text above the Base64 encoded text just now

`DESIGN-DEVELOP-DEFEND`

![](<.gitbook/assets/image (460).png>)

At this point, I recalled a similar forensics challenge that I solved it the past [here](https://gadiel-lau.gitbook.io/2020-writeups/govtech-stack-the-flags-ctf-2020/forensics), which also had a password protected zip file. The password of the zip file was a fake flag embedded in another file. Could the password be `DESIGN-DEVELOP-DEFEND`?

Indeed, now I could unlock all these file and view its content.

An alternative approach I tried is to save the strings we found previously into a .txt file

![](<.gitbook/assets/image (410).png>)

Use `zip2john file.zip hash` command to save the zip hash to hash file

Then, use `john --wordlist=Challenge.txt hash` to crack the password using the strings saved earlier.

![Password: DESGIN-DEVELOP-DEFEND](<.gitbook/assets/image (497).png>)

Fun fact: Many people actually submitted `DESIGN-DEVELOP-DEFEND` as the flag for this challenge. I was told by one of the challenge author - Samuel Teo.&#x20;

However, I clearly knew this wasn't the secret message or flag based on past CTF experiences.

## STAGE 2

Among the 4 files in the zip, 3 of them are PDFs containing information about CSIT, while the last file `secret` could likely contain the secret message or flag. This `secret` file cannot be identified as any file type and cannot be opened normally.&#x20;

I opened this in GHex to analyze further. Here I saw `CSIT` appear a few times

![](<.gitbook/assets/image (407).png>)

Running `strings` and `grep` command confirmed it.

![](<.gitbook/assets/image (440).png>)

At this point, there were a few questions in my mind. The data in the file is all gibberish text, could it be encrypted somehow? Could `CSIT` be a key to solve this challenge?

Having seen quite a few CTF challenges on XOR, I guessed that it could be XOR encrypted. The XOR encryption algorithm is an example of symmetric encryption where **the same key is used to both encrypt and decrypt a message**. More information about XOR can be found [here. ](https://en.wikipedia.org/wiki/XOR\_cipher)

Now, we could use an online tool like [XOR Cracker](https://wiremask.eu/tools/xor-cracker/) to guess the key used to encrypt the data.

Uploading the file on the website will get us the most probable key lengths and the possible keys.

![](<.gitbook/assets/image (469).png>)

Alternatively, I could run `xortool` with `-b` option to brute force the possible key. `xortool` can be downloaded [here](https://github.com/hellman/xortool).

![](<.gitbook/assets/image (465).png>)

After we know the key, we could decrypt it on [CyberChef](https://cyberchef.org/#recipe=XOR\(%7B'option':'UTF8','string':'CSIT'%7D,'Standard',false\)). Then we save it as `flag.jpg` as I realised the `JFIF` usually suggest that it is a JPG file.

![XOR operation on CyberChef with key — CSIT on secret file](<.gitbook/assets/image (432).png>)

However, the file is corrupted and I could not view the image.&#x20;

## STAGE 3

Opening it on HxD suggest that the first 4 bytes are all 0.&#x20;

![](<.gitbook/assets/image (477).png>)

This should not be the case. Every file type will have [file signatures](https://en.wikipedia.org/wiki/List\_of\_file\_signatures) at the beginning of the data.

If we look up `jpg`, we would find that it should start with `FF D8 FF E0`.&#x20;

![](<.gitbook/assets/image (446).png>)

Alternatively, we could open up the `Original.jpg` file provided in the challenge in HxD and check the correct values.

![](<.gitbook/assets/image (427).png>)

Using HxD, I modified the first 4 bytes to `FF D8 FF E0` and saved the file.

![](<.gitbook/assets/image (405).png>)

Finally, we can open the JPG file and see the secret message below

![](<.gitbook/assets/image (422).png>)

Note: I did not realise there were hints in the PDFs probably because I was too focused in trying to get out the secret message from `secret` file.&#x20;

Check out the author's writeup [here.](https://medium.com/csit-tech-blog/challenge-of-wits-challenge-3-solution-writeup-37e9f65d024d)

Secret message : CSIT{Lik3d\_th1s\_ch4llen9e?\_c0me\_j01n\_CSIT!}
