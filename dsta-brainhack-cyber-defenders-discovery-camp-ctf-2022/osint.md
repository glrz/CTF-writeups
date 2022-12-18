# Osint

## The place

![](<../.gitbook/assets/image (183).png>)

For this challenge, I used [TinEye](https://tineye.com/) to perform reverse image search. Basically just `SHIFT+WINDOWS+S` to screenshot the picture and paste on `TinEye`.

Alternatively, you could download the image and upload it on [Google reverse image search](https://images.google.com/). Both would lead you to the same page.

![](<../.gitbook/assets/image (151) (1).png>)

If we go into the page, notice there is a `Facebook` icon at the bottom.

![](<../.gitbook/assets/image (185).png>)

Click on the Facebook icon and the flag is the number

![](<../.gitbook/assets/image (167).png>)

Flag: CDDC22{+4928418896097}

## Darknet

![](<../.gitbook/assets/image (182).png>)

For this challenge, we are given a `.onion` link. We had previously encountered this kind of link before in [CDDC Training 2022](https://gadiel-lau.gitbook.io/2022-writeups/dsta-brainhack-cyber-defenders-discovery-camp-training-2022/ctf-topics/open-source-intelligence-osint#foot\_comment).&#x20;

We first open this in [Tor Browser](https://www.torproject.org/download/) to access the dark web. Here we could see that the zip file download from the site is password protected. In the next line, we should note that password needs to be converted to lower case and space is replaced with `_`

![](<../.gitbook/assets/image (153) (1).png>)

![password protected zip file](<../.gitbook/assets/image (108) (1).png>)

I did a Google search with the following query and found an [article](https://edition.cnn.com/2021/05/25/uk/drug-dealer-cheese-sentenced-scli-gbr-intl/index.html). We could already see his name from the article's description: `Carl Stewart`, or you could click into the link to read more about it.

![](<../.gitbook/assets/image (180).png>)

Now if we go back and use the password : `carl_stewart` to unlock the zip file, we will get the flag.

![](<../.gitbook/assets/image (146).png>)

Flag: CDDC22{Be\_c@r3fu1\_wh3n\_p0st1ng\_p1ctures\_0n\_th@\_1nt3rn3t}

## flying squirrel

![](<../.gitbook/assets/image (154) (1).png>)

For this challenge, we were given a `Public_key.zip` containing a `Public_Key` file.

{% file src="../.gitbook/assets/Public_Key.zip" %}

If we open up the file, we would see the public key block. We copy this block which looked Base64 encoded.

![](<../.gitbook/assets/image (160).png>)

Paste it onto an [online Base64 decoder](https://www.base64decode.org/) and we would get the flag.

![](<../.gitbook/assets/image (164).png>)

Flag: CDDC22{naldaramgi@key.key}

## What's your name?

![](<../.gitbook/assets/image (140).png>)

The challenge mentioned about `fake photo company`. We could go to LinkedIn to search that. Take note of the second search result, we could already see his name here.

![](<../.gitbook/assets/image (136).png>)

We could also Google it just to confirm. Here we could see his name and enter his LinkedIn profile.

![](<../.gitbook/assets/image (197).png>)

Flag: CDDC22{wolfgodafrid}

