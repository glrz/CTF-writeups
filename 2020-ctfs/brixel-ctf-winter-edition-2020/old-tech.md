# Old tech

## punchcard

![](<../../.gitbook/assets/image (12).png>)

For this challenge, we were given a `.png` file.

{% file src="../../.gitbook/assets/punchcard.png" %}

If we look at the punchcard, we can see that there is a section that is been blacked out.&#x20;

This is where the plaintext normally would be, but the punched out parts are still visible. Using an online tool [here](https://www.masswerk.at/cardreader/), we can still read what's on the card without having to see the paintext part.

![](<../../.gitbook/assets/image (2).png>)

Flag: BRIXELCTF(M41NFR4M3)

## The tape

![](<../../.gitbook/assets/image (88).png>)

For this challenge, we were given a `.wav` file.

{% file src="../../.gitbook/assets/CTF-TAPe.wav" %}

We can tell by the sound that it's a machine signal that has been recorded, in the description they speak of games and the 80's so that narrows it down quite a bit.&#x20;

The commodore64 was commonly used with cassette tapes to store/load programs on it, so that's what we are going to try. We could either record the sound to a real cassette and play it on a real C64, but for this challenge let's use emulators.&#x20;

First we need to change the sound to a TAP file (a tape file for the emulator) We do this by using audioTAP (download [here](https://sourceforge.net/projects/wav-prg/files/audiotap/2.2.1/audiotap-2.2.1-win32.zip/download)). When we have the TAP file we can get the PRG file from it using wavPRG (download [here](http://sourceforge.net/projects/wav-prg/files/wav-prg/4.2.1/wavprg-4.2.1-win32.zip/download))&#x20;

Now we need an emulator to run the PRG file, we use C64 forever (download [here](https://www.c64forever.com/)). Install it and then double click the prg file it should run the program on the emulator.&#x20;

It reads: CONGRATULATIONS! THE FLAG IS BASIC

_Flag:_ brixelCTF{BASIC}

