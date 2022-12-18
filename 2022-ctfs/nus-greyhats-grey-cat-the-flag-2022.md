---
description: >-
  NUS Greyhats Grey Cat The Flag 2022 is a CTF competition organised by NUS
  Greyhats, held from 6 - 10 June 2022.
---

# NUS Greyhats Grey Cat The Flag 2022

I participated in this this CTF as solo with the team name : onetime. This CTF was during my exam week. Initially, I wasn't planning to join this event since I had exams on 6 June and 9 June.  &#x20;

After some thought, I decided to join on the 7/8 June but I did not spend too much time attempting the challenges. More information about the CTF competition could be found [here.](https://ctftime.org/event/1643/)&#x20;

For this CTF competition, I solved 2 challenges in the MISC category.

## Image Upload

![](<../.gitbook/assets/image (500).png>)

In this challenge, we were given  .pcap file.&#x20;

{% file src="../.gitbook/assets/dump.pcap" %}

First, We open `dump.pcap` on [Wireshark](https://www.wireshark.org/) to analyse further.

If we read the challenge description, it mentioned that `HTTP is not secure`.

We could inspect the packets by applying this filter

`http.request.method == POST`

![](<../.gitbook/assets/image (583).png>)

There is only 1 packet shown. We could right click on that packet, and select `Follow > TCP Stream`. If we paid close attention, we could already see the flag here.

![](<../.gitbook/assets/image (586).png>)

An alternative solution would be to select file, `Export Objects > HTTP`&#x20;

![](<../.gitbook/assets/image (587).png>)

As you can see, we found the same packet, `packet 27331`.

We could get the flag by inspecting and expanding this packet information under `MIME Multipart Media Encapsulation > Portable Network Graphics > Textual data`

We can see the flag under `String`

![](<../.gitbook/assets/image (591).png>)

The challenge mentioned `extract the image. Then find the name of the creator of this image`.

If we were to follow the instructions provided in the challenge description, we could go to the same packet, go to `MIME Multipart Media Encapsulation` and expand until we see `Portable Network Graphics`, right click and select `Copy Bytes as Hex + ASCII Dump`.

![](<../.gitbook/assets/image (548).png>)

Then, we could go to [CyberChef](https://cyberchef.org/) and paste the data in the Input.

CyberChef would suggest to `Render Image` and we could just click on the `magic wand` icon

After clicking the icon, we would get a PNG Image from this [CyberChef recipe](https://cyberchef.org/#recipe=From\_Hexdump\(\)Render\_Image\('Raw'\)).

![](<../.gitbook/assets/image (547).png>)

We save this output to a file `flag.png`

![](<../.gitbook/assets/image (543).png>)

Finally, we upload `flag.png` on an [online exiftool](https://exif.tools/) and we will see the flag appear in `Author` description.

![](<../.gitbook/assets/image (518).png>)

Check out my other writeups where I used Wireshark [here](https://gadiel-lau.gitbook.io/2022-writeups/sg-cyber-olympian-trials-2022#what-did-i-send) and [here.](https://gadiel-lau.gitbook.io/2022-writeups/lagncrash-interpoly-ctf-2022#nothing-here)

Flag: grey{wireshark\_exiftool\_are\_good}

## Ghost

![](<../.gitbook/assets/image (502).png>)

In this challenge, we are provided a `ghost` file. This file does not have any file extensions and cannot be opened "normally".

{% file src="../.gitbook/assets/ghost" %}

First, I opened it in notepad to check its contents. In notepad, we are presented with a bunch of encoded messages.

![](<../.gitbook/assets/image (560).png>)

```
I got message for you:

NTQgNjggNjkgNzMgMjAgNjkgNzMgMjAgNmUgNmYgNzQgMjAgNjkgNzQgMjAgNmQgNjEgNmUgMmMgMjAgNzQgNzIgNzkgMjAgNjggNjEgNzIgNjQgNjUgNzIgMjE=

++++++++++[>+>+++>+++++++>++++++++++<<<<-]>>>++++++++++++++.>++++.+.++++++++++.<<++.>>----------.++++++++++.<<.>>----------.+++++++++++.<---------------------.<.>>------.-------------.+++++++.

pi pi pi pi pi pi pi pi pi pi pika pipi pi pipi pi pi pi pipi pi pi pi pi pi pi pi pipi pi pi pi pi pi pi pi pi pi pi pichu pichu pichu pichu ka chu pipi pipi pipi pipi pi pi pi pi pi pi pi pi pikachu pi pi pi pikachu ka ka ka pikachu pichu pichu pi pi pikachu pipi pipi pi pi pikachu pi pikachu
 		  			 			  	  		  	 	 				  	 				 		 		  			 		 	     		     			  		  		 			 	 					 		   	  				  	 			 	    		  		  	  	   	 					 		 			   		     			 	   	 					  		   	 		 			  			 		  		 	  	 			  		 	  	  	 		   	  		 		    		  		 					 	
KRUGS4ZANFZSA3TPOQQHI2DFEBTGYYLHEBWWC3RAIQ5A====

synt{abgGungFvzcyr:C}

Me: Message received.
```

The first message `NTQgNjggNjkgNzMgMjAgNjkgNzMgMjAgNmUgNmYgNzQgMjAgNjkgNzQgMjAgNmQgNjEgNmUgMmMgMjAgNzQgNzIgNzkgMjAgNjggNjEgNzIgNjQgNjUgNzIgMjE=`

is encoded in Base64, we know this from the commonly appended `=` or `==` in Base64.

The second message consisting of `+`, `[`, `>` etc.,&#x20;

`++++++++++[>+>+++>+++++++>++++++++++<<<<-]>>>++++++++++++++.>++++.+.++++++++++.<<++.>>----------.++++++++++.<<.>>----------.+++++++++++.<---------------------.<.>>------.-------------.+++++++.`

is clearly [brainfuck](https://esolangs.org/wiki/Brainfuck). We had encountered `brainfuck` before in another challenge [here](https://gadiel-lau.gitbook.io/2020-writeups/govtech-stack-the-flags-ctf-2020/forensics).

The third message consisting of `pi`,`pika`,`pipi` etc., is [Pikalang](https://esolangs.org/wiki/Pikalang).

`pi pi pi pi pi pi pi pi pi pi pika pipi pi pipi pi pi pi pipi pi pi pi pi pi pi pi pipi pi pi pi pi pi pi pi pi pi pi pichu pichu pichu pichu ka chu pipi pipi pipi pipi pi pi pi pi pi pi pi pi pikachu pi pi pi pikachu ka ka ka pikachu pichu pichu pi pi pikachu pipi pipi pi pi pikachu pi pikachu`

&#x20;If you had never heard of this before, you could just Google `Pikachu Language` and you would find similar results.

The fourth message is&#x20;

``![](<../.gitbook/assets/image (511).png>)``

is encoded in Base32, we know this from the commonly appended `===` or `====` in Base32.&#x20;

The fifth message is&#x20;

`synt{abgGungFvzcyr:C}`

is encoded in ROT13, we know this as it looked like there is a shift in characters.

Note that we had encountered Base64, Base32 and ROT13 in my previous [writeup](https://gadiel-lau.gitbook.io/2022-writeups/aisp-cyber-wellness-ctf#mix-and-match).

We could try to decrypt these messages using online tools listed below:

[CybefChef](https://cyberchef.org/): [Base64](https://cyberchef.org/#recipe=From\_Base64\('A-Za-z0-9%2B/%3D',true,false\)From\_Hex\('Space'\)\&input=TlRRZ05qZ2dOamtnTnpNZ01qQWdOamtnTnpNZ01qQWdObVVnTm1ZZ056UWdNakFnTmprZ056UWdNakFnTm1RZ05qRWdObVVnTW1NZ01qQWdOelFnTnpJZ056a2dNakFnTmpnZ05qRWdOeklnTmpRZ05qVWdOeklnTWpFPQ), [Base32](https://cyberchef.org/#recipe=From\_Base32\('A-Z2-7%3D',false\)\&input=S1JVR1M0WkFORlpTQTNUUE9RUUhJMkRGRUJUR1lZTEhFQldXQzNSQUlRNUE9PT09), [ROT13](https://cyberchef.org/#recipe=ROT13\(true,true,false,13\)\&input=c3ludHthYmdHdW5nRnZ6Y3lyOkN9)

[dCode](https://www.dcode.fr/tools-list#programming\_language): [Brainfuck](https://www.dcode.fr/brainfuck-language), [Pikalang](https://www.dcode.fr/pikalang-language)

Base64 output:

![This is not it man, try harder!](<../.gitbook/assets/image (512).png>)

Brainfuck output:

![This is it? nah](<../.gitbook/assets/image (515).png>)

Pikalang output:

![lol no](<../.gitbook/assets/image (523).png>)

Base32 output:

![This is not the flag man D:](<../.gitbook/assets/image (517).png>)

ROT13 output:

![flag{notThatSimple:P}](<../.gitbook/assets/image (528).png>)

As we can see, none of the 5 decoded messages gave us the correct flag.

At this point, it seemed like a dead end. How could we solve this?

I tried pressing `CTRL+A` on Notepad to see if there could be some possible ways of hiding messages in the file, but could not find anything as well.

Next, I opened it in my hex editor : [HxD](https://mh-nexus.de/en/hxd/), and found something interesting. Note that you can use any [online hex editor](https://hexed.it/) too. I noticed a bunch of dots and spaces in between from the decoded text.

![](<../.gitbook/assets/image (522).png>)

My first thought is... could this be morse code? I typed out the dots and spaces manually onto a new Notepad file. This was quite time consuming and there is actually an easier way to solve this. Continue reading till the end to find out :)

```
.. ..  ... ...  .  ..  . . ....  . .... .. ..  ... .. .     ..     ...  ..  .. ... . ..... ..   .  ....  . ... .    ..  ..  .  .   . ..... .. ...   ..     ... .   . .....  ..   . .. ...  ... ..  .. .  . ...  .. .  .  . ..   .  .. ..    ..  .. ..... ...
```

If I input this in an[ online morse code decoder](https://morsecode.world/international/translator.html), the output would not make any sense

![](<../.gitbook/assets/image (526).png>)

After some searching online, I found out this is `Whitespace steganography`. I decided to try [stegsnow](https://manpages.ubuntu.com/manpages/bionic/man1/stegsnow.1.html) - whitespace steganography program. But as you can see, it didn't work or produce any output.

![](<../.gitbook/assets/image (541).png>)

Then, I found 2 writeups [here](https://shankaraman.wordpress.com/tag/hackyou-2012-stegano-writeups/) and [here](https://reese.dev/codemash2019-ctf-solutions/#ghost-text) which were useful in helping me solve this challenge.

I replaced dots with `1` and spaces with `0` in a code editor like [Visual Studio Code](https://code.visualstudio.com/) using the `CTRL+H` shortcut to find and replace and `CTRL+ALT+ENTER` shortcut to replace all, which would give me this output:

`110110011101110010011001010111100101111011011001110110100000110000011100110011011101011111011000100111100101110100001100110010010001011111011011100011000001110100010111110011000101101110011101100110100101110011010010010110001001101100001100110111110111`

I went on to copy paste these binary into a text converter [here](https://www.asciitohex.com/), however this did not give me any output for `Text`.

Since I know the flag format (i.e. `grey{ }`) , I checked for what `grey` in binary looked like

![](<../.gitbook/assets/image (534).png>)

I compared this binary output to the binary output I had earlier and I noticed 2 extra `1`s in front. Those 2 extra dots probably represented an extra new line but I copied it as well. Removing the extra `1` s would give me the flag.

![](<../.gitbook/assets/image (532).png>)

For this challenge, the Author's writeup solution was simple and easy to follow. Refer to the image below for author writeup solution. Notice there are repeating `20` and `09` in the hex data.&#x20;

By using this [CyberChef recipe](https://cyberchef.org/#recipe=Find\_/\_Replace\(%7B'option':'Regex','string':'20'%7D,'0',true,false,true,false\)Find\_/\_Replace\(%7B'option':'Regex','string':'09'%7D,'1',true,false,true,false\)From\_Binary\('Space',8\)\&input=MjAgMDkgMDkgMjAgMjAgMDkgMDkgMDkgMjAgMDkgMDkgMDkgMjAgMjAgMDkgMjAgMjAgMDkgMDkgMjAgMjAgMDkgMjAgMDkgMjAgMDkgMDkgMDkgMDkgMjAgMjAgMDkgMjAgMDkgMDkgMDkgMDkgMjAgMDkgMDkgMjAgMDkgMDkgMjAgMjAgMDkgMDkgMDkgMjAgMDkgMDkgMjAgMDkgMjAgMjAgMjAgMjAgMjAgMDkgMDkgMjAgMjAgMjAgMjAgMjAgMDkgMDkgMDkgMjAgMjAgMDkgMDkgMjAgMjAgMDkgMDkgMjAgMDkgMDkgMDkgMjAgMDkgMjAgMDkgMDkgMDkgMDkgMDkgMjAgMDkgMDkgMjAgMjAgMjAgMDkgMjAgMjAgMDkgMDkgMDkgMDkgMjAgMjAgMDkgMjAgMDkgMDkgMDkgMjAgMDkgMjAgMjAgMjAgMjAgMDkgMDkgMjAgMjAgMDkgMDkgMjAgMjAgMDkgMjAgMjAgMDkgMjAgMjAgMjAgMDkgMjAgMDkgMDkgMDkgMDkgMDkgMjAgMDkgMDkgMjAgMDkgMDkgMDkgMjAgMjAgMjAgMDkgMDkgMjAgMjAgMjAgMjAgMjAgMDkgMDkgMDkgMjAgMDkgMjAgMjAgMjAgMDkgMjAgMDkgMDkgMDkgMDkgMDkgMjAgMjAgMDkgMDkgMjAgMjAgMjAgMDkgMjAgMDkgMDkgMjAgMDkgMDkgMDkgMjAgMjAgMDkgMDkgMDkgMjAgMDkgMDkgMjAgMjAgMDkgMDkgMjAgMDkgMjAgMjAgMDkgMjAgMDkgMDkgMDkgMjAgMjAgMDkgMDkgMjAgMDkgMjAgMjAgMDkgMjAgMjAgMDkgMjAgMDkgMDkgMjAgMjAgMjAgMDkgMjAgMjAgMDkgMDkgMjAgMDkgMDkgMjAgMjAgMjAgMjAgMDkgMDkgMjAgMjAgMDkgMDkgMjAgMDkgMDkgMDkgMDkgMDkgMjAgMDk), we could get the flag.

![](<../.gitbook/assets/image (569).png>)

Flag: grey{gh0s7\_byt3$\_n0t\_1nvisIbl3}

## Grab Food Voucher

Some joked that this is the actual CTF challenge. This was a $20 Grab Food Voucher giveaway during the CTF competition. A Grab Food link was provided every day from 6 - 9 June. Participants are required to fill up a Google Forms to include information such as name, email and team name.

![](<../.gitbook/assets/image (578).png>)

![](<../.gitbook/assets/image (558).png>)

These vouchers are only limited to the first 150 participants who submit the form. I missed the first 2 days of this giveaway event as I joined this CTF late...

In the subsequent days, I managed to submit the form within 1 minute and got $20 x 2 = $40 worth of Grab Food Vouchers. Thanks to the sponsors : CSA, GuardRails, Ensign.&#x20;

Notice we need to submit the form really fast here to get the vouchers, at 9.01pm which is 1 minute+ later, all 150 vouchers would be gone.

![](<../.gitbook/assets/image (594).png>)

![](<../.gitbook/assets/image (545).png>)

![](<../.gitbook/assets/image (525).png>)
