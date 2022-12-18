# MISC

## Diving in

![](<../../.gitbook/assets/image (236).png>)

We were given this image that was described as papers in the bin. Seemed like dumpster diving.

![](<../../.gitbook/assets/image (139).png>)

I zoomed in each one of them to identify the flag

![Flag part1: govtech-csg{dump](<../../.gitbook/assets/image (214).png>)

![Flag part2: ster\_diving](<../../.gitbook/assets/image (27).png>)

![Flag part3: \_is\_impre](<../../.gitbook/assets/image (246).png>)

![Flag part4: ssive}](<../../.gitbook/assets/image (208).png>)

Combining the 4 parts, we get the flag.

Flag: govtech-csg{dumpster\_diving\_is\_impressive}

## FWO FWF

![](<../../.gitbook/assets/image (150).png>)

We are given a link to this web server

![This does not look anything like a flag to me.](<../../.gitbook/assets/image (197).png>)

Go to Inspect the page(CTRL+SHIFT+I or F12), we can see something interesting here

![](<../../.gitbook/assets/image (186).png>)

Here I realised that some class are hidden, in this case a and b are hidden and only c is showing. Following the steps below, I solved the challenge.

1. Show .a , hide .c and .b

![Here we get the message that the flag is hidden in a file](<../../.gitbook/assets/image (200).png>)

2\. Show .b, hide .a and .c

![Now we can tell that the flag is hidden in CSG.TXT file](<../../.gitbook/assets/image (267).png>)

3\. Go to the /CSG.TXT path by adding /CSG.TXT to the end of the web address&#x20;

![encoded in base 64 format](<../../.gitbook/assets/image (188).png>)

4\. Decode the base 64 string on [here ](https://cryptii.com/)

![Get output : Fj4c\_Gu3\_fGlY3\_i1f1o1Y1Gl](<../../.gitbook/assets/image (108).png>)

Realised it’s still not yet the flag, but it looks like a flag, so there might be a shift in characters

5\. Decode it with ROT13 and get the flag

![](<../../.gitbook/assets/image (226).png>)

Flag: govtech-csg{Sw4p\_Th3\_sTyL3\_v1s1b1L1Ty}

## REconstrucQ

![](<../../.gitbook/assets/image (228).png>)

We were given a torn/broken QR code for this challenge

![](<../../.gitbook/assets/image (255).png>)

I tried to use cyberchef – randomize color palette

![](<../../.gitbook/assets/image (249).png>)

![](<../../.gitbook/assets/image (103).png>)

Somehow, I was really lucky? This worked for my first try and I scanned the QR code and got the flag. But later, I realised this does not work 100%, the QR code could not be scanned after a few more tries.

For this challenge, we could probably use other tools like QRazybox, stegsolve, stegoveritas to solve.

![](<../../.gitbook/assets/image (69).png>)

![](<../../.gitbook/assets/image (129).png>)

Flag: govtech-csg{QR\_3rr0r\_R3c0v3ry\_M4giC!}

## Welcome Challenge

After spending much time searching on google, found this Github page and we can get the flag here.

![](<../../.gitbook/assets/image (256).png>)

Flag : govtech-csg{W3lcom3\_to\_ST4CK\_TH3\_FL4GS\_2o2o!}

## Emmel

This challenge provided us with a login page.

Visiting the login page shows us a file prompt for a JPG image and the question ‘What is my favorite thing?’.

![](<../../.gitbook/assets/image (138).png>)

I was really lucky again I just uploaded a random JPG image and got the flag.

![](<../../.gitbook/assets/image (109).png>)

## Beep Boop

![](<../../.gitbook/assets/image (120).png>)

In this challenge, we are given a .wav file.&#x20;

{% file src="../../.gitbook/assets/misc-challenge-2.wav" %}

After doing some research online, I found out that this is `Slow Scan Television Transmission`(SSTV). We can use robot36-sstv image decoder on phone to get the flag. Some other tools like QSSTV/RX-SSTV could be used as well.

![](<../../.gitbook/assets/image (187).png>)

Flag: govtech-csg{C00L\_SL0w\_Sc4n\_T3L3v1S1on\_tR4nsM1ss10N}

