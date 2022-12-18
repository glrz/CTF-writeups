# OSINT

## A quick search

![](<../../.gitbook/assets/image (110).png>)

For this challenge, we were given an image file.

{% file src="../../.gitbook/assets/image.jpg" %}

Here we can simply go [here](https://images.google.com/), press the camera icon and upload the image.&#x20;

![](<../../.gitbook/assets/image (262).png>)

We can see that the tower is called Eben-Ezer.

Flag: brixelCTF{Eben-Ezer}

## Manhunt #1

![](<../../.gitbook/assets/image (179).png>)

For this challenge we are given a JPG file.

{% file src="../../.gitbook/assets/icecream.jpg" %}

We can simply use an online tool [here](https://exif.tools/) or `exiftool` command on Kali Linux machine to solve this

![](<../../.gitbook/assets/image (28).png>)

Flag: brixelCTF{Johnny\_Dorfmeister}

## Manhunt #5

![](<../../.gitbook/assets/image (115).png>)

In this challenge, we could tell that there could be a deleted page on his twitter account.

The webpage could be saved in Internet Archive. We could use waybackmachine here, which could crawl sites and store backups.&#x20;

As we search the site [http://www.howitshould.be/test-page](http://www.howitshould.be/test-page), we found a snapshot of the page on 15/01/2019.&#x20;

![](<../../.gitbook/assets/image (178).png>)

![](<../../.gitbook/assets/image (78).png>)

If we look into it we see the flag is w@yb@ck!

![](<../../.gitbook/assets/image (128).png>)

Flag: brixelCTF{w@yb@ck!}

## Bird Call

![](<../../.gitbook/assets/image (136).png>)

For this challenge, we are given a MP3 file.

{% file src="../../.gitbook/assets/birdcall.mp3" %}

If we google search `bird sound recognizer` , we will find this online tool [here](https://birdnet.cornell.edu/api/) which can help us to get the flag.

Uploading the audio on the site, we could tell the bird is most probably White Stork.

![](<../../.gitbook/assets/image (174).png>)

If we search the latin name for white stork, it is also known as Ciconia ciconia.

Flag: brixelCTF{Ciconia\_ciconia}
