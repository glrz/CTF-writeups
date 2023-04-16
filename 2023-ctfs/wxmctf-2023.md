---
description: >-
  This CTF was held from 1 Mar - 14 Mar 2023, hosted by MGCI and WLMAC. This
  contest was organized by WLMAC's Cybersecurity club and MGCI's CTF club.
---

# WxMCTF 2023

In this capture the flag (CTF) contest, teams of middle and high school students across Ontario battled it out with their skills in digital forensics, website and binary exploitation, reverse engineering, and cryptography!&#x20;

Intended for students of all experience types, the challenges are designed with a low barrier of entry to enable even first-time competitors to gain experience and knowledge in an enjoyable, cooperative way.

Although this Capture the Flag (CTF) event permitted teams of up to four individuals, I chose to compete independently to both relish and enhance my proficiency in tackling these challenges.

I participated as an individual with the username `glrz01` and placed 112/244. The scoreboard can be found [here](https://ctftime.org/event/1911).

I spent some time tackling these challenges and found most of the challenges which I solved to be pretty easy and straightforward.

## Sanity Check

<figure><img src="../.gitbook/assets/image (12) (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

Super straightforward, a challenge to get participants to familiarize with the flag format, just copy paste and submit the flag.

Flag: wxmctf{welcome\_2023}

## PROPRIETARY EOL

<figure><img src="../.gitbook/assets/image (4) (1) (2) (1).png" alt=""><figcaption></figcaption></figure>

This challenge was under the forensics category, also a relatively simple challenge. I first-blooded this challenge within seconds.

First, we could check the file type by running the `file` command.

<figure><img src="../.gitbook/assets/image (10) (3).png" alt=""><figcaption></figcaption></figure>

This confirmed that it was a [`PCX` ](https://en.wikipedia.org/wiki/PCX)file. We could then open this file in `GIMP`.

```
┌──(kali㉿kali)-[~/Downloads]
└─$ gimp public.pcx  
```

Opening it in GIMP, we would be able to see the flag.

<figure><img src="../.gitbook/assets/image (1) (1) (3) (1).png" alt=""><figcaption></figcaption></figure>

Alternatively, we could also open the file using `ImageMagick` as such:

```
┌──(kali㉿kali)-[~/Downloads]
└─$ display public.pcx  
```

Similarly, we would get the flag for the challenge.

<figure><img src="../.gitbook/assets/image (23) (3).png" alt=""><figcaption></figcaption></figure>

Flag: CTF{digital\_archaeology\_42}

## The Maze

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

This was an easy web challenge. First, lets click on the link provided in the challenge description. Upon clicking it, we will be redirected to this site.\


<figure><img src="../.gitbook/assets/image (1) (3) (2).png" alt=""><figcaption></figcaption></figure>

If we noticed, at the bottom it indicated that this is `Room 1` and the flag is at `room 0`. If we tried clicking on any of the 3 numbers, it would just bring us to another room but not room 0.

How can we navigate to Room 0 then?

Lets take a look at the source code of this site.

```html
<html>
	<head>
	<link href="/static/style.css" rel="stylesheet">
	<script src="/static/script.js"></script>
	<title>Room 1 | The Maze</title>
	</head>
	<body>
	<div class="container">
	<div class="grid">
	<div class="door" onclick="window.location.href = '/room/2'">2</div>
	<div class="door" onclick="window.location.href = '/room/3'">3</div>
	<div class="door" onclick="window.location.href = '/room/2'">2</div>
	</div>
	</div>
	<div class="main">
	<h2>Room 1</h2>
	Welcome to the Maze. You are currently in room 1. Click on a door to navigate to another room. The flag is at room 0. Good luck!
	</div>
	</body>
	</html>
```

Based on the source code, we can tell that it changes to a different room by using the `onclick` event and `window.location.href` to redirect the browser to a new URL.

As such, if we navigate to the URL: [https://weba.jonathanw.dev:3001/room/0](https://weba.jonathanw.dev:3001/room/0), we will get the flag at the bottom.

<figure><img src="../.gitbook/assets/image (7) (4) (1).png" alt=""><figcaption></figcaption></figure>

Flag: wxmctf{J5\_d0EsnT\_L13\_bUT\_urL\_m1Ght}

## Natural Selection

<figure><img src="../.gitbook/assets/image (5) (4).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was under the `Reverse Engineering` category. I seldom get any solves in this category due to my lack of knowledge and experience in this area.

I'm glad that I managed to solve this challenge. However, after I solved it, I felt like this was more of a `Cryptography` challenge.  This solution was a series of decoding `Base64` and `Base32` encoded strings in Python scripts.

I most likely solved it using an unintended approach and there should be an easier way to solve this using a script.

First, lets download the `.py` file provided in the challenge description.

Next, I proceeded to read the contents of this file.

```python
┌──(kali㉿kali)-[~/Downloads]
└─$ cat main_xiRTmuC.py 
from base64 import *
from os import *
from sys import *
exec(b64decode("aW1wb3J0IGJhc2U2NAoKYiA9IGludChpbnB1dCgiYmFzZSA/IGRlY29kZT8gIikpCgpleGVjKGdldGF0dHIoYmFzZTY0LCBmImJ7Yn1kZWNvZGUiKSgiTVY0R0tZWklNSTNESVpERk1OWFdJWkpJRUpORzRTVFdNSkpVRU1EQks0WVdZU0tITlIyR0dSWlpQRlNFR1FUMk1KRFZNM0RESUZZRzJZU0RJRTRVU1IzTU9WUlVRVlJRSk5CVVVXREJJNUREQVNLSEtKM0VTU0RNT1pTRkdRUlFNRkRXWTVMQlBGQkRBWUtIS1ZUVlUzTFlOQk5IU1FUUU1ONURTWTNDTkZFWEFRM09KWlpWVVYyV081RlVJUUxWSlpCV1dTM0RKQkZIQVlUT0tGWFVTMjNJT1JSRkdTTFFJTlhFNDQyMks1TEhPUzJFSVYyVTQyTExKTlJVUVNUUU1KWEZDMzJKTk5WV09aQ0hOQllHRTNMVE01U1ZPT0pSSklaVVUzQ0pKQlNIU1lSU0dWWEVZUTJDTkZTRlFVTEhNSkRWTU1DS0dOR1dPWkNJSkkyVVNSMkdPVlNWUVpESU1WTUUyMktMS0ZZR1laS0hLWlZFV1IySkdKSEVPVVRNTEVaRFMyMjJLTlRXU1dLV01ONEdJTVNKUEpKV1VRU0tLTkRFVTUyWk5SU0ZNVVpTSlpFVkczU0NORlJHWVJUV0tOTFhJTkRFTlJXRlFWTE9JSlVXRVYyT09CS0VLVFNETUpEVVU1Q1ZLUldFVVlLVk5SNUZHVkxFTUZSVEVVU1pLUldUU1VLV05SRkRLV1NHTVJMR0dSS09PUkxXNFdUS01GS1VVNTJUS1ZTSEdaQ1ZOUkVWRzNMSU5GUkZPVVRUS01ZRkVWVERJVTRXNFlSU01SRkZHUlNLTzVNV1laQ1dNUkxVMjZMRkk1NEdDVjJGSVozRklWM01PWlJWT1JTVU1FWUhJU1NSR0JGREdXSlNHRlpXSVYyU0lSTkRFM0NOTUZLV1k2U1RLVlNGT1pDV09CQ1UyUjNNSkpRVlFaRE9LNVdUQ05DTks1R1hTV1QyTlJMVkdSTFBQQkxXWVRUU0tNWkZFU0RDSkJKR0NWTDJLWTNGUzIzRUs1UkVPVFNFTEo1RU1UQ1ZMQkJER1dKU0dGWldJVjJTSVJOREUzQ1RLSjVHWU1LWE5SSEVNWUtWT1JKR0dTREVOSlJGTzZCUkxKQ1U0M1RCS1pGSElaS0hOQlFVMlJKVk9aTFdZWkNQTU5XSEFXS1RLNVNHV1lMTEtZWVZJVktOR0JHVks2Q1pLUldYUVdTTkdGTkRLVjNNSlpGR0dSS09PVklXNDNESUtaNUZLNTJUR0JIRVdZS1hLWktGQzIyV0xKTFVLMzMyTEZMR0dNREJLVjJGRVkySFBCV0ZFTUsyT0ZKVEFaQ0tKVlZUS1NDVk5WNEZVVExLTlJaRk8zQ09OWlFWTTNDWExKREhBWUtOSTU0RENWM0xOQkJXQ1YyR0taUkVPTksyS1pXVTI1MlhOSkZFNlUySEtaRUdDUjNVS05HVlFRTFpLNUtFUzUzRUdBMlhFVkRPSUpKRk1NU1NPRktUQVZUWE1RWVdZNUNPS1pGR1NUS0hQQjVGUzIzSU1GUVRDVkxYS05YRU1XQ1dOVkdYT1dMTkdGSlZFUlNHT1ZSRU81Q1hNVldFVTVLWE5OTEdXWVJTSlpFRkkyU1dLSlJHWTREUUxGTEZNUzJYS1pXRk9XTDJJWlVFMjIzTUdaTFdXMkRYS05XRks1MlROUk5GVVRMS0taNFZPMlNHS05MVU1TVFVNTkRGTVRTV0tSREhLVjJXTEpWRTJWMldPUktXVzJDWE1KTFdRMkNWS1JCSEdaQlJJVjRVMlZURU5KR1dXV1NaS1lZV0kyMlROVkZGT1UzTkhGTkUyMlNXT0pNVEFaQ0xNTkRFNFdDMkk1VUZPWkxNSkoyVk9WQ0NOTkhFT1JTSUtWVldRV0RDTlJZSENXTE1LSkJFMjNDRlBGUkVLU1RCSlZWVEtTU1ZHSTJVR1lLWEpKWlZFM1MyS1JMREcyRDJMSkRUQ1UyV0laREhJWTJHT0JMV0szQ0tHRkxXV1ZTUEtFWkZNV0NWTlJVRTZVUlNLSlpGSzJTS041U0RDMjMyTUpDVTQyM0NLVllIT1ZLWE9NWVZPM0NaTzVIRk1SU1hLNURYUVIyWE5KREdDVTJXSlpZVk0yM1FLTkxVTzJCVEs1TFRBTUtXR0EyVU1ZU0ZOQlVWR1JTMk9GS0ZJUlNMTU1ZV0lWMjJJWkZHUVZTWUtKSlZTTURFR1JRVk1TTFpNVkVGRVZDV0tVMlVZV0wySkpEVk9SSlZLVkpHMjZDU0pWRFhRNUtYS1pOR1VUS0dONTRWSTIzSU5SSkRFMkRTS1ZWRU01Mk5OUlZYU1RLSU1SSFdDTUJWTzVLVk1aRExNRldFNFJUREpCU0ZVWVNVS1pKVlMyU0NPTlJURVNTSks1V1hJVlNOSVZZSFFWUlJMSlZFMlIyS09SS1dXVVNTTUpXWFE0U1dOWllGR1lUTU9CREZVUlpaTkpKREFOQlJLVkxUS1lMQks1REZNVTNMR1ZORk0zS05QQktGTVpDWEtKREVVV0MySVpTRklVU1hIQjRGS01LV01GUVRFVFNJS05YRkVWVENOUllIRVZDVUlGNEdFM0RNSzVNWFVSVE1NSkxFVVNLV05VWVc2V0tXSVYzV0VTREVLSkdXVVJTWUxGNUVVVFRGS1pORktWM0xLSlVGTVZLMk9WTFZJUVRQS01aRTRTQ1ROWkxGTVZUMk5SRlZTMjNFR1JHV1k0Q0hLUlZVNDJEQ0k1NEZTVkRMTU1ZV0NNS0ZPNUpXVVZUQktKV1UyNTJYTkpGRkdVMkhJWkVWQzNMUU5STEZLMzNaSzVMVEM0MlJHSkpIR1lTSUtaS1dFV0NDT0pMREFWVFhNTVlVNFZUQklWSEdVVEtYUEJORk1WWlFQQlFWS01EWE1OQ0VFV1NOR0o0RU9WM0tJWlFWR1ZTT09GTEdXNENUSlZYR1FVU1dOUlVIR1VKU0paRUZHM1NXS1ZRV1dTVElLWlZFRVlMRE5SSEZRWVNJSkpLRTJXQ0NMSk1WSzJDRE1FWVVLNksySVJIRklUS1ZMSVpWUzIzRUs1SlVNV1RVTU5DWFFVMk5JNTJES1ZTSE9SVlZLTVNLSTVRVEczQ1FLWVpWRTJDV0tSRkdXWTJHTVJLVkMzSlpLUkdXV05LSktVWkRLVjJXTlJORE1ZU0ZPUk5HQ01MUUpSTkVPNkRMS1laRU1SMlROVldHU1ZTVUtGNEZNVlMyTkpIRk9STFlLTlZGVTJDTkdKSkZTVlROR0ZKRTJSVE1HWkpXWVpDWEtJWUZNTktYTk5TSEdZS1dMSkVHSVJDT0taR1ZNV1RXS1pLRVVTVEZJNUhFT1ZMTUpKVVZNUksyTzVMRk80Q0RMRkxWRVYyVU5SU0ZLWUpUSUpVRklWM1VNRkxWTVdMWUxKRFhJMkNTTlJYVEVWVE5PQkhWU1ZTS09SUVVNVFMyTUZWVVM1MldOTk5FT1ZTWEpKRFZFM0MySlpKRk00QlRLWVpISVUyVUdKRVhTVkxMTVJVRTJNMkNLNU1XWVVTSE1NWVhBV0REUEpCRTRVVE1KSkxGS01UVEdWTVZPU1NXSlZLRk1XREJOTTJUR1dLV01SRFdHTUtPT0ZKR1lWU1hNSkxFVTZDV0laTEdXVVpTSlpMVk8zU0dORkpGUVFUUEtaV0ZNNTNGTlJTRlFaQ0hIRktVMjIzUUk1TVdXVlNUS1pEVVVSMlhOVTRWTVlMTEpKUVZVUkNHSjVSVk1VVFNKWkxVTVRUQkdOQVhPVlNFSVpKVkNNS09PTktHV1pDVU1KV0hBV0taTk5LVENVU0dOUlpWVVJMVUtSSkdXNEJRS1JXRk01M0JJWk1YVVZDVUtaS0ZNTVRZUEZNVEFUU0tNTkNYSVVTUUtRWUdTUzJUTk02U0VLSkpFQT09PT09PSIpKQ=="))                              
```

This looked like a python script that was decoding the `Base64` encoded string.

We could copy the string and decode it as such

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ >....                                                                                                           
WRTJWMldPUktXVzJDWE1KTFdRMkNWS1JCSEdaQlJJVjRVMlZURU5KR1dXV1NaS1lZV0kyMlROVkZGT1UzTkhGTkUyMlNXT0pNVEFaQ0xNTkRFNFdDMkk1VUZPWkxNSkoyVk9WQ0NOTkhFT1JTSUtWVldRV0RDTlJZSENXTE1LSkJFMjNDRlBGUkVLU1RCSlZWVEtTU1ZHSTJVR1lLWEpKWlZFM1MyS1JMREcyRDJMSkRUQ1UyV0laREhJWTJHT0JMV0szQ0tHRkxXV1ZTUEtFWkZNV0NWTlJVRTZVUlNLSlpGSzJTS041U0RDMjMyTUpDVTQyM0NLVllIT1ZLWE9NWVZPM0NaTzVIRk1SU1hLNURYUVIyWE5KREdDVTJXSlpZVk0yM1FLTkxVTzJCVEs1TFRBTUtXR0EyVU1ZU0ZOQlVWR1JTMk9GS0ZJUlNMTU1ZV0lWMjJJWkZHUVZTWUtKSlZTTURFR1JRVk1TTFpNVkVGRVZDV0tVMlVZV0wySkpEVk9SSlZLVkpHMjZDU0pWRFhRNUtYS1pOR1VUS0dONTRWSTIzSU5SSkRFMkRTS1ZWRU01Mk5OUlZYU1RLSU1SSFdDTUJWTzVLVk1aRExNRldFNFJUREpCU0ZVWVNVS1pKVlMyU0NPTlJURVNTSks1V1hJVlNOSVZZSFFWUlJMSlZFMlIyS09SS1dXVVNTTUpXWFE0U1dOWllGR1lUTU9CREZVUlpaTkpKREFOQlJLVkxUS1lMQks1REZNVTNMR1ZORk0zS05QQktGTVpDWEtKREVVV0MySVpTRklVU1hIQjRGS01LV01GUVRFVFNJS05YRkVWVENOUllIRVZDVUlGNEdFM0RNSzVNWFVSVE1NSkxFVVNLV05VWVc2V0tXSVYzV0VTREVLSkdXVVJTWUxGNUVVVFRGS1pORktWM0xLSlVGTVZLMk9WTFZJUVRQS01aRTRTQ1ROWkxGTVZUMk5SRlZTMjNFR1JHV1k0Q0hLUlZVNDJEQ0k1NEZTVkRMTU1ZV0NNS0ZPNUpXVVZUQktKV1UyNTJYTkpGRkdVMkhJWkVWQzNMUU5STEZLMzNaSzVMVEM0MlJHSkpIR1lTSUtaS1dFV0NDT0pMREFWVFhNTVlVNFZUQklWSEdVVEtYUEJORk1WWlFQQlFWS01EWE1OQ0VFV1NOR0o0RU9WM0tJWlFWR1ZTT09GTEdXNENUSlZYR1FVU1dOUlVIR1VKU0paRUZHM1NXS1ZRV1dTVElLWlZFRVlMRE5SSEZRWVNJSkpLRTJXQ0NMSk1WSzJDRE1FWVVLNksySVJIRklUS1ZMSVpWUzIzRUs1SlVNV1RVTU5DWFFVMk5JNTJES1ZTSE9SVlZLTVNLSTVRVEczQ1FLWVpWRTJDV0tSRkdXWTJHTVJLVkMzSlpLUkdXV05LSktVWkRLVjJXTlJORE1ZU0ZPUk5HQ01MUUpSTkVPNkRMS1laRU1SMlROVldHU1ZTVUtGNEZNVlMyTkpIRk9STFlLTlZGVTJDTkdKSkZTVlROR0ZKRTJSVE1HWkpXWVpDWEtJWUZNTktYTk5TSEdZS1dMSkVHSVJDT0taR1ZNV1RXS1pLRVVTVEZJNUhFT1ZMTUpKVVZNUksyTzVMRk80Q0RMRkxWRVYyVU5SU0ZLWUpUSUpVRklWM1VNRkxWTVdMWUxKRFhJMkNTTlJYVEVWVE5PQkhWU1ZTS09SUVVNVFMyTUZWVVM1MldOTk5FT1ZTWEpKRFZFM0MySlpKRk00QlRLWVpISVUyVUdKRVhTVkxMTVJVRTJNMkNLNU1XWVVTSE1NWVhBV0REUEpCRTRVVE1KSkxGS01UVEdWTVZPU1NXSlZLRk1XREJOTTJUR1dLV01SRFdHTUtPT0ZKR1lWU1hNSkxFVTZDV0laTEdXVVpTSlpMVk8zU0dORkpGUVFUUEtaV0ZNNTNGTlJTRlFaQ0hIRktVMjIzUUk1TVdXVlNUS1pEVVVSMlhOVTRWTVlMTEpKUVZVUkNHSjVSVk1VVFNKWkxVTVRUQkdOQVhPVlNFSVpKVkNNS09PTktHV1pDVU1KV0hBV0taTk5LVENVU0dOUlpWVVJMVUtSSkdXNEJRS1JXRk01M0JJWk1YVVZDVUtaS0ZNTVRZUEZNVEFUU0tNTkNYSVVTUUtRWUdTUzJUTk02U0VLSkpFQT09PT09PSIpKQ==  |base64 -d
```

&#x20;This would give us the output, which is another Python script

```python
import base64

b = int(input("base ? decode? "))

exec(getattr(base64, f"b{b}decode")("MV4GKYZIMI3DIZDFMNXWIZJIEJNG4STWMJJUEMDBK4YWYSKHNR2GGRZZPFSEGQT2MJDVM3DDIFYG2YSDIE4USR3MOVRUQVRQJNBUUWDBI5DDASKHKJ3ESSDMOZSFGQRQMFDWY5LBPFBDAYKHKVTVU3LYNBNHSQTQMN5DSY3CNFEXAQ3OJZZVUV2WO5FUIQLVJZBWWS3DJBFHAYTOKFXUS23IORRFGSLQINXE4422K5LHOS2EIV2U42LLJNRUQSTQMJXFC32JNNVWOZCHNBYGE3LTM5SVOOJRJIZUU3CJJBSHSYRSGVXEYQ2CNFSFQULHMJDVMMCKGNGWOZCIJI2USR2GOVSVQZDIMVME22KLKFYGYZKHKZVEWR2JGJHEOUTMLEZDS222KNTWSWKWMN4GIMSJPJJWUQSKKNDEU52ZNRSFMUZSJZEVG3SCNFRGYRTWKNLXINDENRWFQVLOIJUWEV2OOBKEKTSDMJDUU5CVKRWEUYKVNR5FGVLEMFRTEUSZKRWTSUKWNRFDKWSGMRLGGRKOORLW4WTKMFKUU52TKVSHGZCVNREVG3LINFRFOUTTKMYFEVTDIU4W4YRSMRFFGRSKO5MWYZCWMRLU26LFI54GCV2FIZ3FIV3MOZRVORSUMEYHISSRGBFDGWJSGFZWIV2SIRNDE3CNMFKWY6STKVSFOZCWOBCU2R3MJJQVQZDOK5WTCNCNK5GXSWT2NRLVGRLPPBLWYTTSKMZFESDCJBJGCVL2KY3FS23EK5REOTSELJ5EMTCVLBBDGWJSGFZWIV2SIRNDE3CTKJ5GYMKXNRHEMYKVORJGGSDENJRFO6BRLJCU43TBKZFHIZKHNBQU2RJVOZLWYZCPMNWHAWKTK5SGWYLLKYYVIVKNGBGVK6CZKRWXQWSNGFNDKV3MJZFGGRKOOVIW43DIKZ5FK52TGBHEWYKXKZKFC22WLJLUK332LFLGGMDBKV2FEY2HPBWFEMK2OFJTAZCKJVVTKSCVNV4FUTLKNRZFO3CONZQVM3CXLJDHAYKNI54DCV3LNBBWCV2GKZREONK2KZWU252XNJFE6U2HKZEGCR3UKNGVQQLZK5KES53EGA2XEVDOIJJFMMSSOFKTAVTXMQYWY5COKZFGSTKHPB5FS23IMFQTCVLXKNXEMWCWNVGXOWLNGFJVERSGOVREO5CXMVWEU5KXNNLGWYRSJZEFI2SWKJRGY4DQLFLFMS2XKZWFOWL2IZUE223MGZLWW2DXKNWFK52TNRNFUTLKKZ4VO2SGKNLUMSTUMNDFMTSWKRDHKV2WLJVE2V2WORKWW2CXMJLWQ2CVKRBHGZBRIV4U2VTENJGWWWSZKYYWI22TNVFFOU3NHFNE22SWOJMTAZCLMNDE4WC2I5UFOZLMJJ2VOVCCNNHEORSIKVVWQWDCNRYHCWLMKJBE23CFPFREKSTBJVVTKSSVGI2UGYKXJJZVE3S2KRLDG2D2LJDTCU2WIZDHIY2GOBLWK3CKGFLWWVSPKEZFMWCVNRUE6URSKJZFK2SKN5SDC232MJCU423CKVYHOVKXOMYVO3CZO5HFMRSXK5DXQR2XNJDGCU2WJZYVM23QKNLUO2BTK5LTAMKWGA2UMYSFNBUVGRS2OFKFIRSLMMYWIV22IZFGQVSYKJJVSMDEGRQVMSLZMVEFEVCWKU2UYWL2JJDVORJVKVJG26CSJVDXQ5KXKZNGUTKGN54VI23INRJDE2DSKVVEM52NNRVXSTKIMRHWCMBVO5KVMZDLMFWE4RTDJBSFUYSUKZJVS2SCONRTESSJK5WXIVSNIVYHQVRRLJVE2R2KORKWWUSSMJWXQ4SWNZYFGYTMOBDFURZZNJJDANBRKVLTKYLBK5DFMU3LGVNFM3KNPBKFMZCXKJDEUWC2IZSFIUSXHB4FKMKWMFQTETSIKNXFEVTCNRYHEVCUIF4GE3DMK5MXURTMMJLEUSKWNUYW6WKWIV3WESDEKJGWURSYLF5EUTTFKZNFKV3LKJUFMVK2OVLVIQTPKMZE4SCTNZLFMVT2NRFVS23EGRGWY4CHKRVU42DCI54FSVDLMMYWCMKFO5JWUVTBKJWU252XNJFFGU2HIZEVC3LQNRLFK33ZK5LTC42RGJJHGYSIKZKWEWCCOJLDAVTXMMYU4VTBIVHGUTKXPBNFMVZQPBQVKMDXMNCEEWSNGJ4EOV3KIZQVGVSOOFLGW4CTJVXGQUSWNRUHGUJSJZEFG3SWKVQWWSTIKZVEEYLDNRHFQYSIJJKE2WCCLJMVK2CDMEYUK6K2IRHFITKVLIZVS23EK5JUMWTUMNCXQU2NI52DKVSHORVVKMSKI5QTG3CQKYZVE2CWKRFGWY2GMRKVC3JZKRGWWNKJKUZDKV2WNRNDMYSFORNGCMLQJRNEO6DLKYZEMR2TNVWGSVSUKF4FMVS2NJHFORLYKNVFU2CNGJJFSVTNGFJE2RTMGZJWYZCXKIYFMNKXNNSHGYKWLJEGIRCOKZGVMWTWKZKEUSTFI5HEOVLMJJUVMRK2O5LFO4CDLFLVEV2UNRSFKYJTIJUFIV3UMFLVMWLYLJDXI2CSNRXTEVTNOBHVSVSKORQUMTS2MFVUS52WNNNEOVSXJJDVE3C2JZJFM4BTKYZHIU2UGJEXSVLLMRUE2M2CK5MWYUSHMMYXAWDDPJBE4UTMJJLFKMTTGVMVOSSWJVKFMWDBNM2TGWKWMRDWGMKOOFJGYVSXMJLEU6CWIZLGWUZSJZLVO3SGNFJFQQTPKZWFM53FNRSFQZCHHFKU223QI5MWWVSTKZDUUR2XNU4VMYLLJJQVURCGJ5RVMUTSJZLUMTTBGNAXOVSEIZJVCMKOONKGWZCUMJWHAWKZNNKTCUSGNRZVURLUKRJGW4BQKRWFM53BIZMXUVCUKZKFMMTYPFMTATSKMNCXIUSQKQYGSS2TNM6SEKJJEA======"))
```

As we can see, the variable `b` takes in an integer which will determine the decode function. As I looked at the string, I also realized there were 5 `=` appended at the end of the string. This suggested that it was most likely `Base64` or `Base32` encoded which required the padding.

We could decode the `Base32` encoded as such and get the following

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ >....                                                                                                           
WOBCU2R3MJJQVQZDOK5WTCNCNK5GXSWT2NRLVGRLPPBLWYTTSKMZFESDCJBJGCVL2KY3FS23EK5REOTSELJ5EMTCVLBBDGWJSGFZWIV2SIRNDE3CTKJ5GYMKXNRHEMYKVORJGGSDENJRFO6BRLJCU43TBKZFHIZKHNBQU2RJVOZLWYZCPMNWHAWKTK5SGWYLLKYYVIVKNGBGVK6CZKRWXQWSNGFNDKV3MJZFGGRKOOVIW43DIKZ5FK52TGBHEWYKXKZKFC22WLJLUK332LFLGGMDBKV2FEY2HPBWFEMK2OFJTAZCKJVVTKSCVNV4FUTLKNRZFO3CONZQVM3CXLJDHAYKNI54DCV3LNBBWCV2GKZREONK2KZWU252XNJFE6U2HKZEGCR3UKNGVQQLZK5KES53EGA2XEVDOIJJFMMSSOFKTAVTXMQYWY5COKZFGSTKHPB5FS23IMFQTCVLXKNXEMWCWNVGXOWLNGFJVERSGOVREO5CXMVWEU5KXNNLGWYRSJZEFI2SWKJRGY4DQLFLFMS2XKZWFOWL2IZUE223MGZLWW2DXKNWFK52TNRNFUTLKKZ4VO2SGKNLUMSTUMNDFMTSWKRDHKV2WLJVE2V2WORKWW2CXMJLWQ2CVKRBHGZBRIV4U2VTENJGWWWSZKYYWI22TNVFFOU3NHFNE22SWOJMTAZCLMNDE4WC2I5UFOZLMJJ2VOVCCNNHEORSIKVVWQWDCNRYHCWLMKJBE23CFPFREKSTBJVVTKSSVGI2UGYKXJJZVE3S2KRLDG2D2LJDTCU2WIZDHIY2GOBLWK3CKGFLWWVSPKEZFMWCVNRUE6URSKJZFK2SKN5SDC232MJCU423CKVYHOVKXOMYVO3CZO5HFMRSXK5DXQR2XNJDGCU2WJZYVM23QKNLUO2BTK5LTAMKWGA2UMYSFNBUVGRS2OFKFIRSLMMYWIV22IZFGQVSYKJJVSMDEGRQVMSLZMVEFEVCWKU2UYWL2JJDVORJVKVJG26CSJVDXQ5KXKZNGUTKGN54VI23INRJDE2DSKVVEM52NNRVXSTKIMRHWCMBVO5KVMZDLMFWE4RTDJBSFUYSUKZJVS2SCONRTESSJK5WXIVSNIVYHQVRRLJVE2R2KORKWWUSSMJWXQ4SWNZYFGYTMOBDFURZZNJJDANBRKVLTKYLBK5DFMU3LGVNFM3KNPBKFMZCXKJDEUWC2IZSFIUSXHB4FKMKWMFQTETSIKNXFEVTCNRYHEVCUIF4GE3DMK5MXURTMMJLEUSKWNUYW6WKWIV3WESDEKJGWURSYLF5EUTTFKZNFKV3LKJUFMVK2OVLVIQTPKMZE4SCTNZLFMVT2NRFVS23EGRGWY4CHKRVU42DCI54FSVDLMMYWCMKFO5JWUVTBKJWU252XNJFFGU2HIZEVC3LQNRLFK33ZK5LTC42RGJJHGYSIKZKWEWCCOJLDAVTXMMYU4VTBIVHGUTKXPBNFMVZQPBQVKMDXMNCEEWSNGJ4EOV3KIZQVGVSOOFLGW4CTJVXGQUSWNRUHGUJSJZEFG3SWKVQWWSTIKZVEEYLDNRHFQYSIJJKE2WCCLJMVK2CDMEYUK6K2IRHFITKVLIZVS23EK5JUMWTUMNCXQU2NI52DKVSHORVVKMSKI5QTG3CQKYZVE2CWKRFGWY2GMRKVC3JZKRGWWNKJKUZDKV2WNRNDMYSFORNGCMLQJRNEO6DLKYZEMR2TNVWGSVSUKF4FMVS2NJHFORLYKNVFU2CNGJJFSVTNGFJE2RTMGZJWYZCXKIYFMNKXNNSHGYKWLJEGIRCOKZGVMWTWKZKEUSTFI5HEOVLMJJUVMRK2O5LFO4CDLFLVEV2UNRSFKYJTIJUFIV3UMFLVMWLYLJDXI2CSNRXTEVTNOBHVSVSKORQUMTS2MFVUS52WNNNEOVSXJJDVE3C2JZJFM4BTKYZHIU2UGJEXSVLLMRUE2M2CK5MWYUSHMMYXAWDDPJBE4UTMJJLFKMTTGVMVOSSWJVKFMWDBNM2TGWKWMRDWGMKOOFJGYVSXMJLEU6CWIZLGWUZSJZLVO3SGNFJFQQTPKZWFM53FNRSFQZCHHFKU223QI5MWWVSTKZDUUR2XNU4VMYLLJJQVURCGJ5RVMUTSJZLUMTTBGNAXOVSEIZJVCMKOONKGWZCUMJWHAWKZNNKTCUSGNRZVURLUKRJGW4BQKRWFM53BIZMXUVCUKZKFMMTYPFMTATSKMNCXIUSQKQYGSS2TNM6SEKJJEA====== | base32 -d
exec(b64decode("ZnJvbSB0aW1lIGltcG9ydCBzbGVlcApmbCA9IGlucHV0KCJXaGF0IGRvIHlvdSB0aGluayB0aGUgZmxhZyBpcz9cbiIpCnNsZWVwKDAuNCkKcHJpbnQoIkhtbSIpCnNsZWVwKDEuNikKcHJpbnQoIkkgdGhpbmsgeW91J3JlIHdyb25nLCBidXQgbGV0J3MgdHJ5IGFueXdheXMiKQpleGVjKGI2NGRlY29kZSgiYVcxd2IzSjBJSFJwYldVS2NISnBiblFvSWt4dllXUnBibWNpTENCbGJtUTlJaUlzSUdac2RYTm9QVlJ5ZFdVcENtWnZjaUJwSUdsdUlISmhibWRsS0RVcE9nb2dJSFJwYldVdWMyeGxaWEFvTWlvcWFTa0tJQ0J3Y21sdWRDZ2lMaUlzSUdWdVpEMGlJaXdnWm14MWMyZzlWSEoxWlNrS2RHbHRaUzV6YkdWbGNDZzFLUXB3Y21sdWRDZ2lSRzl1WlNFaUtRcHdjbWx1ZENnaVJteGhaME5vWldOclpYSWdkakV1TUM0MUxYTmxZM1Z5WlNJcENuQnlhVzUwS0NKaWVTQkVZWEozYVc0aUtRcGxlR1ZqS0dJMk5HUmxZMjlrWlNnaVlWZFpaMGx1WkhCaWFVbG5ZVmMwWjJOSGVHaGtSMXAyWTIwd05rTnBRV2RqU0Vwd1ltNVJiMGxzYkhaa1UwSnFXVmMwYm1SRFFubGtWelJuWkVkb2NHTjVRblppYVVKWVlWYzFhMkl6WkhwSlUwSlZZMjVyWjFSWFJtcFVNVTFuWVZjMWVtUkhWbWhhUTBsd1EyMVdjMkZYV1dkSmJWSm9ZMjVrY0dKcFNXZGhWelJuWTBkNGFHUkhXblpqYlRBMlEybEJaMk5JU25CaWJsRnZTV3hzZG1SVFFtcFpWelJ1WkVOQ2VXUlhOR2RrUjJod1kzbENkbUpwUWs1WlYwNVFWWGxGWjFaSVNqVkpSWGh3WW01V05FbEhiSFZqTTFKc1dWZFJhVXRSY0d4aVIyeHRTVU5LYzJGWE5URmxRMGxuWVZjMFoyTkhlR2hrUjFwMlkyMHdOa05wUVdkalNFcHdZbTVSYjBsc2JIWmtVMEpxV1ZjMGJtUkRRbmxrVnpSblpFZG9jR041UW5aaWFVSk5ZVmMxTVdWRFJXZFdTRW8xU1Vaa2NHSnRVblprTTAxbllWYzFlbVJIVm1oYVEwbHdRMjFXYzJNeVZUWkRhVUZuWTBoS2NHSnVVVzlKYkd4MlpGTkNhbGxYTkc1a1EwSjVaRmMwWjJSSGFIQmplVUoyWW1sQ2RsbHVUbXBrV0Vwc1NVaENjMWxZVW0xaU0wcDBZM2xGWjFaSVNqVkpSMnhRVlhsQ2NHSnVUakJhVjBaclNXbHJTMXBZYUhCa1EyZDNTMUZ3YkdWSFZtcExSMGt5VGtkU2JGa3lPV3RhVTJkcFdUQm9TMk5IU25WVlZ6bEtZa1pLZGxkV2FGSmliVTQxVVZjNWExSjZhM2RYVm1RMFl6SldWR0V5WkdsaVZHdDNVMVZvVTJJeGNGUlJiVEZwVWpCYWRWTldUa3BhTWtaWVYxZGthRlo2VmpOYVJtaFNZakIwVkZGVWJGRlZNRVp3V2tST2IyUkdhM3BWYlRGc1pXczBNRlJVU2s5YWJVMTVXak53YVdGc1NqRlVWbVJxVFVkS2NWWnFiRXBoVlVweldXdG9UMkpGYkVSVGJGWm9VakJaZDFOcVRrNWFNa3AwVDFSQ1NsTkdTblpYYkU1RFlsZEtTRkp0TlVwaFYzTTVTV2xyY0NJcEtRPT0iKSk="))
```



Next, we could proceed to decode this `Base64` encoded string and we will get the following Python script output

```python
from time import sleep
fl = input("What do you think the flag is?\n")
sleep(0.4)
print("Hmm")
sleep(1.6)
print("I think you're wrong, but let's try anyways")
exec(b64decode("aW1wb3J0IHRpbWUKcHJpbnQoIkxvYWRpbmciLCBlbmQ9IiIsIGZsdXNoPVRydWUpCmZvciBpIGluIHJhbmdlKDUpOgogIHRpbWUuc2xlZXAoMioqaSkKICBwcmludCgiLiIsIGVuZD0iIiwgZmx1c2g9VHJ1ZSkKdGltZS5zbGVlcCg1KQpwcmludCgiRG9uZSEiKQpwcmludCgiRmxhZ0NoZWNrZXIgdjEuMC41LXNlY3VyZSIpCnByaW50KCJieSBEYXJ3aW4iKQpleGVjKGI2NGRlY29kZSgiYVdZZ0luZHBiaUlnYVc0Z2NHeGhkR1p2Y20wNkNpQWdjSEpwYm5Rb0lsbHZkU0JqWVc0bmRDQnlkVzRnZEdocGN5QnZiaUJYYVc1a2IzZHpJU0JVY25rZ1RXRmpUMU1nYVc1emRHVmhaQ0lwQ21Wc2FXWWdJbVJoY25kcGJpSWdhVzRnY0d4aGRHWnZjbTA2Q2lBZ2NISnBiblFvSWxsdmRTQmpZVzRuZENCeWRXNGdkR2hwY3lCdmJpQk5ZV05QVXlFZ1ZISjVJRXhwYm5WNElHbHVjM1JsWVdRaUtRcGxiR2xtSUNKc2FXNTFlQ0lnYVc0Z2NHeGhkR1p2Y20wNkNpQWdjSEpwYm5Rb0lsbHZkU0JqWVc0bmRDQnlkVzRnZEdocGN5QnZiaUJNYVc1MWVDRWdWSEo1SUZkcGJtUnZkM01nYVc1emRHVmhaQ0lwQ21Wc2MyVTZDaUFnY0hKcGJuUW9JbGx2ZFNCallXNG5kQ0J5ZFc0Z2RHaHBjeUJ2YmlCdlluTmpkWEpsSUhCc1lYUm1iM0p0Y3lFZ1ZISjVJR2xQVXlCcGJuTjBaV0ZrSWlrS1pYaHBkQ2d3S1FwbGVHVmpLR0kyTkdSbFkyOWtaU2dpWTBoS2NHSnVVVzlKYkZKdldWaFJibU41UVc5a1J6a3dXVmQ0YzJWVGEyZGliVGt3U1VoU2IxcFRRbTFpUjBadVNWTkpaMkZYV1dkaFZ6VjNaRmhSYjB0VFFUbFFVMEZwWkROb2RGa3pVbTFsZWs0MFRUSk9abU15WjNwaWFsSjFUVmRqTUdKcVZqbEphVUpzWWtoT2JFbERTbFZoUjBZd1NqTk5aMkp0T1RCSlNGSnZXbE5DYldKSFJtNUphV3M5SWlrcCIpKQ=="))
```

As we can see, there's another `Base64 encoded` string and we have to decode it again. This  gives us the following output.

```python
┌──(kali㉿kali)-[~/Downloads]
└─$ echo aW1wb3J0IHRpbWUKcHJpbnQoIkxvYWRpbmciLCBlbmQ9IiIsIGZsdXNoPVRydWUpCmZvciBpIGluIHJhbmdlKDUpOgogIHRpbWUuc2xlZXAoMioqaSkKICBwcmludCgiLiIsIGVuZD0iIiwgZmx1c2g9VHJ1ZSkKdGltZS5zbGVlcCg1KQpwcmludCgiRG9uZSEiKQpwcmludCgiRmxhZ0NoZWNrZXIgdjEuMC41LXNlY3VyZSIpCnByaW50KCJieSBEYXJ3aW4iKQpleGVjKGI2NGRlY29kZSgiYVdZZ0luZHBiaUlnYVc0Z2NHeGhkR1p2Y20wNkNpQWdjSEpwYm5Rb0lsbHZkU0JqWVc0bmRDQnlkVzRnZEdocGN5QnZiaUJYYVc1a2IzZHpJU0JVY25rZ1RXRmpUMU1nYVc1emRHVmhaQ0lwQ21Wc2FXWWdJbVJoY25kcGJpSWdhVzRnY0d4aGRHWnZjbTA2Q2lBZ2NISnBiblFvSWxsdmRTQmpZVzRuZENCeWRXNGdkR2hwY3lCdmJpQk5ZV05QVXlFZ1ZISjVJRXhwYm5WNElHbHVjM1JsWVdRaUtRcGxiR2xtSUNKc2FXNTFlQ0lnYVc0Z2NHeGhkR1p2Y20wNkNpQWdjSEpwYm5Rb0lsbHZkU0JqWVc0bmRDQnlkVzRnZEdocGN5QnZiaUJNYVc1MWVDRWdWSEo1SUZkcGJtUnZkM01nYVc1emRHVmhaQ0lwQ21Wc2MyVTZDaUFnY0hKcGJuUW9JbGx2ZFNCallXNG5kQ0J5ZFc0Z2RHaHBjeUJ2YmlCdlluTmpkWEpsSUhCc1lYUm1iM0p0Y3lFZ1ZISjVJR2xQVXlCcGJuTjBaV0ZrSWlrS1pYaHBkQ2d3S1FwbGVHVmpLR0kyTkdSbFkyOWtaU2dpWTBoS2NHSnVVVzlKYkZKdldWaFJibU41UVc5a1J6a3dXVmQ0YzJWVGEyZGliVGt3U1VoU2IxcFRRbTFpUjBadVNWTkpaMkZYV1dkaFZ6VjNaRmhSYjB0VFFUbFFVMEZwWkROb2RGa3pVbTFsZWs0MFRUSk9abU15WjNwaWFsSjFUVmRqTUdKcVZqbEphVUpzWWtoT2JFbERTbFZoUjBZd1NqTk5aMkp0T1RCSlNGSnZXbE5DYldKSFJtNUphV3M5SWlrcCIpKQ== | base64 -d
import time
print("Loading", end="", flush=True)
for i in range(5):
  time.sleep(2**i)
  print(".", end="", flush=True)
time.sleep(5)
print("Done!")
print("FlagChecker v1.0.5-secure")
print("by Darwin")
exec(b64decode("aWYgIndpbiIgaW4gcGxhdGZvcm06CiAgcHJpbnQoIllvdSBjYW4ndCBydW4gdGhpcyBvbiBXaW5kb3dzISBUcnkgTWFjT1MgaW5zdGVhZCIpCmVsaWYgImRhcndpbiIgaW4gcGxhdGZvcm06CiAgcHJpbnQoIllvdSBjYW4ndCBydW4gdGhpcyBvbiBNYWNPUyEgVHJ5IExpbnV4IGluc3RlYWQiKQplbGlmICJsaW51eCIgaW4gcGxhdGZvcm06CiAgcHJpbnQoIllvdSBjYW4ndCBydW4gdGhpcyBvbiBMaW51eCEgVHJ5IFdpbmRvd3MgaW5zdGVhZCIpCmVsc2U6CiAgcHJpbnQoIllvdSBjYW4ndCBydW4gdGhpcyBvbiBvYnNjdXJlIHBsYXRmb3JtcyEgVHJ5IGlPUyBpbnN0ZWFkIikKZXhpdCgwKQpleGVjKGI2NGRlY29kZSgiY0hKcGJuUW9JbFJvWVhRbmN5QW9kRzkwWVd4c2VTa2dibTkwSUhSb1pTQm1iR0ZuSVNJZ2FXWWdhVzV3ZFhRb0tTQTlQU0FpZDNodFkzUm1lek40TTJOZmMyZ3pialJ1TVdjMGJqVjlJaUJsYkhObElDSlVhR0YwSjNNZ2JtOTBJSFJvWlNCbWJHRm5JaWs9Iikp"))
```

Again, we  can see a `Base64` encoded string at the bottom of the Python script, so we have to decode it again. This gives us another Python script which has a new `Base64` encoded string.

```python
┌──(kali㉿kali)-[~/Downloads]
└─$ echo aWYgIndpbiIgaW4gcGxhdGZvcm06CiAgcHJpbnQoIllvdSBjYW4ndCBydW4gdGhpcyBvbiBXaW5kb3dzISBUcnkgTWFjT1MgaW5zdGVhZCIpCmVsaWYgImRhcndpbiIgaW4gcGxhdGZvcm06CiAgcHJpbnQoIllvdSBjYW4ndCBydW4gdGhpcyBvbiBNYWNPUyEgVHJ5IExpbnV4IGluc3RlYWQiKQplbGlmICJsaW51eCIgaW4gcGxhdGZvcm06CiAgcHJpbnQoIllvdSBjYW4ndCBydW4gdGhpcyBvbiBMaW51eCEgVHJ5IFdpbmRvd3MgaW5zdGVhZCIpCmVsc2U6CiAgcHJpbnQoIllvdSBjYW4ndCBydW4gdGhpcyBvbiBvYnNjdXJlIHBsYXRmb3JtcyEgVHJ5IGlPUyBpbnN0ZWFkIikKZXhpdCgwKQpleGVjKGI2NGRlY29kZSgiY0hKcGJuUW9JbFJvWVhRbmN5QW9kRzkwWVd4c2VTa2dibTkwSUhSb1pTQm1iR0ZuSVNJZ2FXWWdhVzV3ZFhRb0tTQTlQU0FpZDNodFkzUm1lek40TTJOZmMyZ3pialJ1TVdjMGJqVjlJaUJsYkhObElDSlVhR0YwSjNNZ2JtOTBJSFJvWlNCbWJHRm5JaWs9Iikp | base64 -d
if "win" in platform:
  print("You can't run this on Windows! Try MacOS instead")
elif "darwin" in platform:
  print("You can't run this on MacOS! Try Linux instead")
elif "linux" in platform:
  print("You can't run this on Linux! Try Windows instead")
else:
  print("You can't run this on obscure platforms! Try iOS instead")
exit(0)
exec(b64decode("cHJpbnQoIlRoYXQncyAodG90YWxseSkgbm90IHRoZSBmbGFnISIgaWYgaW5wdXQoKSA9PSAid3htY3RmezN4M2Nfc2gzbjRuMWc0bjV9IiBlbHNlICJUaGF0J3Mgbm90IHRoZSBmbGFnIik="))         
```

Finally, if we decode that `Base64` encoded string, we will be presented with the flag in the Python script.

```python
┌──(kali㉿kali)-[~/Downloads]
└─$ echo cHJpbnQoIlRoYXQncyAodG90YWxseSkgbm90IHRoZSBmbGFnISIgaWYgaW5wdXQoKSA9PSAid3htY3RmezN4M2Nfc2gzbjRuMWc0bjV9IiBlbHNlICJUaGF0J3Mgbm90IHRoZSBmbGFnIik= | base64 -d
print("That's (totally) not the flag!" if input() == "wxmctf{3x3c_sh3n4n1g4n5}" else "That's not the flag")
```

Flag: wxmctf{3x3c\_sh3n4n1g4n5}

## Survey

<figure><img src="../.gitbook/assets/image (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

A simple survey challenge which I first blooded haha. Simply give feedback for the CTF and at the end of the survey, the flag is given.

<figure><img src="../.gitbook/assets/image (2) (4).png" alt=""><figcaption></figcaption></figure>

Flag: wxmctf{supported\_by\_digitalocean}

## Zip Gauntlet

<figure><img src="../.gitbook/assets/image (5) (5).png" alt=""><figcaption></figcaption></figure>

I did not solve this challenge during the CTF, but I solved it after. I found that this challenge was pretty interesting as it included different stages of forensics challenges.&#x20;

For this challenge, we were given a `zip` file.

{% file src="../.gitbook/assets/stage_zero.zip" %}

### Stage zero

First, lets extract  the contents in the zip  file.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ 7z x stage_zero.zip 

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 22213943 bytes (22 MiB)

Extracting archive: stage_zero.zip
--
Path = stage_zero.zip
Type = zip
Physical Size = 22213943

Everything is Ok

Files: 2
Size:       22213700
Compressed: 22213943
```

Next, we read the contents extracted. From here, we can obtain the password for `stage_one.zip` file.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cat README.txt 
Welcome to the Zip Gauntlet! Here, you'll test your forensics skills by solving five stages and unlocking nested zips until you get the flag!

To enter stage one, use the password "start".
```

We use  the password: `start` to extract the contents from the zip file.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ 7z x stage_one.zip 

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 22213510 bytes (22 MiB)

Extracting archive: stage_one.zip
--
Path = stage_one.zip
Type = zip
Physical Size = 22213510

    
Enter password (will not be echoed):
Everything is Ok  

Files: 2
Size:       22223147
Compressed: 22213510
```

### Stage one

Once we extracted the files, we will get a  `p1c7ur3.jpg` file with an image of a skeleton stegosaurus.

<figure><img src="../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

This most likely suggest that this is a steganography challenge. By running `StegoVeritas`, we are able to obtain some useful information.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ stegoveritas p1c7ur3.jpg  
Running Module: SVImage
+------------------+------+
|   Image Format   | Mode |
+------------------+------+
| JPEG (ISO 10918) | RGB  |
+------------------+------+
Found something with StegHide: /home/kali/Downloads/results/steghide_964494712a76f5e28e9355b2a95d0253.bin
+---------+------------------+------------------------------------------------------------------------------------------------+-----------+
| Offset  | Carved/Extracted | Description                                                                                    | File Name |
+---------+------------------+------------------------------------------------------------------------------------------------+-----------+
| 0x9be2  | Carved           | LZMA compressed data, properties: 0x92, dictionary size: 0 bytes, uncompressed size: 512 bytes | 9BE2.7z   |
| 0x9be2  | Extracted        | LZMA compressed data, properties: 0x92, dictionary size: 0 bytes, uncompressed size: 512 bytes | 9BE2      |
| 0x15101 | Carved           | LZMA compressed data, properties: 0xB4, dictionary size: 0 bytes, uncompressed size: 112 bytes | 15101.7z  |
| 0x15101 | Extracted        | LZMA compressed data, properties: 0xB4, dictionary size: 0 bytes, uncompressed size: 112 bytes | 15101     |
| 0x1a99e | Carved           | LZMA compressed data, properties: 0x7E, dictionary size: 0 bytes, uncompressed size: 128 bytes | 1A99E.7z  |
| 0x1a99e | Extracted        | LZMA compressed data, properties: 0x7E, dictionary size: 0 bytes, uncompressed size: 128 bytes | 1A99E     |
| 0x1ae9a | Carved           | LZMA compressed data, properties: 0xC0, dictionary size: 0 bytes, uncompressed size: 120 bytes | 1AE9A.7z  |
| 0x1ae9a | Extracted        | LZMA compressed data, properties: 0xC0, dictionary size: 0 bytes, uncompressed size: 120 bytes | 1AE9A     |
+---------+------------------+------------------------------------------------------------------------------------------------+-----------+
```

As we can see, it found something with StegHide. If we navigate to the directory, we can read the contents found.

This looked like it was part of a password.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cat /home/kali/Downloads/results/steghide_964494712a76f5e28e9355b2a95d0253.bin

s4nd_w0rd5      
```

However, this is not the password to the `stage_two.zip` file.

I looked through the `results` directory which contained images of different contrast extracted by `StegoVeritas` and found that there were some `QR Code` in the images.

Running `zbarimg` would give us what seemed like another part of the password.

```bash
┌──(kali㉿kali)-[~/Downloads/results]
└─$ zbarimg p1c7ur3.jpg_equalize.png 
QR-Code:_w0rth_4_th0u
scanned 1 barcode symbols from 1 images in 0.05 seconds
```

If we combined this two parts, it would be `_w0rth_4_th0us4nd_w0rd5`. However, this was still not the password to the next zip file and it seemed like there were still some part(s) of it missing.

I tried to look around using other tools like `exiftool`, `binwalk` and `ghex`, but could not find anything that could be hidden as part of the password.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ exiftool p1c7ur3.jpg 
ExifTool Version Number         : 12.44
File Name                       : p1c7ur3.jpg
Directory                       : .
File Size                       : 402 kB
File Modification Date/Time     : 2023:02:26 15:49:25-05:00
File Access Date/Time           : 2023:03:08 03:23:48-05:00
File Inode Change Date/Time     : 2023:03:08 03:23:50-05:00
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : inches
X Resolution                    : 72
Y Resolution                    : 72
Image Width                     : 850
Image Height                    : 637
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:4:4 (1 1)
Image Size                      : 850x637
Megapixels                      : 0.541
```

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ binwalk p1c7ur3.jpg 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01

```

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ ghex p1c7ur3.jpg
```

Then, I realized that the combined password was in leetspeak previously. The image filename was also in leetspeak. If we combined those, we will get `p1c7ur3_w0rth_4_th0us4nd_w0rd5` which is the password for `stage_two.zip`.

We can extract the contents of stage two using the password

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ 7z x stage_two.zip

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 21820661 bytes (21 MiB)

Extracting archive: stage_two.zip
--
Path = stage_two.zip
Type = zip
Physical Size = 21820661

    
Would you like to replace the existing file:
  Path:     ./README.txt
  Size:     0 bytes
  Modified: 2023-02-26 20:06:55
with the file from archive:
  Path:     README.txt
  Size:     61 bytes (1 KiB)
  Modified: 2023-02-26 20:06:55
? (Y)es / (N)o / (A)lways / (S)kip all / A(u)to rename all / (Q)uit? y

                 
Enter password (will not be echoed):
Everything is Ok 

Files: 2
Size:       21820343
Compressed: 21820661
```

### Stage two

At stage two, there is a `README.txt` file. We read the contents of it to get more information about the password.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cat README.txt
The password is at most 8 characters, all lowercase alphabet.   
```

Now that we know the password is at most 8 characters and all lowercase, we can use `John The Ripper` to perform a dictionary attack on it.

First, we convert it to the hash and use the `rockyou.txt` file to crack the password.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ zip2john stage_three.zip > hash              
ver 2.0 stage_three.zip/broken.png PKZIP Encr: cmplen=217796, decmplen=218305, crc=D94A1499 ts=9726 cs=d94a type=8
ver 2.0 stage_three.zip/stage_four.zip PKZIP Encr: cmplen=21602192, decmplen=21602180, crc=05D30748 ts=9896 cs=05d3 type=0
NOTE: It is assumed that all files in each archive have the same password.
If that is not the case, the hash may be uncrackable. To avoid this, use
option -o to pick a file at a time.
                                                                                                                   
┌──(kali㉿kali)-[~/Downloads]
└─$ john -w=/usr/share/wordlists/rockyou.txt hash
Using default input encoding: UTF-8
Loaded 1 password hash (PKZIP [32/64])
Will run 2 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
scrabble         (stage_three.zip)     
1g 0:00:00:00 DONE (2023-03-19 02:22) 100.0g/s 1638Kp/s 1638Kc/s 1638KC/s havana..cocoliso
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
```

The password cracked is: `scrabble` and we can use it to extract the contents of `stage_three.zip`.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ 7z x stage_three.zip 

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 21820282 bytes (21 MiB)

Extracting archive: stage_three.zip
--
Path = stage_three.zip
Type = zip
Physical Size = 21820282

    
Enter password (will not be echoed):
Everything is Ok 

Files: 2
Size:       21820485
Compressed: 21820282
```

### Stage three

In stage three, the file given is `broken.png`. Opening it on hex editor showed that there were multiple bytes that were incorrect and needed fixing.

<figure><img src="../.gitbook/assets/image (1) (1) (2) (2).png" alt=""><figcaption></figcaption></figure>

The headers can be replaced as follows:

* `NEV` to `PNG`
* `ERGO` to `IHDR`
* `NNAG` to `sRGB`
* `IVEY` to `pHYs`
* `OUUP` to `IDAT`

Once they are replaced, the `.png` file will be fixed.

<figure><img src="../.gitbook/assets/image (7) (6).png" alt=""><figcaption></figcaption></figure>

We can then open the image in image viewer using the `eog` command

<figure><img src="../.gitbook/assets/image (4) (1) (2).png" alt=""><figcaption></figcaption></figure>

This is a statue with a toga in a box, implying the use of Caesar Box Cipher on the text below. We can decrypt this in [CyberChef](https://cyberchef.org/#recipe=Caesar\_Box\_Cipher\(4\)To\_Lower\_case\(\)\&input=VlZWQjMxMTBORENDMTExMQ).

<figure><img src="../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

This gives us the password: `v3n1v1d1v1c1b0c1`which can be used to extract the contents of `stage_four.zip`.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ 7z x stage_four.zip 

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 21602180 bytes (21 MiB)

Extracting archive: stage_four.zip
--
Path = stage_four.zip
Type = zip
Physical Size = 21602180

    
Enter password (will not be echoed):
Everything is Ok        

Files: 3
Size:       23520385
Compressed: 21602180
```

### Stage four

In stage four we can read the `clarification.txt` file to get a better idea of the password.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cat clarification.txt 
Whatever letters in the password will be lowercase.   
```

We were also given a `track.wav` file which is an audio file. If we listened to it carefully, we can hear morse code at around `1:19 to 1:46`.

We can convert the `Morse Code` in [CyberChef](https://cyberchef.org/#recipe=From\_Morse\_Code\('Space','Line%20feed'\)To\_Lower\_case\(\)\&input=LS0gLS0tLS0gLi0uIC4uLiAuLi4tLSAtLSAuLi0gLi4uLi4gLi0tLS0gLS4tLiAuLi4), which gives us the password for the last zip file: `stage_five.zip`. The password is: `m0rs3mu51cs`.

Using this password, we extract the contents in `stage_five.zip`.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ 7z x stage_five.zip 

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 188 bytes (1 KiB)

Extracting archive: stage_five.zip
--
Path = stage_five.zip
Type = zip
Physical Size = 188

    
Would you like to replace the existing file:
  Path:     ./flag
  Size:     45 bytes (1 KiB)
  Modified: 2023-03-14 22:29:52
with the file from archive:
  Path:     flag
  Size:     34 bytes (1 KiB)
  Modified: 2023-02-26 19:52:26
? (Y)es / (N)o / (A)lways / (S)kip all / A(u)to rename all / (Q)uit? y

           
Enter password (will not be echoed):
Everything is Ok

Size:       34
Compressed: 188
```

### &#x20;Stage five

Finally, we can read the contents of the flag extracted from the zip file.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cat flag     
wxmctf{unz1pp3d_4nd_0p3n3d_7a6970}    
```

Flag: wxmctf{unz1pp3d\_4nd\_0p3n3d\_7a6970}&#x20;
