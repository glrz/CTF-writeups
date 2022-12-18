# Forensic

## Unknown file

![](<../../.gitbook/assets/image (189).png>)

For this challenge, we were given a `.txt` file with a bunch of hex values.

First, I copy paste this data in [CyberChef](https://cyberchef.org/). CyberChef would suggest to render image.

![](<../../.gitbook/assets/image (107).png>)

Using this [recipe](https://cyberchef.org/#recipe=From\_Hex\('None'\)Render\_Image\('Raw'\)), I got the image, but not the flag. I thought the flag could be hidden in this image.

To solve this, I used [fotoforensics](https://fotoforensics.com/) to get the hidden flag.

On fotoforensics site, change the analysis to `Hidden Pixels`.

![](<../../.gitbook/assets/image (152) (1).png>)

If we scroll down, we would see the flag. Alternatively, hover your mouse over the original image.

![](<../../.gitbook/assets/image (127) (1).png>)

Check out another similar challenge [here ](https://gadiel-lau.gitbook.io/2020-writeups/brixel-ctf-winter-edition-2020/forensics#lottery-ticket)where I used fotoforensics to solve it.

Flag: CDDC22{S6oW\_me\_y0u're\_4he\_8est}

## Unknown file2

![](<../../.gitbook/assets/image (134).png>)

For this challenge, we were given an `Unknown_file_2` file.

If we open it on a hex editor like [GHex](https://wiki.gnome.org/Apps/Ghex), we could see that there are embedded file(s) in the file.

![](<../../.gitbook/assets/image (162).png>)

We could use [`binwalk` ](https://github.com/ReFirmLabs/binwalk/wiki/Usage)to check and indeed there are quite a few files in there.

![](<../../.gitbook/assets/image (115).png>)

We then use `binwalk -e Unknown_file_2` command to extract the files.

One of the files that caught my attention was `dictionary.pdf`. If we open up this file, we would see a github link.

![](<../../.gitbook/assets/image (190).png>)

Next, we browse to the link provided and download the txt file.

We could then use this file as wordlist and perform dictionary attack to crack the `flag.pdf` file. Check out this [Pentester Academy Blog](https://blog.pentesteracademy.com/cracking-password-of-a-protected-pdf-file-using-hashcat-and-john-the-ripper-1b50074eeabd) which could guide you to crack PDF files.

![Password cracked: copacaban](<../../.gitbook/assets/image (122).png>)

Open the `flag.pdf` file , then press `Ctrl+A`  and scroll down to see the flag.

![](<../../.gitbook/assets/image (144).png>)

If you are interested, check out another similar [writeup](https://gadiel-lau.gitbook.io/2022-writeups/lagncrash-interpoly-ctf-2022#riddle-me-this) where I used [`John` ](https://github.com/openwall/john)and [`Binwalk` ](https://github.com/ReFirmLabs/binwalk)to solve the challenge.

Flag: CDDC22{T6is\_is\_4he\_9re@tes4\_D@y\_0f\_my\_1ife!}
