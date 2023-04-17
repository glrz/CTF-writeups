# Reverse

## Baby Shark

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.pcapng` file.

I simply `grep` for the fiag and specified the `-a` option to treat it as a binary file.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ grep -a LNC babyshark.pcapng
���`$�=P▒�X^PASS LNC2022{nice}
��ao����e�P▒�XlPASS LNC2023{doodoodoodoodoodoo}
```

Flag: LNC2023{doodoodoodoodoodoo}

## The abandoned computer

<figure><img src="../../.gitbook/assets/image (1) (8).png" alt=""><figcaption></figcaption></figure>

For this challenge, I discussed with my teammate and I solved it after.

We were given a  `.exe` file.

First, I ran `strings` on this file to do some static analysis.

Note: I will not be pasting all the data here because the data is too large.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ strings computer.exe 
!This program cannot be run in DOS mode.
.text
`.data
.rdata
@.buildid5
@.pdata
@.xdata
@.bss
.idata
.rsrc
.reloc
B/19
B/31
B/45
B/57
B/70
B/81
B/97
userH
admif
twwU
D$,H
AUATH
(A\A]
Z40nj$q9Ul
Enter your username: 
Enter your password: 
user10218012437
Welcome, %s!
Role: %s
admin
Access granted.
INPUT any key to continue
56 47 38 67 64 32 68 76 5a 58 5a 6c 63 69 42 70 63 79 42 79 5a 57 46 6b 61 57 35 6e 49 48 52 6f 61 58 4d 73 49 45 6b 67 61 47 39 77 5a 53 42 30 61 47 6c 7a 49 47 31 6c 63 33 4e 68 5a 32 55 67 5a 6d 6c 75 5a 48 4d 67 65 57 39 31 49 48 64 6c 62 47 77 75 49 45 31 35 49 47 35 68 62 57 55 67 61 58 4d 67 65 79 6f 6d 58 69 55 6c 49 47 46 75 5a 43 42 4a 49 47 46 74 49 48 64 79 61 58 52 70 62 6d 63 67 64 47 68 70 63 79 42 70 62 69 42 30 61 47 55 67 65 57 56 68 63 69 41 79 4d 44 4d 31 4c 69 42 55 61 47 55 67 64 32 46 79 49 47 6c 7a 49 47 35 76 64 43 42 6e 5a 58 52 30 61 57 35 6e 49 47 46 75 65 53 42 69 5a 58 52 30 5a 58 49 67 59 57 35 6b 49 48 73 67 5a 47 39 75 4a 33 51 67 64 47 68 70 62 6d 73 67 64 47 68 68 64 43 42 70 64 43 64 7a 49 47 56 75 5a 47 6c 75 5a 79 42 68 62 6e 6c 30 61 57 31 6c 49 48 4e 76 62 32 34 75 49 45 4a 35 49 48 52 6f 5a 53 42 30 61 57 31 6c 49 47 6c 30 49 47 52 76 5a 58 4d 73 49 48 52 6f 5a 58 4a 6c 4a 33 4d 67 63 48 4a 76 59 6d 46 69 62 48 6b 67 62 6d 39 30 61 47 6c 75 5a 79 42 74 62 33 4a 6c 49 48 52 76 49 47 74 70 62 47 77 67 62 32 5a 6d 4c 69 42 4a 49 47 46 74 49 48 64 79 61 58 52 70 62 6d 63 67 64 47 68 70 63 79 42 74 5a 58 4e 7a 59 57 64 6c 49 48 64 70 64 47 67 67 64 47 68 6c 49 47 68 76 63 47 55 67 64 47 68 68 64 43 42 68 49 48 4e 31 63 6e 5a 70 64 6d 39 79 49 48 64 70 62 47 77 67 59 6e 4a 70 62 6d 63 67 59 6d 46 6a 61 79 42 33 61 47 46 30 49 48 64 68 63 79 42 73 62 33 4e 30 4c 69 42 37 62 79 42 33 61 47 39 74 49 48 52 6f 61 58 4d 67 62 57 46 35 49 47 4e 76 62 6d 4e 6c 63 6d 34 73 49 48 64 6f 59 58 51 67 65 57 39 31 49 48 4e 6c 5a 57 73 67 62 47 6c 6c 63 79 42 69 5a 58 6c 76 62 6d 51 67 64 47 68 70 63 79 42 30 62 33 64 75 4c 69 42 55 61 47 56 79 5a 53 42 6f 59 58 5a 6c 49 47 4a 6c 5a 57 34 67 63 6e 56 74 62 33 56 79 63 79 42 76 5a 69 42 68 49 48 42 73 59 57 4e 6c 49 48 64 6f 5a 58 4a 6c 49 47 68 31 62 57 46 75 61 58 52 35 49 47 4e 68 62 69 42 7a 5a 57 56 72 49 48 4a 6c 5a 6e 56 6e 5a 53 42 68 62 6d 51 67 63 6d 56 69 64 57 6c 73 5a 43 42 76 64 58 49 67 62 47 39 7a 64 43 42 6a 61 58 5a 70 62 47 6c 7a 59 58 52 70 62 32 34 75 49 45 35 76 49 47 39 75 5a 53 42 72 62 6d 39 33 63 79 42 6c 65 47 46 6a 64 47 78 35 49 48 64 6f 5a 58 4a 6c 4c 43 42 69 64 58 51 67 61 57 59 67 65 57 39 31 49 47 52 76 49 47 5a 70 62 6d 51 67 61 58 51 73 49 48 52 6f 61 58 4d 67 62 57 6c 6e 61 48 51 67 61 47 56 73 63 43 42 35 62 33 55 67 5a 57 35 30 5a 58 49 36 49 45 78 4f 51 7a 49 77 4d 6a 4e 37 63 6a 4d 31 64 56 4a 53 5a 57 4e 30 4d 54 42 75 66 51 3d 3d
user
ENTER to continue
This file explorer is empty...
Access denied.
GCC: (GNU) 11.3.0
GCC: (GNU) 11.3.0
GCC: (GNU) 11.3.0
GCC: (GNU) 11.3.0
GCC: (GNU) 11.3.0
GCC: (GNU) 11.3.0
GCC: (GNU) 11.3.0
GCC: (GNU) 11.3.0
GCC: (GNU) 11.3.0
GCC: (GNU) 11.3.0
GCC: (GNU) 11.3.0
GCC: (GNU) 11.3.0
GCC: (GNU) 11.3.0
GCC: (GNU) 11.3.0
GCC: (GNU) 11.3.0
RSDS
__cxa_atexit
__main
_dll_crt0
_impure_ptr
calloc
cygwin_detach_dll
cygwin_internal
dll_dllcrt0
free
malloc
posix_memalign
printf
puts
realloc
scanf
strcmp
GetModuleHandleA
cygwin1.dll
KERNEL32.dll
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">
```

From the above strings, we could see some interesting hexadecimal.

We could change it from hex to ascii and we would get `Base64` encoded string. Finally, we could decode the `Base64` encoded message. All these can be done in CyberChef to obtain the flag.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Flag: LNC2023{r35uRRect10n}
