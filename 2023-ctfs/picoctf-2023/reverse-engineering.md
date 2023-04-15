# Reverse Engineering

## Reverse

<figure><img src="../../.gitbook/assets/image (1) (3) (3).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a binary executable file. To verify this, we can use the `file` command.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ file ret 
ret: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=5b418a8324e272ecb905431b840cf2b7d0a7a509, for GNU/Linux 3.2.0, not stripped
```

We can simply run `strings` on this file and `grep` for pico.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ strings ret | grep pico     
picoCTF{H
Password correct, please see flag: picoCTF{3lf_r3v3r5ing_succe55ful_8108250b}
```

Flag: picoCTF{3lf\_r3v3r5ing\_succe55ful\_8108250b}

## Safe Opener 2

<figure><img src="../../.gitbook/assets/image (1) (3).png" alt=""><figcaption></figcaption></figure>

For this challenge, we  were given a `.class` file which contained compiled Java class data.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ file SafeOpener.class 
SafeOpener.class: compiled Java class data, version 52.0 (Java 1.8)
```

We could use an [online Java decompiler](http://www.javadecompilers.com/) to decompile the data.

Within the decompiled code, we will be able to see the flag.

```bash
import java.io.IOException;
import java.util.Base64;
import java.io.Reader;
import java.io.BufferedReader;
import java.io.InputStreamReader;

// 
// Decompiled by Procyon v0.5.36
// 

public class SafeOpener
{
    public static void main(final String[] args) throws IOException {
        final BufferedReader keyboard = new BufferedReader(new InputStreamReader(System.in));
        final Base64.Encoder encoder = Base64.getEncoder();
        String encodedkey = "";
        String key = "";
        for (int i = 0; i < 3; ++i) {
            System.out.print("Enter password for the safe: ");
            key = keyboard.readLine();
            encodedkey = encoder.encodeToString(key.getBytes());
            System.out.println(encodedkey);
            final boolean isOpen = openSafe(encodedkey);
            if (isOpen) {
                break;
            }
            System.out.println("You have  " + (2 - i) + " attempt(s) left");
        }
    }
    
    public static boolean openSafe(final String password) {
        final String encodedkey = "picoCTF{SAf3_0p3n3rr_y0u_solv3d_it_ccb5525e}";
        if (password.equals(encodedkey)) {
            System.out.println("Sesame open");
            return true;
        }
        System.out.println("Password is incorrect\n");
        return false;
    }
}
```

Flag: picoCTF{SAf3\_0p3n3rr\_y0u\_solv3d\_it\_ccb5525e}

## timer

<figure><img src="../../.gitbook/assets/image (3) (9) (1) (1).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.zip` file.

First, lets unzip the file.

There were way too many files extracted, hence I won't be pasting all the extracted contents here.

