---
description: >-
  For the challenges that are like MCQ questions, I will not be doing any
  further explanations since it was pretty straightforward.
---

# Cryptography

## Length of Plain text and Cipher text

<figure><img src="../../../.gitbook/assets/image (39) (4).png" alt=""><figcaption></figcaption></figure>

Flag: 125

## dggnbh

<figure><img src="../../../.gitbook/assets/image (20) (6).png" alt=""><figcaption></figcaption></figure>

At first glance, this looked like `Enigma Machine`. I have previously solved a similar challenge [here](https://gadiel-lau.gitbook.io/2020-writeups-1/2020-ctfs/gsctf-2020#crypto-war).

Similarly, we can use [cryptii](https://cryptii.com/pipes/enigma-machine) to solve it. Key in the values accordingly and we will get the flag.

<figure><img src="../../../.gitbook/assets/image (49) (6).png" alt=""><figcaption></figcaption></figure>

Flag: bigbrotheriswatchingyou

## Number of primes

<figure><img src="../../../.gitbook/assets/image (11) (4).png" alt=""><figcaption></figcaption></figure>

Flag: 4

## Modular operation

<figure><img src="../../../.gitbook/assets/image (21) (1).png" alt=""><figcaption></figcaption></figure>

For this challenge, it can be done using Euler’s theorem by hand manually.

However, to save some time, we can use `WolframAlpha` to simplify things and get the flag in a shorter time.

The basic idea of solving this is:

x+y mod p = (x mod p + y mod p) mod p

So once wolfram alpha gives us the mod p of the two summands here,

We can add them up and mod p again

Note that this is done using a `TeXit` bot in Discord that uses `WolframAlpha` to solve.

<figure><img src="../../../.gitbook/assets/image (18) (4).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (51) (4).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (16) (6).png" alt=""><figcaption></figcaption></figure>

Flag: 39

## ECC

<figure><img src="../../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

For this challenge, we could simply search up : `ecc point addition calculator`

Input the values respectively starting from curve, field, all the way to values of Q.

<figure><img src="../../../.gitbook/assets/image (23) (4).png" alt=""><figcaption></figcaption></figure>

Add up `R1` and `R2` manually and we will get the flag.

38 + 12 = 50

Flag: 50

## Attack

<figure><img src="../../../.gitbook/assets/image (15) (4).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given poorly generated, vulnerable RSA public key and a ciphertext of a message encrypted with that public key. Our objective is to decrypt the ciphertext.

This is similar to the challenge I solved here: [https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/lagncrash-interpoly-ctf-2022#weak...-r.essurection-s.word-a.ni-mator](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/lagncrash-interpoly-ctf-2022#weak...-r.essurection-s.word-a.ni-mator)

Similarly, we can use RsaCtfTool to solve.

```bash
┌──(kali㉿kali)-[~/Downloads/RsaCtfTool]
└─$ python3 RsaCtfTool.py -n 52821092352056891108634371032255980789902606938110292352446249989420510518409201116621640857171136374508176588086468825442385323152338182499920328187870897957935244716046599631793403500453743947449747924237637706570219423388542879844421592223041386443952395719288553980810360587525755265802170825753068223161 -e 65537 --uncipher 31271761600949955082244252192430781629338529281368280264088968996037979357288300694674758647673503534075637674011717935231913501391357902687788141513501051133674176329726519979229788612864155610364266442889594038413523942956330665290297228274203490185118409636482221253706336295604512813002633777605991620598
private argument is not set, the private key will not be displayed, even if recovered.

[*] Testing key /tmp/tmp8kb9y3_t.
attack initialized...
attack initialized...
[*] Performing factordb attack on /tmp/tmp8kb9y3_t.
[!] Composite not in factordb, couldn't factorize...
[+] Time elapsed: 0.7404 sec.
[*] Performing mersenne_primes attack on /tmp/tmp8kb9y3_t.
 27%|████████████████████▎                                                     | 14/51 [00:00<00:00, 165409.17it/s]
[+] Time elapsed: 0.0099 sec.
[*] Performing lucas_gcd attack on /tmp/tmp8kb9y3_t.
100%|███████████████████████████████████████████████████████████████████████| 9999/9999 [00:00<00:00, 77948.03it/s]
[+] Time elapsed: 0.1289 sec.
[*] Performing pastctfprimes attack on /tmp/tmp8kb9y3_t.
100%|████████████████████████████████████████████████████████████████████████| 113/113 [00:00<00:00, 849384.14it/s]
[+] Time elapsed: 0.0006 sec.
[*] Performing fibonacci_gcd attack on /tmp/tmp8kb9y3_t.
100%|███████████████████████████████████████████████████████████████████████| 9999/9999 [00:00<00:00, 93688.57it/s]
[+] Time elapsed: 0.1072 sec.
[*] Performing smallq attack on /tmp/tmp8kb9y3_t.
[+] Time elapsed: 0.3273 sec.
[*] Performing nonRSA attack on /tmp/tmp8kb9y3_t.
[+] Time elapsed: 0.0021 sec.
[*] Performing system_primes_gcd attack on /tmp/tmp8kb9y3_t.
100%|██████████████████████████████████████████████████████████████████████| 7007/7007 [00:00<00:00, 568088.45it/s]
[+] Time elapsed: 0.0373 sec.
[*] Performing compositorial_pm1_gcd attack on /tmp/tmp8kb9y3_t.
100%|███████████████████████████████████████████████████████████████████████| 9999/9999 [00:00<00:00, 16104.68it/s]
[+] Time elapsed: 0.6215 sec.
[*] Performing hart attack on /tmp/tmp8kb9y3_t.
[*] Attack success with hart method !
[+] Total time elapsed min,max,avg: 0.0006/0.7404/0.2194 sec.

Results for /tmp/tmp8kb9y3_t:

Unciphered data :
HEX : 0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000277e949c
INT (big endian) : 662607004
INT (little endian) : 109954250319984557046968991119222149470458792856558691154178978068216936850508462074743666910796996113415352100767018503392323773276229851763997096572379626060785084002076382852805400984788013945599674619676748736463947879247838580103440916065008606651228780303028265101488454927900127152529771231861301837824
utf-16 : 縧鲔
STR : b"\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00'~\x94\x9c"

```

The flag is found under `INT (big endian)`.

Flag: 662607004

