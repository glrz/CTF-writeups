# Network Security

## Found a Note 1

<figure><img src="../../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given an image. This looked like a series of bytes which we normally see in a packet.

<figure><img src="../../../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>

We can take a look at the IP packet.

<figure><img src="../../../.gitbook/assets/image (49) (5).png" alt=""><figcaption></figcaption></figure>

According to the IP packet header specifications, `c0 a8 14 46` is the source IP address.

Using [CyberChef](https://cyberchef.org/#recipe=From\_Hex\('Auto'\)To\_Decimal\('Space',false\)Find\_/\_Replace\(%7B'option':'Regex','string':'%20'%7D,'.',true,false,true,false\)MD5\(\)\&input=YzAgYTggMTQgNDY), we can get the flag following these steps:

1. Convert `c0 a8 14 46` from hex to decimal
2. Replace space with `.`
3. Convert to MD5

Flag: d37d3b3583dd7fdcca04728994bad42f

## Found a Note 2

<figure><img src="../../../.gitbook/assets/image (10) (11).png" alt=""><figcaption></figcaption></figure>

For this challenge, it is slightly similar to the previous challenge. We were given an image of packet as well.

&#x20;

<figure><img src="../../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

However, we will not be dealing with IP packet now, but rather [TCP](https://en.wikipedia.org/wiki/Transmission\_Control\_Protocol).

<figure><img src="../../../.gitbook/assets/image (119).png" alt=""><figcaption></figcaption></figure>

We can see that the source port is the first 2 bytes or 16 bits: `41B6`.

To convert "41B6" to decimal, each digit represents a power of 16:

41B6 base 16 = (4 \* 16^3) + (1 \* 16^2) + (B \* 16^1) + (6 \* 16^0)

However, we encounter a hexadecimal digit "B" in this value. In hexadecimal, "B" represents the decimal value 11. Therefore, we can substitute "B" with 11:

41B6 base 16 = (4 \* 16^3) + (1 \* 16^2) + (11 \* 16^1) + (6 \* 16^0) = (4 \* 4096) + (1 \* 256) + (11 \* 16) + (6 \* 1) = 16384 + 256 + 176 + 6 = 16822

Therefore, the source port running in this TCP packet is 16822.

Convert the source port number to MD5 to get the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ echo -n 16822 | md5sum
feddfedc98490ed7e123db392f076fa1  -
```

Flag: feddfedc98490ed7e123db392f076fa1

## USB! We can Read it!

<figure><img src="../../../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>

For this challenge, I unlocked the hint: USB keyboard.

<figure><img src="../../../.gitbook/assets/image (118).png" alt=""><figcaption></figcaption></figure>

In this case, we are given a packet capture file of USB keyboard.

<figure><img src="../../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

In Wireshark, we can filter by

`usb.transfer_type == 0x01 and frame.len == 35 and !(usb.capdata == 00:00:00:00:00:00:00:00)`

From here, we are able to see the keystrokes captured under HID Data.

<figure><img src="../../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

Next, `CTRL+A` to select all packets and go to `File > Export Specified Packets`

<figure><img src="../../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

Save the filename of the exported packets as  `keystrokes.pcapng`

We  can then  run  the  following `tshark` command to get the keystrokes saved in `keystrokes.txt`.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ tshark -r keystrokes.pcapng -Y 'usb.capdata && usb.data_len == 8' -T fields -e usb.capdata | sed 's/../:&/g2' > keystrokes.txt
```

We can take a look at the `keystrokes.txt` file.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cat keystrokes.txt
08:00:00:00:00:00:00:00
08:00:15:00:00:00:00:00
00:00:15:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:11:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:12:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:17:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:08:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:13:00:00:00:00:00
00:00:13:04:00:00:00:00
00:00:04:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:07:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:28:00:00:00:00:00
00:00:00:00:00:00:00:00
01:00:00:00:00:00:00:00
00:00:00:00:00:00:00:00
02:00:00:00:00:00:00:00
02:00:0b:00:00:00:00:00
00:00:0b:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:08:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:1c:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:36:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:2c:00:00:00:00:00
00:00:00:00:00:00:00:00
02:00:00:00:00:00:00:00
02:00:09:00:00:00:00:00
00:00:09:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0c:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:11:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:04:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0f:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0f:00:00:00:00:00
00:00:0f:1c:00:00:00:00
00:00:1c:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:2c:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:1c:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:12:00:00:00:00:00
00:00:12:18:00:00:00:00
00:00:18:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:2c:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0e:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:11:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:12:00:00:00:00:00
00:00:12:1a:00:00:00:00
00:00:1a:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:2c:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:17:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0b:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:08:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:2c:00:00:00:00:00
00:00:00:00:00:00:00:00
02:00:00:00:00:00:00:00
02:00:18:00:00:00:00:00
02:00:18:16:00:00:00:00
02:00:16:00:00:00:00:00
02:00:00:00:00:00:00:00
02:00:05:00:00:00:00:00
00:00:05:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:2c:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:13:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:04:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:06:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0e:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:08:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:17:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:2c:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:04:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:11:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:04:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0f:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:1c:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:16:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0c:00:00:00:00:00
00:00:0c:16:00:00:00:00
00:00:16:00:00:00:00:00
00:00:00:00:00:00:00:00
20:00:00:00:00:00:00:00
20:00:1e:00:00:00:00:00
20:00:00:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:28:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:28:00:00:00:00:00
00:00:00:00:00:00:00:00
02:00:00:00:00:00:00:00
02:00:17:00:00:00:00:00
00:00:17:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0b:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:08:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:2c:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:09:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0f:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:04:00:00:00:00:00
00:00:04:0a:00:00:00:00
00:00:0a:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:2c:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0c:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:16:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:2c:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:10:00:00:00:00:00
00:00:10:07:00:00:00:00
00:00:07:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:22:00:00:00:00:00
00:00:00:00:00:00:00:00
20:00:00:00:00:00:00:00
20:00:26:00:00:00:00:00
20:00:00:00:00:00:00:00
00:00:00:00:00:00:00:00
02:00:00:00:00:00:00:00
02:00:1a:00:00:00:00:00
00:00:1a:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0c:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:17:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0b:00:00:00:00:00
00:00:00:00:00:00:00:00
02:00:00:00:00:00:00:00
02:00:2d:00:00:00:00:00
02:00:00:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0a:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:15:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:08:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:04:00:00:00:00:00
00:00:04:17:00:00:00:00
00:00:17:00:00:00:00:00
00:00:00:00:00:00:00:00
02:00:00:00:00:00:00:00
02:00:2d:00:00:00:00:00
02:00:00:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:13:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:12:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:1a:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:08:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:15:00:00:00:00:00
00:00:00:00:00:00:00:00
02:00:00:00:00:00:00:00
02:00:2d:00:00:00:00:00
02:00:00:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:06:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:12:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:10:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:08:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:16:00:00:00:00:00
00:00:00:00:00:00:00:00
02:00:00:00:00:00:00:00
02:00:2d:00:00:00:00:00
02:00:00:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0a:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:15:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:08:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:04:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:17:00:00:00:00:00
00:00:00:00:00:00:00:00
02:00:00:00:00:00:00:00
02:00:2d:00:00:00:00:00
02:00:00:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:15:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:08:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:16:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:13:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:12:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:11:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:16:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0c:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:05:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0c:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0f:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0c:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:17:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:1c:00:00:00:00:00
00:00:00:00:00:00:00:00
20:00:00:00:00:00:00:00
20:00:27:00:00:00:00:00
20:00:00:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:28:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:28:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:2d:00:00:00:00:00
00:00:00:00:00:00:00:00
02:00:00:00:00:00:00:00
02:00:16:00:00:00:00:00
00:00:16:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:13:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0c:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:07:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:08:00:00:00:00:00
00:00:08:15:00:00:00:00
00:00:15:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:10:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:04:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:11:00:00:00:00:00
00:00:00:00:00:00:00:00
```

Run the following script on the `keystrokes.txt`, the script can be found here: [https://github.com/carlospolop-forks/ctf-usb-keyboard-parser](https://github.com/carlospolop-forks/ctf-usb-keyboard-parser)

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

import sys

#More symbols in https://www.fileformat.info/search/google.htm?q=capslock+symbol&domains=www.fileformat.info&sitesearch=www.fileformat.info&client=pub-6975096118196151&forid=1&channel=1657057343&ie=UTF-8&oe=UTF-8&cof=GALT%3A%23008000%3BGL%3A1%3BDIV%3A%23336699%3BVLC%3A663399%3BAH%3Acenter%3BBGC%3AFFFFFF%3BLBGC%3A336699%3BALC%3A0000FF%3BLC%3A0000FF%3BT%3A000000%3BGFNT%3A0000FF%3BGIMP%3A0000FF%3BFORID%3A11&hl=en
KEY_CODES = {
    0x04:['a', 'A'],
    0x05:['b', 'B'],
    0x06:['c', 'C'],
    0x07:['d', 'D'],
    0x08:['e', 'E'],
    0x09:['f', 'F'],
    0x0A:['g', 'G'],
    0x0B:['h', 'H'],
    0x0C:['i', 'I'],
    0x0D:['j', 'J'],
    0x0E:['k', 'K'],
    0x0F:['l', 'L'],
    0x10:['m', 'M'],
    0x11:['n', 'N'],
    0x12:['o', 'O'],
    0x13:['p', 'P'],
    0x14:['q', 'Q'],
    0x15:['r', 'R'],
    0x16:['s', 'S'],
    0x17:['t', 'T'],
    0x18:['u', 'U'],
    0x19:['v', 'V'],
    0x1A:['w', 'W'],
    0x1B:['x', 'X'],
    0x1C:['y', 'Y'],
    0x1D:['z', 'Z'],
    0x1E:['1', '!'],
    0x1F:['2', '@'],
    0x20:['3', '#'],
    0x21:['4', '$'],
    0x22:['5', '%'],
    0x23:['6', '^'],
    0x24:['7', '&'],
    0x25:['8', '*'],
    0x26:['9', '('],
    0x27:['0', ')'],
    0x28:['\n','\n'],
    0x29:['␛','␛'],
    0x2a:['⌫', '⌫'],
    0x2b:['\t','\t'],
    0x2C:[' ', ' '],
    0x2D:['-', '_'],
    0x2E:['=', '+'],
    0x2F:['[', '{'],
    0x30:[']', '}'],
    0x32:['#','~'],
    0x33:[';', ':'],
    0x34:['\'', '"'],
    0x36:[',', '<'],
    0x37:['.', '>'],
    0x38:['/', '?'],
    0x39:['⇪','⇪'],
    0x4f:[u'→',u'→'],
    0x50:[u'←',u'←'],
    0x51:[u'↓',u'↓'],
    0x52:[u'↑',u'↑']
}


#tshark -r ./usb.pcap -Y 'usb.capdata && usb.data_len == 8' -T fields -e usb.capdata | sed 's/../:&/g2' > keyboards.txt
def read_use(file):
    with open(file, 'r') as f:
        datas = f.readlines()
    
    datas = [d.strip() for d in datas if d] 
    cursor_x = 0
    cursor_y = 0
    lines = []
    output = ''
    skip_next = False
    lines.append("")
    
    for data in datas:
        shift = int(data.split(':')[0], 16) # 0x2 is left shift 0x20 is right shift
        key = int(data.split(':')[2], 16)

        if skip_next:
            skip_next = False
            continue
        
        if key == 0 or int(data.split(':')[3], 16) > 0:
            continue
        
        #If you don't like output get a more verbose output here (maybe you need to map new rekeys or remap some of them)
        if not key in KEY_CODES:
            #print("Not found: "+str(key))
            continue
        
        if shift != 0:
            shift=1
            skip_next = True

        if KEY_CODES[key][shift] == u'↑':
            lines[cursor_y] += output
            output = ''
            cursor_y -= 1
        
        elif KEY_CODES[key][shift] == u'↓':
            lines[cursor_y] += output
            output = ''
            cursor_y += 1

        elif KEY_CODES[key][shift] == u'→':
            cursor_x += 1

        elif KEY_CODES[key][shift] == u'←':
            cursor_x -= 1

        elif KEY_CODES[key][shift] == '\n':
            lines.append("")
            lines[cursor_y] += output
            cursor_x = 0
            cursor_y += 1
            output = ''

        elif KEY_CODES[key][shift] == '[BACKSPACE]':
            output = output[:cursor_x-1] + output[cursor_x:]
            cursor_x -= 1
        
        else:
            output = output[:cursor_x] + KEY_CODES[key][shift] + output[cursor_x:]
            cursor_x += 1
    
    if lines == [""]:
        lines[0] = output
    
    if output != '' and output not in lines:
        lines[cursor_y] += output
    
    return '\n'.join(lines)

if __name__ == '__main__':
    if len(sys.argv) < 2:
        print('Missing file to read...')
        exit(-1)
    sys.stdout.write(read_use(sys.argv[1]))
```

Run the script and we will get the string to be converted  to MD5.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ python usbkeyboard.py keystrokes.txt      
Rnotepad
Hey, Finally you know the USB packet analysis!

The flag is md5(With_great_power_comes_great_responsibility)

-Spiderman                   
```

Get the  MD5 hash value.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ echo -n With_great_power_comes_great_responsibility | md5sum
7f37b1af11faa23608c7c0a7aef10fa3  -
```

Check out this video does a pretty good walkthrough on a similar challenge as well:&#x20;

{% embed url="https://www.youtube.com/watch?v=EnOgRyio_9Q" %}

Flag: 7f37b1af11faa23608c7c0a7aef10fa3

## Insiders

<figure><img src="../../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.pcap` file.

First, I opened it  in WIreshark to briefly look through the packets.

Upon  initial analysis, I saw some TLS packets while scrolling.

Next, I checked if leaked file could be transferred by HTTPS which uses SSL.

<figure><img src="../../../.gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>

As I  looked further  into the packets, the cipher suite used was `ECDHE`, which meant that the data cannot be decrypted because the session keys are not derived from private key.

<figure><img src="../../../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

At this point, I unlocked a hint which pointed to ICMP:

<figure><img src="../../../.gitbook/assets/image (116).png" alt=""><figcaption></figcaption></figure>

I found a pretty basic blog which covered pcap ctf  challenges [here](https://www.packetsafari.com/blog/2023/01/13/ctf-pcap-challenges/).

I filtered by: `icmp`

<figure><img src="../../../.gitbook/assets/image (112).png" alt=""><figcaption></figcaption></figure>

Note that we can also filter by `icmp.type == 8`  to  display echo request packets only, but I realized that all icmp packets were echo request and there were no echo reply, hence I simply used icmp as filter.

Checking the first packet's ICMP data section shows there’s PDF

<figure><img src="../../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

If we filter by `frame contains PDF-` we will see it too

<figure><img src="../../../.gitbook/assets/image (114).png" alt=""><figcaption></figcaption></figure>

Going back to our filtered icmp packets, the first packet showed the start of the PDF file. If we went through the rest of the ICMP packets, we will see that we need to combine all these data in the packets to form a PDF file.

The last packet showed the last part of a PDF file as denoted by `%%EOF`.

<figure><img src="../../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

From here, I will be covering two methods to get the hex data of this PDF file. One using `Scapy` and  the other using  `tshark` command.

We previously filtered by `icmp`. Now, we can `CTRL+A` to select all packets and `file > Export Specified Packets > Save as : icmp.pcap`

Next, we will launch `Scapy`.

<figure><img src="../../../.gitbook/assets/image (84) (2).png" alt=""><figcaption></figcaption></figure>

In scapy, we can view the first packet and we will see that it has PDF with version 1.7 showed as well.

```bash
>>> from scapy.all import *
>>> ps = rdpcap("icmp.pcap")
>>> ps
<icmp.pcap: TCP:0 UDP:0 ICMP:21581 Other:0>
>>> ps[0]
<Ether  dst=00:0c:29:70:db:d9 src=00:0c:29:8a:4c:5f type=IPv4 |<IP  version=4 ihl=5 tos=0x0 len=428 id=1 flags= frag=0 ttl=64 proto=icmp chksum=0xf6f8 src=192.168.0.129 dst=192.168.0.134 |<ICMP  type=echo-request code=0 chksum=0xd69c id=0x0 seq=0x0 |<Raw  load='%PDF-1.7\n%\xe2\xe3\xcf\xd3\n1 0 obj\n<</Subtype/XML/Type/Metadata/Length 0>>stream\n\nendstream\nendobj\n2 0 obj\n<</Thumb 3 0 R/Resources<</ColorSpace<</CS0 4 0 R>>/ExtGState<</GS0 5 0 R>>/ProcSet[/PDF/Text]/Font<</TT1 6 0 R/TT2 7 0 R/TT0 8 0 R>>/XObject<</Fm0 9 0 R/Fm1 10 0 R>>>>/Annots 11 0 R/Parent 12 0 R/Rotate 0/MediaBox[0.0 0.0 612.0 792.0]/Tabs/W/Contents 13 0 R/BleedBox[0.0 0.0 612.0 792.0]/Type/Page/ArtBox' |>>>> 
>>> ps[0].show
<bound method Packet.show of <Ether  dst=00:0c:29:70:db:d9 src=00:0c:29:8a:4c:5f type=IPv4 |<IP  version=4 ihl=5 tos=0x0 len=428 id=1 flags= frag=0 ttl=64 proto=icmp chksum=0xf6f8 src=192.168.0.129 dst=192.168.0.134 |<ICMP  type=echo-request code=0 chksum=0xd69c id=0x0 seq=0x0 |<Raw  load='%PDF-1.7\n%\xe2\xe3\xcf\xd3\n1 0 obj\n<</Subtype/XML/Type/Metadata/Length 0>>stream\n\nendstream\nendobj\n2 0 obj\n<</Thumb 3 0 R/Resources<</ColorSpace<</CS0 4 0 R>>/ExtGState<</GS0 5 0 R>>/ProcSet[/PDF/Text]/Font<</TT1 6 0 R/TT2 7 0 R/TT0 8 0 R>>/XObject<</Fm0 9 0 R/Fm1 10 0 R>>>>/Annots 11 0 R/Parent 12 0 R/Rotate 0/MediaBox[0.0 0.0 612.0 792.0]/Tabs/W/Contents 13 0 R/BleedBox[0.0 0.0 612.0 792.0]/Type/Page/ArtBox' |>>>>>       
```

We can use ps\[0].load to see the first packet data

```bash
>>> ps[0].load
b'%PDF-1.7\n%\xe2\xe3\xcf\xd3\n1 0 obj\n<</Subtype/XML/Type/Metadata/Length 0>>stream\n\nendstream\nendobj\n2 0 obj\n<</Thumb 3 0 R/Resources<</ColorSpace<</CS0 4 0 R>>/ExtGState<</GS0 5 0 R>>/ProcSet[/PDF/Text]/Font<</TT1 6 0 R/TT2 7 0 R/TT0 8 0 R>>/XObject<</Fm0 9 0 R/Fm1 10 0 R>>>>/Annots 11 0 R/Parent 12 0 R/Rotate 0/MediaBox[0.0 0.0 612.0 792.0]/Tabs/W/Contents 13 0 R/BleedBox[0.0 0.0 612.0 792.0]/Type/Page/ArtBox' 
```

The above is just covering  the basics of Scapy (not really needed  to solve the challenge). Scapy might be a little complicated where we have to run this to save the hex data to a file

```bash
>>> from scapy.all import *
>>> ps = rdpcap("icmp.pcap")
>>> pdf_data = b"".join(packet.load for packet in ps[:21581])  # Join the .load data
...: pdf_data_hex = pdf_data.hex()  # Convert the data to hexadecimal representation
...: 
...: # Save the hexadecimal data to a file
...: file_path = "hex_data.txt"  # Specify the path and filename for the output file
...: 
...: with open(file_path, "w") as file:
...:     file.write(pdf_data_hex)
...: 
...: print("Hexadecimal data saved to", file_path)
Hexadecimal data saved to hex_data.txt
```

Alternatively, the other method is to use tshark command as such to extract all ICMP data.

* \-r \<input\_file>: Specifies the input file from which you want to extract ICMP data. Replace \<input\_file> with the path to your capture file (e.g., capture.pcap).
* \-Y "icmp": Filters the captured packets to only include ICMP packets.
* \-T fields: Specifies the output format as individual fields.
* \-e data: Specifies the specific field to extract, in this case, the data field of the ICMP packets.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ tshark -r prob.pcap -Y "icmp" -T fields -e data > hexpdf.txt
```

Next, we load this file: `hexpdf.txt` into [CyberChef ](https://cyberchef.org/#recipe=From\_Hex\('Auto'\))and convert from hex, followed by saving it as a PDF file.

<figure><img src="../../../.gitbook/assets/image (50) (6).png" alt=""><figcaption></figcaption></figure>

We can open the pdf file and we will see a PDF file related to Cisco 2023 Data Privacy Benchmark Study.

Find the SHA1 of this file  to get the flag.

```
┌──(kali㉿kali)-[~/Downloads]
└─$ sha1sum flag.pdf 
9a8f4bd1c07e53d7996586fa875b7e21f4b93c1e  flag.pdf
```

Flag: 9a8f4bd1c07e53d7996586fa875b7e21f4b93c1e

## Private&#x20;

<figure><img src="../../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

For this challenge, I unlocked a hint which pointed to  `network analysis (torrent)`.

<figure><img src="../../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

Before  I unlocked the hint, I followed the `UDP` stream. However, I did not find any useful information.

<figure><img src="../../../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>

Next, I followed the `TCP` stream. In the first few streams, I thought that the value of `h` was the  info hash. I later realized it's not.

<figure><img src="../../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>

At stream  88,  I found the IP address of the tracker server and what I thought was the info hash as well.

<figure><img src="../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

Similarly, on stream 110, I found the same info\_hash value

<figure><img src="../../../.gitbook/assets/image (117).png" alt=""><figcaption></figcaption></figure>

However, even after removing the `%` in between the value, it was still incorrect.

At this point, I went ahead  to do further research and came across this [good read](https://www.malware-traffic-analysis.net/2013/09/14/index.html) on malware traffic analysis.

After reading, I used the search filter to filter by: `bittorrent.info_hash` in  Wireshark.

<figure><img src="../../../.gitbook/assets/image (17) (6).png" alt=""><figcaption></figcaption></figure>

Looking into this packet showed the info hash, which is under the `SHA1 Hash of info dictionary`.

<figure><img src="../../../.gitbook/assets/image (108).png" alt=""><figcaption></figcaption></figure>

We can get the `info_hash by` right clicking  and copying the value

Finally, the flag is the `SHA1` of the information (i.e. IP address and information hash) we acquired.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ echo -n ac6d15fb79d4a413b37328fbeffe3bb001cab080_3.35.175.197 | sha1sum
1e19a3f32b1b56eb1fdf717d2b0900a315ba070b  -
```

Flag: 1e19a3f32b1b56eb1fdf717d2b0900a315ba070b

## Find My Ports

<figure><img src="../../../.gitbook/assets/image (115).png" alt=""><figcaption></figcaption></figure>

For this challenge, we need to find the opened ports in a packet capture file.

<figure><img src="../../../.gitbook/assets/image (11) (5).png" alt=""><figcaption></figcaption></figure>

There are many ports to check. One way we could do the checking is to apply filter on the destination ports, by right clicking and `Apply as filter > Selected`.

<figure><img src="../../../.gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>

Change `tcp.dstport == {port number}` to `tcp.port == {port number}`

From here, we could try different port numbers

We can see that port 21 is closed.

<figure><img src="../../../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>

Port 22, which is the port for SSH is open. There is full TCP handshake, SYN, SYN-ACK, ACK.

<figure><img src="../../../.gitbook/assets/image (113).png" alt=""><figcaption></figcaption></figure>

Port 80, which is the port for HTTP is open. There is full TCP handshake, SYN, SYN-ACK, ACK.

<figure><img src="../../../.gitbook/assets/image (92).png" alt=""><figcaption></figcaption></figure>

Finally, port 443, which is the port for HTTPS is open. There is full TCP handshake, SYN, SYN-ACK, ACK.

<figure><img src="../../../.gitbook/assets/image (19) (4).png" alt=""><figcaption></figcaption></figure>

Combine the three ports with underscore and convert to MD5 to get the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ echo -n 22_80_443 | md5sum 
b7e52801b09fa7ae0f22dc7f33696d39 -
```

Flag: b7e52801b09fa7ae0f22dc7f33696d39

## Can you log in?

<figure><img src="../../../.gitbook/assets/image (18) (3).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a challenge link.

We can first browse to the link with port number 9103: [http://3.38.185.151:9103/](http://3.38.185.151:9103/)

Next, lets take a look at the source code

````html
```


<!DOCTYPE html>
	<html>
	<head>
	<title>Security Centre</title>
	</head>
	<body>
	<h1>HELLO SECURITY CENTRE</h1>
	This Page is not working....
	<!-- '/cred' -->
	</body>
	</html>
	

```
````

Notice there is a `/cred` path commented out.

Using curl command, we could get what seemed to be a list of usernames(since the password is already given in this challenge):

```bash
┌──(kali㉿kali)-[~]
└─$ curl 3.38.185.151:9103/cred 
ihunter
cherry
killer
sandra
alejandro
buster
george
brittany
alejandra
patricia
rachel
tequiero
7777777
cheese
159753
arsenal
dolphin
antonio
heather
david
ginger
stephanie
peanut
blink182
sweetie
222222
beauty
987654
victoria
honey
00000
fernando
pokemon
glory
maggie
corazon
chicken
pepper
cristina
rainbow
kisses
manuel
myspace
rebelde
angel1
ricardo
babygurl
heaven
55555
baseball
martin
greenday
november
alyssa
madison
mother
```

Again, since the password to ssh was already given for this challenge, we will just need to use this wordlist provided in `/cred` to brute force the username.

Let's save this username wordlist to a file called `username.txt`

```bash
┌──(kali㉿kali)-[~]
└─$ curl 3.38.185.151:9103/cred > username.txt
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   433  100   433    0     0   2347      0 --:--:-- --:--:-- --:--:--  2353

```

Check that we have the wordlist in `username.txt`

```bash
┌──(kali㉿kali)-[~]
└─$ cat username.txt                          
ihunter
cherry
killer
sandra
alejandro
buster
george
brittany
alejandra
patricia
rachel
tequiero
7777777
cheese
159753
arsenal
dolphin
antonio
heather
david
ginger
stephanie
peanut
blink182
sweetie
222222
beauty
987654
victoria
honey
00000
fernando
pokemon
glory
maggie
corazon
chicken
pepper
cristina
rainbow
kisses
manuel
myspace
rebelde
angel1
ricardo
babygurl
heaven
55555
baseball
martin
greenday
november
alyssa
madison
mother
```

Now that we have username.txt, we can brute force the username using Hydra

The commonly used options for Hydra  are:\
\-l == single login / username

\-L == file containing list of usernames, one per line

\-p == single password

\-P == file containing list of passwords, one per line

\-s == port number

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ hydra -L username.txt -p glory 3.38.185.151 ssh -s 5891
Hydra v9.3 (c) 2022 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2023-05-18 03:31:20
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[WARNING] Restorefile (you have 10 seconds to abort... (use option -I to skip waiting)) from a previous session found, to prevent overwriting, ./hydra.restore
[DATA] max 16 tasks per 1 server, overall 16 tasks, 58 login tries (l:58/p:1), ~4 tries per task
[DATA] attacking ssh://3.38.185.151:5891/
[5891][ssh] host: 3.38.185.151   login: cristina   password: glory
1 of 1 target successfully completed, 1 valid password found
[WARNING] Writing restore file because 1 final worker threads did not complete until end.
[ERROR] 1 target did not resolve or could not be connected
[ERROR] 0 target did not complete
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2023-05-18 03:31:35
```

With this, we’ve successfully cracked the username: `cristina` and we can now ssh into the server.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ ssh -p 5891 cristina@3.38.185.151
cristina@3.38.185.151's password: 
Last login: Thu May 18 07:33:07 2023 from 202.90.244.90
```

Once we are in, we navigate to the flag directory containing flag.txt

```bash
cristina@de9a540efc85:~$ ls
bin  flag  white_list_command
cristina@de9a540efc85:~$ cd flag
cristina@de9a540efc85:~/flag$ ls
flag.txt
```

However, `cat` command cannot be used to read the flag and we are unable to change permissions as well.

```bash
cristina@de9a540efc85:~/flag$ cat flag.txt 
-bash: /usr/bin/cat: Permission denied
cristina@de9a540efc85:~/flag$ chmod +x flag.txt 
chmod: changing permissions of 'flag.txt': Operation not permitted
```

We can use the `tac` command to read the flag. I previously solved [another challenge](https://gadiel-lau.gitbook.io/2023-writeups/2023-ctfs/dsta-brainhack-cyber-defenders-discovery-camp-training-2023/basic-concepts-of-cybersecurity/fundamentals-of-linux#2-intermediate-terminal-practice) in CDDC  training 2023 using this command as well.

```bash
cristina@de9a540efc85:~/flag$ tac flag.txt 
512bad81faf8db0bf9a80a68efdc8525
```

Flag: 512bad81faf8db0bf9a80a68efdc8525

## Subnet

<figure><img src="../../../.gitbook/assets/image (88) (3).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was quite similar to previous [CDDC 2022 training](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/dsta-brainhack-cyber-defenders-discovery-camp-training-2022/ctf-topics/network-security#network-divider).

However,  instead of getting 10 correct answers consecutively to get the flag, we  will need to get 50 in a row correct before getting the flag.

Initially, I  tried a different approach by using CHATGPT. However, after around 19 rounds, I got one incorrect.

<figure><img src="../../../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

I decided to go back to the old school method by using this subnet calculator: [https://www.calculator.net/ip-subnet-calculator.html](https://www.calculator.net/ip-subnet-calculator.html)

However, after a few tries, I encountered some human error.

Finally, I decided to search for another tool which allowed copy and paste of subnet mask instead of manually searching for it through drop-down list.

This is when I found: [https://planetcalc.com/1669/](https://planetcalc.com/1669/)

Using this, I  can copy and paste IP into network address and subnet mask accordingly and we would get the subnet which is under `Network`.

<figure><img src="../../../.gitbook/assets/image (90).png" alt=""><figcaption></figcaption></figure>

Getting 50 in a row correct required a certain level of focus for the repetition of task. At times, it can be quite annoying when I pressed CTRL+C instead of CTRL+SHIFT+C on terminal to copy which terminated the connection:

<figure><img src="../../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

After couple of minutes of copy pasting, I finally got the flag.

```bash
46 round Correct
IP = 117.86.72.206
SUBNET MASK = 255.255.255.224
SUBNET >> 117.86.72.192
47 round Correct
IP = 230.123.234.219
SUBNET MASK = 255.0.0.0
SUBNET >> 230.0.0.0
48 round Correct
IP = 53.197.115.156
SUBNET MASK = 224.0.0.0
SUBNET >> 32.0.0.0
49 round Correct
IP = 114.29.68.151
SUBNET MASK = 255.255.255.240
SUBNET >> 114.29.68.144
50 round Correct
FLAG is 8bd6201e1860f10bd6a2488d8a7ab436
```

Flag: 8bd6201e1860f10bd6a2488d8a7ab436

