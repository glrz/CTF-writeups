# Open Source Intelligence (OSINT)

## Simple Search

<figure><img src="../../../.gitbook/assets/image (55) (3).png" alt=""><figcaption></figcaption></figure>

For this challenge, we can go to GitHub and type `user:sanjawa` into the search bar.

<figure><img src="../../../.gitbook/assets/image (89) (2).png" alt=""><figcaption></figcaption></figure>

This will show the repository: [https://github.com/sanjawa/simplica](https://github.com/sanjawa/simplica)

Upon clicking into the repository, we will see that there was an update on `flag.txt`

Click on `Update flag.txt` to see the changes made.

<figure><img src="../../../.gitbook/assets/image (20) (5).png" alt=""><figcaption></figcaption></figure>

From here, we will be able to see the updated flag.

<figure><img src="../../../.gitbook/assets/image (23) (6).png" alt=""><figcaption></figcaption></figure>

Finally, we get the MD5 of the string from terminal

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ echo -n Simp1e_0sin7 | md5sum 
489b14d0c1bdeb037327f3fe6291bf8a  -
```

Flag: 489b14d0c1bdeb037327f3fe6291bf8a

## BF..?

<figure><img src="../../../.gitbook/assets/image (63) (3).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.txt` file.

First,  lets try to read the contents of the file.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cat Esoteric.txt            
++++++++++[>+>+++>+++++++>++++++++++<<<<-]>>>>+++++++++++++++++++++.<<++++++++++++++++++.>>----.----------------------.++++.--.+++++++++++++.---------------.++++++++++.+++++.<<+++++++.>>---------.+++++++++++++.--.++.-------------.<<.>>------.++++++++++.<<.                                                                                                                   
```

Based on experience, this is BrainFuck. We have seen this before [here ](https://gadiel-lau.gitbook.io/2020-writeups-1/2020-ctfs/govtech-stack-the-flags-ctf-2020/forensics#voices-in-the-head)and [here](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/nus-greyhats-grey-cat-the-flag-2022#ghost).

We can simply decode it on [dCode](https://www.dcode.fr/brainfuck-language) which gives us the output: `y0u_can_in7erpre7_i7`.

Lastly, get the MD5 hash value of the string.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ echo -n y0u_can_in7erpre7_i7 | md5sum
e419954f806c1faa2fc7e85ee11fd972  -
```

Flag: e419954f806c1faa2fc7e85ee11fd972

## Somewhere

<figure><img src="../../../.gitbook/assets/image (93) (2).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given 9 torn images taken in combination.

I searched up for an online image merge and found this [website](https://www.filesmerge.com/merge-images).

I proceeded to merge the images in ascending order&#x20;

&#x20;

<figure><img src="../../../.gitbook/assets/image (19) (4).png" alt=""><figcaption></figcaption></figure>

Set Merge options: Fix columns 3

We will then get the following full image:

<figure><img src="../../../.gitbook/assets/image (49) (4).png" alt=""><figcaption></figcaption></figure>

Next, we can do a reverse image search [here](https://www.duplichecker.com/reverse-image-search.php) which gives us the location.

<figure><img src="../../../.gitbook/assets/image (86) (2).png" alt=""><figcaption></figcaption></figure>

Finally, get the MD5 hash value to get the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ echo -n la_mer_beach | md5sum
88987115ad0a7ce0e473439efb5bedb4  -
```

## Find me, if you can.

<figure><img src="../../../.gitbook/assets/image (51) (3).png" alt=""><figcaption></figcaption></figure>

For this challenge, it provided what seemed like a username tag: `@RansomVault.` I thought that this could be a Telegram username or channel.

Indeed, when I searched it, I found this channel: [https://t.me/RansomVault](https://t.me/RansomVault).

In the channel, there were a bunch of pictures, links etc.

<figure><img src="../../../.gitbook/assets/image (94) (2).png" alt=""><figcaption></figcaption></figure>

While scrolling through the contents, I saw a `.docx` file which looked like it could be a ransomware file. I opened it and on the 2nd page, I found the flag at the bottom.

<figure><img src="../../../.gitbook/assets/image (91) (2).png" alt=""><figcaption></figcaption></figure>

However, somehow when trying to convert this flag string into MD5 in terminal, it did not work very well, probably due to the `!!` at the end of the string which caused some issues.&#x20;

Hence, I used an Online md5 hash generator instead.

<figure><img src="../../../.gitbook/assets/image (92) (2).png" alt=""><figcaption></figcaption></figure>

Flag: 209a5d3b3e9f8c0d7ad6abadc30da8c9

## The key is sometimes nearby.

<figure><img src="../../../.gitbook/assets/image (54) (3).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.onion` site link.

First, we could open this up in `Tor` browser.

If we view the source code, we would see that it mentioned backup is extremely important under  the comments.

<figure><img src="../../../.gitbook/assets/image (84) (2).png" alt=""><figcaption></figcaption></figure>

Additionally, if we go to the `server-status`: [http://y7dxireflp5yxffv4z4c2jqsyinx2jtcsezqrn3bv6deif6z24ugd2ad.onion/server-status/](http://y7dxireflp5yxffv4z4c2jqsyinx2jtcsezqrn3bv6deif6z24ugd2ad.onion/server-status/)

We can see the server running, with the Request GET `/backup` HTTP/1.1

```html
Srv	PID	Acc	M	CPU 	SS	Req	Dur	Conn	Child	Slot	Client	Protocol	VHost	Request
0-5	49177	1/3/4	W 	0.01	0	0	1	0.0	0.32	0.32 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /server-status/ HTTP/1.1
0-5	49177	0/2/4	_ 	0.03	30	0	1	0.0	0.00	0.01 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /backup/ HTTP/1.1
0-5	49177	0/0/1	_ 	0.00	25	0	0	0.0	0.00	0.23 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /jennie-image3.jpg HTTP/1.1
0-5	49177	0/1/2	_ 	0.01	25	0	0	0.0	0.00	0.15 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET / HTTP/1.1
0-5	49177	0/2/3	_ 	0.01	2076	0	1	0.0	0.15	0.34 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /backup/onion_service/authorized_clients/ HTTP/1.1
0-5	49177	0/3/3	_ 	0.01	2032	0	1	0.0	0.24	0.24 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET / HTTP/1.1
0-5	49177	0/1/1	_ 	0.01	2027	0	0	0.0	0.00	0.00 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /backup/onion_service/hs_ed25519_public_key HTTP/1.1
0-5	49177	0/1/1	_ 	0.01	2027	0	0	0.0	0.00	0.00 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /backup/onion_service/hostname HTTP/1.1
0-5	49177	0/2/2	_ 	0.01	297	0	0	0.0	0.00	0.00 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET / HTTP/1.1
0-5	49177	0/3/3	_ 	0.01	296	0	1	0.0	0.64	0.64 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /jennie-image.jpg HTTP/1.1
0-5	49177	0/3/3	_ 	0.01	295	0	1	0.0	0.42	0.42 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /jennie-image2.jpg HTTP/1.1
0-5	49177	0/2/3	_ 	0.01	296	0	0	0.0	0.15	0.15 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /favicon.ico HTTP/1.1
0-5	49177	0/2/3	_ 	0.01	2076	0	0	0.0	0.15	0.30 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /jennie-image1.jpg HTTP/1.1
0-5	49177	0/3/4	_ 	0.01	294	0	1	0.0	0.24	0.56 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /jennie-image3.jpg HTTP/1.1
0-5	49177	0/2/2	_ 	0.01	291	0	0	0.0	0.32	0.32 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET / HTTP/1.1
0-5	49177	0/2/3	_ 	0.01	291	0	0	0.0	0.32	0.32 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /jennie-image.jpg HTTP/1.1
0-5	49177	0/1/1	_ 	0.01	290	0	0	0.0	0.19	0.19 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /jennie-image2.jpg HTTP/1.1
0-5	49177	0/1/1	_ 	0.01	290	0	0	0.0	0.23	0.23 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /jennie-image3.jpg HTTP/1.1
0-5	49177	0/1/1	_ 	0.00	289	0	0	0.0	0.00	0.00 	127.0.0.1	http/1.1		
0-5	49177	0/1/1	_ 	0.01	155	0	0	0.0	0.19	0.19 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /jennie-image2.jpg HTTP/1.1
0-5	49177	0/2/2	_ 	0.01	160	0	0	0.0	0.24	0.24 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /server-status/ HTTP/1.1
0-5	49177	0/2/2	_ 	0.01	155	0	0	0.0	0.15	0.15 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /jennie-image1.jpg HTTP/1.1
0-5	49177	0/3/3	_ 	0.03	31	0	0	0.0	0.00	0.00 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /backup HTTP/1.1
1-5	49176	0/1/2	_ 	0.01	1723	0	0	0.0	0.00	0.32 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /jennie-image4.jpg HTTP/1.1
1-5	49176	0/0/1	_ 	0.00	1723	0	0	0.0	0.00	0.00 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET / HTTP/1.1
1-5	49176	0/2/2	_ 	0.01	1728	0	0	0.0	0.00	0.00 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET / HTTP/1.1
1-5	49176	0/1/1	_ 	0.00	2220	0	0	0.0	0.00	0.00 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /favicon.ico HTTP/1.1
1-5	49176	0/3/4	_ 	0.01	1381	0	0	0.0	0.00	0.01 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET / HTTP/1.1
1-5	49176	0/2/2	_ 	0.00	1376	0	0	0.0	0.32	0.32 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /key.html HTTP/1.1
1-5	49176	0/2/3	_ 	0.01	1376	0	1	0.0	0.19	0.19 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET / HTTP/1.1
1-5	49176	0/3/3	_ 	0.01	295	0	0	0.0	0.47	0.47 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /jennie-image1.jpg HTTP/1.1
1-5	49176	0/2/4	_ 	0.01	290	0	1	0.0	0.15	0.39 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /favicon.ico HTTP/1.1
1-5	49176	0/1/2	_ 	0.00	290	0	0	0.0	0.00	0.19 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /favicon.ico HTTP/1.1
1-5	49176	0/1/1	_ 	0.02	108	0	0	0.0	0.00	0.00 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /mirrors.txt HTTP/1.1
1-5	49176	0/0/1	_ 	0.00	103	0	0	0.0	0.00	0.00 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET / HTTP/1.1
1-5	49176	0/2/4	_ 	0.02	6	0	1	0.0	0.00	0.01 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /server-status HTTP/1.1
1-5	49176	0/2/3	_ 	0.01	2223	1	1	0.0	0.42	0.42 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /jennie-image2.jpg HTTP/1.1
1-5	49176	0/3/4	_ 	0.01	1	0	0	0.0	0.51	0.51 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /jennie-image.jpg HTTP/1.1
1-5	49176	0/3/4	_ 	0.01	2223	0	1	0.0	0.53	0.53 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /jennie-image3.jpg HTTP/1.1
1-5	49176	0/2/3	_ 	0.01	2221	0	0	0.0	0.19	0.19 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /favicon.ico HTTP/1.1
1-5	49176	0/1/2	_ 	0.00	1	0	0	0.0	0.23	0.24 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /jennie-image3.jpg HTTP/1.1
1-5	49176	0/0/1	_ 	0.00	2220	0	0	0.0	0.00	0.00 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET / HTTP/1.1
1-5	49176	0/1/1	_ 	0.00	2218	0	0	0.0	0.00	0.00 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /backup HTTP/1.1
1-5	49176	0/1/1	_ 	0.00	2218	0	0	0.0	0.00	0.00 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /backup/ HTTP/1.1
1-5	49176	0/1/2	_ 	0.00	2218	0	0	0.0	0.00	0.00 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /icons/blank.gif HTTP/1.1
1-5	49176	0/0/1	_ 	0.00	2216	0	0	0.0	0.00	0.00 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /backup/onion_service/ HTTP/1.1
1-5	49176	0/1/2	_ 	0.01	2216	0	0	0.0	0.19	0.19 	127.0.0.1	http/1.1	ip-172-31-59-73.ap-northeast-2.	GET /jennie-image2.jpg HTTP/1.1
________________________________________
Srv	Child Server number - generation
PID	OS process ID
Acc	Number of accesses this connection / this child / this slot
M	Mode of operation
CPU	CPU usage, number of seconds
SS	Seconds since beginning of most recent request
Req	Milliseconds required to process most recent request
Dur	Sum of milliseconds required to process all requests
Conn	Kilobytes transferred this connection
Child	Megabytes transferred this child
Slot	Total megabytes transferred this slot
```

We can navigate to the `/backup` directory

<figure><img src="../../../.gitbook/assets/image (38) (4).png" alt=""><figcaption></figcaption></figure>

Next, go into the onion\_service folder.

<figure><img src="../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

In the `hostname` file, can see the flag string.

<figure><img src="../../../.gitbook/assets/image (83) (2).png" alt=""><figcaption></figcaption></figure>

Get the MD5 hash value for the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ echo -n 57ay_hun9ry_57ay_f00li5h | md5sum
7412f2529d4d87f89751698a82f4bde8  -
```

This challenge is slightly similar to the [Mod\_Status challenge](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/dsta-brainhack-cyber-defenders-discovery-camp-training-2022/ctf-topics/open-source-intelligence-osint#mod\_status) in CDDC 2022 training where we could check `server-status` to get the running processes.

Flag: 7412f2529d4d87f89751698a82f4bde8

## You can connect, If you don’t give up.

<figure><img src="../../../.gitbook/assets/image (22) (5).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given the password length which is a 5-digit number.

First, I used `crunch` to generate the digits list.

Crunch is very useful in generating password list. I have previously used it in [CDDC CTF 2022's WiFi challenge](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/dsta-brainhack-cyber-defenders-discovery-camp-ctf-2022/network#wifi) as well.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ crunch 5 5 -t %%%%% -o password.txt 
Crunch will now generate the following amount of data: 600000 bytes
0 MB
0 GB
0 TB
0 PB
Crunch will now generate the following number of lines: 100000 

crunch: 100% completed generating output
```

Next, I tried to do some research on how to access `Tor` site that required password.

I found two different ways from here: [https://forums.kali.org/showthread.php?18055-Hydra-using-Proxy](https://forums.kali.org/showthread.php?18055-Hydra-using-Proxy)

I tried the 2nd method.

I ran `tor` command to start the tor services.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ tor
May 18 04:55:59.600 [notice] Tor 0.4.7.13 running on Linux with Libevent 2.1.12-stable, OpenSSL 3.0.8, Zlib 1.2.13, Liblzma 5.4.1, Libzstd 1.5.4 and Glibc 2.36 as libc.
May 18 04:55:59.600 [notice] Tor can't help you if you use it wrong! Learn how to be safe at https://support.torproject.org/faq/staying-anonymous/
May 18 04:55:59.600 [warn] Tor was compiled with zstd 1.5.2, but is running with zstd 1.5.4. For safety, we'll avoid using advanced zstd functionality.
May 18 04:55:59.604 [notice] Read configuration file "/etc/tor/torrc".
May 18 04:55:59.621 [notice] Opening Socks listener on 127.0.0.1:9050
May 18 04:55:59.621 [notice] Opened Socks listener connection (ready) on 127.0.0.1:9050
May 18 04:55:59.000 [notice] Parsing GEOIP IPv4 file /usr/share/tor/geoip.
May 18 04:56:00.000 [notice] Parsing GEOIP IPv6 file /usr/share/tor/geoip6.
May 18 04:56:01.000 [notice] Bootstrapped 0% (starting): Starting
May 18 04:56:02.000 [notice] Starting with guard context "default"
May 18 04:56:03.000 [notice] Bootstrapped 5% (conn): Connecting to a relay
May 18 04:56:03.000 [notice] Bootstrapped 10% (conn_done): Connected to a relay
May 18 04:56:04.000 [notice] Bootstrapped 14% (handshake): Handshaking with a relay
May 18 04:56:04.000 [notice] Bootstrapped 15% (handshake_done): Handshake with a relay done
May 18 04:56:04.000 [notice] Bootstrapped 20% (onehop_create): Establishing an encrypted directory connection
May 18 04:56:05.000 [notice] Bootstrapped 25% (requesting_status): Asking for networkstatus consensus
May 18 04:56:05.000 [notice] Bootstrapped 30% (loading_status): Loading networkstatus consensus
May 18 04:56:07.000 [notice] Bootstrapped 75% (enough_dirinfo): Loaded enough directory info to build circuits
May 18 04:56:08.000 [notice] Bootstrapped 90% (ap_handshake_done): Handshake finished with a relay to build circuits
May 18 04:56:08.000 [notice] Bootstrapped 95% (circuit_create): Establishing a Tor circuit
May 18 04:56:10.000 [notice] Bootstrapped 100% (done): Done
ba
```

Next, I configured the environment.

```bash
┌──(kali㉿kali)-[~]
└─$ HYDRA_PROXY=socks5://127.0.0.1:9050

┌──(kali㉿kali)-[~]
└─$ printenv | grep HYDRA                                                                                       
HYDRA_PROXY=socks5://127.0.0.1:9050
```

However, using this command did not work:

`hydra -l connectme -P password.txt ssh://aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222`

It would produce some error:

```bash
[INFO] Using Connect Proxy: socks4://aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222
[ERROR] could not resolve proxy target aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion, entry ignored
[ERROR] proxy defined but not valid, exiting
```

Next, I tried the 1st method using `proxychains`.

However, it took too long to crack with `proxychains.`

At this point, I  unlocked the hint.

<figure><img src="../../../.gitbook/assets/image (39) (3).png" alt=""><figcaption></figcaption></figure>

This hint was  actually very useful  compared to the other challenges hints I unlocked. Now that we know the first 2 digits of the password, we could craft a new password list that is much smaller in size, which will allow us to crack the password faster.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ crunch 5 5 -t 57%%% -o password.txt
Crunch will now generate the following amount of data: 6000 bytes
0 MB
0 GB
0 TB
0 PB
Crunch will now generate the following number of lines: 1000 

crunch: 100% completed generating output
```

At this point, I also found two links: [here ](https://harshdushyants.medium.com/using-hydra-to-brute-force-different-services-3ea73470d213)and [here ](https://linuxhint.com/proxychains-tutorial/)that were useful in helping me understand how to use hydra and proxychains to solve the challenge.

Using the following command, we will get the password.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ proxychains hydra -l connectme -P password.txt ssh://aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222

[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.16
Hydra v9.3 (c) 2022 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2023-05-18 06:24:39
[WARNING] module ssh does not support HYDRA_PROXY* !
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[WARNING] Restorefile (you have 10 seconds to abort... (use option -I to skip waiting)) from a previous session found, to prevent overwriting, ./hydra.restore
[INFO] Using Connect Proxy: socks5://127.0.0.1:9050
[DATA] max 16 tasks per 1 server, overall 16 tasks, 1000 login tries (l:1/p:1000), ~63 tries per task
[DATA] attacking ssh://aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222/
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222  ...  OK
[proxychains] Strict chain  ...  127.0.0.1:9050 [proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222 [proxychains] Strict chain  ...  127.0.0.1:9050 [proxychains] Strict chain  ...  127.0.0.1:9050 [proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222 [proxychains] Strict chain  ...  127.0.0.1:9050 [proxychains] Strict chain  ...  127.0.0.1:9050 [proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222 [proxychains] Strict chain  ...  127.0.0.1:9050 [proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222 [proxychains] Strict chain  ...  127.0.0.1:9050 [proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222 [proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222 [proxychains] Strict chain  ...  127.0.0.1:9050 [proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222 [proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222  ...  OK
 ...  OK
 ...  OK
 ...  OK
 ...  OK
 ...  OK
 ...  OK
 ...  OK
[STATUS] 26.00 tries/min, 26 tries in 00:01h, 980 to do in 00:38h, 10 active
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222 [proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222  ...  OK
 ...  OK
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222 [proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222  ...  OK
 ...  OK
[STATUS] 15.33 tries/min, 46 tries in 00:03h, 960 to do in 01:03h, 10 active
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222 [proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222  ...  OK
 ...  OK
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222  ...  OK
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222  ...  OK
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222  ...  OK
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222 <--denied
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222 [proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222  ...  OK
 ...  OK
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222  ...  OK
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222  ...  OK
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222  ...  OK
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222  ...  OK
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222  ...  OK
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222  ...  OK
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222  ...  OK
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222  ...  OK
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222  ...  OK
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222  ...  OK
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222 [proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222  ...  OK
 ...  OK
[2222][ssh] host: aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion   login: connectme   password: 57913      
```

We can login using the password through ssh on port 2222 and read the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ proxychains ssh connectme@aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion -p 2222
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.16
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion:2222  ...  OK
connectme@aqseksjbef46d7nf77oeowxpkm4cy25msipq6hittx5qq45u5eic3qqd.onion's password: 

 .d8888b.                                              888             888          888    d8b                            
d88P  Y88b                                             888             888          888    Y8P                            
888    888                                             888             888          888                                   
888         .d88b.  88888b.   .d88b.  888d888  8888b.  888888 888  888 888  8888b.  888888 888  .d88b.  88888b.  .d8888b  
888        d88""88b 888 "88b d88P"88b 888P"       "88b 888    888  888 888     "88b 888    888 d88""88b 888 "88b 88K      
888    888 888  888 888  888 888  888 888     .d888888 888    888  888 888 .d888888 888    888 888  888 888  888 "Y8888b. 
Y88b  d88P Y88..88P 888  888 Y88b 888 888     888  888 Y88b.  Y88b 888 888 888  888 Y88b.  888 Y88..88P 888  888      X88 
 "Y8888P"   "Y88P"  888  888  "Y88888 888     "Y888888  "Y888  "Y88888 888 "Y888888  "Y888 888  "Y88P"  888  888  88888P' 
                                  888                                                                                     
                             Y8b d88P                                                                                     
                              "Y88P"                                                                                      

Last login: Thu May 18 02:05:57 2023 from 172.20.0.1
connectme@a12ba0d745eb:~$ ls
bin  flag
connectme@a12ba0d745eb:~$ cat flag
Brutef0rc3_15_50m3t1m35_4_g00d_m3th0d
```

Finally, get the MD5 hash value of it.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ echo -n Brutef0rc3_15_50m3t1m35_4_g00d_m3th0d | md5sum
38780352f99777c811b44ac57301e7b4  -
```

Flag: 38780352f99777c811b44ac57301e7b4

## Who’s that?

<figure><img src="../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given an email. I realized the username used for the email looked like it could be used for Instagram.

Hence, I searched up Instagram and found the [user](https://www.instagram.com/forhu.719/).

<figure><img src="../../../.gitbook/assets/image (90) (2).png" alt=""><figcaption></figcaption></figure>

Among the pictures, I saw the words `THEORY Final Edition` which looked like an album's name. I googled and searched for the images and confirmed that this person is `Younha`.

<figure><img src="../../../.gitbook/assets/image (43) (3).png" alt=""><figcaption></figcaption></figure>

Next, it was quite easy to find her Twitter once we know her name.

<figure><img src="../../../.gitbook/assets/image (81) (2).png" alt=""><figcaption></figcaption></figure>

Since the challenge asked for `Twitter ID`, I searched up tools to find her Twitter ID [here ](https://www.codeofaninja.com/tools/find-twitter-id/)and [here](https://tweeterid.com/).&#x20;

<figure><img src="../../../.gitbook/assets/image (10) (10).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (11) (4).png" alt=""><figcaption></figcaption></figure>

There was another site [here ](https://twiteridfinder.com/)which gave the same Twitter ID: `62755629`.

<figure><img src="../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

However, after several failed attempts of submitting the flag, I later realized what they wanted was not the Twitter ID but the Twitter username or handle which was even more straightforward.

Next, I searched up her birthday which can be found on [Wikipedia](https://en.wikipedia.org/wiki/Younha).

<figure><img src="../../../.gitbook/assets/image (85) (2).png" alt=""><figcaption><p>880429</p></figcaption></figure>

Next, I found that she has two dogs or chihuahuas to be exact. I also found this [YouTube video](https://www.youtube.com/watch?v=u1V8VGi38P0) where she talked about her dogs.

<figure><img src="../../../.gitbook/assets/image (50) (5).png" alt=""><figcaption></figcaption></figure>

Lastly, I found the password number which was one of her songs.

<figure><img src="../../../.gitbook/assets/image (82) (2).png" alt=""><figcaption><p>486</p></figcaption></figure>

Combining all the above information found and getting the MD5 hash value would give us the flag.

```bash
┌──(kali㉿kali)-[~]
└─$ echo -n younhaholic_880429_dog_486 | md5sum 
33f7403a27e2b6d893043f8d965796cd  -
```

## I’d like to hire you.

<figure><img src="../../../.gitbook/assets/image (57) (3).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given this link: [https://ibb.co/TvqfwG8](https://ibb.co/TvqfwG8)

We could save the Kakao image as an image file and do a reverse image search.

<figure><img src="../../../.gitbook/assets/image (87) (2).png" alt=""><figcaption></figcaption></figure>

If we click into the photo, we would get the month of the magazine: `March`. Another important information to note is that the person in the picture is `nana`.

<figure><img src="../../../.gitbook/assets/image (16) (5).png" alt=""><figcaption></figcaption></figure>

Next, after some searching, we would find that she renewed contract with `PLEDIS`.

<figure><img src="../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

The final information we need to collect is the phone number of PLEDIS, which can be found easily as well.

<figure><img src="../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

Combining the three pieces of information, we get the following: `03_pledis_025481677`

Finally, the MD5 hash value of this string is the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ echo -n 03_pledis_025481677 | md5sum 
4d48830d9bbc0259eecd5da93b488994  -
```

Flag: 4d48830d9bbc0259eecd5da93b488994

