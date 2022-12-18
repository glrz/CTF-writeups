---
description: CTF.SG CTF 2021 is a 24 hours CTF competition held from 13 Mar - 14 Mar 2021.
---

# CTF.SG CTF 2021

This competition allowed up to 4 members to form a team but I participated solo in this CTF competition with the team name: TeamNotFound and came in 27/123 teams, pretty satisfied with the results. I solved a few challenges which includes the insanity challenge and a web challenge.

![](<../.gitbook/assets/image (83).png>)

## Insanity challenge

This challenge was slightly more difficult than other CTFs welcome / sanity check challenge.

Challenge description:

> We hid a flag in one of the private channels on the [CTF.SG CTF discord](https://gist.github.com/duckness/39f8feab4cb8ef0db075f30a29547827). Can you find it?

If we go to the discord server to search for `CTFSG`{, which is the flag format, we will not find anything. At this point, it might seem like a dead end for some.

For me, I went on to Google `how to view hidden channels on discord` and came across an extension for Discord called `BetterDiscord`

I proceeded to download `BetterDiscord` [here](https://betterdiscord.app/), and installed the ShowHiddenChannels plugin [here](https://betterdiscord.app/plugin/ShowHiddenChannels). Once everything is set up correctly, we can go back to the CTF.SG discord server. We will notice a hidden channel called `Insanity` appear now. \
If we right click and click channel access, we will see the flag under `Channel Topic`

![](<../.gitbook/assets/image (3).png>)

_Author's writeup :_ [_here_](https://isopach.dev/CTFSG-CTF-2021/#insanity-check)__

_CTFSG{4LL\_uR\_cH4nn3lS\_R\_13eLonG\_t0\_uS!}_

## Wildest Dream

![](<../.gitbook/assets/image (18).png>)

For this challenge, we are given a website link and a php file.&#x20;

{% file src="../.gitbook/assets/1989 (1).php" %}

The website looks normal and nothing out of the ordinary.&#x20;

![](<../.gitbook/assets/image (92).png>)

First, lets inspect the php code provided. This is the php source code provided.

```php
<?php
    if(!empty($_GET['i1']) && !empty($_GET['i2'])){
        $i1 = $_GET['i1'];
        $i2 = $_GET['i2'];
        if($i1 === $i2){
            die("i1 and i2 can't be the same!");
        }
        $len1 = strlen($i1);
        $len2 = strlen($i2);
        if($len1 < 20){
            die("i1 is too shorttttttt pee pee pee pee pee");
        }
        if($len2 < 20){
            die("i2 is too shorttttttt pee pee pee pee pee");
        }
        if(sha1(hex2bin($i1)) === sha1(hex2bin($i2)));
            if(md5(hex2bin($i1)) !== md5(hex2bin($i2)))
                echo "All I want to be is in your wildest dreams";
                if(md5(hex2bin($i1)) == md5(hex2bin($i2)))echo $flag;
        echo "<br>I think he did it, but i just cant prove it.";
    } else {
        echo "<br> You need to provide two strings, i1 and i2. /1989.php?i1=a&i2=b";
    }
?
```

Upon inspection, I found something which looks interesting on line 19 of the code

`if(md5(hex2bin($i1)) == md5(hex2bin($i2))) echo $flag;`

It looks like if this condition is satisfied, it will print out the flag for us.

After a few attempts, I realised we can find 2 md5 values `i1` and `i2`, both should not contain hexadecimals, and input this into the php URL query like this, which will give us the flag below the image.

![](<../.gitbook/assets/image (60).png>)

Flag: CTFSG{1-+h1nk-h3-d1d-1+bu+-I-ju5t-c4n+-pr0v3-1t}

