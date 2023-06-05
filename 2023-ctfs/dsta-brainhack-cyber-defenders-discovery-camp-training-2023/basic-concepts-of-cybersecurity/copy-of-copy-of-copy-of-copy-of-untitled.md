# Introduction to Cryptography

## Snow Country <a href="#modal_title" id="modal_title"></a>

<figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given the ciphertext and we know that it was encrypted with vigenere cipher. Additionally, we know that the key length is 7.

Looking at the challenge title, `Country` is also 7 characters.

Before we use Vigenere Cipher decode with the key: Country, we would see that  the ciphertext has `==` appended at  the end, which likely suggest that it was `Base64` encoded as well.

We could decode the `Base64` first followed by `Vigenere cipher` using [CyberChef](https://cyberchef.org/#recipe=From\_Base64\('A-Za-z0-9%2B/%3D',true,false\)Vigen%C3%A8re\_Decode\('Country'\)\&input=Vm5aNVoydHlaM0J4ZFhwNFpuTjJZM3BuWVhacWNXSmhaMjVsYkdkNlkyRnRabkpxYzIxaGFHNWhjV2xvWjJ0d0xnPT0) to get the flag.

Flag: Thetraincameoutofthelongtunnelintothesnowcountry

## Hash Functions <a href="#modal_title" id="modal_title"></a>

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Pretty straightforward challenge, if we watch the lecture videos and do some additional research,  we will get the correct answer.

Flag: 124

## Cryptographic Primitives

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Similarly, if we watch the lecture videos and do some additional research,  we will get the correct answer.

Flag: 45
