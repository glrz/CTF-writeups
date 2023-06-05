# Fundamentals of Linux

## #1 Intermediate terminal practice

<figure><img src="../../../.gitbook/assets/image (30) (4).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a piece of `C` code.

```bash
int main(void)
{
    setup();

    unsigned char buf[0x100] = {0, };
    int len = 0;

    puts("# Linux Basic 1 #");
    puts("Find flag where it is!");
    printf("\n");

    int count = 0;
    while(count < 4)
    {
        memset(buf, 0, LEN);
        printf("$ ");
        len = read(STDIN, buf, LEN - 1);

        if(!checkPrintable(buf, len))
        {
            printf("Non-printable character in command.\n");
            continue;
        }

        if(checkBlacklist(buf))
        {
            printf("Some strings in blacklist.\n");
            continue;
        }

        printf("Wait 3 seconds ...\n");
        sleep(3);
        system(buf);

        count++;
    }
}
```

Many commands have been blacklisted, including `ls`, `cd` etc.

I came across this [documentation guide](https://www.linode.com/docs/guides/find-files-in-linux-using-the-command-line/) which used the `find` command to search for files and directories.

We can use `find` command. However, there were thousands of directories and only one contained the flag file (I won’t paste all the output here due to the large size).

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ nc 52.78.16.36 3284
# Linux Basic 1 #
Find flag where it is!

$ find
Wait 3 seconds ...
.
./directory
./directory/209
./directory/209/flag
./directory/1094
./directory/1094/flag
./directory/1168
./directory/1168/flag
./directory/280
./directory/280/flag
./directory/1184
./directory/1184/flag
./directory/1140
./directory/1140/flag
./directory/835
./directory/835/flag
./directory/1043
./directory/1043/flag
./directory/607
./directory/607/flag
./directory/688
./directory/688/flag
./directory/998
./directory/998/flag
./directory/337
./directory/337/flag
./directory/628
./directory/628/flag
./directory/19
./directory/19/flag
./directory/170
./directory/170/flag
./directory/575
./directory/575/flag
./directory/868
./directory/868/flag

```

We can find a directory that is not empty. `directory/257` has the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ nc 52.78.16.36 3284

# Linux Basic 1 #
Find flag where it is!

$ find directory -type f -not -empty
Wait 3 seconds ...
directory/257/flag
$            
```

Finally, we can read the contents of flag file.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ nc 52.78.16.36 3284

# Linux Basic 1 #
Find flag where it is!

$ less directory/257/flag
Wait 3 seconds ...
sh: 1: less: not found
$ cat directory/257/flag
Wait 3 seconds ...
bd6ed675ab5e64c9e5130772969eff83
```

Flag: bd6ed675ab5e64c9e5130772969eff83

## #2 Intermediate terminal practice

<figure><img src="../../../.gitbook/assets/image (65) (3).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given two files, a png file and a txt file.

Opening up the txt file, we see this

<figure><img src="../../../.gitbook/assets/image (77) (2).png" alt=""><figcaption></figcaption></figure>

For the png file, we will see this

<figure><img src="../../../.gitbook/assets/image (29) (3).png" alt=""><figcaption></figcaption></figure>

However, I did not find the two pieces of  information above to be too useful. Instead, my approach to solve this challenge was similar to the previous challenge.

I used the `find` command to search for the files and directories within. I then used the `tac` command which allowed me to read the contents of the flag.

You could find out more about `tac` command [here](https://www.liquidweb.com/kb/how-to-display-contents-of-a-file-linux/) and read about the other commands to display contents in a file.

> Another exciting way to display the contents of a file in Linux is in reverse order. To do so, use the _tac_ command. It is similar to _cat_ but reversed, reading and displaying the file starting from the last line.

```bash
┌──(kali㉿kali)-[~]
└─$ nc 52.78.16.36 3285                 
# Linux Basic 2 #
Read flag if you want ...

$ find
.
./414g_1s_flag
./basic2
./run.sh
$ tac 414g_1s_flag
1cae3c98d4f321517c45a971740484a7
```

Flag: 1cae3c98d4f321517c45a971740484a7

## Basic Quiz

<figure><img src="../../../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

For this challenge, I did not really understand the first question at first. It used `composed by` which made me think that it was asking for the person who created Linux.

However, after watching the lecture video, I understood that it could be a typo and what it meant was `composed of`

Also, I'm not sure why it was accepting `file` but not `files` for the first question. Besides this challenge, there were also a few other challenges which had typos and made some of the challenges quite guessy in nature.

Simply convert the answers into the correct format to get the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ echo -n file_daemon_cat_kernel_7 | md5sum 
da6097d5f4ff7b3c8133a370e37985d2  
```

Flag: da6097d5f4ff7b3c8133a370e37985d2