Initially, I thought I could use an[ online APK decompiler](http://www.javadecompilers.com/apk) to search for the flag manually. However, I realized that this process will be very time-consuming.

How I solved it was to go to the extracted directory which contained two other sub-directories, ran the `grep` command with `-r` option to search recursively within the two sub-directories for the keyword `pico`.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cd timer_source_from_JADX 
                                                                                                                  
┌──(kali㉿kali)-[~/Downloads/timer_source_from_JADX]
└─$ ls
resources  sources

┌──(kali㉿kali)-[~/Downloads/timer_source_from_JADX]
└─$ grep -r pico                                                
sources/com/example/timer/BuildConfig.java:    public static final String VERSION_NAME = "picoCTF{t1m3r_r3v3rs3d_succ355fully_17496}";
resources/AndroidManifest.xml:<manifest xmlns:android="http://schemas.android.com/apk/res/android" android:versionCode="1" android:versionName="picoCTF{t1m3r_r3v3rs3d_succ355fully_17496}" android:compileSdkVersion="32" android:compileSdkVersionCodename="12" package="com.example.timer" platformBuildVersionCode="32" platformBuildVersionName="12">
grep: resources/classes3.dex: binary file matches
```

Flag: picoCTF{t1m3r\_r3v3rs3d\_succ355fully\_17496}

## Ready Gladiator 0

<figure><img src="../../.gitbook/assets/image (2) (12).png" alt=""><figcaption></figcaption></figure>

For this challenge, I connected to the server and it automatically ran the `redcode`

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ nc saturn.picoctf.net 50902 < imp.red
;redcode
;name Imp Ex
;assert 1
mov 0, 1
end
Submit your warrior: (enter 'end' when done)

Warrior1:
;redcode
;name Imp Ex
;assert 1
mov 0, 1
end

Rounds: 100
Warrior 1 wins: 0
Warrior 2 wins: 0
Ties: 100
Try again. Your warrior (warrior 1) must lose all rounds, no ties.
```

I edited the code using `gedit` by changing `mov 0, 1` to `mov 1, 0`

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ gedit imp.red
Change the code to:
;redcode

;name Imp Ex

;assert 1

mov 1, 0

end
```

I saved it and ran this code on the server again which gave me the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ nc saturn.picoctf.net 50902 < imp.red
;redcode
;name Imp Ex
;assert 1
mov 1, 0
end
Submit your warrior: (enter 'end' when done)

Warrior1:
;redcode
;name Imp Ex
;assert 1
mov 1, 0
end

Rounds: 100
Warrior 1 wins: 0
Warrior 2 wins: 100
Ties: 0
You did it!
picoCTF{h3r0_t0_z3r0_4m1r1gh7_a220a377}
```

For your information, Corewar is a programming game in which players write programs called warriors that compete for control of a virtual computer memory. Warriors are written in Redcode, a simple assembly language that is specific to Corewar.

In Redcode, the `mov` instruction is used to copy a value from one memory location (the source) to another memory location (the destination). The correct syntax for the `mov` instruction is `mov destination, source`.

In Corewar, each warrior is loaded into a specific area of memory, and the first instruction of each warrior is executed in turn. This means that the first instruction of a warrior is critical to its operation, since it determines the initial behavior of the warrior in the game.

If a `mov` instruction is used to copy a value from a memory location that is not intended to be used as a source, the resulting behavior of the warrior could be unpredictable or even harmful to the warrior's chances of success. For example, if a `mov` instruction is used to overwrite the first instruction of a warrior, the warrior may not be able to function properly and may lose the game.

Therefore, it is important to be careful when using `mov` instructions in Redcode programs for Corewar, and to ensure that the source and destination memory locations are used correctly to avoid unintended consequences.

If you use `mov 0, 1`, you are attempting to move the value stored in memory location 1 to memory location 0. This would overwrite the first instruction of the program with the value stored at memory location 1, which could cause the program to malfunction or crash since the first instruction is usually critical to the program's operation.

On the other hand, using `mov 1, 0` would move the value stored in memory location 0 to memory location 1. This would not affect the program's operation as drastically, since the value stored in memory location 0 is typically not critical to the program's function.

Flag: picoCTF{h3r0\_t0\_z3r0\_4m1r1gh7\_a220a377}

## Ready Gladiator 1

<figure><img src="../../.gitbook/assets/image (49) (2).png" alt=""><figcaption></figcaption></figure>

For this challenge, I searched online for a [simple warrior](https://corewar-docs.readthedocs.io/en/latest/corewar/warriors/) named 'Dwarf'.

I used the warrior and it gave me the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ gedit imp.red
Edit this into the code:
add #4, 3
mov 2, @2
jmp -2
dat #0, #0

Note: Number of wins quite random.
┌──(kali㉿kali)-[~/Downloads]
└─$ nc saturn.picoctf.net 54835 < imp.red
;redcode
;name Imp Ex
;assert 1
add #4, 3
mov 2, @2
jmp -2
dat #0, #0
end
Submit your warrior: (enter 'end' when done)

Warrior1:
;redcode
;name Imp Ex
;assert 1
add #4, 3
mov 2, @2
jmp -2
dat #0, #0
end

Rounds: 100
Warrior 1 wins: 24
Warrior 2 wins: 0
Ties: 76
You did it!
picoCTF{1mp_1n_7h3_cr055h41r5_0b0942be}
```

Note that the number of wins is not deterministic, meaning it changed almost everytime the program ran.

On 2nd run it gets the following

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ nc saturn.picoctf.net 53640 < imp.red
;redcode
;name Imp Ex
;assert 1
add #4, 3
mov 2, @2
jmp -2
dat #0, #0
end
Submit your warrior: (enter 'end' when done)

Warrior1:
;redcode
;name Imp Ex
;assert 1
add #4, 3
mov 2, @2
jmp -2
dat #0, #0
end

Rounds: 100
Warrior 1 wins: 33
Warrior 2 wins: 0
Ties: 67
You did it!
picoCTF{1mp_1n_7h3_cr055h41r5_0b0942be}
```

Flag: picoCTF{1mp\_1n\_7h3\_cr055h41r5\_0b0942be}
