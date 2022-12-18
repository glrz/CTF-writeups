# Reverse engineering and cracking

## Cookie

![Not attempted during CTF](<../../.gitbook/assets/image (13).png>)

For this challenge, we were given 2 files.

{% file src="../../.gitbook/assets/cookieclicker_linux.tar" %}

{% file src="../../.gitbook/assets/cookieclicker_win.zip" %}

There might be a few ways to get the required result, but we can edit the memory values of the game using artmoney (free download [here](http://artmoney.ru/)).&#x20;

First, we run the game and make a few clicks to get a base score to find. Then run artmoney, select the process and do a search for the amount of clicks we made.&#x20;

It should take a few and show a lot of results. Make some more clicks to change the click counter, and press filter in artmoney. Change the value to the new amount of clicks and let it filter.&#x20;

Repeat the process until only 1 value remains, then press the red button to move it to the right column. Here we can edit the value by double clicking it. Set it to 10000000 and make another click, giving us the flag.



## no peeking!

![](<../../.gitbook/assets/image (29).png>)

For this challenge, we were given a `.exe` file.

{% file src="../../.gitbook/assets/noPEEKing.exe" %}

Here we used a program called dotPEEK by jetbrains, which is basicaly a .NET decompiler.&#x20;

We can use it to convert .exe files (written in .NET) back to a semi-readable source code.&#x20;

We can download it [here](https://www.jetbrains.com/decompiler/). Install the program, open it and select file open. Point it to the nopeeking.exe file.&#x20;

Now we expand the project in the left column and expand the code part called noPEEKing, double click on Form1 and navigate to the showFlag() function. It will now decompile and show us the flag.

![](<../../.gitbook/assets/image (86).png>)

Flag: brixelCTF{d0tP33K}

## Registerme

![Not attempted during CTF](<../../.gitbook/assets/image (274).png>)

For this challenge, we were given a `.exe` file.

{% file src="../../.gitbook/assets/registerme.exe" %}

There is a tool that helps us monitor what a process is doing, it's called procmon and it's free to download [here](https://docs.microsoft.com/en-us/sysinternals/downloads/procmon).&#x20;

Run the registerme program, and then run procmon. Drag the 'target' icon next to the big A on the toolbar to the registerme.exe window. Here we can see what calls the program is making to the OS, one of those calls is 'QueryDirectory' for a file called activation.key which returned NO SUCH FILE.&#x20;

We create an empty file called activation.key in the same folder as the registerme app and that should register it.

Flag: brixelCTF{f1l34cc3ss}&#x20;

## Android app

![Not attempted during CTF](<../../.gitbook/assets/image (35).png>)

For this challenge, we were given a `.apk` file.

{% file src="../../.gitbook/assets/brixelCTF.apk" %}

First we need to extract the APK file and decompile the javascript, we can use an online tool [here, ](http://www.javadecompilers.com/apk)this spits out a zipfile containing the android package. This was a similar challenge to what I had done before [here](https://gadiel-lau.gitbook.io/2020-writeups/gsctf-2020#apk), where I used the same tool to get the flag.

In these files there is a folder under sources called appinventor, if we go down that folder there are 4 java files. A quick search of the flag format: "brixelCTF{" will find the flag quickly in screen1.java

![](<../../.gitbook/assets/image (9).png>)

Flag: brixelCTF{th3\_4ndr0ids\_y0u\_4r3\_l00k1ng\_f0r}

