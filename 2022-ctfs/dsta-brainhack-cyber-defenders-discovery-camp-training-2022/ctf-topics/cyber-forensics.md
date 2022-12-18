---
description: This topic consists of 9 challenges and I solved all of them.
---

# Cyber Forensics

## Hidden Zip

![](<../../../.gitbook/assets/image (654).png>)

In this challenge, we were given a `hidden.zip` file.&#x20;

{% file src="../../../.gitbook/assets/hidden.zip" %}

If we try to extract using [`Binwalk`](https://www.kali.org/tools/binwalk/) or [`foremost`](https://www.kali.org/tools/foremost/), we would be able to extract 2 PNG files from the zip file. However, these PNG files are not the files that we want.

We could open this file in [HxD](https://mh-nexus.de/en/hxd/) to analyze the data further.

I found an article which was related to [File Carving](https://resources.infosecinstitute.com/topic/file-carving/) and it helped me to solve this challenge. Also, check the [list of file signatures](https://en.wikipedia.org/wiki/List\_of\_file\_signatures) to find the file signature for JPG files.

We could search the JPG file header by pressing `ctrl + f` and keying in the hex-value : `FFD8FFE0`. We would realise that other than 2 PNG files, there is also a JPG file embedded in the zip file.

![Take note of the starting offset value below : 9900](<../../../.gitbook/assets/image (623).png>)

Now, we search the JPG file trailer: FFD9

![Take note of the ending offset value below : 1CF63](<../../../.gitbook/assets/image (602).png>)

Then, we proceed with `HxD > Edit > Select block (Ctrl + E)`

![](<../../../.gitbook/assets/image (599).png>)

We set the `Start-offset` and `End-offset` according to what we noted down earlier, then press `ok`.

![](<../../../.gitbook/assets/image (613).png>)

If these steps are done correctly, the entire selected block will be highlighted in blue

![](<../../../.gitbook/assets/image (611).png>)

Next, we could right click and copy

![](<../../../.gitbook/assets/image (687).png>)

After copying the data, we start a new file in HxD by clicking `File > New (Ctrl+N)` and paste the contents to the new file.

![](<../../../.gitbook/assets/image (685).png>)

Save this file as `flag.jpg`. Open the `flag.jpg` file and we will get the flag.

Alternatively, we could `Ctrl+F` and search for : `JFIF`

![](<../../../.gitbook/assets/image (646).png>)

Select the block before the JPG header (i.e. before FFD8FFE0)

![](<../../../.gitbook/assets/image (630).png>)

Right click and `delete` this block

![](<../../../.gitbook/assets/image (642).png>)

Save the file as `flag.jpg`

![](<../../../.gitbook/assets/image (98) (1).png>)

Open the `flag.jpg` file and we would get the flag as well.

![](<../../../.gitbook/assets/image (69) (1).png>)

## Historian

![](<../../../.gitbook/assets/image (51).png>)

In the challenge, the challenge description mentioned `I hid a flag in chrome`. If we unlock the hint for this challenge, we would know that we need to `understand analysis of chrome history`.

![](<../../../.gitbook/assets/image (26).png>)

First, we `cd` to change directory to `User Data`

![](<../../../.gitbook/assets/image (41).png>)

Next, I noticed there is a `history` file. If we run `strings` command on it, we could see a list of strings in `history`. I tried clicking into each link to check its contents, then I found this ctftime link which contained the flag at the end of the URL.

![](<../../../.gitbook/assets/image (40) (1).png>)

Alternatively, an easier way could be to `grep flag`, this would reduce the amount of data to analyze.

![](<../../../.gitbook/assets/image (31).png>)

## I Am Here

![](<../../../.gitbook/assets/image (48) (1).png>)

For this challenge, we were given a [Google docs](https://docs.google.com/document/d/1ZQ2bo2k28du3K7upbMHaU6Lo94GwcxYL/edit) word document in `.docx` format.

![](<../../../.gitbook/assets/image (45) (1).png>)

First thing I tried was to `CTRL+A` to check if there could be any hidden text in this page. However, I could not find anything.

Next, I tried downloading this file in different formats. If we download it as `.txt` format, we would get some messages when we open the `.txt` file.

![](<../../../.gitbook/assets/image (44) (1).png>)

I tried `CTRL+A` again but do not see anything else in this file.

I proceeded to download this file as Rich text format `.rtf`

This time opening the file would give us the flag.

![](<../../../.gitbook/assets/image (53).png>)

## Least Significant

![](<../../../.gitbook/assets/image (42).png>)

For this challenge, we were given a `.zip` file.

{% file src="../../../.gitbook/assets/least_significant.zip" %}

The title is `Least Significant`, so I assumed we could try to get the Least Significant Bit(LSB) of the `least_significant.png` file provided.

For this there are a couple of tools we could use. You could try [StegoLSB](https://gist.github.com/dhondta/d2151c82dcd9a610a7380df1c6a0272c), [Zsteg](https://github.com/zed-0xff/zsteg) or any preferred tool that can extract LSB.

If we use `Zsteg`, we could run the command

`zsteg --lsb least_significant.png`

![](<../../../.gitbook/assets/image (91).png>)

Alternatively, we could use `StegoLSB` and run the command

`stegolsb bruteforce least_significant.png`

![](<../../../.gitbook/assets/image (74) (1).png>)

Both tools would give us a Base64 encoded string, we know this from `=` appended at the back.

We could decode the Base64 encoded string on the terminal using this command

`echo [base64string] | base64 --decode`

&#x20;

![](<../../../.gitbook/assets/image (10) (1).png>)

Alternatively, we could replace `--decode` with `-d` which also stands for decode.

This would give us the output which is the flag.

## Mirror

![](<../../../.gitbook/assets/image (50).png>)

For this challenge, we were given a `strange_file` with no file extensions.

{% file src="../../../.gitbook/assets/strange_file (1)" %}

First, I opened this file and analyzed this in [GHex](https://wiki.gnome.org/Apps/Ghex), you could use any other hex editor for this. I realised this data looked reversed. The `B.DNEI` should be `IEND.B` and it should be at the end of a `PNG` file, not the start. We could check [PNG Structure](https://www.w3.org/TR/PNG-Structure.html) if needed.

![](<../../../.gitbook/assets/image (92).png>)

To confirm, I scrolled all the way to the bottom. As you can see, the data is indeed reversed. `GNP` should be `PNG` instead.

![](<../../../.gitbook/assets/image (28).png>)

At this point, I found a [writeup ](https://ctftime.org/writeup/18056)that seemed similar to this challenge.

We will use [Vim ](https://en.wikipedia.org/wiki/Vim\_\(text\_editor\))to create a python file to reverse this data, again you could use any other text editors for this.

![](<../../../.gitbook/assets/image (84).png>)

If you are using Vim, a quick simple guide is&#x20;

Press `i` to go into insert mode and start editing the file.

Once we are in insert mode, we could type a simple Python script to reverse the data

```python
with open('strange_file', 'rb') as fp_in:
    reversed_data = fp_in.read()[::-1]
    with open('flag.png', 'wb') as fp_out:
        fp_out.write(reversed_data)
```

In the above script we are going to reverse the data and save the output as `flag.png`. Once we are done, we press `esc` and type `:wq` to write the changes and quit `Vim`.

We proceed to run the Python script

![](<../../../.gitbook/assets/image (9).png>)

Opening up the `flag.png` file gives us the flag.

![](<../../../.gitbook/assets/image (58).png>)

## My Secret Folder

![](<../../../.gitbook/assets/image (67) (1).png>)

For this challenge, we were given a `.ad1` file.

{% file src="../../../.gitbook/assets/FS.ad1" %}

The challenge description mentioned `logical image`. These are already 2 big hints, we know we could analyze this file in [FTK Imager](https://accessdata.com/product-download/ftk-imager-version-4-5).

I opened up the file in `FTK imager, file -> add evidence item -> image file`

![](<../../../.gitbook/assets/image (38).png>)

Next, we could see a `flag.jpg` file in the file list. Right click and export this file.

![](<../../../.gitbook/assets/image (21) (1).png>)

![](<../../../.gitbook/assets/image (97).png>)

Once it has exported successfully, we open up `flag.jpg` and we would get the flag.

![](<../../../.gitbook/assets/image (33) (1).png>)

## PNG File is Corrupted

![](<../../../.gitbook/assets/image (39) (1).png>)

For this challenge, we were given a `.png` file.

{% file src="../../../.gitbook/assets/SecretMessage.png" %}

First, I opened this file on HxD. From the challenge title and the file extension, we know this should be a `PNG` file. However, the file signature is clearly incorrect.

![](<../../../.gitbook/assets/image (1) (1).png>)

You could check [PNG Structure](https://www.w3.org/TR/PNG-Structure.html) if needed. However, after changing the file signature to `89 50 4E 47`, the file still cannot be opened.

![](<../../../.gitbook/assets/image (95) (1).png>)

I decided to move on to [GHex](https://wiki.gnome.org/Apps/Ghex) on my Kali Linux VM. I prefer the dark background and linux environment is often easier to do stuff.

![](<../../../.gitbook/assets/image (71).png>)

At this point, I also tried [PCRT (PNG Check & Repair Tool)](https://github.com/sherlly/PCRT) but it did not work.

![](<../../../.gitbook/assets/image (81).png>)

Next, I ran [`pngcheck`](http://www.libpng.org/pub/png/apps/pngcheck.html)and it shows invalid image dimensions (0x0)

![](<../../../.gitbook/assets/image (5).png>)

To solve this challenge, I found this [writeup](https://ctftime.org/writeup/31187) which was good at showing the `PNG file structure` and this [writeup](https://programmer.ink/think/ctfshowmisc-file-structure.html) which provided a decent Python script.

We could go back to GHex and check the CRC value first. This value is important as it will be included in our script later to determine the width and height of the image.

The CRC value is `25 43 85 AF`

![](<../../../.gitbook/assets/image (83).png>)

Now we will create a Python script to get the width and height of the image.&#x20;

```python
import binascii
import struct

crcbp = open("SecretMessage.png", "rb").read()
for i in range(3000):
    for j in range(3000):
        data = crcbp[12:16] + struct.pack('>i', i)+struct.pack('>i', j)+crcbp[24:29]
        crc32 = binascii.crc32(data) & 0xffffffff
        if(crc32 == 0x254385AF):
            print(i, j)
            print('hex:', hex(i), hex(j))
```

After we are done with the script, we will run it to get the width and height of the image. In this case, the width is `69d` and height is `69d`.

![](<../../../.gitbook/assets/image (47).png>)

We go back to GHex and change the Width and Height to 69d, and save the file `(ctrl + s)`

![](<../../../.gitbook/assets/image (49) (1).png>)

Finally, the PNG file is fixed and we get the image:

![](<../../../.gitbook/assets/image (2) (1).png>)

Generate the MD5 of `Forensic_Is_beautiful`  on our terminal using the command

`echo -n string | md5sum`

![](<../../../.gitbook/assets/image (62) (1).png>)

## Spy Camera

![](<../../../.gitbook/assets/image (87) (1).png>)

For this challenge, we know that we are dealing with `Android phone` and our goal is to try to get past the android lock pattern. I unlocked the hint which provided this [link](https://www.droidthunder.com/crack-android-password-pin-pattern-lock-of-any-android-phone/). However, it was not really useful in providing the tool.

Instead, we could Google `android pattern github`. Click on the first [link](https://github.com/sch3m4/androidpatternlock).

![](<../../../.gitbook/assets/image (35) (1).png>)

Download the `aplc.py` file from the link.

We could analyze the data in `gesture.key` from the directory, which consist of values that looks hashed.

![](<../../../.gitbook/assets/image (43) (1).png>)

Using the `aplc.py`, file we can get the pattern using python2(somehow python3 didn't work)

![](<../../../.gitbook/assets/image (13) (1).png>)

Generate the SHA1 of the string in terminal and we would get the flag.

`echo -n strings | sha1sum`

![](<../../../.gitbook/assets/image (25) (1).png>)

## Wav Spec

![](<../../../.gitbook/assets/image (77).png>)

In this challenge, we were given a zip file that contains a `.wav` file.&#x20;

{% file src="../../../.gitbook/assets/wav_spec.zip" %}

First, we could open `Audacity` and analyze the wav file.

![](<../../../.gitbook/assets/image (7).png>)

Next, click on the `wav_spec` drop down list on the middle left and select `Spectrogram`. This would allow us to view in Spectrogram mode.

![](<../../../.gitbook/assets/image (11).png>)

Once it is changed to spectrogram mode, we could see the flag.

![](<../../../.gitbook/assets/image (63) (1).png>)

We could drag it down or change the settings to make it clearer.

![](<../../../.gitbook/assets/image (57).png>)
