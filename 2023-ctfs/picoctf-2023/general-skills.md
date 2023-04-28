# General Skills

## Rules 2023

<figure><img src="../../.gitbook/assets/image (3) (8).png" alt=""><figcaption></figcaption></figure>

For this challenge, we could navigate to the rules page.

However, if we tried to search for the flag using `CTRL+F` shortcut, we will not be able to find the flag since it was uploaded as an image.

I had to scroll down somewhere near the bottom to see the flag.

<figure><img src="../../.gitbook/assets/image (4) (3).png" alt=""><figcaption></figcaption></figure>

Alternatively, an easier way could be to view the source code and search for the flag.

<figure><img src="../../.gitbook/assets/image (5) (6).png" alt=""><figcaption></figcaption></figure>

Flag: picoCTF{h34rd\_und3r5700d\_4ck\_cba1c711}

## money-ware



<figure><img src="../../.gitbook/assets/image (2) (11).png" alt=""><figcaption></figcaption></figure>

For this challenge, we could simply `Google` the transaction address and we would come across this [link](https://qz.com/1016525/the-petya-ransomware-cyberattack-has-earned-hackers-20k-less-than-wannacry-in-its-first-24-hours) which tells us the malware name.

Flag: picoCTF{Petya}

## repetitions

<figure><img src="../../.gitbook/assets/image (9) (3).png" alt=""><figcaption></figcaption></figure>

For this challenge, we can download the `enc_flag` file.

We can run the `file` command to check the file type.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ file enc_flag        
enc_flag: ASCII text
```

We can then read the ASCII text which looked like `Base64` encoded.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cat enc_flag         
VmpGU1EyRXlUWGxTYmxKVVYwZFNWbGxyV21GV1JteDBUbFpPYWxKdFVsaFpWVlUxWVZaS1ZWWnVh
RmRXZWtab1dWWmtSMk5yTlZWWApiVVpUVm10d1VWZFdVa2RpYlZaWFZtNVdVZ3BpU0VKeldWUkNk
MlZXVlhoWGJYQk9VbFJXU0ZkcVRuTldaM0JZVWpGS2VWWkdaSGRXCk1sWnpWV3hhVm1KRk5XOVVW
VkpEVGxaYVdFMVhSbGhhTTBKeldXeGtiMlZXV2tWU2JFNVdDazFyV25sVVZsWnZWbTFHZEdWRlZs
aGkKYlRrelZERldUMkpzUWxWTlJYTkxDZz09Cg==
```

We can copy paste this into [CyberChef](https://cyberchef.org/#recipe=From\_Base64\('A-Za-z0-9%2B/%3D',true,false\)From\_Base64\('A-Za-z0-9%2B/%3D',true,false\)From\_Base64\('A-Za-z0-9%2B/%3D',true,false\)From\_Base64\('A-Za-z0-9%2B/%3D',true,false\)From\_Base64\('A-Za-z0-9%2B/%3D',true,false\)From\_Base64\('A-Za-z0-9%2B/%3D',true,false\)) and `Base64` decode it six times, which gives us the flag. The need to decode multiple times can probably be inferred from the challenge name `repetitions`.

<figure><img src="../../.gitbook/assets/image (5) (6) (1).png" alt=""><figcaption></figcaption></figure>

Flag: picoCTF{base64\_n3st3d\_dic0d!n8\_d0wnl04d3d\_c8d94c0d}

## chrono

<figure><img src="../../.gitbook/assets/image (6) (5).png" alt=""><figcaption></figcaption></figure>

For this challenge, we can `ssh` as `picoplayer` into the server using  the given `port number`.

```bash
┌──(kali㉿kali)-[~/Desktop]
└─$ ssh picoplayer@saturn.picoctf.net -p 54984
picoplayer@saturn.picoctf.net's password: 
Welcome to Ubuntu 20.04.5 LTS (GNU/Linux 5.15.0-1031-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.
```

If we search online, a cronjob can be also run from /etc/crontab file. To view it, we can simply use `cat` command which gives us the flag.

```
picoplayer@challenge:~$ cat /etc/crontab 
# picoCTF{Sch3DUL7NG_T45K3_L1NUX_1d781160}
```

Flag: picoCTF{Sch3DUL7NG\_T45K3\_L1NUX\_1d781160}

## Permissions

<figure><img src="../../.gitbook/assets/image (8) (4).png" alt=""><figcaption></figcaption></figure>

Similar to the previous challenge, we can `ssh` into the server as such

```bash
┌──(kali㉿kali)-[~]
└─$ ssh -p 55213 picoplayer@saturn.picoctf.net
The authenticity of host '[saturn.picoctf.net]:55213 ([13.59.203.175]:55213)' can't be established.
ED25519 key fingerprint is SHA256:Km7la74G7/fztU37KiXuMDlWhxowKKAxA3TjvWy1Y0o.
This host key is known by the following other names/addresses:
    ~/.ssh/known_hosts:7: [hashed name]
    ~/.ssh/known_hosts:12: [hashed name]
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[saturn.picoctf.net]:55213' (ED25519) to the list of known hosts.
picoplayer@saturn.picoctf.net's password: 
Welcome to Ubuntu 20.04.5 LTS (GNU/Linux 5.15.0-1031-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.
```

If we go to the `root` directory, we will see an interesting directory name: `challenge` which probably should not be there by default.&#x20;

```bash
picoplayer@challenge:~$ cd /
picoplayer@challenge:/$ ls
bin   challenge  etc   lib    lib64   media  opt   root  sbin  sys  usr
boot  dev        home  lib32  libx32  mnt    proc  run   srv   tmp  var
```

To read about the basic of Linux file systems, click [here](https://opensource.com/life/16/10/introduction-linux-filesystems).

If we go into the `challenge` directory, we will see a `.json` file and reading the contents of it gives us the flag.

```bash
picoplayer@challenge:/$ cd challenge/
picoplayer@challenge:/challenge$ ls
metadata.json
picoplayer@challenge:/challenge$ cat metadata.json 
{"flag": "picoCTF{uS1ng_v1m_3dit0r_3dd6dcf4}", "username": "picoplayer", "password": "GhHrPQ2+zL"}picoplayer@challenge:/challenge$       
```

I think there was some issue with the challenge, where it should not allow us to read the flag directly. It should only allow users to view the flag through vim editor as seen in the flag we obtained in leetspeak.

Flag: picoCTF{uS1ng\_v1m\_3dit0r\_3dd6dcf4}

## useless

<figure><img src="../../.gitbook/assets/image (7) (2).png" alt=""><figcaption></figcaption></figure>

Similar to previous challenges, I had to `ssh` into the server

```bash
┌──(kali㉿kali)-[~]
└─$ ssh -p 52588 picoplayer@saturn.picoctf.net
The authenticity of host '[saturn.picoctf.net]:52588 ([13.59.203.175]:52588)' can't be established.
ED25519 key fingerprint is SHA256:ves7M6DhshpiJSsScBWo3n34oOFTUXvLZqPyqLWeTHk.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[saturn.picoctf.net]:52588' (ED25519) to the list of known hosts.
picoplayer@saturn.picoctf.net's password: 
Welcome to Ubuntu 20.04.6 LTS (GNU/Linux 5.15.0-1031-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.
```

If we list the files, we can see a `useless` file. We can read the contents of this file which contained some bash code.

```bash
picoplayer@challenge:~$ ls 
useless
picoplayer@challenge:~$ cat useless 
#!/bin/bash
# Basic mathematical operations via command-line arguments

if [ $# != 3 ]
then
  echo "Read the code first"
else
 if [[ "$1" == "add" ]]
 then 
   sum=$(( $2 + $3 ))
   echo "The Sum is: $sum"  

 elif [[ "$1" == "sub" ]]
 then 
   sub=$(( $2 - $3 ))
   echo "The Substract is: $sub" 

 elif [[ "$1" == "div" ]]
 then 
   div=$(( $2 / $3 ))
   echo "The quotient is: $div" 

 elif [[ "$1" == "mul" ]]
 then
   mul=$(( $2 * $3 ))
   echo "The product is: $mul" 

 else
   echo "Read the manual"
  
 fi
fi
```

If we pay close attention to the last part, it says `read the manual`.

To read the manual in Linux, we can use the `man` command followed by the name of the command, function, or file that we want to read the manual for.

This would give us the flag at the bottom.

```bash
picoplayer@challenge:~$ man useless

useless
     useless, — This is a simple calculator script

SYNOPSIS
     useless, [add sub mul div] number1 number2

DESCRIPTION
     Use the useless, macro to make simple calulations like addition,subtraction, multiplication and division.

Examples
     ./useless add 1 2
       This will add 1 and 2 and return 3

     ./useless mul 2 3
       This will return 6 as a product of 2 and 3

     ./useless div 6 3
       This will return 2 as a quotient of 6 and 3

     ./useless sub 6 5
       This will return 1 as a remainder of substraction of 5 from 6

Authors
     This script was designed and developed by Cylab Africa

     picoCTF{us3l3ss_ch4ll3ng3_3xpl0it3d_1155}
```

Flag: picoCTF{us3l3ss\_ch4ll3ng3\_3xpl0it3d\_1155}

## Special

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

I solved this challenge shortly after the competition when I had some free time to attempt it.

For this challenge, we could first ssh into the `special` shell using the credentials given.

In this shell, most of the linux commands have been changed to random English words.

We could try using `;` to perform command injection. However, it seemed like we could only use `ls` after the semicolon to list the directories present.

```bash
Special$ whoami;
Whoami; 
sh: 1: Whoami: not found
Special$ whoami;ls
Whoami;ls 
sh: 1: Whoami: not found
blargh
Special$ whoami;cd blargh
Whoami;cd large 
sh: 1: Whoami: not found
sh: 1: cd: can't cd to large
Special$ whoami; grep pico
Whoami; grew pico 
sh: 1: Whoami: not found
sh: 1: grew: not found
Special$ whoami;ls;cd blargh
Whoami;ls;cd large 
sh: 1: Whoami: not found
blargh
sh: 1: cd: can't cd to large
```

From here, we could use the `python3` command after the semicolon to open the python IDLE. We can then import the `os` module and execute the commands to read the flag.

```bash
Special$ ls;python3
Ls;python3 
sh: 1: Ls: not found
Python 3.8.10 (default, Nov 14 2022, 12:59:47) 
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import os
>>> os.system('ls')
blargh
0
>>> os.system('cd blargh')
0
>>> os.system('ls')
blargh
0
>>> os.chdir('blargh')
>>> os.system('ls')
flag.txt
0
>>> os.system('cat flag.txt')
picoCTF{5p311ch3ck_15_7h3_w0r57_3befb794}0
>>> 
```

An alternative easier solution is to `grep` recursively on the directory for the flag format `pico` in Python IDLE

```bash
Special$ ls;python3
Ls;python3 
sh: 1: Ls: not found
Python 3.8.10 (default, Nov 14 2022, 12:59:47) 
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import os
>>> os.system('grep -r pico')
blargh/flag.txt:picoCTF{5p311ch3ck_15_7h3_w0r57_3befb794}
0h
```

I discovered there were other solutions to solve this challenge as well, without the use of Python IDLE. For example, we could use certain commands when issued within quotation marks.

Hence, we could `grep` recursively like this as well

```bash
Special$ 'grep' '-r' pico
'grep' '-r' pico 
blargh/flag.txt:picoCTF{5p311ch3ck_15_7h3_w0r57_3befb794}
```

Flag: picoCTF{5p311ch3ck\_15\_7h3\_w0r57\_3befb794}

## Specialer

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

This challenge was similar to the previous challenge - `Special` and I solved it after the competition as well.

First, we could ssh into the server with the credentials given once we `launch instance`.

Next, we will try some commands and play around with the syntax like what we did previously.

We could try running `compgen -c` to see what commands we could use

```bash
Specialer$ compgen -c
if
then
else
elif
fi
case
esac
for
select
while
until
do
done
in
function
time
{
}
!
[[
]]
coproc
.
:
[
alias
bg
bind
break
builtin
caller
cd
command
compgen
complete
compopt
continue
declare
dirs
disown
echo
enable
eval
exec
exit
export
false
fc
fg
getopts
hash
help
history
jobs
kill
let
local
logout
mapfile
popd
printf
pushd
pwd
read
readarray
readonly
return
set
shift
shopt
source
suspend
test
times
trap
true
type
typeset
ulimit
umask
unalias
unset
wait
bash
```

This would list out the various commands available to use in the shell. However, if we would like a better view sorted in alphabetical order, we could press the tab key twice.

```bash
Specialer$ 
!          bind       compopt    elif       fc         if         printf     shift      true       while
./         break      continue   else       fg         in         pushd      shopt      type       {
:          builtin    coproc     enable     fi         jobs       pwd        source     typeset    }
[          caller     declare    esac       for        kill       read       suspend    ulimit     
[[         case       dirs       eval       function   let        readarray  test       umask      
]]         cd         disown     exec       getopts    local      readonly   then       unalias    
alias      command    do         exit       hash       logout     return     time       unset      
bash       compgen    done       export     help       mapfile    select     times      until      
bg         complete   echo       false      history    popd       set        trap       wait  
```

We can see that we can use commands such as `cd` and `echo` which could be useful to help us solve this challenge.

I used the `cd` command and pressed the tab key twice which showed the available directories that I could change directory to

```bash
Specialer$ cd 
.hushlogin  .profile    abra/       ala/        sim/  
```

If we take a look again at the commands avaialbe to use, we would see that we cannot use `cat` or other common file-viewing commands to view the contents of a file. Furthermore, we cannot use `grep` to search for the flag. However, we could still use `echo`.

In this case, we could view the file contents using the syntax: `echo "$(<filename)"`

```bash
Specialer$ echo "$(<.hushlogin)"

Specialer$ echo "$(<.profile)"
export PS1='Specialer$ '
```

These does not contain the flag, so we shall proceed to look into the other directories.

In `abra`, there were 2 txt files.

```bash
Specialer$ cd abra
Specialer$ cd cada
cadabra.txt   cadaniel.txt  
```

We could read the contents using the `echo` command. However, no flags are found here.

```bash
Specialer$ echo "$(<cadabra.txt)"
Nothing up my sleeve!
Specialer$ echo "$(<cadaniel.txt)"
Yes, I did it! I really did it! I'm a true wizard!
```

We move on to the next directory `ala/` where we will find the flag.

```bash
Specialer$ cd ..
Specialer$ cd abra/
Specialer$ cd ..
Specialer$ cd ala/
Specialer$ cd 
kazam.txt  mode.txt   
Specialer$ echo "$(<kazam.txt)"
return 0 picoCTF{y0u_d0n7_4ppr3c1473_wh47_w3r3_d01ng_h3r3_a8567b6f}
Specialer$ 
```

Flag: picoCTF{y0u\_d0n7\_4ppr3c1473\_wh47\_w3r3\_d01ng\_h3r3\_a8567b6f}
