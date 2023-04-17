# Misc

## Invisibility

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was pretty easy and straightforward.

I opened the `.txt` file in a text editor like `Sublime Text`&#x20;

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ subl Invisibility.txt   
```

I pressed `CTRL + A` which showed a bunch of dot and dashes. This likely implied that it is `morse code`.

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

We could manually type out these and paste it into [CyberChef ](https://cyberchef.org/#recipe=From\_Morse\_Code\('Space','Line%20feed'\)Remove\_whitespace\(true,true,true,true,true,false\)\&input=Li0tLS0KLS4KLi4uLQouLS0tLQouLi4KLi0tLS0KLS4uLgouLS0tLQouIAotLi0uCi0tLS0tCi0uLgouLi4tLSAKCgogICAJCgogCQkJCQoKICAgCgogCQkJCQoKCSAgIAoKIAkJCQkKCiAKCgkgCSAKCgkJCQkJCgoJICAKCiAgIAkJCgogCQkJCQoKCSAgIAoKIAkJCQkKCiAKCgkgCSAKCgkJCQkJCgoJICAKCiAgIAkJ)to get the flag.

A few other similar challenges which I attempted and solved previously could be found [here ](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/dsta-brainhack-cyber-defenders-discovery-camp-ctf-2022/misc#invisible-morse)and [here](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/nus-greyhats-grey-cat-the-flag-2022#ghost).

Flag: LNC2023{1NV1S1B1EC0D3}

## Swiftly

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

We were given a `.gif` file. We could open this `.gif` file and see that there are various QR codes that changed upon transition.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ eog Flag.gif 
```

