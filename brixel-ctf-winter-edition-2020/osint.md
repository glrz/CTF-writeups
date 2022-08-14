# OSINT

## A quick search

For this challenge, we were given an image file.

![](<../.gitbook/assets/image (208).png>)

Here we can simply go [here](https://images.google.com/), press the camera icon and upload the image.&#x20;

![](<../.gitbook/assets/image (40).png>)

We can see that the tower is called Eben-Ezer.

Flag: brixelCTF{Eben-Ezer}

## Manhunt #1

For this challenge we are given a JPG file.

![](<../.gitbook/assets/image (254).png>)

We can simply use an online tool [here](https://exif.tools/) or `exiftool` command on Kali Linux machine to solve this

![](<../.gitbook/assets/image (141).png>)

Flag: brixelCTF{Johnny\_Dorfmeister}

## Manhunt #5

In this challenge, we could tell that there could be a deleted page on his twitter account.

![](<../.gitbook/assets/image (217).png>)

The webpage could be saved in Internet Archive. We could use waybackmachine here, which could crawl sites and store backups.&#x20;

As we search the site [http://www.howitshould.be/test-page](http://www.howitshould.be/test-page), we found a snapshot of the page on 15/01/2019.&#x20;

![](<../.gitbook/assets/image (260).png>)

![](<../.gitbook/assets/image (177).png>)

If we look into it we see the flag is w@yb@ck!

![](<../.gitbook/assets/image (257).png>)

Flag: brixelCTF{w@yb@ck!}

## Bird Call

For this challenge, we are given a MP3 file.

![](<../.gitbook/assets/image (240).png>)

If we google search `bird sound recognizer` , we will find this online tool [here](https://birdnet.cornell.edu/api/) which can help us to get the flag.

Uploading the audio on the site, we could tell the bird is most probably White Stork.

![](<../.gitbook/assets/image (218).png>)

If we search the latin name for white stork, it is also known as Ciconia ciconia.

Flag: brixelCTF{Ciconia\_ciconia}
