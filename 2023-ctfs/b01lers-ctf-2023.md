---
description: >-
  b01lers CTF is the public competitive CTF hosted by the Purdue Capture The
  Flag team. It was held from 18 Mar - 20 Mar 2023.
---

# b01lers CTF 2023

I participated in this CTF with team `Social Engineering Expert`. Even though I participated with them, the team did not commit to this CTF due to some the nature of challenges being guessy. I solved most of the challenges at the start of the CTF for the team.

The challenges solved were:\


<figure><img src="../.gitbook/assets/image (3) (6).png" alt=""><figcaption></figcaption></figure>

Surprisingly, the `sanity check` challenge had fewer solves than `switcheroo` challenge and thus more points allocated to it.

## sanity check

<figure><img src="../.gitbook/assets/image (7) (1) (2).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a link to the Discord server.&#x20;

Fun fact: I actually solved this challenge a day before the CTF started. I just happened to join the Discord server and found the flag.

Once we join the Discord server, we can navigate to the `Announcements` channel.

From there, we will notice that there is an ongoing thread.

<figure><img src="../.gitbook/assets/image (81) (1).png" alt=""><figcaption></figcaption></figure>

If we clicked on it, we can see an active thread which displayed part of the flag.

<figure><img src="../.gitbook/assets/image (5) (1) (3) (1).png" alt=""><figcaption></figcaption></figure>

Once we click into this thread, we will get the full flag :)

<figure><img src="../.gitbook/assets/image (90) (1).png" alt=""><figcaption></figcaption></figure>

Flag: bctf{wow\_yet\_another\_place\_to\_put\_the\_sanity\_check\_flag\_hope\_you\_find\_it}

## switcheroo

<figure><img src="../.gitbook/assets/image (87) (1).png" alt=""><figcaption></figcaption></figure>

For this challenge, it provided a link to WolvCTF 2023 as well as a `gift` which looked like an encoded string.

First, I went on to `CyberChef` to decode this string.

<figure><img src="../.gitbook/assets/image (83) (1).png" alt=""><figcaption></figcaption></figure>

After it was `Base64` decoded, it looked like we obtained a flag. However, the flag format is not correct and looked like it was a flag for `WolvCTF 2023` instead.

I went on to check out the link provided which brings me to the `WolvCTF 2023` platform.

After I created an account and team on the platform, I could browse the challenges there.

I noticed that there was a similar `switcheroo` challenge under the `misc` category as well.

<figure><img src="../.gitbook/assets/image (86) (1).png" alt=""><figcaption></figcaption></figure>

```
It's a busy weekend, with tens of CTF happening at the same time :) If there is extra time, why not check out https://ctf.b01lers.com? BTW, take this as a gift: YmN0ZntoMzExMF93MHIxZF9nMWY3X2ZyMG1fN2gzX2IwMWxlcl9zMWQzfQ==
```

