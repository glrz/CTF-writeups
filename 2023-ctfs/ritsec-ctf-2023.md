---
description: RITSEC CTF 2023 was held from 1 Apr - 3 Apr 2023.
---

# RITSEC CTF 2023

RITSEC CTF 2023 is a security-focused competition that featured the following categories: BIN\PWN, Crypto, Reversing, Forensics, Web, Misc, and more.

More information can be found [here](https://ctftime.org/event/1860).

I participated in the CTF with team [`youtiaos`](https://ctftime.org/team/194864) with my username `RZ`.

<figure><img src="../.gitbook/assets/image (4) (6).png" alt=""><figcaption></figcaption></figure>

I spent some time enjoying some of the simpler challenges during the weekend. I solved challenges in the `Introduction`, `Chandi Bot`, `Reversing` and `Steganography` categories.

## Intro

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was similar to the challenges I solved [here ](https://gadiel-lau.gitbook.io/2023-writeups/2023-ctfs/irisctf-2023#discord)and [here](https://gadiel-lau.gitbook.io/2023-writeups/2023-ctfs/wolvctf-2023#sanity-check).

Upon joining the discord server and navigating the the `rules` channel, we can see the flag displayed beside the top of the channel header.

<figure><img src="../.gitbook/assets/image (49) (1).png" alt=""><figcaption></figcaption></figure>

Flag: RS{!flag}

## Chandi Bot 2

<figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

There were a series of Chandi Bot challenges in the `Chandi Bot` category and I solved one of them. I found that this was pretty interesting and different from usual CTFs as they created a discord bot specifically for the challenges.

For this challenge, I navigated to the `Chandi Bot` channel on Discord.

Next, I tested the possible `commands` which I can issue to the bot on the server by typing `/` on the chat.

I was then presented with a few of the `FREQUENTLY USED` functions. One of them was `/flag` &#x20;

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

Issuing the `/flag` command on the server would get the flag from the bot.

<figure><img src="../.gitbook/assets/image (50) (1).png" alt=""><figcaption></figcaption></figure>

Flag: RS{HMMM\_WHAT\_ARE\_YOU\_LOOKING\_AT}



## Weird

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `blank.png` file.

First, we could open this in image viewer and we would see that it's just a blank image.

<figure><img src="../.gitbook/assets/image (3) (9).png" alt=""><figcaption></figcaption></figure>

Since the challenge was in the `steganography` category, I ran my favourite stego tool: `stegoveritas` as usual

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ stegoveritas blank.png        
Running Module: SVImage
+---------------------------+------+
|        Image Format       | Mode |
+---------------------------+------+
| Portable network graphics | RGBA |
+---------------------------+------+
Found something worth keeping!
International EBCDIC text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (45000), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (45000), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
International EBCDIC text, with very long lines (65536), with no line terminators
Found something worth keeping!
International EBCDIC text, with very long lines (65536), with no line terminators
Found something worth keeping!
International EBCDIC text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (45000), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
International EBCDIC text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
Found something worth keeping!
ISO-8859 text, with very long lines (65536), with no line terminators
ERROR:stegoveritas.helpers:not supported for this image mode
ERROR:stegoveritas.helpers:
"""                                                                                                                 
Traceback (most recent call last):                                                                                  
  File "/usr/lib/python3.10/multiprocessing/pool.py", line 125, in worker                                           
    result = (True, func(*args, **kwds))                                                                            
  File "/home/kali/.local/lib/python3.10/site-packages/stegoveritas/modules/image/analysis/filters.py", line 33, in run_image_op                                                                                                        
    img = op(image.file)                                                                                            
  File "/usr/lib/python3/dist-packages/PIL/ImageOps.py", line 153, in autocontrast                                  
    return _lut(image, lut)                                                                                         
  File "/usr/lib/python3/dist-packages/PIL/ImageOps.py", line 58, in _lut                                           
    raise OSError("not supported for this image mode")                                                              
OSError: not supported for this image mode                                                                          
"""                                                                                                                 
ERROR:stegoveritas.helpers:not supported for this image mode
ERROR:stegoveritas.helpers:
"""                                                                                                                 
Traceback (most recent call last):                                                                                  
  File "/usr/lib/python3.10/multiprocessing/pool.py", line 125, in worker                                           
    result = (True, func(*args, **kwds))                                                                            
  File "/home/kali/.local/lib/python3.10/site-packages/stegoveritas/modules/image/analysis/filters.py", line 33, in run_image_op                                                                                                        
    img = op(image.file)                                                                                            
  File "/usr/lib/python3/dist-packages/PIL/ImageOps.py", line 383, in equalize                                      
    return _lut(image, lut)                                                                                         
  File "/usr/lib/python3/dist-packages/PIL/ImageOps.py", line 58, in _lut                                           
    raise OSError("not supported for this image mode")                                                              
OSError: not supported for this image mode                                                                          
"""                                                                                                                 
ERROR:stegoveritas.helpers:not supported for this image mode
ERROR:stegoveritas.helpers:
"""                                                                                                                 
Traceback (most recent call last):                                                                                  
  File "/usr/lib/python3.10/multiprocessing/pool.py", line 125, in worker                                           
    result = (True, func(*args, **kwds))                                                                            
  File "/home/kali/.local/lib/python3.10/site-packages/stegoveritas/modules/image/analysis/filters.py", line 33, in run_image_op                                                                                                        
    img = op(image.file)                                                                                            
  File "/usr/lib/python3/dist-packages/PIL/ImageOps.py", line 528, in invert                                        
    return image.point(lut) if image.mode == "1" else _lut(image, lut)                                              
  File "/usr/lib/python3/dist-packages/PIL/ImageOps.py", line 58, in _lut                                           
    raise OSError("not supported for this image mode")                                                              
OSError: not supported for this image mode                                                                          
"""                                                                                                                 
ERROR:stegoveritas.helpers:not supported for this image mode
ERROR:stegoveritas.helpers:
"""                                                                                                                 
Traceback (most recent call last):                                                                                  
  File "/usr/lib/python3.10/multiprocessing/pool.py", line 125, in worker                                           
    result = (True, func(*args, **kwds))                                                                            
  File "/home/kali/.local/lib/python3.10/site-packages/stegoveritas/modules/image/analysis/filters.py", line 33, in run_image_op                                                                                                        
    img = op(image.file)                                                                                            
  File "/usr/lib/python3/dist-packages/PIL/ImageOps.py", line 570, in solarize                                      
    return _lut(image, lut)                                                                                         
  File "/usr/lib/python3/dist-packages/PIL/ImageOps.py", line 58, in _lut                                           
    raise OSError("not supported for this image mode")                                                              
OSError: not supported for this image mode                                                                          
"""                                                                                                                 
Running Module: MultiHandler

Exif
====
+---------------------------+----------------------------------------------------------------------------+
| key                       | value                                                                      |
+---------------------------+----------------------------------------------------------------------------+
| SourceFile                | /home/kali/Downloads/blank.png                                             |
| ExifToolVersion           | 12.44                                                                      |
| FileName                  | blank.png                                                                  |
| Directory                 | /home/kali/Downloads                                                       |
| FileSize                  | 3.6 kB                                                                     |
| FileModifyDate            | 2023:04:01 22:53:02-04:00                                                  |
| FileAccessDate            | 2023:04:01 22:53:13-04:00                                                  |
| FileInodeChangeDate       | 2023:04:01 22:53:05-04:00                                                  |
| FilePermissions           | -rw-r--r--                                                                 |
| FileType                  | PNG                                                                        |
| FileTypeExtension         | png                                                                        |
| MIMEType                  | image/png                                                                  |
| ImageWidth                | 600                                                                        |
| ImageHeight               | 600                                                                        |
| BitDepth                  | 8                                                                          |
| ColorType                 | RGB with Alpha                                                             |
| Compression               | Deflate/Inflate                                                            |
| Filter                    | Adaptive                                                                   |
| Interlace                 | Noninterlaced                                                              |
| ProfileName               | ICC profile                                                                |
| ProfileCMMType            | Little CMS                                                                 |
| ProfileVersion            | 4.3.0                                                                      |
| ProfileClass              | Display Device Profile                                                     |
| ColorSpaceData            | RGB                                                                        |
| ProfileConnectionSpace    | XYZ                                                                        |
| ProfileDateTime           | 2023:03:22 13:04:33                                                        |
| ProfileFileSignature      | acsp                                                                       |
| PrimaryPlatform           | Apple Computer Inc.                                                        |
| CMMFlags                  | Not Embedded, Independent                                                  |
| DeviceManufacturer        |                                                                            |
| DeviceModel               |                                                                            |
| DeviceAttributes          | Reflective, Glossy, Positive, Color                                        |
| RenderingIntent           | Perceptual                                                                 |
| ConnectionSpaceIlluminant | 0.9642 1 0.82491                                                           |
| ProfileCreator            | Little CMS                                                                 |
| ProfileID                 | 0                                                                          |
| ProfileDescription        | GIMP built-in sRGB                                                         |
| ProfileCopyright          | Public Domain                                                              |
| MediaWhitePoint           | 0.9642 1 0.82491                                                           |
| ChromaticAdaptation       | 1.04788 0.02292 -0.05022 0.02959 0.99048 -0.01707 -0.00925 0.01508 0.75168 |
| RedMatrixColumn           | 0.43604 0.22249 0.01392                                                    |
| BlueMatrixColumn          | 0.14305 0.06061 0.71393                                                    |
| GreenMatrixColumn         | 0.38512 0.7169 0.09706                                                     |
| RedTRC                    | base64:cGFyYQAAAAAAAwAAAAJmZgAA8qcAAA1ZAAAT0AAACls=                        |
| GreenTRC                  | base64:cGFyYQAAAAAAAwAAAAJmZgAA8qcAAA1ZAAAT0AAACls=                        |
| BlueTRC                   | base64:cGFyYQAAAAAAAwAAAAJmZgAA8qcAAA1ZAAAT0AAACls=                        |
| ChromaticityChannels      | 3                                                                          |
| ChromaticityColorant      | Unknown (0)                                                                |
| ChromaticityChannel1      | 0.64 0.33002                                                               |
| ChromaticityChannel2      | 0.3 0.60001                                                                |
| ChromaticityChannel3      | 0.15001 0.06                                                               |
| DeviceMfgDesc             | GIMP                                                                       |
| DeviceModelDesc           | sRGB                                                                       |
| BackgroundColor           | 255 255 255                                                                |
| PixelsPerUnitX            | 11811                                                                      |
| PixelsPerUnitY            | 11811                                                                      |
| PixelUnits                | meters                                                                     |
| ModifyDate                | 2023:03:22 13:06:17                                                        |
| Comment                   | Created with GIMP                                                          |
| ImageSize                 | 600x600                                                                    |
| Megapixels                | 0.36                                                                       |
+---------------------------+----------------------------------------------------------------------------+
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
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
WARNING:StegoVeritas:Modules:Multi:Analysis:Exif:Exif outpat already exists, modifying.
Found something worth keeping!
PNG image data, 600 x 600, 8-bit/color RGBA, non-interlaced
+--------+------------------+----------------------------------------+-----------+
| Offset | Carved/Extracted | Description                            | File Name |
+--------+------------------+----------------------------------------+-----------+
| 0x218  | Carved           | Zlib compressed data, best compression | 218.zlib  |
| 0x218  | Extracted        | Zlib compressed data, best compression | 218       |
+--------+------------------+----------------------------------------+-----------+

```

I navigated to the `results` directory which contained several images of different contrast extracted. One of the image: `blank.png_Blue_0.png` contained the flag.&#x20;

By viewing the image, I was presented with the flag.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Flag: RS{Th4t5\_w4cky\_m4n}

## Cats At Play

<figure><img src="../.gitbook/assets/image (2) (13).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was under the `reversing` category.

First, we could run the `file` command to check the file type. Next, we could try to `grep` the flag format. Note that we need to specify the `-a` option to process the binary file as if it were text.

Also note that this would only work for simple `reverse` challenges like this.

As we can see, the flag can be seen somewhere in the middle of the chunk of text.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ file meow.exe 
meow.exe: PE32 executable (console) Intel 80386, for MS Windows
                                                                                                                    
┌──(kali㉿kali)-[~/Downloads]
└─$ grep RS{ meow.exe             
grep: meow.exe: binary file matches

┌──(kali㉿kali)-[~/Downloads]
└─$ grep -a RS{ meow.exe
�▒�(�4�H�X�j�t�������������(�:�N�d�v������������UnhandledExceptionFilterqSetUnhandledExceptionFilter▒GetCurrentProcess�TerminateProcess�IsProcessorFeaturePresentOQueryPerformanceCounteretCurrentProcessIdGetCurrentThreadId�GetSystemTimeAsFileTimefInitializeSListHead�IsDebuggerPresent�GetStartupInfoW{GetModuleHandleWKERNEL32.dll�RtlUnwinddGetLastError4SetLastError4EnterCriticalSection�LeaveCriticalSectionDeleteCriticalSectionbInitializeCriticalSectionAndSpinCount�TlsAlloc�TlsGetValue�TlsSetValue�TlsFree�FreeLibrary�GetProcAddress�LoadLibraryExWdRaiseException�GetStdHandleWriteFilewGetModuleFileNameWaExitProcesszGetModuleHandleExW�GetCommandLineA�GetCommandLineWHHeapAllocLHeapFree�CompareStringW�LCMapStringWQGetFileTypexFindClose~FindFirstFileExW�FindNextFileW�IsValidCodePage�GetACP�GetOEMCP�GetCPInfo�MultiByteToWideCharWideCharToMultiByte:GetEnvironmentStringsW�FreeEnvironmentStringsWSetEnvironmentVariableWNSetStdHandle�GetStringTypeW�GetProcessHeap�FlushFileBuffersGetConsoleOutputCP�GetConsoleModeOGetFileSizeEx%SetFilePointerExQHeapSizeOHeapReAlloc�CloseHandle�CreateFileWWriteConsoleW
                                                        DecodePointer⠀⠀⠀⠀⠀⠀⠀⠙⣿⣷⣄⠀⠀⠀⠀⠀⠀⠀⠀⠀⢺⣿⣿⡆⠀⠀⠀⠀⠀⠀⠀⠀⠀⢸⣿⣿⡇⠀⠀⠀⠀⠀⠀⣾⢡⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢢⡀⠀⠀RS{C4tsL1keStr1ng5}⠀⠀⠀⠀⠀⠀⠀⠀⠈⣿⣿⣷⡦⠀⠀⠀⠀⢰⣿⣿⣷⠀⠀⠀⠀⠀⠀⠀⠀⠃⣠⣾⡇⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢻⣿⣿⣿⣆⠀⠀⠀⣾⣿⣿⣿⣷⠄⠀⠰⠤⣀⠀⠀⣴⣿⣿⡇°. •* .°•⁎⁺˳✧༚☆*⠀⠀⠀⠀⠀⠀⠀⠀⠃⢺⣿⣿⣿⣿⡄⠀⠀⣿⣿⢿⣿⣿⣦⣦⣦⣶⣼⣭⣼⣿⣿⣿⠇  ∧,,,∧⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⢿⣿⣿⣿⣷⡆⠂⣿⣿⣞⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡄⠀⠀(  • · • )⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⢙⣿⣿⣿⣿⣷⠸⣿⣿⣿⣿⣿⣿⠟⠻⣿⣿⣿⣿⡿⣿⣿⣷⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠄⢿⣿⣿⣿⣿⡄⣿⣿⣿⣿⣿⣿⡀⢀⣿⣿⣿⣿⠀⢸⣿⣿⠅⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠸⣿⣿⣿⣿⣇⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠠⢐⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡿⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣀⣤⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠟⠁/    > >☆ meow!⠀⠀⠀⠀⠀⠀⠀⢀⣴⣾⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠀⠀⠀⠀⠀⡀⣠⣾⣾⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡔       /\___/\

```

Another similar challenge where I used `grep -a` can be found [here](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/lagncrash-interpoly-ctf-2022#plumber).

Flag: RS{C4tsL1keStr1ng5}

