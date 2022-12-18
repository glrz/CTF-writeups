# Internet

## Easy

This challenge mentions that there is a hidden flag on the homepage.

![](<../../.gitbook/assets/image (132).png>)

Lets go to the homepage

![](<../../.gitbook/assets/image (142).png>)

Then, we press CTRL+U or right click view page source

![Press Ctrl+F to find for HTML comments \<!--](<../../.gitbook/assets/image (141).png>)

Here we can see the hidden flag : brixelCTF{notsosecret}

Flag: brixelCTF{notsosecret}

## Hidden Code

This challenge mentions something about the konami code.

![](<../../.gitbook/assets/image (146).png>)

A quick google search tells us that konami code, a cheatcode used in many konami games on consoles, can be performed by pressing **Up, Up, Down, Down, Left, Right, Left, Right, B, A** in this sequence. In this case, we can press these on our keyboard on this [site](https://www.brixel.be/)

After pressing these on my keyboard, we can see Mario floating by.

![](<../../.gitbook/assets/image (183).png>)

Flag:  brixelCTF{mario}

## Robotopia

![](<../../.gitbook/assets/image (16).png>)

Keeping robots out is done by using a robots.txt file, so if we go to the website and add robots.txt we will find the flag: _#you found a flag! it is: brixelCTF{sadr0b0tz}_

_Flag: brixelCTF{sadr0b0tz}_

## Hiding in the background

![](<../../.gitbook/assets/image (48).png>)

I did not attempt this during the CTF but I thought this was a pretty interesting one.

_The background is a .svg file._

We can actually save the background as `.svg` file and open it on `Inkscape`.

Remove the green background square and we will see a text field behind it.

Flag: brixelCTF{happy\_holidays}

## Flat Earth

![](<../../.gitbook/assets/image (6).png>)

For this challenge, we can try if it's vulnerable for SQL injection by entering a single quote (') as the username. The website will return an SQL error.&#x20;

We can assume that the admin account was the first account created, so if we use username&#x20;

**' OR 1=1;--**&#x20;

it will change the query from something like **SELECT \* FROM users WHERE username = AND password =** to **SELECT \* FROM users WHERE username = '' OR 1=1;--**&#x20;

This means that it will search for an empty username OR check if 1=1 (which is always true), and then comment out the rest of the query so it will no longer check for passwords.

If we enter that username, we will get **That should do the trick, the flag is brixelCTF{aroundtheglobe}**

_Flag: brixelCTF{aroundtheglobe}_

## login5

![](<../../.gitbook/assets/image (98).png>)

Here it seemed like the author used a obfuscation tool to mask the javascript function that does the processing,  but he forgot we can edit the javascript since it's running in our own browser.&#x20;

By inspecting the code, we can see somewhere near the end that it checks if `password==newpassword`, so we need to get the variable called `newpassword`.&#x20;

We can do that by using the console tool in our browser.&#x20;

First, open our inspector (F12 in firefox/chrome), and go to the console. Then press the login button on the site and while the 'invalid password' alert is shown, we type "alert(newpassword);" into the debugger and press enter.&#x20;

When we press ok on the alert another one will appear with the correct password. Logging in with the correct password gives us the flag.

Flag: brixelctf{0bfuscati0n}

## SnackShack awards

![](<../../.gitbook/assets/image (96).png>)

If we go to the site, we can press F12 > go to inspect elements mode

Then, we simply change the votes by clicking on the dropdown list for the desired snackbar and change the value to 5000 and submit the vote.

Flag: brixelCTF{bakpau}

## Pathfinders #1

![](<../../.gitbook/assets/image (57).png>)

If we look at the website we see that they link to their admin section, however it's password protected using a .htaccess and .htpasswd file (we know because of the login prompt).&#x20;

We can also see that the homepage is an index page that loads in another page (index.php?page=home.php) so the code reads and executes code from another file, in this case home.php.

We can leverage this to access the .htpasswd file that sits in the admin/ folder by altering the url to page=admin/.htpasswd

![](<../../.gitbook/assets/image (11).png>)

Flag: brixelCTF{unsafe\_include}

## Pathfinders #2

![](<../../.gitbook/assets/image (68).png>)

Note: I did not attempt this during the CTF but it is quite interesting so lets include it in.

If we go to the site, it reads: _Due to a recent hacker intrusion, we upgraded our security to only allow for php files to be included._&#x20;

This means we can't use the trick of just including the .htpasswd file anymore like what we did for Pathfinders #1, or can we? This exploit had been fixed since php 5.3.4 but we can actually trick the code into not reading parts of your query from the URL.&#x20;

We can add a `'%00'` in the URL. Request a page called&#x20;

`index.php?page=admin/.htpasswd%00.php`&#x20;

This way the script checks and sees .php at the end, but the include will drop that part and show the .htpasswd file, giving us the flag.

Flag: brixelCTF{outdated\_php}

## **Browsercheck**

![](<../../.gitbook/assets/image (90).png>)

On the website, we need to trick the server into thinking we are the ask jeeves crawler.&#x20;

Every browser uses a 'user-agent' to identify itself to the server, we can change this in most modern browsers. A quick google search reveals that the ask jeeves crawler (it's an old search engine by the way) uses this user-agent: _**Mozilla/2.0 (compatible; Ask Jeeves/Teoma)**_&#x20;

So we go to the website and press F12 to open the inspector.&#x20;

Depending on the browser we are using, there are different ways to solve this challenge.

Basically, we have to create a custom user-agent, select add custom device. Give it a name, and in the user-agent field enter Mozilla/2.0 (compatible; Ask Jeeves/Teoma). Save the profile and refresh the page, it should now accept us as being an official ask jeeves crawler and greet us with the message: the flag is 'brixelCTF{askwho?}'

Flag: brixelCTF{askwho?}

