---
description: This topic consists of 3 challenges and I solved all of them.
---

# Introduction to Web Security

## Web Security 1

![](<../../.gitbook/assets/image (783).png>)

For this challenge, we were given a link to a simple login page. The challenge mentioned that we need to login as the `admin`.

For this, I used [EditThisCookie](https://chrome.google.com/webstore/detail/editthiscookie/fngmhnnpilhplaeedifhccceomclgfbg?hl=en), a Google Chrome extensions cookie manager that can add, delete, edit, search, protect and block cookies.

I changed the `value` to `admin` and saved it by clicking the `tick` icon

![](<../../.gitbook/assets/image (748).png>)

Refresh the page and we will get the flag.

![](<../../.gitbook/assets/image (764).png>)

## Web Security 2

![](<../../.gitbook/assets/image (709).png>)

For this challenge, we were given similar description as the previous challenge, to login as the `admin`.

If we go to inspect elements, `F12` on Google Chrome, we would notice a HTML code with&#x20;

`value="guest"`

We could change this `value` to `admin`

![](<../../.gitbook/assets/image (715).png>)

Next, we key in a random password and press submit and we will get the flag

![](<../../.gitbook/assets/image (712).png>)

An alternative solution is using [Burp Suite](https://portswigger.net/burp/communitydownload).

Go to `proxy -> intercept (make sure intercept is on) -> open browser`

![](<../../.gitbook/assets/image (747).png>)

Key in the URL of the website (The page will not load since its being intercepted)

![](<../../.gitbook/assets/image (756).png>)

Go back to burp suite and `Forward` the connection

![](<../../.gitbook/assets/image (705).png>)

Key in a random password and press submit

![](<../../.gitbook/assets/image (770).png>)

Now we check burp suite again

![](<../../.gitbook/assets/image (792).png>)

Change the `id` to admin and press `Forward`.

![](<../../.gitbook/assets/image (790).png>)

Similarly, we would get the flag.

![](<../../.gitbook/assets/image (729).png>)

## Web Security 3

![](<../../.gitbook/assets/image (773).png>)

This challenge provided similar description as the previous 2 challenges we solved. Again, we have to login as the `admin`.

If we try to sign in with username : `admin` and password : `admin`, we could see the URL change to `id=admin&pw=admin`, which suggests that this page might be prone to SQL injection.

Typing `‘ OR 1=1#` for username and password and clicking submit will give us the flag.

![](<../../.gitbook/assets/image (717).png>)

![](<../../.gitbook/assets/image (759).png>)

Read more about SQL injection [here](https://www.w3schools.com/sql/sql\_injection.asp).
