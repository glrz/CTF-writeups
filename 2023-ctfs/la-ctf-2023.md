---
description: >-
  LA CTF is an annual Capture the Flag (CTF) cybersecurity competition hosted by
  ACM Cyber at UCLA & Psi Beta Rho. It was held from 11 Feb - 13 Feb 2023.
---

# LA CTF 2023

More information about the event can be found [here](https://ctftime.org/event/1732).

For this CTF, I participated with team [`Social Engineering Expert`](https://ctftime.org/team/151372) and we obtained the position of `8/980` teams. Pretty satisfied with the results and definitely learned a lot from interacting with my teammates as well.

<figure><img src="../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

I managed to dedicate some time during the weekend to solve quite a number of challenges in categories such as MISC(OSINT, Forensics) and Cryptography.

Overall, I enjoyed this CTF and learned more about how data could be "extracted" from hidden sheets in `Google docs` despite having view only access and no permissions to make a copy of  the file. These challenges helped me to think critically and improved my problem-solving skills.

## discord

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was similar to previous `Welcome` or `Sanity Check` types of challenges, where the flag could be found easily. The challenge is mainly for us to familiarize with the flag format.&#x20;

In this case, the flag was in the Discord server. Upon joining the server, we could go to the FAQ channel, click on the top bar beside the channel name, and we would see the flag.\


<figure><img src="../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

Flag: lactf{i\_joined\_discord\_and\_read\_the\_faq}

## hidden in plain sheets&#x20;

<figure><img src="../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

For this challenge, I found it to be very interesting. It was in the misc category and it's likely to be forensics related. We were given a [link](https://docs.google.com/spreadsheets/d/1OYx3lCccLKYgOvzxkRZ5-vAwCn3mOvGUvB4AdnSbcZ4/edit) to a `Google docs excel sheet`. However, only `view only` permission is allowed and `make a copy` has been disabled.&#x20;

I looked around the sheets and found that there was a `flag` sheet being protected or hidden.\


<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

Next, I went online to search for a way to unhide protected sheets in Google docs and found [this](https://blog.golayer.io/google-sheets/how-to-unhide-sheets-in-google-sheets).&#x20;

I tried following the blog, by going to `View` > `Hidden sheets`. However, this did not work either since we only had `view only` permissions.

<figure><img src="../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

If I were to go to bottom right and try to view the flag sheet, it would not work as well.\


<figure><img src="../.gitbook/assets/image (7) (2).png" alt=""><figcaption></figcaption></figure>

While searching online, I found this [YouTube video ](https://www.youtube.com/watch?v=FOs-LjXw2Q0)which briefly covered the use of `Find and Replace` function to search for hidden data in hidden sheets.

I proceeded to try this by going to `Edit > Find and replace`. Alternatively, we could use the keyboard shortcut: `CTRL+H`.

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

Next, I tried to Find `L` which is the first letter for the flag, since the flag format is `lactf{}`. Indeed, I was able to find this value in the hidden sheet under Cell `A1`.

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

Next, I tried to find the next letter, which is `a`. I found it in the flag sheet again, this time under Cell `B1`.

<figure><img src="../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

Next, I moved on to the third letter for the flag, which is `c`. I found it at Cell `C1`.

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

Next, the fourth letter of the flag, which is `t` was found on Cell `D1`.

<figure><img src="../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

Next, the fifth letter of the flag, which is `f` was found on Cell `E1`.

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

The next character which is `{` was found on Cell `F1`.

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

At this point, we would probably have realized that the flag is very likely to be hidden horizontally on the first row of the sheet, with each letter on a cell, since it goes from A1, B1, C1 ... F1.

However, I soon realized that by searching each character on the keyboard, it was not able to tell me whether there were duplicates of the character in another cell. Using this method of searching, I was only able to find a few other characters of the flag.&#x20;

<figure><img src="../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

Finally, I searched for the ending brace `}` for the flag which was found in Cell `AR1`.

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

If I were to join all the information gathered above based on the alphabet or cell sequence, I would get: `lactf{H1d3n_prO5}`.  However, this was not the flag.

At this point, it became quite clear to me that I needed to find the duplicated alphanumeric characters that were not found in the other cells.

I saw that the `Find and Replace` function allowed the use of `regular expressions`. Hence, I decided to use a `regex` : `^[a-z0-9]*` to search for all possible alphanumeric characters.

I changed the Search from `All sheets` to `Specific Range`. Using the `regex`, and specifying the search to search for those missing cells, I was able to find the other duplicated characters that I was missing.

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

For example, here I am specifying to search the hidden `flag` sheet on Cell `T1` for the alphanumeric character. I get the result which is a value of `3`.

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (37) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

After I had all the alphanumeric characters gathered from cell `A1` to cell `Z1`, I targeted cells `AA1` to `AR1` individually. I already knew the last cell would likely be `AR1` from the closing brace found earlier.

<figure><img src="../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption><p><br></p></figcaption></figure>

By joining all the values above from `A1` to `AR1`, we will get the flag. Essentially, I could have used `Regex` to target Cell `A1` to `AR1` from the beginning to solve this challenge faster.&#x20;

After solving it, I did try specifying a range from `A1 to AR1` using Regex to see if it's possible to search through all the cells in the range sequentially so that it would be much faster. However, this did not work.\


<figure><img src="../.gitbook/assets/image (70).png" alt=""><figcaption><p>Partially broken which did not work</p></figcaption></figure>

This process of finding the flag by searching in each individual cell was quite tedious. After the competition, I found an alternative way which was much easier.&#x20;

By running this script, it can be solved in [Google Apps Script](https://www.google.com/script/start/).

```javascript
function myFunction() {
  const sheet = SpreadsheetApp.openById("1OYx3lCccLKYgOvzxkRZ5-vAwCn3mOvGUvB4AdnSbcZ4");
  const sheets = sheet.getSheets();
  const secret = sheets.find(x => x.getName() == "flag");
  console.log(secret.getDataRange().getValues().map(l => l.join("")).join("\n"));
}
```

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

The last method which I found to solve this challenge was to use [IMPORTRANGE function](https://support.google.com/a/users/answer/9308940?hl=en) to import data from another Google Sheet.

First, we should create an empty spreadsheet.\
Next, we enter the `URL` for the Google Sheet that we want the data imported and specify the range in an empty cell as such\


```
=importrange("https://docs.google.com/spreadsheets/d/1OYx3lCccLKYgOvzxkRZ5-vAwCn3mOvGUvB4AdnSbcZ4","flag!A1:AR1")
```

I found a [YouTube Video](https://www.youtube.com/watch?v=5S7laJS9meU) that was quite useful in explaining this.

By using this `importrange` function, we will see the flag printed in the first row horizontally.\


<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

Next, we could copy the cells from `A1` to `AR1` and paste it in CyberChef. There will  be some space in between but we can use  the `find and replace` [recipe](https://cyberchef.org/#recipe=Find\_/\_Replace\(%7B'option':'Regex','string':'%5Ct'%7D,'',true,false,true,false\)\&input=bAlhCWMJdAlmCXsJSAkxCWQJZAkzCW4JXwkmCV8JcAlyCU8JdAkzCWMJVAkzCUQJXwk1CWgJMwkzCVQJNQlfCUEJcgkzCV8JbgkzCTEJdAloCTMJcgl9) to get the flag.

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Flag: lactf{H1dd3n\_&\_prOt3cT3D\_5h33T5\_Ar3\_n31th3r}

## EBE

<figure><img src="../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was in the misc category and likely to be network forensics related. First, we could open the `.pcap` file in `Wireshark` and analyze its contents. Upon opening in Wireshark, we would see a bunch of `UDP` packets.\


<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

We could get the header checksum for all these packets using a simple script that uses `Scapy`.&#x20;

The final two bytes of the UDP header is the checksum, a field that's used by the sender and receiver to check for data corruption.

By using the simple script below, I was able to extract the header checksum from all the packets.

```python
from scapy.all import *

# Load the pcap file
packets = rdpcap("your_capture_file.pcap")

# Extract header checksum values from all packets
for pkt in packets:
    if IP in pkt and pkt[IP].chksum:
        chksum = pkt[IP].chksum
        print(f"Header checksum: {hex(chksum)}")
```

After analyzing these header checksum, we would see that there are 2 checksums: `0xe4c0` and `0x64c1`.

```
┌──(kali㉿kali)-[~/Downloads]
└─$ python extract_checksum.py
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0x64c1
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0xe4c0
Header checksum: 0x64c1

```

By running another script that uses `Scapy`, we can extract the payload of each filtered packet and decode the concatenated payloads as ASCII text, which will give us the flag.

```python
from scapy.all import *

# Load the pcap file
packets = rdpcap("EBE.pcap")

# Filter the packets to only include those sent from source IP 10.0.1.10 to destination IP 10.0.1.5 over UDP with header checksum 0x64c1
filtered_packets = [pkt for pkt in packets if pkt.haslayer(UDP) and pkt[IP].src == "10.0.1.10" and pkt[IP].dst == "10.0.1.5" and pkt[IP].chksum == 0x64c1]

# Extract the payload of each filtered packet and concatenate into a single string
payloads = b''.join([bytes(pkt[UDP].payload) for pkt in filtered_packets])

# Decode the concatenated payloads as ASCII text
text = payloads.decode('ascii')

print(text)
```

Running this script will give us the flag.\


```
┌──(kali㉿kali)-[~/Downloads]
└─$ python script.py
lactf{3V1L_817_3xf1l7R4710N_4_7H3_W1N_51D43c8000034d0c}
```

<figure><img src="../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

Flag: lactf{3V1L\_817\_3xf1l7R4710N\_4\_7H3\_W1N\_51D43c8000034d0c}

## rolling in the mud

<figure><img src="../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was under the `crypto` category. Upon reading the first few words of the description, I kind of knew this was probably `PigPen Cipher` because I had solved such similar challenge before [here](https://gadiel-lau.gitbook.io/2021-writeup/2021-ctfs/lagncrash-interpoly-ctf-2021#pigs-can-write).

We were give a `cipher.png` file. Upon opening it, we get this image.\


<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

This looked similar to `PigPen cipher`. However, I quickly noticed something was quite off, that is this image looked inverted or rather rotated. How did I know? The opening and closing braces gave it away. We can see on the top-left that it starts with the opening brace which does not quite make any sense.\


Hence, I tried rotating this image and I got this. Now, this looked more like the encoded flag.\


<figure><img src="../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

I proceeded to decode it manually [here](https://www.dcode.fr/pigpen-cipher). After selecting all the characters manually and matching it with the image, I will get the following result.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

I then converted the flag to all small letters in `Word` using the `SHIFT+F3` shortcut, which gives me the flag.

Flag: lactf{rolling\_and\_rolling\_and\_rolling\_until\_the\_pigs\_go\_home}

## hike to where?

<figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was in the misc category, most probably `OSINT` related. I think I solved it with an unintended solution.

We were given this image which looked like it was cropped.&#x20;

<figure><img src="../.gitbook/assets/picture.jpg" alt=""><figcaption></figcaption></figure>

We basically had to find the location of this place. However, I tried some simple `reverse image search` but could not find anything. Next, I thought we could probably use `Google maps`, but where in Google maps do we start searching? There were way too many hiking spots to search around.&#x20;

At some point, a thought struck me. I thought.. what if I could search for the name of this person first? Then, perhaps he could have posted this on his social media and I could find the original image or even information about the place that he hiked to.

I suddenly recalled that this person was one of the speakers for the `LACTF 2023` event. He was also an adjunct lecturer at UCLA.

By going to the official `LACTF` website, I was able to find his name under one of the speakers.

<figure><img src="../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

With this information, I went to `Google` to search for  `Carey Nachenberg`, and found his [personal blog](http://careynachenberg.weebly.com/rock-climbing.html). On the site, it contained several pictures of him doing mountain climbing, however none of it matches the one for this challenge.&#x20;

I also saw that he was climbing the `Santa Monica Mountain`.

<figure><img src="../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

However, this was not the flag. I guess one could possibly search for possible hiking routes from `Santa Monica Mountains` but it would probably take quite some time to find the flag using `Google maps`.

For me, I just searched for `where carey nachenberg hiked to` and found this [site](https://www.tickettailor.com/events/peaksprofessorsatucla/792649).

<figure><img src="../.gitbook/assets/image (2) (4).png" alt=""><figcaption></figcaption></figure>

Upon browsing the site, I can see that it mentioned `We'll stop at Skull Rock to take in the views`. That was the flag, the location was at `Skull Rock`.

<figure><img src="../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

Flag: lactf{skull\_rock}

## feedback

<figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

This was a feedback challenge. Normally, closing to the end of each CTF competition, there will be this challenge for participants to give their feedback.\


Typically, the flag will be found at the end of completing the feedback form. However, if we completed it too fast and did not go through the details, we would find ourselves missing `Part 1` and `Part 2` of the flag.\


<figure><img src="../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

If we look closely, `Part 1` of the flag could be found at the top in the description section.\


<figure><img src="../.gitbook/assets/image (58).png" alt=""><figcaption><p>Flag part one : i_give_my</p></figcaption></figure>

For flag part two, I used `CTRL+F` to search through the form and found it under one of the options for `favourite challenge(s)`.

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption><p>Flag Part Two: very_helpful</p></figcaption></figure>

Combining these two parts of the flag, with the final flag at the end of the feedback form, we get the complete flag.

lactf{i\_give\_my\_very\_helpful\_feedback\_and\_i\_actually\_submitted}
