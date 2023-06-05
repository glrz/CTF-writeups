# Introduction to Web Security

## I like cookies <a href="#modal_title" id="modal_title"></a>

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a link. Upon navigating to the link, we will be greeted with a simple Login  page.

<figure><img src="../../../.gitbook/assets/image (108).png" alt=""><figcaption></figcaption></figure>

We could use chrome extension - `EditThisCookie` for this challenge as the challenge already suggested `cookies`.

We can see that the current cookie is set to `guest`

<figure><img src="../../../.gitbook/assets/image (104).png" alt=""><figcaption></figcaption></figure>

Simply change `guest` to `admin` and refresh the page and the flag will be presented.

<figure><img src="../../../.gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>

This challenge was similar to [CDDC training 2022](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/dsta-brainhack-cyber-defenders-discovery-camp-training-2022/basic-concepts-of-cybersecurity/introduction-to-web-security#web-security-1).

Flag : 571067f03b08cf290673a3b75e028d4e

## Client is not always smart

<figure><img src="../../../.gitbook/assets/image (107).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a link again.

This time, I used the `curl` command to view the source code of the site.

```html
┌──(kali㉿kali)-[~/Downloads]
└─$ curl http://52.78.16.36:7777/web2/
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>Login Page</title>
    <link rel="stylesheet" href="./css.css">
</head>

<body>
    <div class="login-box">
        <h1>Login</h1>
        <label for="username">Username:</label>
        <input type="text" id="username" name="username" placeholder="Enter username">
        <label for="password">Password:</label>
        <input type="password" id="password" name="password" placeholder="Enter password">
        <input type="submit" value="Login" onclick="login()">
        <br>
        <p id="message">
        </p>
    </div>
    <script src="./script.js"></script>
</body>

</html>                      
```

We could see that there is `script.js` included.

Again, we can `curl` the `script.js` and we will see the username and password in plaintext.

```javascript
┌──(kali㉿kali)-[~/Downloads]
└─$ curl http://52.78.16.36:7777/web2/script.js
function login() {
    var username = document.getElementById("username").value;
    var password = document.getElementById("password").value;
    if (username === "" || password === "") {
        document.getElementById("message").innerHTML = "Please enter a username and password.";
    } else if (username === "admin" && password === "very_hard_admin_pw") {
        document.getElementById("message").innerHTML = "Login successful!";
        const xhr = new XMLHttpRequest();
        xhr.open("POST", 'login.php', true);

        //Send the proper header information along with the request
        xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
        xhr.onreadystatechange = function () {
            if (xhr.readyState === XMLHttpRequest.DONE && xhr.status === 200) {
                // console.log(xhr.responseText); // log the response text to the console
                document.getElementById("message").innerHTML = xhr.responseText;
            }
        };

        xhr.send("login=success&admin=true");

    } else {
        document.getElementById("message").innerHTML = "Invalid username or password.";
    }
}            
```

We can login with the following credentials:

Username: admin

Password: very\_hard\_admin\_pw    &#x20;

After press Login, we will get the flag

<figure><img src="../../../.gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>

Flag : 50939418569729868a65f6262123fc72

## Are you admin? <a href="#modal_title" id="modal_title"></a>

<figure><img src="../../../.gitbook/assets/image (109).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were provided with a link as well.

However, there was no particularly useful information in source code.

I tried `‘` in username field to check for possible SQLi vulnerability.

<figure><img src="../../../.gitbook/assets/image (111).png" alt=""><figcaption></figcaption></figure>

The link became [http://52.78.16.36:7777/web3/?id=%27\&pw=](http://52.78.16.36:7777/web3/?id=%27\&pw=) which suggested that it could be prone to SQLi.

Simply type ' or 1=1# in username and Login would give us the flag.

<figure><img src="../../../.gitbook/assets/image (110).png" alt=""><figcaption></figcaption></figure>

This challenge was also similar to [CDDC training 2022](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/dsta-brainhack-cyber-defenders-discovery-camp-training-2022/basic-concepts-of-cybersecurity/introduction-to-web-security#web-security-3).

Flag : 065354fc55d82ca723c345cb4f8918ac
