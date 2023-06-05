# Fundamentals of Cybersecurity

## Welcome

<figure><img src="../../../.gitbook/assets/image (4) (7).png" alt=""><figcaption></figcaption></figure>

This challenge is very straightforward. Similar to previous year CDDC training, most challenges required us to have the flag in MD5 hash format. We can get the MD5 from the bash terminal as such

```bash
┌──(kali㉿kali)-[~]
└─$ echo -n HelloCDDC2023 | md5sum
1da67d97d656b83385abfdef59ddca83  -
```

Flag: 1da67d97d656b83385abfdef59ddca83

## Basic Quiz

<figure><img src="../../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

A simple quiz with basic cyber security  questions. We could simply use CHATGPT to solve this.

<figure><img src="../../../.gitbook/assets/image (65) (3).png" alt=""><figcaption></figcaption></figure>

Convert all to lowercase and  to MD5.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ echo -n log4j_phishing_cryptojacking_automotive_ransomware | md5sum
ca6d9ec38c49e017c4ada4fa969fb78d  -
```

Flag: ca6d9ec38c49e017c4ada4fa969fb78d
