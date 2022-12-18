---
description: Some extra writeups on Cryptography and OSINT
---

# Extra writeups

## Can COViD steal Bob’s idea? (Cryptography)

Note : This was not solved during competition

We open the .pcapng file in WireShark, and extract the following text.

> p = 298161833288328455288826827978944092433
>
> g = 216590906870332474191827756801961881648
>
> g^a = 181553548982634226931709548695881171814
>
> g^b = 64889049934231151703132324484506000958
>
> Hi Alice, could you please help me to design a keystream generator according to the file I share in the file server so that I can use it to encrypt my 500-bytes secret message? Please make sure it run with maximum period without repeating the keystream. The password to protect the file is our shared Diffie-Hellman key in digits. Thanks.

From this information, we know that

x = g^a = 181553548982634226931709548695881171814 (mod p)

y = g^b = 64889049934231151703132324484506000958 (mod p)

a = 211631375588570729261040810141700746731

We could write a simple python code to get the flag based on the information above

```python
a =  = 211631375588570729261040810141700746731
gb = 64889049934231151703132324484506000958
p = 298161833288328455288826827978944092433
print(pow(gb, a, p))
```

This will give us an output: 246544130863363089867058587807471986686 which is the flag&#x20;

Flag: govtech-csg{246544130863363089867058587807471986686}

## Hunt him down! (OSINT)

Note : This was not solved during competition

![](<../../.gitbook/assets/image (191).png>)

We could also use this online tool [here](https://toolbox.googleapps.com/apps/dig/#NS/)&#x20;

When we look up the DNS records for  we can see

![](<../../.gitbook/assets/image (11).png>)

We can use sherlock to check for his social media accounts

![](<../../.gitbook/assets/image (228).png>)

Go to Lionel's Twitter and we can see a tweet

![](<../../.gitbook/assets/image (201).png>)

![We can see his phone number here 963672918](<../../.gitbook/assets/image (70).png>)

To get his full name, we can google his email `lionelcheng@protonmail.com` and we will find his LinkedIn account

![](<../../.gitbook/assets/image (246).png>)

To find his postal code, we go to his Instagram account

![](<../../.gitbook/assets/image (241).png>)

In one of his runs, he mentioned that social space was at his block.

![](<../../.gitbook/assets/image (253).png>)

We can google social space and find his postal code

![](<../../.gitbook/assets/image (54).png>)

Putting all the information together, we get the flag.

Flag: govtech-csg{LionelChengXiangYi-963672918-018935}

## Resources:

[https://dame-dango.github.io/STACKtheFlags2020/](https://dame-dango.github.io/STACKtheFlags2020/)

[https://docs.google.com/document/d/1GrQ6znlN2Z0tu\_uAPAs1qrn6by24I51mq8RIIHmFGDU/edit](https://docs.google.com/document/d/1GrQ6znlN2Z0tu\_uAPAs1qrn6by24I51mq8RIIHmFGDU/edit)

[https://docs.google.com/spreadsheets/d/1EMgqFpcc\_InJZy264AIe1QpvUDFs1-24iTrnKbdoOUo/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1EMgqFpcc\_InJZy264AIe1QpvUDFs1-24iTrnKbdoOUo/edit?usp=sharing)