If I decode this in [`CyberChef`](https://cyberchef.org/#recipe=From\_Base64\('A-Za-z0-9%2B/%3D',true,false\)\&input=WW1OMFpudG9NekV4TUY5M01ISXhaRjluTVdZM1gyWnlNRzFmTjJnelgySXdNV3hsY2w5ek1XUXpmUT09), I'll get the flag.

<figure><img src="../.gitbook/assets/image (85) (1).png" alt=""><figcaption></figcaption></figure>

Flag: bctf{h3110\_w0r1d\_g1f7\_fr0m\_7h3\_b01ler\_s1d3}

## warmup

<figure><img src="../.gitbook/assets/image (80) (1).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was under the web category and we were provided with a link.

If we navigate to the link: [http://ctf.b01lers.com:5115/](http://ctf.b01lers.com:5115/aW5kZXguaHRtbA==), we would be redirected to  [http://ctf.b01lers.com:5115/aW5kZXguaHRtbA==](http://ctf.b01lers.com:5115/aW5kZXguaHRtbA==)

Notice there is a string that looked like `Base64 encoded` after the `/`

<figure><img src="../.gitbook/assets/image (78) (1).png" alt=""><figcaption></figcaption></figure>

First, lets take a look at the source code.

```html
<html lang="en">
	<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>My first flask app</title>
	</head>
	<body>
	<h1>Hello World!</h1>
	</body>
	<script>
	console.log("")
	</script>
	<!-- debug.html -->
	</html>
```

As we can see, `debug.html` had been commented out from the code. We could navigate there to see if we find any useful information.

Before we can do that, we need to remember to encode it in `Base64` first, as seen in the previous link.

We can do that using `CyberChef`.

<figure><img src="../.gitbook/assets/image (2) (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

This gives us the output: `ZGVidWcuaHRtbA==`

Now, we can navigate to the link: [http://ctf.b01lers.com:5115/ZGVidWcuaHRtbA==](http://ctf.b01lers.com:5115/ZGVidWcuaHRtbA==)

From here, we can see that there could be a file `app.py`.

<figure><img src="../.gitbook/assets/image (88) (1).png" alt=""><figcaption></figcaption></figure>

Once again, we can get the `Base64` of app.py through [`CyberChef`](https://cyberchef.org/#recipe=To\_Base64\('A-Za-z0-9%2B/%3D'\)\&input=YXBwLnB5).

This gives us the output: `YXBwLnB5` and we can browse to [http://ctf.b01lers.com:5115/YXBwLnB5](http://ctf.b01lers.com:5115/YXBwLnB5)

<figure><img src="../.gitbook/assets/image (79) (1).png" alt=""><figcaption></figcaption></figure>

If we check out the source code, we can see that there is `flag.txt`.

```python
from base64 import b64decode
	import flask
	
	app = flask.Flask(__name__)
	
	@app.route('/<name>')
	def index2(name):
	name = b64decode(name)
	if (validate(name)):
	return "This file is blocked!"
	try:
	file = open(name, 'r').read()
	except:
	return "File Not Found"
	return file
	
	@app.route('/')
	def index():
	return flask.redirect('/aW5kZXguaHRtbA==')
	
	def validate(data):
	if data == b'flag.txt':
	return True
	return False
	
	
	if __name__ == '__main__':
	app.run()
```

If we were to get the `Base64` of `flag.txt` in [CyberChef](https://cyberchef.org/#recipe=To\_Base64\('A-Za-z0-9%2B/%3D'\)\&input=ZmxhZy50eHQ), the output will be `ZmxhZy50eHQ=`.

<figure><img src="../.gitbook/assets/image (89) (1).png" alt=""><figcaption></figcaption></figure>

However, navigating to the link: [http://ctf.b01lers.com:5115/ZmxhZy50eHQ=](http://ctf.b01lers.com:5115/ZmxhZy50eHQ=) showed that the file is blocked.

<figure><img src="../.gitbook/assets/image (77) (1).png" alt=""><figcaption></figcaption></figure>

If we take a closer look at the source code again, we will be able to understand how the file is opened and read.

We can get the `Base64` of `./flag.txt` from [CyberChef](https://cyberchef.org/#recipe=To\_Base64\('A-Za-z0-9%2B/%3D'\)\&input=Li9mbGFnLnR4dA). This would give us the output: `Li9mbGFnLnR4dA==`

<figure><img src="../.gitbook/assets/image (84) (1).png" alt=""><figcaption></figcaption></figure>

Once we append this to the link, we will get the flag upon reaching the site: [http://ctf.b01lers.com:5115/Li9mbGFnLnR4dA==](http://ctf.b01lers.com:5115/Li9mbGFnLnR4dA==)

<figure><img src="../.gitbook/assets/image (12) (1) (1).png" alt=""><figcaption></figcaption></figure>

Alternatively, we could also use `Burp Suite`, use the proxy and turn on interceptor. Once the packet is captured, we can send it to repeater and change the `GET` to `/Li9mbGFnLnR4dA==`.

Similarly, we would obtain the flag after sending the request. As we can see, the flag is obtained in the response.

<figure><img src="../.gitbook/assets/image (3) (1) (4) (1).png" alt=""><figcaption></figcaption></figure>

Flag: bctf{h4d\_fun\_w1th\_my\_l4st\_m1nut3\_w4rmuP????!}
