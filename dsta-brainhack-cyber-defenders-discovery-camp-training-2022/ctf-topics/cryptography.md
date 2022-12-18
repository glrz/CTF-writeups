---
description: This topic consists of 9 challenges and I solved all of them.
---

# Cryptography

## Symmetric Key 1

![](<../../.gitbook/assets/image (3) (1).png>)

## Symmetric Key 2

![](<../../.gitbook/assets/image (34) (1).png>)

## Symmetric Key 3

![](<../../.gitbook/assets/image (30) (1).png>)

## Symmetric Key 4

![](<../../.gitbook/assets/image (78) (1).png>)

In this challenge, we were given a `CTF_Crypto7.png` file.

![](<../../.gitbook/assets/image (27).png>)

> PKCS#7 is a typical padding method, which the last byte in the block indicates the number of padding elements. If you have 15 bytes and need to add one more byte to fill up the block, you append hex (01). If you need to add 2 bytes, you append hex (02 02). 3 bytes requires you add the 3-byte pad of hex(03 03 03). If the text fills up the 16-byte-block exactly, you add another block that contains 16 bytes hex(10 10 10 10 10 10 10 10 10 10 10 10 10 10 10 10)

Since we have 10 bytes here, we need to add 6 more bytes in the block, which is why 060606060606 padding.

A pretty good writeup explaining padding could be found [here](https://jiang-zhenghong.github.io/blogs/PaddingOracle.html).

## Public Key 1

![](<../../.gitbook/assets/image (76) (1).png>)

## Public Key 2

![](<../../.gitbook/assets/image (23).png>)

## Public Key 3

![](<../../.gitbook/assets/image (85) (1).png>)

Options `1` and `3` are true. Options `2` and `4` are not true.

If we press the `padlock` icon, we could see `Certificate is valid`.&#x20;

![](<../../.gitbook/assets/image (96) (1).png>)

Clicking on it would give us more information such as the information of the issuer under `General` and the public key under `Details`.

![](<../../.gitbook/assets/image (88) (1).png>)

![](<../../.gitbook/assets/image (12) (1).png>)

## Hash function 1

![](<../../.gitbook/assets/image (90) (1).png>)

The correct answer is known as hash collision.

## Hash function 2

![](<../../.gitbook/assets/image (56).png>)

Found some pretty good slides [here](https://www.cs.purdue.edu/homes/ssw/cs355/hash.pdf).
