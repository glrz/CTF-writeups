---
description: This topic consists of 9 challenges and I solved 5/9 of them.
---

# Open Source Intelligence (OSINT)

## Shodan Searching with filter

![](<../../../.gitbook/assets/image (700).png>)

To use Shodan Searching with filter, we first have to login into `Shodan`.&#x20;

After we have logged in into [Shodan](https://www.shodan.io),  we could type in the search bar

`hostname:darktracer.io`

This would search the hostname `darktracer.io`. We could see different information about this site.

![](<../../../.gitbook/assets/image (771).png>)

Next, we could click into `Dark Tracer` to view more information such as the `Cloud Region`. This would give us our flag.

![](<../../../.gitbook/assets/image (755).png>)

## Foot\_Comment

![](<../../../.gitbook/assets/image (697).png>)

For this challenge, we were given a `.onion` link.

[http://bod2wytnn2rz3277qd4riiloedzgekicbrkdz3xozdjxxvsxmoumlmyd.onion/](http://bod2wytnn2rz3277qd4riiloedzgekicbrkdz3xozdjxxvsxmoumlmyd.onion/)&#x20;

We could view this link on [Tor Browser](https://www.torproject.org/download/).

If you would like to read up more about `.onion` websites, check out this [site](https://www.howtogeek.com/272049/how-to-access-.onion-sites-also-known-as-tor-hidden-services/).

Once we are at the webpage, we could right click, `View Page Source`.

![](<../../../.gitbook/assets/image (674).png>)

Scroll down to the bottom and we would see there’s a footer comment which has the flag. Alternatively, we could `CTRL+F` to search for `<!--` which is the start of HTML comments.

![](<../../../.gitbook/assets/image (691).png>)

## Mod\_Status

![](<../../../.gitbook/assets/image (676).png>)

Based on the challenge title, we could Google `mod status`. We would then find this [site](https://osintcurio.us/2019/03/05/apache-mod\_status-in-tor-hidden-services-destroy-anonymity/) which contains helpful information to solve this challenge.

If we visit the `onion address/server-status/`, and we would be directed to another webpage

![](<../../../.gitbook/assets/image (636).png>)

If we continue to scroll down, we will see a password that looked like Base64 encoded at the bottom.&#x20;

![](<../../../.gitbook/assets/image (663).png>)

Like how we solved Base64 challenge [here](https://gadiel-lau.gitbook.io/2021-writeups/lagncrash-interpoly-ctf-2021#broken-keyboard), we could use online [Base64 decoder](https://www.base64decode.org/) to decode it, giving us the ip address/flag for this challenge.

![](<../../../.gitbook/assets/image (618).png>)

Base64 encoded strings/text are commonly seen in CTF or cybersecurity challenges. If you are interested to learn different ways to decode Base64 encoded data, check out my collection of writeups in [2020 ](https://gadiel-lau.gitbook.io/2020-writeups)and [2022 ](https://gadiel-lau.gitbook.io/2022-writeups/)as well.

## Google Dork

![](<../../../.gitbook/assets/image (669).png>)

For this challenge, we need to find the flags of `OSINT 1 - Better Alternative Than TV`

We could use this query to perform Google Dorking and find the site which contains these text

`site:medium.com intext:"OSINT 1 - Better Alternative Than TV"`

This would give us 1 result in the search.

![](<../../../.gitbook/assets/image (608).png>)

If we go into the CDDC 2020 writeup, and `CTRL+F` to find the text: `OSINT 1`, we would find the flag for this challenge.

![](<../../../.gitbook/assets/image (635).png>)

## Meta\_Tags

![](<../../../.gitbook/assets/image (649).png>)

For this challenge, we could use an [online exiftool](https://www.metadata2go.com/) to view the metadata of this file.

![](<../../../.gitbook/assets/image (598).png>)

Check out [here ](https://gadiel-lau.gitbook.io/2021-writeups/csit-the-infosecurity-challenge-tisc-2021#scratching-the-surface-challenge-2)and [here](https://gadiel-lau.gitbook.io/2022-writeups/lagncrash-interpoly-ctf-2022#s3crethero) for some of my other related writeups.
