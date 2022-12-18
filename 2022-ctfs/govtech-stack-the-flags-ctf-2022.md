---
description: >-
  GovTech STACK the Flags CTF 2022  is a Cybersecurity Capture-the-Flag (CTF)
  competition organised by GovTech Cyber Security Group which was held on 2
  December - 4 December 2022.
---

# GovTech STACK the Flags CTF 2022

<figure><img src="../.gitbook/assets/image (876).png" alt=""><figcaption></figcaption></figure>

More information about the event can be found [here](https://ctftime.org/event/1802) or at its [official website](https://jts.tech.gov.sg/2022/stack-the-flags). This year's edition was slightly different from [GovTech STACK the Flags CTF 2020](https://gadiel-lau.gitbook.io/2020-writeups-1/govtech-stack-the-flags-ctf-2020). It was hosted on [Hack The Box CTF](https://ctf.hackthebox.com/event/details/stack-the-flags-category-2-university-polytechnics-747) platform.

I participated in this CTF with the same teammates from [SekaiCTF 2022](https://gadiel-lau.gitbook.io/2022-writeups/sekaictf-2022), with an additional team member from SMU.&#x20;

I participated with the team name `punkcyber` with my username : `glrz01`.&#x20;

My team solved 3 challenges in this CTF. Out of the 3 challenges, I managed to solved 2 of them and was close to solving many others. This years' CTF was definitely more challenging than the previous [STACK the Flags CTF 2020](https://gadiel-lau.gitbook.io/2020-writeups-1/govtech-stack-the-flags-ctf-2020) which I participated in.  I did not spend too much time on this CTF as I had my Final Year Project and other stuffs to work on.

Eventually, we ranked 62/223. The position could have been much better and I could have solved more challenges. I will continue to work harder and build my skills to solve more challenges in future CTFs.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

If there is one thing this CTF could improve on, it would be the `difficulty level` of challenges. Some of the `difficulty` can be misleading. After some clarifications, the admins then told us that the difficulty level is based on what the challenge author think the difficulty level should be, and not an accurate representation of the actual difficulty level for the challenge.

The 2 challenges I solved were in the OSINT and forensics category respectively.

<figure><img src="../.gitbook/assets/image (166).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (869).png" alt=""><figcaption></figcaption></figure>

## Finding Nyan

<figure><img src="../.gitbook/assets/image (108).png" alt=""><figcaption></figcaption></figure>

This should be the easiest challenge compared to the other challenges. This challenge had the most solves. There were around 100+ solves when the competition ended.

<figure><img src="../.gitbook/assets/image (168).png" alt=""><figcaption></figcaption></figure>

This challenge was fairly easy. We were given a .mov file embedded in a zip as shown below.

{% file src="../.gitbook/assets/osint_finding_nyan (1).zip" %}

We can open and play the video in `Media Player`. The audio of the video was not of much help as we could mostly only hear nyan cat music playing or car sounds.&#x20;

However, if we look closely enough at the surroundings outside of the car's window, we will obtain some hints.  We could slow down the speed of the video to `0.25x` under options or use the `CTRL+SHIFT+G` shortcut.&#x20;

At the start of the video, we would see this image. This looked like a company's logo and there could be some kind of work ongoing there. The green road railings can also be a hint to verify the location on Google Maps later.

<figure><img src="../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>

If we continue to play the video, we will get another hint at the end of the video. It confirms that there is some ongoing construction work, and the same company name/logo appears again.

<figure><img src="../.gitbook/assets/image (151).png" alt=""><figcaption></figcaption></figure>

This place was near where I stayed and it looked really familiar because I used to have my driving lessons nearby as well. A quick search on Google Maps and I found the exact location of the place.

<figure><img src="../.gitbook/assets/image (128).png" alt=""><figcaption></figcaption></figure>

If you are interested in more OSINT related challenges, check out my other writeups [here](https://gadiel-lau.gitbook.io/2020-writeups-1/govtech-stack-the-flags-ctf-2020/osint), [here](https://gadiel-lau.gitbook.io/2020-writeups-1/govtech-stack-the-flags-ctf-2020/osint), [here](https://gadiel-lau.gitbook.io/2022-writeups/dsta-brainhack-cyber-defenders-discovery-camp-training-2022/ctf-topics/open-source-intelligence-osint) and [here](https://gadiel-lau.gitbook.io/2022-writeups/dsta-brainhack-cyber-defenders-discovery-camp-ctf-2022/osint)

Flag: STF22{BUKIT\_BATOK\_RD}

## Hit you with that

<figure><img src="../.gitbook/assets/image (863).png" alt=""><figcaption></figcaption></figure>

This challenge was under the forensics category, with 40+ solves at the end of the competition.&#x20;

In this challenge, we were given a `.pcapng` file that was embedded in zip.

{% file src="../.gitbook/assets/forensics_hit_you_with_that.zip" %}

I tried analyzing this file in both `Wireshark` and `NetworkMiner`, but could not seem to find a way to get the flag. I only got to the point where I found the YouTube link to [BlackPink's song](https://youtu.be/IHNzOHi8sJs?t=70) if I follow HTTP/TCP stream. This seemed like a dead end as I could not find any other hints for some time.

Note that I had to convert the `.pcapng` file to `.pcap` file first before I analyzed it in `NetworkMiner` since I was using the free edition. To convert to `.pcap`, run the following tshark command

```
tshark -F pcap -r {pcapng file} -w {pcap file}
```

Once it is converted, we can open it up in `NetworkMiner`.

However, like I mentioned previously, the information in there couldn't help me to get the flag. I looked through the different sections : Files, Sessions, Parameters but did not find anything useful.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

How could we solve this challenge then? I remembered I had solved a `Network` challenge in [DSTA CDDC CTF](https://gadiel-lau.gitbook.io/2022-writeups/dsta-brainhack-cyber-defenders-discovery-camp-ctf-2022/network#simple-shark) previously. That challenge which I solved was of course very easy, I just had to use `strings` and `grep` to find the flag.&#x20;

For this challenge, it wasn't that easy, if we were to try to `grep` the flag, it will not work. What I did was to use `strings` to perform static analysis on the file as follow:

`strings STF22.pcapng | less`

With `less` specified, it allowed me to go through each line of the strings in `STF22.pcapng` while I press/hold on the `Enter` key.

Alterntatively, we could save it to a file and open it in a Text editor like `Sublime Text` as such:

`strings STF22.pcapng > flag.txt | subl flag.txt`

If we scroll down the file, we would see a chunk of text which stands out from the rest.

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

This chunk of data is repeated twice because ICMP echo request and echo reply carries the same data payload. The data can be seen below:

```
iVBORw0KGgoAAAANSUhEUgAAAlwAAALaCAIAAABrlxoiAAAAG3RFWHRmbGFnAFNURjIye0JsQGNrUGluOV9WM24wbX2+lxWpAAEAAElEQVR4nOz92Y4c2Zaui/1jzMbMvImGPZndymY1e1fVVgM9gKCLA92oAc4r6Fn0Budab3AgQBAgHUHQxZHq7L2rVq3Kjkwyk8m+7xmMcDebc4yhi2nu4cFkrkpmJrlYa80PDqaHR4S7mUfCho/u/+nTj36j
```

If we paste this data into CyberChef, the magic wand would suggest that it is `Base64`. This data might not appear as obvious to many to be `Base64` because `Base64` is usually appended with `=` or `==` at the end as the padding. Also, if you have not realized, we the flag is already displayed by hovering on the magic wand.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

To make things clearer, of course we can select `From Base64` and include it in our recipe [here](https://cyberchef.org/#recipe=From\_Base64\('A-Za-z0-9%2B/%3D',true,false\)\&input=aVZCT1J3MEtHZ29BQUFBTlNVaEVVZ0FBQWx3QUFBTGFDQUlBQUFCcmx4b2lBQUFBRzNSRldIUm1iR0ZuQUZOVVJqSXllMEpzUUdOclVHbHVPVjlXTTI0d2JYMitseFdwQUFFQUFFbEVRVlI0bk96OTJZNGMyWmF1aS8xanpNYk12SW1HUFpuZHltWTFlMWZWVmdNOWdLQ0xBOTJvQWM0cjZGbjBCdWRhYjNBZ1FCQWdIVUhReFpIcTdMMnJWcTNLamt3eWs4bSs3eG1NY0RlYmM0eWhpMm51NGNGa3JrcG1KcmxZYTgwUERxYUhSNFM3bVVmQ2hvL3UvK25UajM2ag) and we could just copy and paste the flag from the output.

Alternatively, once we know that it is `Base64` and we can get the flag from decoding it, we could just decode it directly on our terminal as such:

`echo {string} | base64 -d`

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

If you are interested in some other `Network` or `PCAP analysis` related challenge, check out my previous writeup [here](https://gadiel-lau.gitbook.io/2022-writeups/sg-cyber-olympian-2nd-trial-2022#shark-chat).

Flag: STF22{Bl@ckPin9\_V3n0m}
