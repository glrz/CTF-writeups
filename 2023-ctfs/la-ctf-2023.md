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

<figure><img src="../.gitbook/assets/image (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../.gitbook/assets/image (22) (2).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../.gitbook/assets/image (18) (1).png" alt=""><figcaption></figcaption></figure>

At this point, we would probably have realized that the flag is very likely to be hidden horizontally on the first row of the sheet, with each letter on a cell, since it goes from A1, B1, C1 ... F1.

However, I soon realized that by searching each character on the keyboard, it was not able to tell me whether there were duplicates of the character in another cell. Using this method of searching, I was only able to find a few other characters of the flag.&#x20;

<figure><img src="../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (38) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (5) (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

Finally, I searched for the ending brace `}` for the flag which was found in Cell `AR1`.

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

If I were to join all the information gathered above based on the alphabet or cell sequence, I would get: `lactf{H1d3n_prO5}`.  However, this was not the flag.

At this point, it became quite clear to me that I needed to find the duplicated alphanumeric characters that were not found in the other cells.

I saw that the `Find and Replace` function allowed the use of `regular expressions`. Hence, I decided to use a `regex` : `^[a-z0-9]*` to search for all possible alphanumeric characters.

I changed the Search from `All sheets` to `Specific Range`. Using the `regex`, and specifying the search to search for those missing cells, I was able to find the other duplicated characters that I was missing.

<figure><img src="../.gitbook/assets/image (33) (2).png" alt=""><figcaption></figcaption></figure>

For example, here I am specifying to search the hidden `flag` sheet on Cell `T1` for the alphanumeric character. I get the result which is a value of `3`.

<figure><img src="../.gitbook/assets/image (23) (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (37) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (27) (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (12) (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (29) (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (6) (2).png" alt=""><figcaption></figcaption></figure>

After I had all the alphanumeric characters gathered from cell `A1` to cell `Z1`, I targeted cells `AA1` to `AR1` individually. I already knew the last cell would likely be `AR1` from the closing brace found earlier.

<figure><img src="../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (13) (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (10) (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (35) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (9) (2).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../.gitbook/assets/image (3) (4).png" alt=""><figcaption></figcaption></figure>

Flag: lactf{H1dd3n\_&\_prOt3cT3D\_5h33T5\_Ar3\_n31th3r}

## EBE

<figure><img src="../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was in the misc category and likely to be network forensics related. First, we could open the `.pcap` file in `Wireshark` and analyze its contents. Upon opening in Wireshark, we would see a bunch of `UDP` packets.\


<figure><img src="../.gitbook/assets/image (20) (3).png" alt=""><figcaption></figcaption></figure>

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

An alternative approach would be to get the hint from the challenge description. From the challenge  description, it mentioned that `those UDP traffics are abided by RFC 3514.`