We could use many different tools to solve this challenge, including online tools. I had previously completed a similar challenge where I tried using different tools [here](https://gadiel-lau.gitbook.io/2020-writeups-1/2020-ctfs/gsctf-2020#oh-gif).

For this challenge, I'll be using `ffmpeg` to extract each frame

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ ffmpeg -i Flag.gif file%03d.png
ffmpeg version 5.0.1-3+b1 Copyright (c) 2000-2022 the FFmpeg developers
  built with gcc 11 (Debian 11.3.0-4)
  configuration: --prefix=/usr --extra-version=3+b1 --toolchain=hardened --libdir=/usr/lib/x86_64-linux-gnu --incdir=/usr/include/x86_64-linux-gnu --arch=amd64 --enable-gpl --disable-stripping --enable-gnutls --enable-ladspa --enable-libaom --enable-libass --enable-libbluray --enable-libbs2b --enable-libcaca --enable-libcdio --enable-libcodec2 --enable-libdav1d --enable-libflite --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libglslang --enable-libgme --enable-libgsm --enable-libjack --enable-libmp3lame --enable-libmysofa --enable-libopenjpeg --enable-libopenmpt --enable-libopus --enable-libpulse --enable-librabbitmq --enable-librist --enable-librubberband --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libsrt --enable-libssh --enable-libsvtav1 --enable-libtheora --enable-libtwolame --enable-libvidstab --enable-libvorbis --enable-libvpx --enable-libwebp --enable-libx265 --enable-libxml2 --enable-libxvid --enable-libzimg --enable-libzmq --enable-libzvbi --enable-lv2 --enable-omx --enable-openal --enable-opencl --enable-opengl --enable-sdl2 --disable-sndio --enable-pocketsphinx --enable-librsvg --enable-libmfx --enable-libdc1394 --enable-libdrm --enable-libiec61883 --enable-chromaprint --enable-frei0r --enable-libplacebo --enable-libx264 --enable-shared
  libavutil      57. 17.100 / 57. 17.100
  libavcodec     59. 18.100 / 59. 18.100
  libavformat    59. 16.100 / 59. 16.100
  libavdevice    59.  4.100 / 59.  4.100
  libavfilter     8. 24.100 /  8. 24.100
  libswscale      6.  4.100 /  6.  4.100
  libswresample   4.  3.100 /  4.  3.100
  libpostproc    56.  3.100 / 56.  3.100
Input #0, gif, from 'Flag.gif':
  Metadata:
    comment         : Created with ezgif.com GIF maker
  Duration: 00:00:01.00, start: 0.000000, bitrate: 143 kb/s
  Stream #0:0: Video: gif, bgra, 300x300, 5 fps, 5 tbr, 100 tbn
Stream mapping:
  Stream #0:0 -> #0:0 (gif (native) -> png (native))
Press [q] to stop, [?] for help
Output #0, image2, to 'file%03d.png':
  Metadata:
    comment         : Created with ezgif.com GIF maker
    encoder         : Lavf59.16.100
  Stream #0:0: Video: png, rgba(pc, gbr/unknown/unknown, progressive), 300x300, q=2-31, 200 kb/s, 5 fps, 5 tbn
    Metadata:
      encoder         : Lavc59.18.100 png
frame=    5 fps=0.0 q=-0.0 Lsize=N/A time=00:00:01.00 bitrate=N/A speed=6.32x    
video:21kB audio:0kB subtitle:0kB other streams:0kB global headers:0kB muxing overhead: unknown
```

After I have extracted the frames (i.e. the different QR codes) into the directory, I can process and read them all at once using `zbarimg`

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ zbarimg file0*                 
QR-Code:LNC2023{Ar
QR-Code:e_y0u
QR-Code:_FaSt_
QR-Code:En0ugh_4_
QR-Code:th1s}
scanned 5 barcode symbols from 5 images in 0.08 seconds
```

As we can see, there are 5 QR codes scanned. Combining these 5 parts will give us the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ zbarimg -q --raw file0* | tr -d '\n'

LNC2023{Are_y0u_FaSt_En0ugh_4_th1s}
```

Flag: LNC2023{Are\_y0u\_FaSt\_En0ugh\_4\_th1s}

## Hindsight

<figure><img src="../../.gitbook/assets/image (1) (2).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a bunch of text with the flag hidden in it.&#x20;

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cat Hindsight.txt             
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Cursus metus aliquam eleifend mi in nulla posuere sollicitudin. Nisl rhoncus mattis rhoncus urna neque viverra justo nec. In ante metus dictum at tempor commodo ullamcorper a. Volutpat sed cras ornare arcu dui vivamus arcu felis. In egestas erat imperdiet sed euismod nisi porta. Convallis a cras semper auctor neque vitae. Quam viverra orci sagittis eu volutpat odio facilisis. Dolor morbi non arcu risus quis varius quam quisque. Id semper risus in hendrerit gravida rutrum quisque non tellus. Cursus eget nunc scelerisque viverra mauris in aliquam. Tortor aliquam nulla facilisi cras fermentum odio. Sed turpis tincidunt id aliquet risus feugiat in ante metus. Urna nunc id cursus metus aliquam eleifend. At auctor urna nunc id. Sed tempus urna et pharetra pharetra. Odio pellentesque diam volutpat commodo. Eleifend mi in nulla posuere sollicitudin aliquam ultrices sagittis orci. Condimentum id venenatis a condimentum vitae sapien pellentesque. Lacus vel facilisis volutpat est velit egestas dui id ornare. Mi eget mauris pharetra et ultrices neque ornare aenean. Elit sed vulputate mi sit amet. Cursus turpis massa tincidunt dui ut ornare lectus sit amet. Duis convallis convallis tellus id interdum velit laoreet id donec. Proin libero nunc consequat interdum varius sit amet mattis. Tempor id eu nisl nunc mi ipsum faucibus. Purus gravida quis blandit turpis cursus in. Cursus eget nunc scelerisque viverra mauris in. Placerat vestibulum lectus mauris ultrices eros in. Et odio pellentesque diam volutpat. Volutpat lacus laoreet non curabitur gravida arcu ac. At consectetur lorem donec massa sapien. Facilisis sed odio morbi quis. Proin fermentum leo vel orci porta non. Quis lectus nulla at volutpat diam ut venenatis tellus in. Pellentesque nec nam aliquam sem et tortor consequat id. Pretium viverra suspendisse potenti nullam. Sollicitudin ac orci phasellus egestas tellus rutrum tellus pellentesque eu. Vitae turpis massa sed elementum tempus. Mauris rhoncus aenean vel elit scelerisque mauris pellentesque pulvinar pellentesque. Quis varius quam quisque id diam vel. Maecenas sed enim ut sem viverra aliquet eget. Laoreet non curabitur gravida arcu ac. Curabitur vitae nunc sed velit dignissim sodales ut. Quam viverra orci sagittis eu volutpat odio facilisis mauris. Dui ut ornare lectus sit amet est placerat in egestas. At augue eget arcu dictum varius duis. Aliquet nibh praesent tristique magna sit. Ipsum nunc aliquet bibendum enim facilisis gravida neque convallis a. Enim ut tellus elementum sagittis. Eu facilisis sed odio morbi quis. Elit ullamcorper dignissim cras tincidunt lobortis feugiat vivamus. Velit laoreet id donec ultrices tincidunt arcu non sodales neque. Scelerisque mauris pellentesque pulvinar pellentesque habitant morbi tristique senectus et. Congue nisi vitae suscipit tellus. Imperdiet sed euismod nisi porta lorem mollis aliquam. Vulputate mi sit amet mauris commodo quis imperdiet massa. Et netus et malesuada fames ac turpis egestas integer eget. Sit amet consectetur adipiscing elit ut aliquam purus. Tempor commodo ullamcorper a lacus vestibulum sed arcu non. Vestibulum lorem sed risus ultricies tristique nulla. Pellentesque habitant morbi tristique senectus et netus. Egestas sed tempus urna et pharetra pharetra massa. Ullamcorper morbi tincidunt ornare massa eget egestas. Ornare aenean euismod elementum nisi quis. Turpis egestas sed tempus urna et pharetra pharetra. Pulvinar mattis nunc sed blandit. Nunc mi ipsum faucibus vitae aliquet nec. Laoreet suspendisse interdum consectetur libero id. Montes nascetur ridiculus mus mauris. Lobortis feugiat vivamus at augue eget arcu dictum varius duis. Molestie ac feugiat sed lectus vestibulum mattis ullamcorper. Eget magna fermentum iaculis eu non diam phasellus vestibulum lorem. Nunc id cursus metus aliquam. Sollicitudin tempor id eu nisl. Lectus quam id leo in vitae turpis massa. Orci ac auctor augue mauris augue neque gravida in fermentum. Enim nunc faucibus a pellentesque sit amet. Ultrices neque ornare aenean euismod elementum nisi quis eleifend quam. Venenatis tellus in metus vulputate eu scelerisque felis imperdiet. Sed velit dignissim sodales ut eu sem integer vitae justo. Tellus in hac habitasse platea dictumst vestibulum rhoncus est pellentesque. Quam id leo in vitae turpis massa sed elementum tempus. Tempor id eu nisl nunc mi. Volutpat commodo sed egestas egestas fringilla. Condimentum lacinia quis vel eros donec ac odio tempor orci. Egestas integer eget aliquet nibh praesent. Congue quisque egestas diam in arcu. Vitae turpis massa sed elementum tempus egestas sed sed risus. Massa tincidunt nunc pulvinar sapien et. Flag: H1nds3ght In nulla posuere sollicitudin aliquam ultrices sagittis orci. Ultricies tristique nulla aliquet enim tortor. Id consectetur purus ut faucibus pulvinar elementum integer. Lectus mauris ultrices eros in. Volutpat commodo sed egestas egestas fringilla phasellus faucibus. Lobortis scelerisque fermentum dui faucibus in ornare quam viverra orci. Sapien faucibus et molestie ac. Quam lacus suspendisse faucibus interdum posuere lorem ipsum dolor sit. Adipiscing enim eu turpis egestas. Suspendisse sed nisi lacus sed viverra tellus. At auctor urna nunc id cursus metus aliquam eleifend mi. Tristique senectus et netus et malesuada fames ac turpis egestas. Cras pulvinar mattis nunc sed blandit libero volutpat. Viverra vitae congue eu consequat. Nisi porta lorem mollis aliquam ut porttitor. Turpis egestas integer eget aliquet nibh praesent tristique magna sit. Ac odio tempor orci dapibus. Arcu dui vivamus arcu felis bibendum ut tristique et. Tincidunt vitae semper quis lectus. Eu non diam phasellus vestibulum lorem sed risus. Scelerisque fermentum dui faucibus in ornare. Sapien faucibus et molestie ac feugiat sed lectus vestibulum. Purus faucibus ornare suspendisse sed nisi lacus. Nulla pharetra diam sit amet nisl suscipit adipiscing bibendum. Arcu risus quis varius quam quisque. Egestas sed sed risus pretium quam vulputate dignissim. Sapien nec sagittis aliquam malesuada bibendum arcu vitae elementum curabitur. Magna fermentum iaculis eu non. Leo integer malesuada nunc vel risus. Consequat nisl vel pretium lectus. Massa placerat duis ultricies lacus sed. Eget egestas purus viverra accumsan. Iaculis eu non diam phasellus vestibulum lorem sed risus. Tortor at auctor urna nunc id. Adipiscing at in tellus integer. Eget arcu dictum varius duis at. Porttitor eget dolor morbi non arcu. Ac turpis egestas integer eget aliquet. In metus vulputate eu scelerisque felis imperdiet. Et sollicitudin ac orci phasellus egestas tellus rutrum tellus. Consectetur libero id faucibus nisl tincidunt eget nullam non nisi. Enim diam vulputate ut pharetra sit amet. Aliquet bibendum enim facilisis gravida neque convallis a. Sed turpis tincidunt id aliquet risus feugiat. Viverra adipiscing at in tellus. Nunc sed velit dignissim sodales ut eu sem integer vitae. Cras semper auctor neque vitae tempus quam pellentesque. Praesent tristique magna sit amet purus gravida quis. Quam adipiscing vitae proin sagittis. Consectetur adipiscing elit duis tristique sollicitudin nibh sit amet. Ante in nibh mauris cursus mattis molestie a iaculis at. Nunc consequat interdum varius sit. Vitae tempus quam pellentesque nec nam aliquam sem et tortor. Morbi tincidunt augue interdum velit euismod in pellentesque. Sed viverra tellus in hac habitasse platea. Sed vulputate mi sit amet. Sed elementum tempus egestas sed sed risus pretium. Commodo ullamcorper a lacus vestibulum sed arcu. Quam adipiscing vitae proin sagittis nisl rhoncus mattis. Ac turpis egestas sed tempus. Nisi scelerisque eu ultrices vitae auctor eu augue ut. Vitae justo eget magna fermentum iaculis. Neque vitae tempus quam pellentesque nec nam aliquam sem. Dui id ornare arcu odio ut sem nulla pharetra. Neque ornare aenean euismod elementum nisi. Tincidunt eget nullam non nisi est sit amet. Eget aliquet nibh praesent tristique magna. Lorem mollis aliquam ut porttitor leo. Volutpat ac tincidunt vitae semper quis lectus nulla. Neque volutpat ac tincidunt vitae semper quis lectus nulla at. Faucibus vitae aliquet nec ullamcorper sit amet risus nullam.   
```

If we look closely, we would see the flag in it. `Flag: H1nds3ght`

Alternatively, we could grep for flag, specifying the `a` option to look through as binary file and `i` option to ignore casing.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ grep -ai flag Hindsight.txt
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Cursus metus aliquam eleifend mi in nulla posuere sollicitudin. Nisl rhoncus mattis rhoncus urna neque viverra justo nec. In ante metus dictum at tempor commodo ullamcorper a. Volutpat sed cras ornare arcu dui vivamus arcu felis. In egestas erat imperdiet sed euismod nisi porta. Convallis a cras semper auctor neque vitae. Quam viverra orci sagittis eu volutpat odio facilisis. Dolor morbi non arcu risus quis varius quam quisque. Id semper risus in hendrerit gravida rutrum quisque non tellus. Cursus eget nunc scelerisque viverra mauris in aliquam. Tortor aliquam nulla facilisi cras fermentum odio. Sed turpis tincidunt id aliquet risus feugiat in ante metus. Urna nunc id cursus metus aliquam eleifend. At auctor urna nunc id. Sed tempus urna et pharetra pharetra. Odio pellentesque diam volutpat commodo. Eleifend mi in nulla posuere sollicitudin aliquam ultrices sagittis orci. Condimentum id venenatis a condimentum vitae sapien pellentesque. Lacus vel facilisis volutpat est velit egestas dui id ornare. Mi eget mauris pharetra et ultrices neque ornare aenean. Elit sed vulputate mi sit amet. Cursus turpis massa tincidunt dui ut ornare lectus sit amet. Duis convallis convallis tellus id interdum velit laoreet id donec. Proin libero nunc consequat interdum varius sit amet mattis. Tempor id eu nisl nunc mi ipsum faucibus. Purus gravida quis blandit turpis cursus in. Cursus eget nunc scelerisque viverra mauris in. Placerat vestibulum lectus mauris ultrices eros in. Et odio pellentesque diam volutpat. Volutpat lacus laoreet non curabitur gravida arcu ac. At consectetur lorem donec massa sapien. Facilisis sed odio morbi quis. Proin fermentum leo vel orci porta non. Quis lectus nulla at volutpat diam ut venenatis tellus in. Pellentesque nec nam aliquam sem et tortor consequat id. Pretium viverra suspendisse potenti nullam. Sollicitudin ac orci phasellus egestas tellus rutrum tellus pellentesque eu. Vitae turpis massa sed elementum tempus. Mauris rhoncus aenean vel elit scelerisque mauris pellentesque pulvinar pellentesque. Quis varius quam quisque id diam vel. Maecenas sed enim ut sem viverra aliquet eget. Laoreet non curabitur gravida arcu ac. Curabitur vitae nunc sed velit dignissim sodales ut. Quam viverra orci sagittis eu volutpat odio facilisis mauris. Dui ut ornare lectus sit amet est placerat in egestas. At augue eget arcu dictum varius duis. Aliquet nibh praesent tristique magna sit. Ipsum nunc aliquet bibendum enim facilisis gravida neque convallis a. Enim ut tellus elementum sagittis. Eu facilisis sed odio morbi quis. Elit ullamcorper dignissim cras tincidunt lobortis feugiat vivamus. Velit laoreet id donec ultrices tincidunt arcu non sodales neque. Scelerisque mauris pellentesque pulvinar pellentesque habitant morbi tristique senectus et. Congue nisi vitae suscipit tellus. Imperdiet sed euismod nisi porta lorem mollis aliquam. Vulputate mi sit amet mauris commodo quis imperdiet massa. Et netus et malesuada fames ac turpis egestas integer eget. Sit amet consectetur adipiscing elit ut aliquam purus. Tempor commodo ullamcorper a lacus vestibulum sed arcu non. Vestibulum lorem sed risus ultricies tristique nulla. Pellentesque habitant morbi tristique senectus et netus. Egestas sed tempus urna et pharetra pharetra massa. Ullamcorper morbi tincidunt ornare massa eget egestas. Ornare aenean euismod elementum nisi quis. Turpis egestas sed tempus urna et pharetra pharetra. Pulvinar mattis nunc sed blandit. Nunc mi ipsum faucibus vitae aliquet nec. Laoreet suspendisse interdum consectetur libero id. Montes nascetur ridiculus mus mauris. Lobortis feugiat vivamus at augue eget arcu dictum varius duis. Molestie ac feugiat sed lectus vestibulum mattis ullamcorper. Eget magna fermentum iaculis eu non diam phasellus vestibulum lorem. Nunc id cursus metus aliquam. Sollicitudin tempor id eu nisl. Lectus quam id leo in vitae turpis massa. Orci ac auctor augue mauris augue neque gravida in fermentum. Enim nunc faucibus a pellentesque sit amet. Ultrices neque ornare aenean euismod elementum nisi quis eleifend quam. Venenatis tellus in metus vulputate eu scelerisque felis imperdiet. Sed velit dignissim sodales ut eu sem integer vitae justo. Tellus in hac habitasse platea dictumst vestibulum rhoncus est pellentesque. Quam id leo in vitae turpis massa sed elementum tempus. Tempor id eu nisl nunc mi. Volutpat commodo sed egestas egestas fringilla. Condimentum lacinia quis vel eros donec ac odio tempor orci. Egestas integer eget aliquet nibh praesent. Congue quisque egestas diam in arcu. Vitae turpis massa sed elementum tempus egestas sed sed risus. Massa tincidunt nunc pulvinar sapien et. Flag: H1nds3ght In nulla posuere sollicitudin aliquam ultrices sagittis orci. Ultricies tristique nulla aliquet enim tortor. Id consectetur purus ut faucibus pulvinar elementum integer. Lectus mauris ultrices eros in. Volutpat commodo sed egestas egestas fringilla phasellus faucibus. Lobortis scelerisque fermentum dui faucibus in ornare quam viverra orci. Sapien faucibus et molestie ac. Quam lacus suspendisse faucibus interdum posuere lorem ipsum dolor sit. Adipiscing enim eu turpis egestas. Suspendisse sed nisi lacus sed viverra tellus. At auctor urna nunc id cursus metus aliquam eleifend mi. Tristique senectus et netus et malesuada fames ac turpis egestas. Cras pulvinar mattis nunc sed blandit libero volutpat. Viverra vitae congue eu consequat. Nisi porta lorem mollis aliquam ut porttitor. Turpis egestas integer eget aliquet nibh praesent tristique magna sit. Ac odio tempor orci dapibus. Arcu dui vivamus arcu felis bibendum ut tristique et. Tincidunt vitae semper quis lectus. Eu non diam phasellus vestibulum lorem sed risus. Scelerisque fermentum dui faucibus in ornare. Sapien faucibus et molestie ac feugiat sed lectus vestibulum. Purus faucibus ornare suspendisse sed nisi lacus. Nulla pharetra diam sit amet nisl suscipit adipiscing bibendum. Arcu risus quis varius quam quisque. Egestas sed sed risus pretium quam vulputate dignissim. Sapien nec sagittis aliquam malesuada bibendum arcu vitae elementum curabitur. Magna fermentum iaculis eu non. Leo integer malesuada nunc vel risus. Consequat nisl vel pretium lectus. Massa placerat duis ultricies lacus sed. Eget egestas purus viverra accumsan. Iaculis eu non diam phasellus vestibulum lorem sed risus. Tortor at auctor urna nunc id. Adipiscing at in tellus integer. Eget arcu dictum varius duis at. Porttitor eget dolor morbi non arcu. Ac turpis egestas integer eget aliquet. In metus vulputate eu scelerisque felis imperdiet. Et sollicitudin ac orci phasellus egestas tellus rutrum tellus. Consectetur libero id faucibus nisl tincidunt eget nullam non nisi. Enim diam vulputate ut pharetra sit amet. Aliquet bibendum enim facilisis gravida neque convallis a. Sed turpis tincidunt id aliquet risus feugiat. Viverra adipiscing at in tellus. Nunc sed velit dignissim sodales ut eu sem integer vitae. Cras semper auctor neque vitae tempus quam pellentesque. Praesent tristique magna sit amet purus gravida quis. Quam adipiscing vitae proin sagittis. Consectetur adipiscing elit duis tristique sollicitudin nibh sit amet. Ante in nibh mauris cursus mattis molestie a iaculis at. Nunc consequat interdum varius sit. Vitae tempus quam pellentesque nec nam aliquam sem et tortor. Morbi tincidunt augue interdum velit euismod in pellentesque. Sed viverra tellus in hac habitasse platea. Sed vulputate mi sit amet. Sed elementum tempus egestas sed sed risus pretium. Commodo ullamcorper a lacus vestibulum sed arcu. Quam adipiscing vitae proin sagittis nisl rhoncus mattis. Ac turpis egestas sed tempus. Nisi scelerisque eu ultrices vitae auctor eu augue ut. Vitae justo eget magna fermentum iaculis. Neque vitae tempus quam pellentesque nec nam aliquam sem. Dui id ornare arcu odio ut sem nulla pharetra. Neque ornare aenean euismod elementum nisi. Tincidunt eget nullam non nisi est sit amet. Eget aliquet nibh praesent tristique magna. Lorem mollis aliquam ut porttitor leo. Volutpat ac tincidunt vitae semper quis lectus nulla. Neque volutpat ac tincidunt vitae semper quis lectus nulla at. Faucibus vitae aliquet nec ullamcorper sit amet risus nullam.

```

Flag: LNC2023{H1nds3ght}

## Tennis Rookie

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

For this challenge, I solved it after the compeitition. It was actually using `Racket` lang.

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

If we netcat into the server, we would see this shell like interface

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ nc nc.lagncra.sh 8008
Welcome to Racket v7.2.
> 
```

Using these two commands, we can open the flag file and key file

> (read-line (open-input-file "/flag"))
>
> (read-line (open-input-file "/key"))

```bash
> (read-line (open-input-file "/flag"))   
"XLE2023{zuhj_hv_jnhksm_ogsrg_nrnybitkx_rdc_czx_elxxkj_cuut}"
> (read-line (open-input-file "/key"))
"MYCOMPUTERLAGGINGANDCRASHINGFR"
> 
```

We can then decode this as `Vigenere Cipher` using [CyberChef](https://cyberchef.org/#recipe=Vigen%C3%A8re\_Decode\('MYCOMPUTERLAGGINGANDCRASHINGFR'\)\&input=WExFMjAyM3t6dWhqX2h2X2puaGtzbV9vZ3NyZ19ucm55Yml0a3hfcmRjX2N6eF9lbHh4a2pfY3V1dH0).&#x20;

Flag: LNC2023{lisp\_or\_scheme\_based\_languages\_are\_all\_pretty\_cool}
