# Web

## baby web

![](<../.gitbook/assets/image (176).png>)

For this challenge, we first go to one of the links provided.

![](<../.gitbook/assets/image (145).png>)

Next we could `F12` to inspect the code or `CTRL+U` to view the source code. If we scroll down, we would see the flag printed vertically.

![](<../.gitbook/assets/image (107).png>)

Flag: CDDC22{H3lL0\_Spac3\_tr4v3l3r5}

## Little star

![](<../.gitbook/assets/image (142).png>)

For this challenge, I first go to one of the links provided. Here I would see `twinkle_star` and if I click on the `twinkle_star`, I would see the background change to a background full of stars.

![](<../.gitbook/assets/image (150).png>)

Next, I proceed to View the source code(CTRL+U). Notice the HTML comments shows `twinkle_star -> little_star -> flag`.

![](<../.gitbook/assets/image (20).png>)

At this point, I thought it could have something to do with the web `cookies` like how we solved [this ](https://gadiel-lau.gitbook.io/2022-writeups/dsta-brainhack-cyber-defenders-discovery-camp-training-2022/basic-concepts-of-cybersecurity/introduction-to-web-security#web-security-1)during the training.

I browsed the cookies using `EditThisCookie` and the cookie value was initially `twinkle_star`.

Then, I changed the cookie value to `little_star` and saved the changes.

![](<../.gitbook/assets/image (130).png>)

If we go back to the webpage, we could see `little_star` and if we click on `little_star,` we would see falling stars in the background.

![](<../.gitbook/assets/image (41).png>)

Finally, we could change this cookie value to `flag` and save it.

![](<../.gitbook/assets/image (39).png>)

Go back to the webpage and click on `FLAG!` and we would get the flag.

Note: I realised that the changing of cookie value to `little_star` was actually optional and we could directly change the cookie value to `flag` to get the flag.

![](<../.gitbook/assets/image (97).png>)

Flag: CDDC22{B4by\__W3b\_H4cking_\_3asy++}

## js easy

![](<../.gitbook/assets/image (32).png>)

For this challenge, we a `js_easy.html` file.



Upon pressing `F12` to inspect the code, we get an error message in console.

This error mentioned that `g is not defined`.

![](<../.gitbook/assets/image (56).png>)

We could simply add in `var g= ‘’;` to define `g`.

Here I used an [online javascript editor](https://www.w3schools.com/js/js\_editor.asp) to execute the program after defining `g` and I would get the flag.

![](<../.gitbook/assets/image (191).png>)

Flag: CDDC22{h4haHaH4\__it\_Is\_to0\_EASY\_R1ght?}_

__
