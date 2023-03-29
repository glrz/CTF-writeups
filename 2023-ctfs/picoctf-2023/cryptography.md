# Cryptography

## HideToSee

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given an image file.

Upon opening the image, it showed the typical image of an `atbash cipher`.

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

From the challenge title, it was probably referring to `Steghide`.&#x20;

I ran `stegoveritas` which found something with `Steghide` and reading the contents of it will give us a string of characters which looked encoded by `atbash cipher`.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ stegoveritas atbash.jpg                                                
Running Module: SVImage
+------------------+------+
|   Image Format   | Mode |
+------------------+------+
| JPEG (ISO 10918) | RGB  |
+------------------+------+
Found something with StegHide: /home/kali/Downloads/results/steghide_2884c2cac97e251b72b1fbd76c614daf.bin
Running Module: MultiHandler

Exif
====
+---------------------+---------------------------------+
| key                 | value                           |
+---------------------+---------------------------------+
| SourceFile          | /home/kali/Downloads/atbash.jpg |
| ExifToolVersion     | 12.44                           |
| FileName            | atbash.jpg                      |
| Directory           | /home/kali/Downloads            |
| FileSize            | 51 kB                           |
| FileModifyDate      | 2023:03:15 05:07:30-04:00       |
| FileAccessDate      | 2023:03:15 05:07:53-04:00       |
| FileInodeChangeDate | 2023:03:15 05:07:32-04:00       |
| FilePermissions     | -rw-r--r--                      |
| FileType            | JPEG                            |
| FileTypeExtension   | jpg                             |
| MIMEType            | image/jpeg                      |
| JFIFVersion         | 1.01                            |
| ResolutionUnit      | None                            |
| XResolution         | 1                               |
| YResolution         | 1                               |
| ImageWidth          | 465                             |
| ImageHeight         | 455                             |
| EncodingProcess     | Baseline DCT, Huffman coding    |
| BitsPerSample       | 8                               |
| ColorComponents     | 3                               |
| YCbCrSubSampling    | YCbCr4:2:0 (2 2)                |
| ImageSize           | 465x455                         |
| Megapixels          | 0.212                           |
+---------------------+---------------------------------+
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
Found something worth keeping!
JPEG image data, JFIF standard 1.01, aspect ratio, density 1x1, segment length 16, baseline, precision 8, 465x455, components 3
┌──(kali㉿kali)-[~/Downloads]
└─$ cat /home/kali/Downloads/results/steghide_2884c2cac97e251b72b1fbd76c614daf.bin

krxlXGU{zgyzhs_xizxp_03w8uvvu}
```

Decoding it on [dCode ](https://www.dcode.fr/atbash-cipher)will give us the flag.

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

Flag: picoCTF{atbash\_crack\_03d8feef}

## ReadMyCert

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.csr` file.

If we read the contents of it, we would realize that it's most likely `Base64` encoded.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cat readmycert.csr 
-----BEGIN CERTIFICATE REQUEST-----
MIICpzCCAY8CAQAwPDEmMCQGA1UEAwwdcGljb0NURntyZWFkX215Y2VydF8yNzQ0
MmRiYX0xEjAQBgNVBCkMCWN0ZlBsYXllcjCCASIwDQYJKoZIhvcNAQEBBQADggEP
ADCCAQoCggEBAMJgY0GknGgyyJeS+szAH3OaULS+tJsqG6sDRYoNhE+oFfTKiF6q
JTbpo5xR38MyMdBKAusy3GXffuBFfbiJ+2MOtp/Fydc5Gal/fVTnv9+InVeOR1M4
+WsU311IcRK20ZL4vVzZGJJJy3146qXBnWf99O4cOgRDlUJBZzq99cjKPReSWcuN
bicDLRrnWdjkMA5law4j4W8WaWkultVtugCBKyglXghWg++XG5Hf9GomCEXH6AtD
A96Dzfr3p+wL2wgAmzo5d0On312edPONkV6n6rUs2gdV56zo5kT3Y+huU45HfuQm
/rbrP3h2Pt4Keijwnz+Vlk4qZLfFdi6fAzcCAwEAAaAmMCQGCSqGSIb3DQEJDjEX
MBUwEwYDVR0lBAwwCgYIKwYBBQUHAwIwDQYJKoZIhvcNAQELBQADggEBAIgQgNqE
5tog4l4Jp1a9Be2jqiYT22pZfnfsJwyJZrTJgwMNjKnhuWQjERJwbI3NhWneLCa9
dvCPSkg2dn+r1fMIMAtdq1BsKF/qv4RnMBRBuKrCwBoRG21tU/86Closms/wpika
hSzl8wst9TSF03JbtcoEmZ4NEAkjvHzRiZ6q17IH29FcBvmpZB6vYs4Ig9jcviqE
ZVtTD5mFGUbLqUfR/Dd9y6aFXael1pPgFpzMZkZrZn7ogJQJX7dbpoONIslNuU7P
FBZzmZcCgwXru25kuvkDTM+t8bMTUUg9CSH7r8Uj9QhWZklZ8Q2eD/cw/OpPMFQX
yIjuh37qqClf+2I=
-----END CERTIFICATE REQUEST-----
```

We can decode this in `CyberChef` to get the flag

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

Flag: picoCTF{read\_mycert\_27442dba}

## rotation

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

We can download the `encrypted.txt` file which showed some string that looked like it was rotated. We can use the common `ROT13` to decode it. However, this would not give us the flag.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

If we increase the `amount` to 18, we will get the flag.

Note that we can use the `ROT13 Brute Force` to determine the correct `amount`.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Flag: picoCTF{r0tat1on\_d3crypt3d\_9985b7db}
