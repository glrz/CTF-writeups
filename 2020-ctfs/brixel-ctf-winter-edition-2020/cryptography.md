# Cryptography

## Sea Code

![](<../../.gitbook/assets/image (22).png>)

For this challenge, we were given a `.wav` file.

{% file src="../../.gitbook/assets/message.wav" %}

This challenge was similar to what we have solved in GSCTF 2020 before. You can refer to my previous writeup [here](https://gadiel-lau.gitbook.io/2020-writeups/gsctf-2020#beeps). Using the same tool, we get the flag.

Flag: brixelCTF{SEAGULL}

## Merde

![](<../../.gitbook/assets/image (31).png>)

This challenge mentioned about french and war. Could it be an old encryption method used by the french? A quick search and we will find `Vigenère cipher`.&#x20;

This type of cipher is actually a series of interwoven ceasar ciphers using a [tabula recta](https://en.wikipedia.org/wiki/Tabula\_recta).&#x20;

So we need a key that can be used to decrypt the message. hmm... what was that word he shouted? To decrypt this message I used CyberChef [here](https://cyberchef.org/#recipe=Vigen%C3%A8re\_Decode\('confidentiel'\)\&input=VnZyIGt0ZGsgdmwganZ0enN5SEJJe2ZuemNpZXZzfQ).

We enter the encrypted text in the input and use 'confidentiel' as the key. Press the `Bake!` button. On the bottom right we will find the flag.

![](<../../.gitbook/assets/image (94).png>)

Flag: brixelCTF{baguette}

## Merda

![](<../../.gitbook/assets/image (18).png>)

If we search for encryption methods used by the romans, we quickly find the `caesar cipher`. It's a technique used by Julius Caesar's army to encrypt and decrypt messages so when a messenger got captured the enemy would not be able to read the message.

Since the description mentioned `V` , which is 5 in roman numerals, we used dCode [here](https://www.dcode.fr/caesar-cipher) to decode the message, which gives us the flag.

![](<../../.gitbook/assets/image (85).png>)

Flag: brixelCTF{pizzanapoli}

## s̸͖̾̀͊͠h̸̜̒ï̷̧̲͙̭̤͛͒̋t̷̢̲͚͖̑͜

![](<../../.gitbook/assets/image (7).png>)

Based on previous CTF experience, and because the description mentioned `64`, this can be easily recognized as `Base64` encoded message.&#x20;

We can paste this message in CyberChef [here](https://cyberchef.org/#recipe=From\_Base64\('A-Za-z0-9%2B/%3D',true\)\&input=TURFeE1UQXhNREFnTURFeE1ERXdNREFnTURFeE1EQXhNREVnTURBeE1EQXdNREFnTURFeE1EQXhNVEFnTURFeE1ERXhNREFnTURFeE1EQXdNREVnTURFeE1EQXhNVEVnTURBeE1EQXdNREFnTURFeE1ERXdNREVnTURFeE1UQXdNVEVnTURBeE1EQXdNREFnTURFeE1EQXdNVEFnTURFeE1UQXdNVEFnTURFeE1ERXdNREVnTURFeE1URXdNREFnTURFeE1EQXhNREVnTURFeE1ERXhNREFnTURFd01EQXdNVEVnTURFd01UQXhNREFnTURFd01EQXhNVEFnTURFeE1URXdNVEVnTURFeE1UQXdNVEFnTURFeE1ERXhNVEVnTURFeE1EQXdNVEFnTURFeE1ERXhNVEVnTURFeE1EQXdNVEVnTURFeE1ERXhNVEVnTURFeE1UQXdNREFnTURFeE1URXhNREU9) and it will output a bunch of binary. From here, we change it to text and we will get the flag [here](https://cyberchef.org/#recipe=From\_Base64\('A-Za-z0-9%2B/%3D',true\)From\_Binary\('Space',8\)\&input=TURFeE1UQXhNREFnTURFeE1ERXdNREFnTURFeE1EQXhNREVnTURBeE1EQXdNREFnTURFeE1EQXhNVEFnTURFeE1ERXhNREFnTURFeE1EQXdNREVnTURFeE1EQXhNVEVnTURBeE1EQXdNREFnTURFeE1ERXdNREVnTURFeE1UQXdNVEVnTURBeE1EQXdNREFnTURFeE1EQXdNVEFnTURFeE1UQXdNVEFnTURFeE1ERXdNREVnTURFeE1URXdNREFnTURFeE1EQXhNREVnTURFeE1ERXhNREFnTURFd01EQXdNVEVnTURFd01UQXhNREFnTURFd01EQXhNVEFnTURFeE1URXdNVEVnTURFeE1UQXdNVEFnTURFeE1ERXhNVEVnTURFeE1EQXdNVEFnTURFeE1ERXhNVEVnTURFeE1EQXdNVEVnTURFeE1ERXhNVEVnTURFeE1UQXdNREFnTURFeE1URXhNREU9).

![](<../../.gitbook/assets/image (93).png>)

Flag: brixelCTF{robocop}

## Scheiße

![](<../../.gitbook/assets/image (36).png>)

Hmm.. wait a minute, this looks familiar. I have solved a similar challenge before [here](https://gadiel-lau.gitbook.io/2020-writeups/gsctf-2020#crypto-war). This is using enigma machine, we can use the same tool [here](https://cryptii.com/pipes/enigma-machine) to solve it.

Putting in all the information, we will get this output

![derfl agist sauer kraut](<../../.gitbook/assets/image (4).png>)

When correctly formatted it reads: _Der flag ist sauerkraut_ meaning the flag is sauerkraut.

Flag:  brixelCTF{sauerkraut}

## flawed

![](<../../.gitbook/assets/image (272).png>)

From this challenge, it looks like the password is hashed, and we need to retrieve the plaintext of the password. This challenge is similar to what we have solved before [here](https://gadiel-lau.gitbook.io/2020-writeups/gsctf-2020#hash-browns).

We can use the same website to get the flag.

![](<../../.gitbook/assets/image (25).png>)

Flag: brixelCTF{notsecure}

## Don't be salty

![](<../../.gitbook/assets/image (279).png>)

This challenge is slightly different from the previous ones I've attempted. The password is hashed and salt is added to the password after. A pretty good writeup online could be found [here](https://infosecwriteups.com/cracking-hashes-with-hashcat-2b21c01c18ec).

For this, we can use `hashcat` to bruteforce the password. Hashcat can be downloaded [here.](https://hashcat.net/hashcat/)

First, we analyze the hash [here](https://www.tunnelsup.com/hash-analyzer/) and determine it to be md5.

We can refer to the [hashcat documentation](https://hashcat.net/wiki/doku.php?id=example\_hashes) to determine the mode of cracking. We can run this command to get the password/flag.

`hashcat -a 3 -m 10 hash.txt ?l?l?l?l?l`

`-a 3 specifies the attack mode to be brute force attack`

`-m 10 specifies the mode to take in md5(pass+salt)`

`?l?l?l?l?l species the mask which means the password is 5 lowercase letters.`

Note: Sometimes I run into this problem where there is not enough device memory to crack the password.

![Kali Linux VM with 2GB memory](<../../.gitbook/assets/image (271).png>)

After increasing the memory on my VM, the password is easily cracked in 1 second!

![Kali Linux VM with 8GB memory](<../../.gitbook/assets/image (54).png>)

Flag: brixelCTF{brute}
