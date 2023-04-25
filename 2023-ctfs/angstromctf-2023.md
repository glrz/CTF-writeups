---
description: ångstromCTF 2023 was held from 22 Apr - 27 Apr 2023.
---

# ångstromCTF 2023

In this CTF, I participated with team [youtiaos](https://ctftime.org/team/194864) and we achieved the position:&#x20;

The scoreboard can be found on [CTFtime ](https://ctftime.org/event/1859)or on[ ångstromCTF website](https://2023.angstromctf.com/scoreboard).

I managed to dedicate some time during the weekend and solved two of the web challenges.&#x20;

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

I usually go for challenges in the `Misc`, `Forensics` or `Osint`  categories. However, in this CTF, I joined a bit later and my teammates already solved most of the `Misc` challenges. This CTF did not have any challenges in the `Forensics` or `Osint` category.

Overall, I was quite satisfied to be able to solve challenges in the `Web` category and get to practice the use of `Burp Suite`.

## Celeste Speedrunning Assosiation

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a link. Upon visiting the link, we will see the following page.

<figure><img src="../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

First, we can try to play around and navigate to the `/play` page.

If we append `/play` to the URL, we will be redirected to another page.

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

From here, we can try to press the button and see what it does. This redirects us to another `/submit` page.

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

It seems like we are not getting much information from this. So, lets run this in `Burp Suite` to get a better idea on how the requests are being sent over to the server.

In Burp Suite, make sure to turn on interceptor. Once we forward the request, we will see the following.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

It looked like there's some value assigned to `start`.&#x20;

First, I sent this request to the repeater using the `CTRL+R` shortcut.&#x20;

Next, I tried changing this value to a negative value like `-0.1`. However, the response was still the same.

Finally, I tried to change the value to a very large number like `1000000000000000000` and it gave me the flag in the response section after I sent the request.

<figure><img src="../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

Flag: actf{wait\_until\_farewell\_speedrun}

## Celeste Tunneling Association

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a link and a source code.

First, lets check out the link.

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

Next, we can go through the source code.

```python
# run via `uvicorn app:app --port 6000`
import os

SECRET_SITE = b"flag.local"
FLAG = os.environ['FLAG']

async def app(scope, receive, send):
    assert scope['type'] == 'http'

    headers = scope['headers']

    await send({
        'type': 'http.response.start',
        'status': 200,
        'headers': [
            [b'content-type', b'text/plain'],
        ],
    })

    # IDK malformed requests or something
    num_hosts = 0
    for name, value in headers:
        if name == b"host":
            num_hosts += 1

    if num_hosts == 1:
        for name, value in headers:
            if name == b"host" and value == SECRET_SITE:
                await send({
                    'type': 'http.response.body',
                    'body': FLAG.encode(),
                })
                return

    await send({
        'type': 'http.response.body',
        'body': b'Welcome to the _tunnel_. Watch your step!!',
    })
```

Similarly, we can start `Burp Suite`, turn on interceptor and forward the request to see how this web application works.

As we forward the first request, we can send it to the repeater, similar to what we did in the previous challenge.

<figure><img src="../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

If we read the source code carefully, we can probably tell that it would return the flag if the `host` have the value : `SECRET_SITE`, and we know that `SECRET_SITE` was previously assigned with the value `flag.local`.

Hence, we can simply change the `Host` in request from `pioneer.tailec718.ts.net` to `flag.local` and we would be presented with the flag in the response section.

<figure><img src="../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

Flag: actf{reaching\_the\_core\_\_chapter\_8}

For more web challenges where I used Burp Suite to solve, you might want to check out my other writeups in [CDDC 2022 training](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/dsta-brainhack-cyber-defenders-discovery-camp-training-2022/basic-concepts-of-cybersecurity/introduction-to-web-security), [WolvCTF 2023](https://gadiel-lau.gitbook.io/2023-writeups/2023-ctfs/wolvctf-2023), [b01lers CTF 2023](https://gadiel-lau.gitbook.io/2023-writeups/2023-ctfs/b01lers-ctf-2023) and [PicoCTF 2023](https://gadiel-lau.gitbook.io/2023-writeups/2023-ctfs/picoctf-2023/web-exploitation).
