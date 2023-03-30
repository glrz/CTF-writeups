# Reverse Engineering

## Reverse

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

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
