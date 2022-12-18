# Crypto

## Vigenere

![](<../.gitbook/assets/image (113) (1).png>)

For this challenge, we are given a `VIGENERE_encrypt.txt` file in the zip file.

{% file src="../.gitbook/assets/VIGENERE_encrypt.txt.zip" %}

If we open the `.txt` file, we could see the following contents.

`ns wyy ixsu kfmex rri tskcxipo tycwuyvb? sj wyy ukrr ds eox y ppyq, cme rcoh ry olya ylssd zgqilovc. ppyq mq MHBM22{z3pi_wgwtjo_4rb_34cc_abcnd0_gf4vpcxkc}`

From the challenge title, we would already know this is `Vigenѐre Cipher`.

Furthermore, we had encountered such challenge before [here](https://gadiel-lau.gitbook.io/2022-writeups/dsta-brainhack-cyber-defenders-discovery-camp-training-2022/basic-concepts-of-cybersecurity/introduction-to-cryptography), [here](https://gadiel-lau.gitbook.io/2020-writeups/brixel-ctf-winter-edition-2020/cryptography#merde) and [here](https://gadiel-lau.gitbook.io/2022-writeups/aisp-cyber-wellness-ctf#vigenere).

To solve this, we simply use an [online Vigenere Cipher decoder](https://www.dcode.fr/vigenere-cipher), paste in the text and click `AUTOMATIC DECRYPTION`. The flag would appear decoded on the left.

![](<../.gitbook/assets/image (27).png>)

Flag: CDDC22{v3ry\_simple\_4nd\_34sy\_crypt0\_ch4llenge}