I found [this](https://dbpedia.org/page/Evil\_bit) which explained about evil bit.

`The evil bit is a fictional IPv4 packet header field proposed in RFC 3514, a humorous April Fools' Day RFC from 2003 authored by Steve Bellovin. The RFC recommended that the last remaining unused bit, the "Reserved Bit" in the IPv4 packet header, be used to indicate whether a packet had been sent with malicious intent, thus making computer security engineering an easy problem – simply ignore any messages with the evil bit set and trust the rest.`

If we take a look at [RFC 3514](https://www.ietf.org/rfc/rfc3514.txt):

```
[...]
2. Syntax

   The high-order bit of the IP fragment offset field is the only unused
   bit in the IP header.  Accordingly, the selection of the bit position
   is not left to IANA.





Bellovin                     Informational                      [Page 1]

RFC 3514          The Security Flag in the IPv4 Header      1 April 2003


   The bit field is laid out as follows:

             0
            +-+
            |E|
            +-+

   Currently-assigned values are defined as follows:

   0x0  If the bit is set to 0, the packet has no evil intent.  Hosts,
        network elements, etc., SHOULD assume that the packet is
        harmless, and SHOULD NOT take any defensive measures.  (We note
        that this part of the spec is already implemented by many common
        desktop operating systems.)

   0x1  If the bit is set to 1, the packet has evil intent.  Secure
        systems SHOULD try to defend themselves against such packets.
        Insecure systems MAY chose to crash, be penetrated, etc.
[...]
```

With the above information, if the IP "reserved bit" is set to 1 (0x1), it is an evil packet.&#x20;

<figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

Hence, to extract the flag, we need to find all the packets that have the Reserved bit `Not set.`

To do so, we can use `Tshark`, a command line version of `Wireshark`.

```
┌──(kali㉿kali)-[~/Downloads]
└─$ tshark -r EBE.pcap -Y "ip.flags.rb == 0x0" -T fields -e data | xxd -r -p
lactf{3V1L_817_3xf1l7R4710N_4_7H3_W1N_51D43c8000034d0c} 
```

Alternatively, we could also use `Scapy` and filter those that have reserved bits not set as such\


```
from scapy.all import *

# Load the pcap file
packets = rdpcap("EBE.pcap")

# Filter the packets to only include those sent from source IP 10.0.1.10 to destination IP 10.0.1.5 over UDP with reserved bits not set (0x0)
filtered_packets = [pkt for pkt in packets if pkt.haslayer(UDP) and pkt[IP].src == "10.0.1.10" and pkt[IP].dst == "10.0.1.5" and (pkt[IP].flags & 0x7) == 0]

# Extract the payload of each filtered packet and concatenate into a single string
payloads = b''.join([bytes(pkt[UDP].payload) for pkt in filtered_packets])

# Decode the concatenated payloads as ASCII text
text = payloads.decode('ascii')

print(text)
```

Flag: lactf{3V1L\_817\_3xf1l7R4710N\_4\_7H3\_W1N\_51D43c8000034d0c}

## rolling in the mud

<figure><img src="../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was under the `crypto` category. Upon reading the first few words of the description, I kind of knew this was probably `PigPen Cipher` because I had solved such similar challenge before [here](https://gadiel-lau.gitbook.io/2021-writeup/2021-ctfs/lagncrash-interpoly-ctf-2021#pigs-can-write).

We were give a `cipher.png` file. Upon opening it, we get this image.\


<figure><img src="../.gitbook/assets/image (25) (1).png" alt=""><figcaption></figcaption></figure>

This looked similar to `PigPen cipher`. However, I quickly noticed something was quite off, that is this image looked inverted or rather rotated. How did I know? The opening and closing braces gave it away. We can see on the top-left that it starts with the opening brace which does not quite make any sense.\


Hence, I tried rotating this image and I got this. Now, this looked more like the encoded flag.\


<figure><img src="../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

I proceeded to decode it manually [here](https://www.dcode.fr/pigpen-cipher). After selecting all the characters manually and matching it with the image, I will get the following result.

<figure><img src="../.gitbook/assets/image (4) (3).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../.gitbook/assets/image (30) (2).png" alt=""><figcaption><p>Flag Part Two: very_helpful</p></figcaption></figure>

Combining these two parts of the flag, with the final flag at the end of the feedback form, we get the complete flag.

lactf{i\_give\_my\_very\_helpful\_feedback\_and\_i\_actually\_submitted}

## a hacker's note

<figure><img src="../.gitbook/assets/image (2) (5).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was under the misc category, most likely a Forensics challenge from the challenge description. I partially solved this during the competition but nonetheless decided to include it for documentation purposes.\


We were given a zip file for this challenge.

{% file src="../.gitbook/assets/hackers-drive.dd.zip" %}

FIrst, lets unzip this file.

```
┌──(kali㉿kali)-[~/Downloads]
└─$ unzip hackers-drive.dd.zip 
Archive:  hackers-drive.dd.zip
  inflating: hackers-drive.dd
```

Upon unzipping the file, we get the `hackers-drive.dd` file. The `.dd` file suggest that this is likely a disk  image file.

We can run the `file` command to check the file type. As we can see, this file has been encrypted as stated in the challenge description as well.

```
┌──(kali㉿kali)-[~/Downloads]
└─$ file hackers-drive.dd
hackers-drive.dd: LUKS encrypted file, ver 1 [twofish, cbc-plain, sha1] UUID: 456aa573-ab59-4146-a2f3-874a808b9c08
```

From the challenge description, we know that the organization uses password in the format of `hacker###` (hacker + 3 digits).

With this information, we can construct a wordlist using `Crunch`. This will effectively  generate the wordlist: `hacklist` with the words ranging from `hacker000` to `hacker999`.

```
┌──(kali㉿kali)-[~/Downloads]
└─$ crunch 9 9 -t hacker%%% -o hacklist               
Crunch will now generate the following amount of data: 10000 bytes
0 MB
0 GB
0 TB
0 PB
Crunch will now generate the following number of lines: 1000 

crunch: 100% completed generating output
```

For more information on how to use `Crunch`, you could also check out my other [writeup ](https://gadiel-lau.gitbook.io/2022-writeups/2022-ctfs/dsta-brainhack-cyber-defenders-discovery-camp-ctf-2022/network#wifi)where I used crunch to solve a challenge.

After the `hacklist` has been generated, we can use `hashcat` to perform a dictionary attack by using the `hacklist`.

Note  that  `-m 14600` sets the mode to `LUKS`. The cracked password is : `hacker765`.

```
┌──(kali㉿kali)-[~/Downloads]
└─$ hashcat -m 14600 hackers-drive.dd hacklist 
hashcat (v6.2.5) starting

OpenCL API (OpenCL 3.0 PoCL 3.0+debian  Linux, None+Asserts, RELOC, LLVM 13.0.1, SLEEF, DISTRO, POCL_DEBUG) - Platform #1 [The pocl project]
============================================================================================================================================
* Device #1: pthread-11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz, 2921/5907 MB (1024 MB allocatable), 2MCU

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Optimizers applied:
* Zero-Byte
* Single-Hash
* Single-Salt
* Slow-Hash-SIMD-LOOP

Watchdog: Temperature abort trigger set to 90c

Host memory required for this attack: 0 MB

Dictionary cache hit:
* Filename..: hacklist
* Passwords.: 1000
* Bytes.....: 10000
* Keyspace..: 1000

hackers-drive.dd:hacker765                                
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 14600 (LUKS)
Hash.Target......: hackers-drive.dd
Time.Started.....: Sat Feb 11 08:51:16 2023 (4 secs)
Time.Estimated...: Sat Feb 11 08:51:20 2023 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (hacklist)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:      232 H/s (14.44ms) @ Accel:64 Loops:1024 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests
Progress.........: 768/1000 (76.80%)
Rejected.........: 0/768 (0.00%)
Restore.Point....: 640/1000 (64.00%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:1024-1085
Candidate.Engine.: Device Generator
Candidates.#1....: hacker640 -> hacker767
Hardware.Mon.#1..: Util: 98%

Started: Sat Feb 11 08:51:16 2023
Stopped: Sat Feb 11 08:51:21 2023
```

From here, we can find out more information about the `.dd`  file.

```
┌──(kali㉿kali)-[~/Downloads]
└─$ cryptsetup luksDump hackers-drive.dd
LUKS header information for hackers-drive.dd

Version:        1
Cipher name:    twofish
Cipher mode:    cbc-plain
Hash spec:      sha1
Payload offset: 4096
MK bits:        256
MK digest:      ef 65 75 d0 72 2f 19 65 ad 19 06 88 06 23 79 f5 54 21 de 64 
MK salt:        43 b8 26 2c a8 34 4e 77 45 f3 c7 3d a3 2a 15 22 
                42 0b 69 46 72 a8 d1 99 0a 33 18 a7 4d 3a 5c ac 
MK iterations:  136000
UUID:           456aa573-ab59-4146-a2f3-874a808b9c08

Key Slot 0: ENABLED
  Iterations:           1086
  Salt:                 d6 78 a6 ea 22 07 0a b7 21 7c 79 79 ab d8 b8 25 
                         f4 62 b0 55 bf af 55 26 43 4c f2 ba 7f 91 4c cb 
  Key material offset:  8
  AF stripes:                  4000
Key Slot 1: DISABLED
Key Slot 2: DISABLED
Key Slot 3: DISABLED
Key Slot 4: DISABLED
Key Slot 5: DISABLED
Key Slot 6: DISABLED
Key Slot 7: DISABLED
```

From here, we could decrypt the file as such\


```
┌──(kali㉿kali)-[~/Downloads]
└─$ sudo cryptsetup -v luksOpen hackers-drive.dd data
[sudo] password for kali: 
Enter passphrase for hackers-drive.dd: 
Key slot 0 unlocked.
Command successful.
```

Next,  we could mount it to our system by clicking on the  `18MB  Volume`.

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

We could then run the `ls -la` command to list  all the files, including hidden or temporary files.

&#x20;

```
┌──(kali㉿kali)-[/media/kali/ed1c79a8-8148-4ce2-b482-91334a211dc9]
└─$ ls -la
total 24
drwxr-xr-x  7 kali steve  1024 Jan 15 21:38 .
drwxr-x---+ 3 root root   4096 Feb 14 02:18 ..
-rw-------  1 kali steve   190 Jan 15 21:38 .bash_history
drwxr-xr-x  3 kali steve  1024 Jan 15 20:06 .config
drwx------  2 kali steve  1024 Jan 15 20:09 .emacs.d
drwxr-xr-x  7 kali steve  1024 Jan 15 20:12 encrypted-notes
drwxr-xr-x  3 kali steve  1024 Jan 15 19:50 .local
drwx------  2 root root  12288 Jan 15 21:37 lost+found
-rw-r--r--  1 kali steve   150 Jan 15 20:35 note_to_self.txt
-rw-------  1 kali steve   705 Jan 15 20:33 .sqlite_history
```

Next, I read the contents  in `.bash_history`

```
┌──(kali㉿kali)-[/media/kali/ed1c79a8-8148-4ce2-b482-91334a211dc9]
└─$ cat .bash_history  
joplin
cd .config/joplin
ls -lah
sqlite3 database.sqlite 
ls
ls -lah
cat database.sqlite | grep lactf
cd ..
cd ..
ls
ls -lah
nano note_to_self.txt
ls -lah
ls
zerofree /dev/mapper/notes
exit
```

I realised that it was using [Joplin](https://joplinapp.org/), an open-source note taking app.&#x20;

I proceeded into the `.config/joplin` directory and  tried to grep for the flag like what I had seen in the `.bash_history`.

However, it looked like the flag was jumbled up and I could not dicipher the flag from here.\


```
┌──(kali㉿kali)-[/media/kali/ed1c79a8-8148-4ce2-b482-91334a211dc91/.config/joplin]
└─$ cat database.sqlite| grep -a lactf
3ncryp71onc4ch3dinfolactf       p422word2s3cur3ecert�n0 113
3ncryp71onc4ch3dinfolactf       p422word2s3cur3ecertyo40 20infosec@0 26infosecert
```

At this point, I was quite close to the flag, but did not continue further as I had dedicated too much time on this challenge. If you are interested in how to solve this, you could check out one pretty good writeup that I found [here](https://github.com/dreeSec/la-ctf-2023/blob/master/LA-CTF-2023.md#misca-hackers-notes).

Flag: lactf{S3cUr3\_yOUR\_C4cH3D\_3nCRYP71On\_P422woRD2}
