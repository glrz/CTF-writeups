# Forensics

## Voices in the head

We are presented with this challenge Voices in the head. Initially, this challenge was tough and there were barely any solves for it. After a while, a hint was released : Xiao wants to help. Will you let him help you?

![](../../.gitbook/assets/11)

We were provided with an audio .wav file.

{% file src="../../.gitbook/assets/forensics-challenge-2.wav" %}

Here I used spectrum analyzer from [here ](https://academo.org/demos/spectrum-analyzer/)to analyze the file.

![](../../.gitbook/assets/13)

From this output : aHR0cHM6Ly9wYXN0ZWJpbi 5jb20vakVUajJ1VWI= , I quickly recognized it as Base64 encoded based on previous CTF experience.

I proceeded to decode it online [here ](https://www.base64decode.org/)

![](../../.gitbook/assets/14)

Decoding it will give us a pastebin link as output : https://pastebin.com/jETj2uUb

Open the pastebin link, we can see some various symbols +-.\[]

![](../../.gitbook/assets/15)

This is my first time seeing something like this in RAW paste data portion, so I went on to Google it and found out that it is an esoteric programming language called brainfuck.

To interpret the brainfuck code, we can use an online tool [here ](https://www.dcode.fr/brainfuck-language)

![](../../.gitbook/assets/16)

This will give us the output: thisisnottheflag

At this point, it just seemed like a dead end. I decided to go back to look at the challenge description and this was when I saw the hint. The first thing that came to my mind was that “xiao” could be a tool that could assist me in this challenge. Hence, I googled “xiao tool” and found this tool Xiao Steganography.

Extract the audio file as TXT file using Xiao Steganography

Password to extract: thisisnottheflag (from the output earlier)

![](../../.gitbook/assets/17)

Opening up the TXT file, I could see a bunch of gibberish text. But at the bottom, it looks like we have something which looks like the flag.

![](../../.gitbook/assets/18)

However, that is not the flag. It turns out flag: govtech-csg{Th1sisn0ty3tthefl@g} could just be a fake flag.. Upon closer inspection, I realized there is a This is it.docx in this TXT file and I suspected that could be a file embedded in it.

Next, I tried extracting the audio file as a zip file while using the same password to extract: thisisnottheflag

I realised there’s a password protected thisisit.docx in the zip file. I tried using ‘govtech-csg{Th1sisn0ty3tthefl@g}’ as the password and surprisingly I got access to it.

Opening up the This is it.docx file gives us the flag

![](../../.gitbook/assets/19)

Flag: govtech-csg{3uph0n1ou5\_@ud10\_ch@ll3ng3}
