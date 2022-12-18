---
description: This topic consists of 9 challenges and I solved 3/9 of them.
---

# Reverse Engineering

## WhoAmI

![](<../../.gitbook/assets/image (54).png>)

For this challenge, we were given a `.cpp` file. In the cpp file, there is `whoami` function and `start` function.

![](<../../.gitbook/assets/image (715).png>)

![](<../../.gitbook/assets/image (589).png>)

From the code, we could tell it is comparing the length of the 2 strings.&#x20;

In cpp, we use the `strcmp` function.

If we generate the SHA1 of `strcmp` [here](http://www.sha1-online.com/), it would give us the flag.

![](<../../.gitbook/assets/image (699).png>)

## Weird Section

![](<../../.gitbook/assets/image (273).png>)

For this challenge, we were given a `.exe` file embedded in the zip file.

{% file src="../../.gitbook/assets/Weird Section.zip" %}

&#x20;If we run `strings` on the file, we could see that it starts with `UPX`, `UPX1`, `UPX2`. It is likely to be packed by [`UPX`](https://upx.github.io/).

We could use `UPX` to unpack the `.exe` file.

`-d` option will decompress the file

`-o` option will output the file

In this case, we saved it to another file `weirdsection`.

![](<../../.gitbook/assets/image (641).png>)

Next, we could load the file into[ IDA freeware](https://hex-rays.com/ida-free/) and we see the string : UPX\_IS\_EASY

![](<../../.gitbook/assets/image (579).png>)

Finally, we generate the SHA1 of `UPX_IS_EASY` using [SHA1 online generator ](http://www.sha1-online.com/)and we will get the flag.

![](<../../.gitbook/assets/image (577).png>)

## (Sharp)

![](<../../.gitbook/assets/image (56).png>)

In this challenges, it provided us with a [link](https://pelock.medium.com/reverse-engineering-tools-for-net-applications-a28275f185b4) with some possible tools we could use for .NET applications. We are also given a zip file.

{% file src="../../.gitbook/assets/Rev#3_CSharp.zip" %}

We already had some experience with[ dotPeek](https://www.jetbrains.com/decompiler/) previously [here](https://gadiel-lau.gitbook.io/2020-writeups/brixel-ctf-winter-edition-2020/reverse-engineering-and-cracking#no-peeking). Hence, I decided to stick with using `dotPeek`. Dotpeek is able to disassemble .NET applications.

I opened the file in `dotPeek`, expanded the application, scroll down and found the `contentloaded` variable. It contains a simple `if else` statement which returns correct/wrong and looked like a flag.

If we generate the SHA1 of the string using [SHA1 online generator](http://www.sha1-online.com/) and we would get the flag.

![](<../../.gitbook/assets/image (63).png>)
