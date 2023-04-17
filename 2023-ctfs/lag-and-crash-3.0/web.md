# Web

## The Password

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a website link.

I used `curl` to view the source code for the website.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ curl thepassword.s.lagncra.sh
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body> 
    <script src="password.js" defer></script>
</body>
</html>                                                                                                                   
```

From here, we could see an interesting `password.js` included.

We could curl the `.js` file as such

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ curl thepassword.s.lagncra.sh/password.js
function promptPassword( )
{

var pwd = prompt ("Enter your Password: ");

while (pwd != 's0m3t1me$_1t_i5_pr377y_s1aY'){
alert("Login is incorrect");
pwd = prompt ("Enter your Password: ");
}

alert("Password is correct, the flag is LNC2023{s0m3t1me$_1t_i5_pr377y_s1aY}");

}
promptPassword();                                   
```

Now, we can see the flag from the alert statement.

Flag: LNC2023{s0m3t1me$\_1t\_i5\_pr377y\_s1aY}
