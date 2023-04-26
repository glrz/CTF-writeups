---
description: DSTA Brainhack Challenge 2023 - Cyber was available from 10 Apr to 17 Apr.
---

# DSTA Brainhack Challenge 2023 - Cyber

I chanced upon this challenge on 10 Apr and solved it on the day itself. Honestly, I'm not too sure why they categorized this as `hard` difficulty. Overall, it was a pretty easy challenge and beginner-friendly challenge to solve.

The challenge concept was mainly about buffer overflow and vulnerable functions in `C` program.

This challenge idea would be quite common in the basic `PWN/binary exploitation` category. However, this challenge does not require us to PWN or perform binary exploitation. It is more about understanding the concept of it and selecting the correct answer in the MCQ.&#x20;

<figure><img src="../.gitbook/assets/image (1) (6) (2).png" alt=""><figcaption></figcaption></figure>

Notice that for the previous 3 choices, A and B will not grant us access to the BrainHack's website. This was a typo on DSTA side and they have corrected it later. The corrected version showed all choices in lower case.

<figure><img src="../.gitbook/assets/image (99).png" alt=""><figcaption></figcaption></figure>

In this case, the correct answer is only A.&#x20;

Option B will grant us access due to `strcmp`  function which fulfilled the if statements

Option C will cause [buffer overflow](https://owasp.org/www-community/vulnerabilities/Buffer\_Overflow) as it has 16 characters. Char password\[15] can only take in 15 characters. Anything more than that causes buffer overflow, which also cause it to execute and launch BrainHack's website.

In the code given, it was using vulnerable C functions  such as `gets` and `strcmp`. These vulnerable functions can lead to buffer overflow. Hackers exploit buffer overflows to infiltrate networks and take control of systems.

More information about vulnerable C functions can be found [here](https://infosecwriteups.com/common-c-vulnerabilities-b84777e071b9).

For beginners who are not familiar with this concept or C functions, you could also try out typing the code manually and compiling it.

Here I have included the code for you to try:

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main(void)
{
char password[15];
int pass = 0;
printf("\n Enter the password: \n");
gets(password);
if (strcmp(password, "brainhack2023") == 0)
{
printf("\n Correct password! \n");
pass = 1;
}
if (pass)
{
printf("\n Connecting to Brainhack 2023 website  ... \n");
system("start https://www.dsta.gov.sg/brainhack");
}
return 0;
}
```

To compile it, we can issue the following command in terminal. In this case, I'll be using Command Prompt.

> gcc -o brainhack \<your .c file with the code>

To run the compiled application, we can just type the filename

> brainhack

On command prompt, it should look like this

```
C:\Users\Gadiel\Desktop\Extracurricular\DSTA\Cyber Quiz - buff overflow concept>gcc -o brainhack brainhack.c

C:\Users\Gadiel\Desktop\Extracurricular\DSTA\Cyber Quiz - buff overflow concept>brainhack

 Enter the password:m
```

After testing out the application, option B and C will grant access to BrainHack's website, while option A will not.

<figure><img src="../.gitbook/assets/image (28) (3).png" alt=""><figcaption></figcaption></figure>

Answer: A
