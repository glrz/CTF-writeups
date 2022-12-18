# Steganography

## Doc-ception

![](<../../.gitbook/assets/image (24).png>)

For this challenge, we were given a `.docx` file.

{% file src="../../.gitbook/assets/loremipsum.docx" %}

Using the `binwalk` we can see that there are hidden files in this word document.

![](<../../.gitbook/assets/image (74).png>)

We can proceeded to use `-e` to extract the embedded files.

![](<../../.gitbook/assets/image (95).png>)

Then, we can go to the extracted directory and check the contents

![](<../../.gitbook/assets/image (23).png>)

There is another word document. Lets check if there are embedded files using `binwalk` command again.

![flag.txt file inside](<../../.gitbook/assets/image (58).png>)

Now, we use `-e` to extract the files again

![](<../../.gitbook/assets/image (67).png>)

Go to the extracted directory and simply use `cat` command to read the contents of flag.txt

![](<../../.gitbook/assets/image (17).png>)

Flag: brixelCTF{openxml}

## Limewire audio

![](<../../.gitbook/assets/image (32).png>)

In this challenge, we are given a .wav audio file.

{% file src="../../.gitbook/assets/sweet_tune.wav" %}

If we play the audio, we will recognise its an audio of [Darude sandstorm](https://www.youtube.com/watch?v=y6120QOlsfU), nothing out of the ordinary.

Lets use Audacity to analyze it further.

If we open the audio file in Audacity and change the mode to spectrogram

![](<../../.gitbook/assets/image (53).png>)

we can see a hello kitty in the middle.

![](<../../.gitbook/assets/image (79).png>)

Flag: brixelCTF{hellokitty}

## Scan me

![](<../../.gitbook/assets/image (56).png>)

In this challenge, we were given a `.png` file.

{% file src="../../.gitbook/assets/qr-code.png" %}

This challenge is a scan puzzle. We can use this online tool [here](https://online-barcode-reader.inliteresearch.com/), which is able to scan different types of barcode or QR codes, to solve this challenge.

For the first part, if we scan the QR code, we can see that there's another QR code in the QR code.

![http://www.timesink.be/qrcode/flag.html
](<../../.gitbook/assets/image (15).png>)

If we enter the website, we are greeted with a barcode, this is the standard code-128, if scanned it reads: code-128-easy, enter it on the website.

The next one is a ean13 barcode, reading: 5449000133335, enter it on the website.

The next one is a Pdf417 type barcode: reading: congratulations\_this\_is\_the\_last\_barcode if you enter this on the site you get the flag

Flag: brixelCTF{m4st3r\_0f\_sc4n5}

## Rufus the vampire cat

![](<../../.gitbook/assets/image (60).png>)

In this challenge, we are given a jpg image and we know this is a steganography challenge.&#x20;

{% file src="../../.gitbook/assets/rufus.jpg" %}

First we can try using `stegoveritas` like how we did it [here](https://gadiel-lau.gitbook.io/2020-writeups/gsctf-2020#wheres-the-file).

![](<../../.gitbook/assets/image (71).png>)

It looks like it found something with StegHide, lets go to the directory to check. Opening the file gives us the flag.

![the flag is: chucktesta](<../../.gitbook/assets/image (137).png>)

Flag: brixelCTF{chucktesta}
