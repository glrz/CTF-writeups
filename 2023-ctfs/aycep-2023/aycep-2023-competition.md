---
description: >-
  I placed 17/22 and solved a total of 21 challenges. I will not be doing
  explanations for MCQ questions since they are pretty straightforward.
---

# AYCEP 2023 Competition

<figure><img src="../../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>

## MCQs

### Yes Ma'am&#x20;

<figure><img src="../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

Flag: Ye$M@'@m!

<figure><img src="../../.gitbook/assets/image (147).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (150).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (121).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (142).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (122).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

## Encryption

### Johannes Trithemius

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

If we Google `Johannes Trithemius decoder,` we would find this.

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

If we click on the second link, we would find the [`Trithemius Ave Maria` decoder](https://www.dcode.fr/trithemius-ave-maria).

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

Note that this is different from `trithemius cipher`.

We will get the output: `AUEMARIA`.

However, The Latin alphabet does not differentiate letter 'U' and 'V' or 'W' and also 'I' and 'J'. Hence, U should be replaced with V in this case to form the flag: AVEMARIA

Flag: AVEMARIA

## Forensics

### Home Baked Treats

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a link. Upon visiting the link, we see the following:

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

First, lets view the source code

```html
<!DOCTYPE html>
	<html>
	
	<head>
	<title>AYCEP 2023</title>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<link rel="shortcut icon" href="/themes/ctfd-neon-theme-main/static/img/favicon.ico?d=3d4fe0e8" type="image/x-icon">
	<link rel="stylesheet" href="https://cdn.cloud.ctfd.io/a-ycep/themes/core/static/css/fonts.min.css?t=1645257065">
	<link rel="stylesheet" href="https://cdn.cloud.ctfd.io/a-ycep/themes/core/static/css/core.min.css?t=1642090259">
	<link rel="stylesheet" href="https://cdn.cloud.ctfd.io/a-ycep/themes/ctfd-neon-theme-main/static/css/style.dev.css?t=1676189106">
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/HackerThemes/theme-machine@latest/dist/neon-glow/css/bootstrap4-neon-glow.min.css">
	
	<link rel='stylesheet' href='https://cdn.jsdelivr.net/font-hack/2.020/css/hack.min.css'>
	
	
	
	<script type="text/javascript">
	var init = {
	'urlRoot': "",
	'csrfNonce': "2ca60e3ea84bcee2aef2260237e32ed48eb3e17b9402f44d1d210fa8dad293c1",
	'userMode': "teams",
	'userId': 987,
	'start': null,
	'end': null,
	'theme_settings': null
	}
	</script>
	<style id="theme-color"> 
	:root {--theme-color: #8d8b8c;} 
	.navbar{background-color: var(--theme-color) !important;} 
	.jumbotron{background-color: var(--theme-color) !important;} 
	</style> 
	
	</head>
	
	<body>
	<div class="ht-tm-navbar navbar-dark text-white">
	<div class="container">
	<div class="ht-tm-navbar-left">
	<a href="/" class="text-decoration-none text-light">
	<span class="ht-tm-navbar-title">AYCEP 2023</span>
	</a>
	<nav class="ht-tm-nav">
	<a href="/" class="pl-md-0 p-3 text-light">Home</a>
	
	<a class="text-decoration-none text-light" href="/rules">Rules</a>
	
	
	
	<a class="text-decoration-none text-light" href="/users">Users</a>
	
	<a class="text-decoration-none text-light" href="/teams">Teams</a>
	
	
	
	
	<a class="text-decoration-none text-light" href="/scoreboard">Scoreboard</a>
	
	<a class="text-decoration-none text-light" href="/challenges">Challenges</a>
	<a class="text-decoration-none text-light" href="/notifications">Notifications</a>
	</nav>
	</div>
	<div class="ht-tm-element btn-group ml-auto">
	
	
	
	<a class="btn btn-sm btn-outline-light" href="/team">
	<span class="d-block" data-toggle="tooltip" data-placement="bottom" title="Team">
	<i class="fas fa-users d-none d-md-block d-lg-none"></i>
	</span>
	<span class="d-sm-block d-md-none d-lg-block">
	<i class="fas fa-users pr-1"></i>Team
	</span>
	</a>
	
	<a class="btn btn-sm btn-outline-light" href="/user">
	<span class="d-block" data-toggle="tooltip" data-placement="bottom" title="Profile">
	<i class="fas fa-user-circle d-none d-md-block d-lg-none"></i>
	</span>
	<span class="d-sm-block d-md-none d-lg-block">
	<i class="fas fa-user-circle pr-1"></i>Profile
	</span>
	</a>
	<a class="btn btn-sm btn-outline-light" href="/settings">
	<span class="d-block" data-toggle="tooltip" data-placement="bottom" title="Settings">
	<i class="fas fa-cogs d-none d-md-block d-lg-none"></i>
	</span>
	<span class="d-sm-block d-md-none d-lg-block">
	<i class="fas fa-cogs pr-1"></i>Settings
	</span>
	</a>
	<a class="btn btn-sm btn-outline-light" href="/logout">
	<span class="d-block" data-toggle="tooltip" data-placement="bottom" title="Logout">
	<i class="fas fa-sign-out-alt d-none d-md-block d-lg-none"></i>
	</span>
	<span class="d-sm-block d-md-none d-lg-block">
	<i class="fas fa-sign-out-alt pr-1"></i>
	<span class="d-lg-none">Logout</span>
	</span>
	</a>
	
	</div>
	</div>
	</div>
	
	<main role="main">
	
	<div class="container">
	<script>
	monster_name = "S!D_Th3_M0N$T3R";
	
	function validate() {
	let input = document.forms["myForm"]["fname"].value;
	if (monster_name == input) {
	window.location.href = 'https://a-ycep.ctfd.io/cookie-puppies';
	} else {
	alert("That's not my name!");
	}
	}
	
	function myFunction() {
	const inpObj = document.getElementById("id1");
	if (!inpObj.checkValidity()) {
	document.getElementById("demo").innerHTML = inpObj.validationMessage;
	} else {
	document.getElementById("demo").innerHTML = "Input OK";
	} 
	} 
	</script>
	<center>
	<h4>Home Baked Treats</h4>
	<img src="/files/51ea1d5312ff6be9848fe51891aa87ee/cookie_monster.jpg"><br>
	<p>Cookie Monster: Me don’t remember me real name… Maybe it was Sidney?</p>
	<form name="myForm" method="post">
	<p>Say my name: <input type="text" id="fname" name="fname"><button onclick="validate()">Submit</button></p>
	</form>
	</center>
	
	</div>
	
	</main>
	
	<footer class="footer">
	<div class="container text-center">
	<a href="https://ctfd.io" class="text-secondary">
	<small class="text-muted">Powered by CTFd</small>
	</a>
	</div>
	</footer>
	
	<script defer="defer" src="https://cdn.cloud.ctfd.io/a-ycep/themes/core/static/js/vendor.bundle.min.js?t=1651556728"></script>
	<script defer="defer" src="https://cdn.cloud.ctfd.io/a-ycep/themes/core/static/js/core.min.js?t=1602139566"></script>
	<script defer="defer" src="https://cdn.cloud.ctfd.io/a-ycep/themes/core/static/js/helpers.min.js?t=1616194976"></script>
	
	
	<script defer="defer" src="https://cdn.cloud.ctfd.io/a-ycep/themes/core/static/js/pages/main.min.js?t=1651556728"></script>
	
	
	
	
	<script defer src="https://cdn.cloud.ctfd.io/a-ycep/static/recaptcha.js?t=3d4fe0e8"></script>
	<script defer src="https://www.google.com/recaptcha/api.js?onload=onloadCallback&render=explicit"></script>
	
	
	</body>
```

Note this code portion from  the code above:

```
if (monster_name == input) {
window.location.href = 'https://a-ycep.ctfd.io/cookie-puppies';
```

If we navigate to the link, we see the following&#x20;

<figure><img src="../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

If we click on the dogs image, it would download a `dancing.png` file

Opening the file shows that it is `Dancing Men Cipher`. We have encountered this before [here ](https://gadiel-lau.gitbook.io/2020-writeups-1/2020-ctfs/gsctf-2020#just-dance)and [here](https://gadiel-lau.gitbook.io/2023-writeups/2023-ctfs/lag-and-crash-3.0/crypto#multilinguistic).

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

Similarly,  we can use [dCode  ](https://www.dcode.fr/dancing-men-cipher)to decode it.

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

Halfway through decoding, it was pretty obvious and I managed to guess the flag.

Flag: WHOLETTHEDOGSOUT

## Misc

### Tyranny Of Dragons

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

This is just some free points I guess.

Flag: {DRAGON\_QUEEN}

### Missionaries and Cannibals

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

The Missionaries and Cannibals is quite a famous problem,  you could read more [here](https://en.wikipedia.org/wiki/Missionaries\_and\_cannibals\_problem).

I found an[ online solution](https://www.geeksforgeeks.org/missionaries-and-cannibals/) which was quite similar to how  this problem was crafted  (Except it starts from left to right instead of right to left).

Following the  game rules, we will get the flag after all missionaries and cannibals successfully cross the river.

```bash
Game Start
Now the task is to move all of them to right side of the river
rules:
1. The boat can carry at most two people
2. If cannibals num greater than missionaries then the cannibals would eat the missionaries
3. The boat cannot cross the river by itself with no people on board

M M M C C C |    --- |

Left side -> right side river travel
Enter number of Missionaries travel => 0
Enter number of Cannibals travel => 2


M M M C | --> | C C

Right side -> Left side river travel
Enter number of Missionaries travel => 0
Enter number of Cannibals travel => 1


M M M C C | <-- | C

Left side -> right side river travel
Enter number of Missionaries travel => 0
Enter number of Cannibals travel => 2


M M M | --> | C C C

Right side -> Left side river travel
Enter number of Missionaries travel => 0
Enter number of Cannibals travel => 1


M M M C | <-- | C C

Left side -> right side river travel
Enter number of Missionaries travel => 2
Enter number of Cannibals travel => 0


M C | --> | M M C C

Right side -> Left side river travel
Enter number of Missionaries travel => 1
Enter number of Cannibals travel => 1


M M C C | <-- | M C

Left side -> right side river travel
Enter number of Missionaries travel => 2
Enter number of Cannibals travel => 0


C C | --> | M M M C

Right side -> Left side river travel
Enter number of Missionaries travel => 0
Enter number of Cannibals travel => 1


C C C | <-- | M M M

Left side -> right side river travel
Enter number of Missionaries travel => 0
Enter number of Cannibals travel => 2


C | --> | M M M C C

Right side -> Left side river travel
Enter number of Missionaries travel => 0
Enter number of Cannibals travel => 1


C C | <-- | M M M C

Left side -> right side river travel
Enter number of Missionaries travel => 0
Enter number of Cannibals travel => 2


| --> | M M M C C C

You won the game :
        Congrats
Total attempt
For winning the game, here is your flag: LoGiCal_AcE!
11
```

Flag: LoGiCal\_AcE!

## Networking

### Simple Password - Part 1

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

For this challenge,  we could use `strings` on the `pcap` file and `grep` for `pass`

If we look closely enough, we  would see the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ strings simplehttp.pcap | grep pass
  <inputname="password" id="password" maxlength="50"> <label for="password"> Type a fake password here</label> 
  <inputname="password" id="password" maxlength="50"> <label for="password"> Type a fake password here</label> 
  <inputname="password" id="password" maxlength="50"> <label for="password"> Type a fake password here</label> 
  <input name="password" id="password" maxlength="50"> <label for="password"> Type a fake password here</label> 
XGET /index.html?password=flag%7BdontUseHTTPeverSRSLY%7D HTTP/1.1
  <input name="password" id="password" maxlength="50"> <label for="password"> Type a fake password here</label>
```

Alternatively, we could open the file in Wireshark and filter by `frame contains pass`

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

Next, `Follow > TCP Stream` and we would find the flag as well.

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

Flag: dontUseHTTPeverSRSLY
