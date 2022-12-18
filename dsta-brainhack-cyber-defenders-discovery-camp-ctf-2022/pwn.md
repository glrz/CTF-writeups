# Pwn

## Uninitialized

![](<../.gitbook/assets/image (14) (1).png>)

In this challenge, we were given a `uninitialized` file with no file extension.&#x20;

If we use `strings` command to read readable characters, we would see that there is a key : `weakpass` leading to successful login.

![](<../.gitbook/assets/image (54).png>)

Next, we netcat into one of the servers and try to login with the key : `weakpass`

![](<../.gitbook/assets/image (79).png>)

After we are logged in, we could try to select `3` to print flag. However, we would get `Not Implemented` output message. If we try to select `4`, we would get the flag from `name` variable.

![](<../.gitbook/assets/image (29) (1).png>)

Flag: CDDC22{Un1nitialz1ed\_Var14ble\_Fun\_4nd\_Pr0fit\~!}
