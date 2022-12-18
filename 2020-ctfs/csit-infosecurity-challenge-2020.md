---
description: >-
  TISC 2020 is a 48 hours challenge for cybersecurity enthusiasts which was held
  on 8 August 2020.
---

# CSIT InfoSecurity Challenge 2020

## STAGE 1: What is this thing?

![](<../.gitbook/assets/0 (1)>)

![](../.gitbook/assets/1)

![](../.gitbook/assets/2)

We are given this challenge which mentioned that they are using a simple password (6 characters, hexadecimal) on the zip files.

Having no prior experience in CTF or cybersecurity challenges, I spent around 1-2 hours to Google “How to crack zip file password”.

I proceeded to use `zip2john` command to check the hash value of the mess file.

![](../.gitbook/assets/3)

Then, I saved this hash output to a `hash.txt` file.

![](<../.gitbook/assets/4 (1)>)

Finally, I use `john` command to crack the password.

The password cracked is: `ca5671`, and we can use `john -- show` command to display it

![](<../.gitbook/assets/5 (1)>)

This was my first time trying to crack a password. Even though I did not manage to solve the full challenge, I am glad I learned how to crack a zip file password.
