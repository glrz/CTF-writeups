---
description: CTF.SG CTF 2021 is a 24 hours CTF competition held from 12 Mar - 13 Mar 2022.
---

# CTF.SG CTF 2022

I participated with the team name : etc2020 in this CTF competition. I solved 3 challenges - 1 sanity challenge and 2 MISC category challenges. 2 other challenges in the web category were solved by my online discord friend `Tensor`.&#x20;

![](<.gitbook/assets/image (591).png>)

Overall, this CTF was interesting. I enjoyed the experience and playing as a team. We achieved the position : 29/130 and I am pretty satisfied with that too.

![](<.gitbook/assets/image (560).png>)

## CTF.SG CTF Trailer

![](<.gitbook/assets/image (618).png>)

![](<.gitbook/assets/image (251).png>)

In this challenge, we were given a [YouTube video](https://www.youtube.com/watch?v=Qu7s7fr0ppY) and an attached [`Trailer.exe`](https://drive.google.com/file/d/1y9ulde94ZystiRUmmRLjOM3Y-qEhNl4A/view) file.

This challenge was an easy one. I solved it by decreasing the playback speed of the video on YouTube and making pauses in between to read the flag from 0:44 onwards.

![](<.gitbook/assets/image (214).png>)

![Flag part 1:CTF](<.gitbook/assets/image (255).png>)

![Flag part 2: SG{](<.gitbook/assets/image (210).png>)

![Flag part 3: CFG](<.gitbook/assets/image (646).png>)

![Flag part 4: \_4n1](<.gitbook/assets/image (541).png>)

![Flag part 5: m4t1](<.gitbook/assets/image (544).png>)

![Flag part 6: 0n}](<.gitbook/assets/image (685).png>)

Combining 6 parts of the flag above, we will get the flag.

An alternative solution would be to open the `Trailer.exe` file in `IDA freeware`. IDA freeware is a free binary code analysis tool that is used for reverse engineering. For this alternative solution, you could check out the writeup [here](https://shakuganz.com/2022/03/13/ctf-sg-2022-write-up/).

Flag: CTFSG{CFG\_4n1m4t10n}

## Insanity Check-in

![](<.gitbook/assets/image (392).png>)

This was solved after competition but I still decided to include it in. This was quite an interesting one. We were given a `Challenge.png` file which contains a QR code for this challenge.

{% file src=".gitbook/assets/Challenge.png" %}

![](<.gitbook/assets/Challenge (1).png>)

However, if we scan the QR code, it brings us to this [website](https://temperaturepass.ndi-api.gov.sg/login/WH3R3-FL4G), where there seems to be no clue and a possible dead end?

If we read the challenge description again, it reads `The flag lies encoded in the QR code`

So perhaps we could upload this QR on [ZXing Decoder Online](https://zxing.org/w/decode.jspx) and get the hex data.

![](<.gitbook/assets/image (486).png>)

Then, we copy the raw bytes data and paste it on CyberChef, offset the hex data(add 0 in front), and we will get the flag [here](https://gchq.github.io/CyberChef/#recipe=From\_Hex\('Auto'\)\&input=MDQzIDc2IDg3IDQ3IDQ3IDA3IDMzIGEyICAgZjIgZjcgNDYgNTYgZDcgMDYgNTcgMjYKMTcgNDcgNTcgMjYgNTcgMDYgMTcgMzcgICAzMiBlNiBlNiA0NiA5MiBkNiAxNyAwNgo5MiBlNiA3NiBmNyA2MiBlNyAzNiA3MiAgIGY2IGM2IGY2IDc2IDk2IGUyIGY1IDc0CjgzIDM1IDIzIDMyIGQ0IDY0IGMzIDQ0ICAgNzAgNDEgMTQgMzUgNDQgNjUgMzQgNzcKYjQgMzYgODMgMzYgMzYgYjYgNTYgNDMgICAxNiBlMiAxNyBkMCBlYyAxMSBlYyAxMQplYyAxMSBlYyAxMSBlYyAxMSA).

![](<.gitbook/assets/image (585).png>)

Flag: CTFSG{Ch3cked1n!}

## Wildest Dreams Part 2

![](<.gitbook/assets/image (623).png>)

In this challenge, we were provided with a challenge link and an attached php file.

If we download the [1989.php](https://drive.google.com/file/d/1UN3T9qG0diagPYcubYTnJrdQWIQUsyEd/view?usp=sharing) file, we see that is the source code of the website. Based on the PHP code, we can see that the flag will be printed if `md5 hash collision` occurs as both input string (via variable `i1`and `i2` using GET request) must be longer than 15 characters and must be different.

```php
<?php 
 
error_reporting(E_ERROR | E_PARSE);
include('flag.php');
?>
...
            <!-- Main -->
                <div class="wrapper style1">
 
                    <div class="container">
                        <article id="main" class="special">
                            <header>
                                <h2><a href="#">I could be in your wildest dream.</a></h2>
                                <p>
                                    I'm like the water when your ship rolled in that night<br>
                                    Rough on the surface but you cut through like a knife
                                </p>
                            </header>
                            <a href="#" class="image featured"><img src="images/tsbg.jpg" alt="" /></a>
                             
                            <?php
                                if(!empty($_GET['i1']) && !empty($_GET['i2'])){
                                    $i1 = $_GET['i1'];
                                    $i2 = $_GET['i2'];
                                    if($i1 === $i2){
                                        die("i1 and i2 can't be the same!");
                                    }
                                    $len1 = strlen($i1);
                                    $len2 = strlen($i2);
                                    if($len1 < 15){
                                        die("i1 is too shorttttttt pee pee pee pee pee");
                                    }
                                    if($len2 < 15){
                                        die("i2 is too shorttttttt pee pee pee pee pee");
                                    }
                                    if(md5($i1) == md5($i2)){
                                        echo $flag;
                                    }
                                    echo "<br>The more that you say, the less i know.";
                                } else {
                                    echo "<br> You need to provide two strings, i1 and i2. /1989.php?i1=a&i2=b";
                                }
                                 
                                 
                            ?>
                             
                        </article>
                         
                    </div>
 
                </div>
```

To solve this challenge, we need to search for `magic hashes` that are considered equal to each other. Magic h_ashes_ are well known specific hashes used to exploit Type Juggling attacks in PHP.

If we go to the site[ here](https://www.whitehatsec.com/blog/magic-hashes/), we would find this

![](<.gitbook/assets/image (230).png>)

We could use those values and paste it in the URL. The URL would look like this

{% embed url="http://chals.ctf.sg:40401/1989.php?i1=e153958235710973524115407854157&i2=Password147186970!" %}

We could also try out different combinations of strings, which you can find a list of them from this [website](https://github.com/spaze/hashes/blob/master/md5.md). Just take note to use two strings that are more than 15 characters in this case.

For example, this query below would work too

`/1989.php?i1=hello14916008992&i2=hello14943865304`

![](<.gitbook/assets/image (586).png>)

Flag: CTFSG{you\_see\_me\_in\_h1nds1ght\_tangled\_up\_with\_you\_all\_night}

## Chopsticks

![](<.gitbook/assets/image (724).png>)

![](<.gitbook/assets/image (599).png>)

This challenge was an interesting one. I remember I used to play this `chopsticks` game with my friends back then. In the past, I figured out a 100% winning strategy to win chopsticks if I were to start first.

Now, we are going against a bot called Pat. I think the intended solution for this was to boot up another terminal and netcat to the service, and let Pat go against Pat itself. For sure, one of the Pat would be the winner, and we would eventually get the flag. The author's writeup can be found [here](https://juliapoo.github.io/ctf/2022/03/13/ctfsg2022-author-writeup.html#chopsticks).

For this challenge, I decided to go against Pat and I won Pat in my first try!

Here are the rules of the game

![](<.gitbook/assets/image (716).png>)

I am starting with `Box A and Box B` while Pat is `Box C and Box D`

Here we just type `yes` to play with Pat

![](<.gitbook/assets/image (222).png>)

And.. the game has officially started! I start by attacking my own box first.

![](<.gitbook/assets/image (248).png>)

Then Pat attacks its own box too

![](<.gitbook/assets/image (515).png>)

Now, I use Box B to attack Box A, making it `3-2` for my boxes

![](<.gitbook/assets/image (176).png>)

Then, Pat attacked D with C, making it `1-3` for its boxes

![](<.gitbook/assets/image (574).png>)

Now, I was trying things out and decided to "skip" a turn by splitting `3-2` to `2-3`

![](<.gitbook/assets/image (185).png>)

Then, Pat split its boxes from `1-3` to `2-2`

![](<.gitbook/assets/image (613).png>)

Guess what, here I realised I could split my `2-3` back to `3-2`

![](<.gitbook/assets/image (384).png>)

Now, Pat attacks my box B with C

![](<.gitbook/assets/image (418).png>)

At this point, I could split `2-5` or `5-2` but that wouldn't make any sense because Pat could easily eliminate the box with `5` in the next turn. Also, I could split `4-3` but Pat could eliminate the box with `4` in the next turn as well. Both scenarios would put me at the losing end. Thus, I attacked Pat's box C with box B.

![](<.gitbook/assets/image (266).png>)

Now, Pat splits its boxes into `2-6`

![](<.gitbook/assets/image (426).png>)

I saw this as a very good opportunity to eliminate on of its box. I attacked box D with A.

![](<.gitbook/assets/image (507).png>)

Next, Pat attacked box A with C

![](<.gitbook/assets/image (204).png>)

Finally, I attacked C with A, winning the game :)

![](<.gitbook/assets/image (588).png>)

Then Pat gave me the flag

![](<.gitbook/assets/image (415).png>)

Flag: CTFSG{Th3\_Perf3cT\_Pl4YeR\_0j2nlhe}

## Chopsticks 2

![](<.gitbook/assets/image (538).png>)

![](<.gitbook/assets/image (497).png>)

This challenge is similar to the previous challenge `chopsticks`, but designed to be much harder to win. I think the intended solution for this was to boot up another terminal and netcat to the service, and let Pat go against Pat itself. For sure, one of the Pat would be the winner, and we would eventually get the flag. The author's writeup can be found [here.](https://juliapoo.github.io/ctf/2022/03/13/ctfsg2022-author-writeup.html#chopsticks-2)

For this challenge, I decided to go against Pat. It took me a few tries to solve this one but I found 2 different ways to beat Pat and eventually manually solved it within an hour. The game is just like regular chopsticks with reviving, and now it overflows at `7` instead of `5`.

### First solution (Gadiel vs Pat) - 18 moves

I attacked A with B first, to give myself a slight advantage

\


![](<.gitbook/assets/image (440).png>)

Pat attacked D with C. Now we are both `1-2` and `2-1`. You could say we are equal but actually I am still winning slightly because its my turn next.

![](<.gitbook/assets/image (414).png>)

My idea was to get my own boxes to a number high enough, but not that high such that Pat could eliminate my box. Here, I attacked B with A.

![](<.gitbook/assets/image (240).png>)

And Pat was making similar moves as well, attacking C with D.

![](<.gitbook/assets/image (644).png>)

At this point, I realised if I attacked any of Pat's boxes, that would give Pat more advantage. Pat could choose to split or possibly eliminate one of my boxes next turn. In this scenario, I chose to split `2-3` .

![](<.gitbook/assets/image (635).png>)

Then, Pat attacked D with C, making it `3-5`

![](<.gitbook/assets/image (468).png>)

I saw this as good opportunity to eliminate Pat's box D, I attacked D with A.

![](<.gitbook/assets/image (391).png>)

Now it seemed like I'm winning. I have 2 boxes and Pat is left with one. However, the rules allowed the box to revive. That's what Pat did in this move, splitting from `3` to `1-2`

![](<.gitbook/assets/image (495).png>)

I did not want to hit any of Pat's boxes, that could potentially increase his points and winning chances. So I went ahead to split my boxes `4-1`

![](<.gitbook/assets/image (492).png>)

Next, Pat attacked A with D, making my boxes `6-1`

![](<.gitbook/assets/image (510).png>)

In such a scenario, I could eliminate either box C or D with my box A. However, in the next turn, my box A will be eliminated, putting me into a losing position as I would be left with `box B: 1` and I would have no choice but to attack Pat and increase its chances of winning.

Hence, the best move here would be to split. Here I split my boxes `4-3`

![](<.gitbook/assets/image (445).png>)

Pat was quite smart too, it split its boxes `1-2`, and waited for my move

![](<.gitbook/assets/image (254).png>)

I went on to attack Pat's box D with A. Here, I am trying to increase Pat's points so that I could possibly eliminate box D first. Since Pat's box C only has 1 point, it would be easy to handle that box later if Pat doesn't do any splits.

![](<.gitbook/assets/image (231).png>)

Pat decided to split `2-5`, pretty good move, now box C is no longer 1.. which means this game might take longer to win, since Pat could revive a box with points more than 1. I decided to go head and eliminate box D first.

![](<.gitbook/assets/image (223).png>)

Indeed, Pat revived another box, splitting `2` into `1-1`

![](<.gitbook/assets/image (381).png>)

I choose to split my box `5-2` now and wait for Pat to attack me.

![](<.gitbook/assets/image (583).png>)

But Pat did not attack me, it went to split `1-1`

![](<.gitbook/assets/image (500).png>)

I did not want to attack any of Pat's boxes anymore, that could increase its chances of winning. So I went ahead to split `4-3` now

![](<.gitbook/assets/image (563).png>)

Then, Pat attacked A with C

![](<.gitbook/assets/image (537).png>)

I went on to split my boxes `4-4`

![](<.gitbook/assets/image (443).png>)

Then, Pat attacked D with C, making it `1-2`

![](<.gitbook/assets/image (182).png>)

I saw a good opportunity to potentially isolate box C with 1 point again. I choose to attack D with A.

![](<.gitbook/assets/image (249).png>)

Pat decided to split its boxes `2-5`. Oh man, not again....

![](<.gitbook/assets/image (189).png>)

&#x20;I had no choice but to eliminate box D first since that would be the best choice.

![](<.gitbook/assets/image (564).png>)

Next, Pat split `1-1` again like what it did previously.

![](<.gitbook/assets/image (184).png>)

I decided to split `5-3` and wait for Pat to attack me

![](<.gitbook/assets/image (496).png>)

Next, Pat attacked B with C. At this point I started to see the light at the end of the tunnel. I knew I could win this!

![](<.gitbook/assets/image (265).png>)

I went on to split `4-5` and waited for Pat to attack me

![](<.gitbook/assets/image (446).png>)

YES! Pat attacked my box B with C. At this point, I was almost 100% certain that I got this. I also realised 2 possible ways to win Pat. I could either split `5-5` or eliminate one of the boxes with box B first. The later would require more moves though.

![](<.gitbook/assets/image (505).png>)

I decided to split `5-5` first. If you are interested in my 2nd solution from this point onwards, continue reading till the end.

![](<.gitbook/assets/image (447).png>)

Next, Pat attacked D with C.

![](<.gitbook/assets/image (397).png>)

Now, I could either eliminate box D with A or B. I eliminated D with B.

![](<.gitbook/assets/image (534).png>)

Now Pat was having a headache. It had to choose between attacking A or B, but whatever Pat chooses, it would still be a win for me. Pat attacked B with C.

![](<.gitbook/assets/image (229).png>)

At this point, I could delay the game even further if I want by eliminating my box B with A, then let Pat attack me again before I win the game. However I decided to end it here, with 2 of my boxes still alive!

![](<.gitbook/assets/image (567).png>)

Surely, I got the flag after winning.

![](<.gitbook/assets/image (429).png>)

### Second solution (Gadiel vs Pat) - 20 moves

This is an alternative solution continued from the first solution. The first solution discussed about splitting into `5-5` first. In this solution, I would choose to eliminate one of Pat boxes first.

![](<.gitbook/assets/image (850).png>)

I attacked box D with B.

![](<.gitbook/assets/image (464).png>)

Pat attacked B with C. Now, we are both left with 1 box, but I'm still on the winning side.

![](<.gitbook/assets/image (830).png>)

I split my boxes from `4` into `2-2`

![](<.gitbook/assets/image (412).png>)

Pat attacked Box B with C.&#x20;

![](<.gitbook/assets/image (401).png>)

Now, the fastest way I could win and eliminate C is to increase my points. I attacked A with B to boost my points here.

![](<.gitbook/assets/image (452).png>)

Pat does not have any choice. Pat cannot split from just 1 point, so Pat could only choose which box it could attack. If it attacked box A, I would instantly win. In this case, it choose to attack box B.

![](<.gitbook/assets/image (403).png>)

I decided I played enough with Pat and wanted to end this quick, so I eliminated my own box B.

![](<.gitbook/assets/image (855).png>)

Pat could only attack box A now.

![](<.gitbook/assets/image (448).png>)

Finally, I eliminated box C, getting the win and the flag.

![](<.gitbook/assets/image (838).png>)

### Final solution (Pat vs Pat) - 17 moves

This was the intended solution I think? or at least the preferred way which most people used to solve the challenge. This is kind of like the "think out of the box" approach where you don't need to use your own brain power to go against a bot, rather you let the bot play against itself.

We could open 2 terminals and netcat to the same service. This solution is 1 move lesser than my `solution 1` above. However I still think my `solution 1` is better since I had 2 boxes still alive and won with a `5-6` score. If Pat played against Pat, the outcome would always be winning with 1 box alive only.

The solution for Pat vs Pat

![](<.gitbook/assets/image (449).png>)

![](<.gitbook/assets/image (458).png>)

![](<.gitbook/assets/image (437).png>)

![](<.gitbook/assets/image (865).png>)

![](<.gitbook/assets/image (454).png>)

![](<.gitbook/assets/image (869).png>)

![](<.gitbook/assets/image (400).png>)

![](<.gitbook/assets/image (419).png>)

![](<.gitbook/assets/image (895).png>)

![](<.gitbook/assets/image (893).png>)

![](<.gitbook/assets/image (886).png>)

![](<.gitbook/assets/image (471).png>)

![](<.gitbook/assets/image (385).png>)

![](<.gitbook/assets/image (884).png>)

![](<.gitbook/assets/image (880).png>)

![](<.gitbook/assets/image (389).png>)

![](<.gitbook/assets/image (842).png>)

![](<.gitbook/assets/image (878).png>)

![](<.gitbook/assets/image (864).png>)

![](<.gitbook/assets/image (852).png>)

![](<.gitbook/assets/image (890).png>)

![](<.gitbook/assets/image (897).png>)

![](<.gitbook/assets/image (845).png>)

![](<.gitbook/assets/image (441).png>)

![](<.gitbook/assets/image (463).png>)

![](<.gitbook/assets/image (433).png>)

![](<.gitbook/assets/image (858).png>)

![](<.gitbook/assets/image (881).png>)

![](<.gitbook/assets/image (891).png>)

![](<.gitbook/assets/image (377).png>)

![](<.gitbook/assets/image (826).png>)

![](<.gitbook/assets/image (896).png>)

![](<.gitbook/assets/image (862).png>)

![](<.gitbook/assets/image (459).png>)

![](<.gitbook/assets/image (395).png>)

Flag: CTFSG{Ch0pst!ck5\_m4STeR!11!\_aim48djam3}

