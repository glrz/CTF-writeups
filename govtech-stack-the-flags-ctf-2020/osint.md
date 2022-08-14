# OSINT

## Only time will tell!

![](<../.gitbook/assets/image (279).png>)

For this challenge, we are given an image. I used exiftool, coorinate converter tool , online barcode tool and some guessing skills to get the flag.

Use exiftool command to analyze the metadata of the image

![](<../.gitbook/assets/image (27).png>)

Put the latitude an longitude in the converter [here](https://www.pgc.umn.edu/apps/convert/) and we will get the first part of the flag : 1.286647\_103.846836

![](<../.gitbook/assets/image (82).png>)

Use online barcode reader [here](https://online-barcode-reader.inliteresearch.com/) to get the date, this makes up the second part of the flag

![](<../.gitbook/assets/image (31).png>)

For the last part of the flag, which is the time, I just guessed it and after a few tries I got the flag.

Flag : govtech-csg{1.286647\_103.846836\_2020: 10 : 25\_1500-1700}

## What is he working on? Some high value project?

![](<../.gitbook/assets/image (1).png>)

Browsing the developer’s portal [here](https://www.developer.tech.gov.sg/communities/events/stack-the-flags-2020), I did inspect/view source code on the webpage and found something that looked useful.

![](<../.gitbook/assets/image (216).png>)

![On line 858, we can see the comment Will fork to our gitlab - @joshhky](<../.gitbook/assets/image (75).png>)

![logged in to gitlab and searched for the user @joshhky and found the user Josh Hong.](<../.gitbook/assets/image (8).png>)

Another way to get access to his gitlab is to use sherlock:

![](<../.gitbook/assets/image (212).png>)

Here we can see his gitlab activity and personal projects, where the flag could possibly be hidden in these. I was taking note of what could be a possible high value project. Then, something caught my eye. I saw korovax under activity, which sounded like some high value project and the poc done with readme

![](<../.gitbook/assets/image (70).png>)

Browsing the README, I saw something which looked like a repository name and I was right.

![](<../.gitbook/assets/image (256).png>)

Flag: govtech-csg{krs-admin-portal}

## Sounds of freedom

![](<../.gitbook/assets/image (13).png>)

We were given an video .mp4 file for this challenge.

The audio sounds like airplane sound and the video looks like its near park. Hence, concluded its near paya lebar air base at punggol park. The flag is postal code of punggol park.

Flag: govtech-csg{538768}

## Where was he kidnapped?

![](<../.gitbook/assets/image (248).png>)

In this challenge, we were given 3 video files.

In the first video, we can see bus 117 was going towards Punggol interchange.

![](<../.gitbook/assets/image (78).png>)

After some google search on bus 117 route, we concluded that the image shown is opposite khatib station

![](<../.gitbook/assets/image (265).png>)

To confirm, we can go to google maps to view the image opposite khatib station.

![](<../.gitbook/assets/image (64).png>)

Indeed, it looks like the image we saw in the video.

Following the bus route, we get to Blk 761

![This image looked like the one we saw in the second video.](<../.gitbook/assets/image (134).png>)

![Found this image which looked like the image in third video. This is at Blk 870.](<../.gitbook/assets/image (197).png>)

Flag:govtech-csg{760870}

