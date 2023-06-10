# Cyber Forensics

## Zip series 2

<figure><img src="../../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.zip` file.

First, we can run  `binwalk` to check for any hidden files.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ binwalk secret.zip   

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             Zip archive data, at least v2.0 to extract, compressed size: 84316, uncompressed size: 84286, name: .catchme.7z
84357         0x14985         Zip archive data, at least v2.0 to extract, compressed size: 11, uncompressed size: 9, name: password.txt
84410         0x149BA         Zip archive data, at least v2.0 to extract, compressed size: 20, uncompressed size: 18, name: USERINFO.txt
84753         0x14B11         End of Zip archive, footer length: 22

```

We can extract these by using the `-e` option

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ binwalk -e secret.zip 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------

WARNING: Extractor.execute failed to run external extractor 'jar xvf '%e'': [Errno 2] No such file or directory: 'jar', 'jar xvf '%e'' might not be installed correctly
0             0x0             Zip archive data, at least v2.0 to extract, compressed size: 84316, uncompressed size: 84286, name: .catchme.7z
84357         0x14985         Zip archive data, at least v2.0 to extract, compressed size: 11, uncompressed size: 9, name: password.txt
84410         0x149BA         Zip archive data, at least v2.0 to extract, compressed size: 20, uncompressed size: 18, name: USERINFO.txt
84753         0x14B11         End of Zip archive, footer length: 22
```

If we navigate into the directory, we will see that there is a "hidden" `.7z` file. By running the command `ls -la`, we will be able to see it.

```bash
┌──(kali㉿kali)-[~/Downloads/_secret.zip.extracted]
└─$ ls -la
total 252
drwxr-xr-x   2 kali kali  4096 May 15 21:55 .
drwxr-xr-x 198 kali kali 69632 May 15 21:55 ..
-rw-r--r--   1 kali kali 84775 May 15 21:55 0.zip
-rw-r--r--   1 kali kali 84286 Feb 19 22:25 .catchme.7z
-rw-r--r--   1 kali kali     9 Feb 19 09:21 password.txt
-rw-r--r--   1 kali kali    18 Feb 19 09:20 USERINFO.txt
```

Lets check the contents of `password.txt` which likely is the password to unzip the `.7z` file.

```bash
┌──(kali㉿kali)-[~/Downloads/_secret.zip.extracted]
└─$ cat password.txt                      
PQ3$109~!                                           
```

Using the password, we are able to extract a `.FLAG.jpg` file.

```bash
┌──(kali㉿kali)-[~/Downloads/_secret.zip.extracted]
└─$ 7z x .catchme.7z                      

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 84286 bytes (83 KiB)

Extracting archive: .catchme.7z

Enter password (will not be echoed):
--
Path = .catchme.7z
Type = 7z
Physical Size = 84286
Headers Size = 222
Method = LZMA2:96k 7zAES
Solid = -
Blocks = 1

Everything is Ok

Size:       85124
Compressed: 84286
```

Again, using the `ls -la` command, we can see this.

```bash
┌──(kali㉿kali)-[~/Downloads/_secret.zip.extracted]
└─$ ls -la
total 336
drwxr-xr-x   2 kali kali  4096 May 15 21:55 .
drwxr-xr-x 198 kali kali 69632 May 15 21:55 ..
-rw-r--r--   1 kali kali 84775 May 15 21:55 0.zip
-rw-r--r--   1 kali kali 84286 Feb 19 22:25 .catchme.7z
-rw-r--r--   1 kali kali 85124 Feb 19 09:22 .FLAG.jpg
-rw-r--r--   1 kali kali     9 Feb 19 09:21 password.txt
-rw-r--r--   1 kali kali    18 Feb 19 09:20 USERINFO.txt
```

Get the MD5 hash value of the file, which is the flag.

```bash
┌──(kali㉿kali)-[~/Downloads/_secret.zip.extracted]
└─$ md5sum .FLAG.jpg
9bffc1ad4e6e2ee6fb5f472d9bc908ac  .FLAG.jpg
```

Flag: 9bffc1ad4e6e2ee6fb5f472d9bc908ac

## Secret Letter

<figure><img src="../../../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>

For this challenge, I downloaded the `.xls` file and opened it Excel Workbook.&#x20;

We can see that there are macros in the excel file, hence its blocked.

<figure><img src="../../../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>

Notice there is  a key: `Jennis_This_is_our_secret123_XXD` as well.

On my Kali Linux VM, I ran olevba on the `.xls` file.

> olevba is a script to parse OLE and OpenXML files such as MS Office documents (e.g. Word, Excel), to **detect VBA Macros**, extract their **source code** in clear text, and detect security-related patterns such as **auto-executable macros**, **suspicious VBA keywords** used by malware, anti-sandboxing and anti-virtualization techniques, and potential **IOCs** (IP addresses, URLs, executable filenames, etc). It also detects and decodes several common **obfuscation methods including Hex encoding, StrReverse, Base64, Dridex, VBA expressions**, and extracts IOCs from decoded strings. XLM/Excel 4 Macros are also supported in Excel and SLK files

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ olevba Finance\ Data.xls
olevba 0.60.1 on Python 2.7.18 - http://decalage.info/python/oletools
===============================================================================
FILE: Finance Data.xls
Type: OLE
WARNING  invalid value for PROJECTLCID_Id expected 0002 got 004A
WARNING  invalid value for PROJECTLCID_Lcid expected 0409 got 0004
WARNING  invalid value for PROJECTLCIDINVOKE_Id expected 0014 got 0002
WARNING  invalid value for PROJECTCODEPAGE_Id expected 0003 got 0014
WARNING  invalid value for PROJECTCODEPAGE_Size expected 0002 got 0004
WARNING  invalid value for PROJECTNAME_Id expected 0004 got 0000
ERROR    PROJECTNAME_SizeOfProjectName value not in range [1-128]: 131075
ERROR    Error in _extract_vba
Traceback (most recent call last):
  File "/usr/local/lib/python2.7/dist-packages/oletools/olevba.py", line 3528, in extract_macros
    dir_path, self.relaxed):
  File "/usr/local/lib/python2.7/dist-packages/oletools/olevba.py", line 2094, in _extract_vba
    project = VBA_Project(ole, vba_root, project_path, dir_path, relaxed)
  File "/usr/local/lib/python2.7/dist-packages/oletools/olevba.py", line 1752, in __init__
    projectdocstring_id = struct.unpack("<H", dir_stream.read(2))[0]
error: unpack requires a string argument of length 2
-------------------------------------------------------------------------------
VBA MACRO ThisWorkbook 
in file: Finance Data.xls - OLE stream: u'ThisWorkbook'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
Private Sub Workbook_Open()
    MsgBox ("HELLO?")
    
End Sub
-------------------------------------------------------------------------------
VBA MACRO Sheet1 
in file: Finance Data.xls - OLE stream: u'Sheet1'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
(empty macro)
-------------------------------------------------------------------------------
VBA MACRO Module1 
in file: Finance Data.xls - OLE stream: u'Module1'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 

    
Sub TOPSECRET()
    Dim plaintext As String
    Dim key As String
    Dim ciphertext() As Byte
    Dim i As Integer
    Dim hexresult As String
    
    plaintext = InputBox("Enter plaintext:", "Secret Message")
    key = InputBox("Our key:", "Secret Message")
    
    ciphertext = TOPTOPTOPTOP(plaintext, key)
    
    For i = 0 To UBound(ciphertext)
        hexresult = hexresult & Right("0" & hex(ciphertext(i)), 2)
    Next i
    
End Sub



Function TOPTOPTOPTOP(ByVal data As String, ByVal key As String) As String
    Dim s() As Byte
    Dim k() As Byte
    Dim temp As Byte
    Dim i As Integer
    Dim j As Integer
    Dim x As Integer
    Dim result As String
    
    Dim index1 As Integer
    Dim index2 As Integer
    
    index1 = i Mod 256
    index2 = j Mod 256
    
    ' Initialize s array
    ReDim s(255)
    For i = 0 To 255
        s(i) = i
    Next i
    
    ' Initialize k array
    ReDim k(Len(key) - 1)
    For i = 0 To Len(key) - 1
        k(i) = Asc(Mid(key, i + 1, 1))
    Next i
    
    ' Key-scheduling algorithm
    j = 0
    For i = 0 To 255
        j = (j + s(i) + k(i Mod Len(key))) Mod 256
        temp = s(i)
        s(i) = s(j)
        s(j) = temp
    Next i
    
    ' Pseudo-random generation algorithm
    i = 0
    j = 0
    result = ""
    For x = 0 To Len(data) - 1
        i = (i + 1) Mod 256
        j = (j + s(i)) Mod 256
        temp = s(i)
        s(i) = s(j)
        s(j) = temp
        result = result & hex(s((s(index1) + s(index2)) Mod 256) Xor Asc(Mid(data, x + 1, 1)))
    Next x
    
    ' Return encrypted bytes
    TOPTOPTOPTOP = result
End Function
-------------------------------------------------------------------------------
VBA MACRO Sheet2 
in file: Finance Data.xls - OLE stream: u'Sheet2'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
(empty macro)
-------------------------------------------------------------------------------
VBA MACRO UserForm1 
in file: Finance Data.xls - OLE stream: u'UserForm1'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
(empty macro)
-------------------------------------------------------------------------------
VBA MACRO UserForm2 
in file: Finance Data.xls - OLE stream: u'UserForm2'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
(empty macro)
-------------------------------------------------------------------------------
VBA MACRO xlm_macro.txt 
in file: xlm_macro - OLE stream: 'xlm_macro'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
' 0085     14 BOUNDSHEET : Sheet Information - worksheet or dialog sheet, visible - Sheet
' 0085     14 BOUNDSHEET : Sheet Information - worksheet or dialog sheet, hidden - Sheet
-------------------------------------------------------------------------------
VBA FORM STRING IN 'Finance Data.xls' - OLE stream: u'_VBA_PROJECT_CUR/UserForm1/o'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
�please decrypt me 4f0f59a1d8c85e97dc6e52a03ebf617342443cc602b83c2da97d0adf3c72cbe2 ��
-------------------------------------------------------------------------------
VBA FORM STRING IN 'Finance Data.xls' - OLE stream: u'_VBA_PROJECT_CUR/UserForm2/o'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
�Please kill Dorohykl

He will be reached at the Marina Baysands on 21 Nov 2023�
-------------------------------------------------------------------------------
VBA FORM Variable "important" IN 'Finance Data.xls' - OLE stream: u'_VBA_PROJECT_CUR/UserForm1'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
None
-------------------------------------------------------------------------------
VBA FORM Variable "Label1" IN 'Finance Data.xls' - OLE stream: u'_VBA_PROJECT_CUR/UserForm2'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
None
+----------+--------------------+---------------------------------------------+
|Type      |Keyword             |Description                                  |
+----------+--------------------+---------------------------------------------+
|AutoExec  |Workbook_Open       |Runs when the Excel Workbook is opened       |
|Suspicious|kill                |May delete a file                            |
|Suspicious|Xor                 |May attempt to obfuscate specific strings    |
|          |                    |(use option --deobf to deobfuscate)          |
|Suspicious|Hex Strings         |Hex-encoded strings were detected, may be    |
|          |                    |used to obfuscate strings (option --decode to|
|          |                    |see all)                                     |
+----------+--------------------+---------------------------------------------+

/usr/local/lib/python2.7/dist-packages/msoffcrypto/method/rc4.py:5: CryptographyDeprecationWarning: Python 2 is no longer supported by the Python core team. Support for it is now deprecated in cryptography, and will be removed in the next release.
  from cryptography.hazmat.backends import default_backend
```

We can see `please decrypt me 4f0f59a1d8c85e97dc6e52a03ebf617342443cc602b83c2da97d0adf3c72cbe2` and what seemed like a simplified version of the RC4 encryption algorithm based on the code in the macro.

In [CyberChef](https://cyberchef.org/#recipe=RC4\(%7B'option':'UTF8','string':'Jennis\_This\_is\_our\_secret123\_XXD'%7D,'Hex','Hex'\)From\_Hex\('None'\)\&input=NGYwZjU5YTFkOGM4NWU5N2RjNmU1MmEwM2ViZjYxNzM0MjQ0M2NjNjAyYjgzYzJkYTk3ZDBhZGYzYzcyY2JlMg), we can use this input: `4f0f59a1d8c85e97dc6e52a03ebf617342443cc602b83c2da97d0adf3c72cbe2`,  with the following passphrase: `Jennis_This_is_our_secret123_XXD`

<figure><img src="../../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

Alternatively, we could use this simple Python script to decrypt it.

```python
from Crypto.Cipher import ARC4

ciphertext_hex = "4f0f59a1d8c85e97dc6e52a03ebf617342443cc602b83c2da97d0adf3c72cbe2"
key = "Jennis_This_is_our_secret123_XXD"

ciphertext = bytes.fromhex(ciphertext_hex)

cipher = ARC4.new(key.encode())
plaintext = cipher.decrypt(ciphertext)

print(plaintext.decode())
```

Do run pip install cffi pycryptodome first before running the script, make sure the modules are installed.

Run the Python script to get the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ python flag.py  
2c5c4614730d1be9df6116a65a6d8893
```

Flag: 2c5c4614730d1be9df6116a65a6d8893

## Mobile Contract

<figure><img src="../../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was mobile related. I searched online on where contacts are stored on android and  found  [this](https://www.fonepaw.com/transfer/where-are-contacts-stored-on-android.html).

We will get a bunch of  files and folders upon unzipping the `.7z` file.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ 7z x data.7z

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 140975147 bytes (135 MiB)

Extracting archive: data.7z
--
Path = data.7z
Type = 7z
Physical Size = 140975147
Headers Size = 61815
Method = LZMA2:26
Solid = +
Blocks = 1

Everything is Ok                                                               

Folders: 1398
Files: 3350
Size:       309495783
Compressed: 140975147
```

In Kali Linux VM, we can use `SQLite database browser` to view the database.

<figure><img src="../../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

We load the following `com.android.providers.contacts/databases/contacts2.db`

<figure><img src="../../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

Alternatively, I used the `sqlite3` command to view the table and its contents.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ sqlite3 com.android.providers.contacts/databases/contacts2.db
SQLite version 3.40.1 2022-12-28 14:03:47
Enter ".help" for usage hints.
sqlite> .tables
_sync_state               phone_lookup              view_data               
_sync_state_metadata      photo_files               view_data_usage         
accounts                  pre_authorized_uris       view_entities           
agg_exceptions            presence                  view_groups             
agg_presence              properties                view_raw_contacts       
android_metadata          raw_contacts              view_raw_entities       
contacts                  search_index              view_settings           
data                      search_index_content      view_stream_items       
data_usage_stat           search_index_docsize      view_v1_contact_methods 
default_directory         search_index_segdir       view_v1_extensions      
deleted_contacts          search_index_segments     view_v1_group_membership
directories               search_index_stat         view_v1_groups          
groups                    status_updates            view_v1_organizations   
mimetypes                 stream_item_photos        view_v1_people          
name_lookup               stream_items              view_v1_phones          
nickname_lookup           v1_settings               view_v1_photos          
packages                  view_contacts             visible_contacts     
```

From here, I tried a few SQL commands to view the contacts.  However, none of these were the correct flag.

```bash
sqlite> select display_name from view_contacts;
display_name           
-----------------------
BF. Alice              
My Boyfriend Top Secret
My Home                
Friend Darry           
My Mum                 
sqlite> select * from raw_contacts;
1|1|||0|3|1|0|0|1|0|0||0|0||0||0|0|BF. Alice|BF. Alice|40||0|BF. Alice|B|2|BF. Alice|B|2|0||||
2|1|||0|3|1|0|0|2|0|0||0|0||0||0|0|My Boyfriend Top Secret|Top Secret, My Boyfriend|40||0|My Boyfriend Top Secret|M|13|Top Secret, My Boyfriend|T|20|0||||
3|1|||0|3|1|0|0|3|0|0||0|0||0||0|0|My Home|My Home|40||0|My Home|M|13|My Home|M|13|0||||
4|1|||0|3|1|0|0|4|0|0||0|0||0||0|0|Friend Darry|Friend Darry|40||0|Friend Darry|F|6|Friend Darry|F|6|0||||
5|1|||0|3|1|0|0|5|0|0||0|0||0||0|0|My Mum|My Mum|40||0|My Mum|M|13|My Mum|M|13|0||||

sqlite> select display_name from  view_data;
BF. Alice
BF. Alice
My Boyfriend Top Secret
My Boyfriend Top Secret
My Boyfriend Top Secret
My Home
My Home
Friend Darry
Friend Darry
My Mum
My Mum
```

Finally, I found his name from `data`

```bash
sqlite> select * from data;
1||5|1|CEhneIsIf/vbH0NokoaXD+dedug=
|0|0|0|0|+62 254 123358|2||+62254123358||||||||||||||||0|0||
2||7|1|qXVpnXgcBmNoY0Dl6F814V7FW8s=
|0|1|1|1|BF. Alice|BF. Alice||||||||1|0|||||||||0|0||
3||5|2|yBFJkQ+j3IYD+ivlXQu6R4D2s5E=
|0|0|0|0|+32541335812536|2||||||||||||||||||0|0||
4||12|2|xJuILcz1b07dqZDwpbEBUhdgJGg=
|0|0|0|0|His name is Sephana Bow|||||||||||||||||||0|0||
5||7|2|qOsOMTeXIlnxNOYCxodLayq99Ps=
|0|1|1|1|My Boyfriend Top Secret|My Boyfriend|Top Secret|||||||1|0|||||||||0|0||
6||5|3|n0IQQxYwqjVsqqlrZZUTY5PTH8U=
|0|0|0|0|+1 585-632-12|2||||||||||||||||||0|0||
7||7|3|Mvg9WARb/9lyfDs+ysF3nL13p4Y=
|0|1|1|1|My Home|My Home||||||||1|0|||||||||0|0||
8||5|4|QFo9ph1eA83Y31PrIaBhmRHl1Jg=
|0|0|0|0|+65 8541 3226|2||+6585413226||||||||||||||||0|0||
9||7|4|aRaW4cHOmQdDyUA2JXSIgkzrhhE=
|0|1|1|1|Friend Darry|Friend Darry||||||||1|0|||||||||0|0||
10||5|5|Ik1Zil6FWCRWGAOItzSN8kkPV4w=
|0|0|0|0|+4532215544123|2||||||||||||||||||0|0||
11||7|5|ujbjHfkduti+zwDYBFxoW4QF7nk=
|0|1|1|1|My Mum|My Mum||||||||1|0|||||||||0|0||
```

We can see `His name is Sephana Bow`

The MD5 hash value is the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ echo -n Sephana Bow | md5sum 
e54c79f7c32b4dcf5e7360a7698b471c  -
```

Flag: e54c79f7c32b4dcf5e7360a7698b471c

## Finding the boy’s secret document

<figure><img src="../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

This challenge was probably the most interesting one out of the many other challenges I solved in this training. It also had one of the least solves. I got to learn more about PDF structure through my own research as well.

For this challenge, we were given a `.vhd` file. I tried to load this into `FTK Imager` by `Add Evidence Item > Image File`

We can see `secret.pdf` in the Alternate Data Stream(ADS) of `mynote.txt`. I have previously solved a challenge related to ADS in  [CSIT CNY 2023 Challenge](https://gadiel-lau.gitbook.io/2023-writeups/2023-ctfs/csit-cny-2023-challenge).  Do check it out if you would like to find out more.

<figure><img src="../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

Back to the challenge, there were a few other pdf files in there where we could verify the correct format. The PDF should start with %PDF-{version number} and end with %%EOF.&#x20;

In this case, the PDF file seemed reversed.

I tried to reverse it by using [CyberChef](https://cyberchef.org/) and [Online Text Reverse](https://www.textreverse.com/), but this method did not work.

The PDF opened as blank for both pages. Thus, I decided to try an alternative method using Kali Linux VM.

We can use `7z x` to extract the contents in the `.vhd` file, including the ADS.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ 7z x writer.vhd

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz (806C1),ASM,AES-NI)

Scanning the drive for archives:
1 file, 83886592 bytes (81 MiB)

Extracting archive: writer.vhd
--       
Path = writer.vhd
Type = VHD
Physical Size = 83886592
Offset = 0
Created = 2023-03-09 13:10:43
Method = Fixed
Creator Application = win 10.0
Host OS = Windows
Saved State = -
ID = FBD79DE660F9F34DB4C1516C3D7439E7
----
Size = 83886080
Packed Size = 83886080
Created = 2023-03-09 13:10:43
--
Path = writer.gpt
Type = GPT
Physical Size = 83886080
ID = 1BBE4C3B-F82D-4D6D-8908-D1E580288E83
----
Path = Basic data partition.img
Size = 81788928
File System = Windows BDP
Offset = 65536
ID = E1424F3B-9164-496E-8B1A-59CE70DC189F
--
Path = Basic data partition.img
Type = NTFS
Physical Size = 81788928
Label = New Volume
File System = NTFS 3.1
Cluster Size = 4096
Sector Size = 512
Record Size = 1024
Created = 2023-03-09 09:10:56
ID = 188190166569313287

Everything is Ok

Folders: 10
Files: 25
Alternate Streams: 10
Alternate Streams Size: 1382542
Size:       11365663
Compressed: 83886592
```

Lets verify again that  the start and end shows that the PDF is reversed.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cat mynote.txt:secret.pdf | head
%%EOF63385
startxref
<</Size 53/Root 1 0 R/Info 16 0 R/ID[<0414D08488CDAE4893F141967F54B148><0414D08488CDAE4893F141967F54B148>] /Prev 62168/XRefStm 61815>>
trailer
0 0
xref
%%EOF
62168
startxref
<</Size 53/Root 1 0 R/Info 16 0 R/ID[<0414D08488CDAE4893F141967F54B148><0414D08488CDAE4893F141967F54B148>] >>

┌──(kali㉿kali)-[~/Downloads]
└─$ cat mynote.txt:secret.pdf | tail
<</Type/Page/Parent 2 0 R/Resources<</Font<</F1 5 0 R/F2 12 0 R>>/ExtGState<</GS10 10 0 R/GS11 11 0 R>>/ProcSet[/PDF/Text/ImageB/ImageC/ImageI] >>/MediaBox[ 0 0 612 792] /Contents 4 0 R/Group<</Type/Group/S/Transparency/CS/DeviceRGB>>/Tabs/S/StructParents 0>>
3 0 obj
endobj
<</Type/Pages/Count 2/Kids[ 3 0 R 14 0 R] >>
2 0 obj
endobj
<</Type/Catalog/Pages 2 0 R/Lang(en-GB) /StructTreeRoot 17 0 R/MarkInfo<</Marked true>>/Metadata 50 0 R/ViewerPreferences 51 0 R>>
1 0 obj
%����
%PDF-1.7
```

Now, we can reverse the PDF using `tac` command and save it to flag.pdf

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ tac mynote.txt:secret.pdf > flag.pdf
```

Opening the PDF showed a story of tortoise and hare on Page 1. However, Page 2 seemed blank or corrupted.

<figure><img src="../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

I started to do more research on PDFs and found that [this ](https://resources.infosecinstitute.com/topic/pdf-file-format-basic-structure/)was pretty good at covering the structure of PDF.

Next, I ran `exiftool` and saw a warning: `Kids object (14 0 obj) not found`

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ exiftool flag.pdf
ExifTool Version Number         : 12.57
File Name                       : flag.pdf
Directory                       : .
File Size                       : 64 kB
File Modification Date/Time     : 2023:05:21 07:41:31-04:00
File Access Date/Time           : 2023:05:21 07:41:31-04:00
File Inode Change Date/Time     : 2023:05:21 07:41:31-04:00
File Permissions                : -rw-r--r--
File Type                       : PDF
File Type Extension             : pdf
MIME Type                       : application/pdf
PDF Version                     : 1.7
Linearized                      : No
Page Count                      : 2
Warning                         : Kids object (14 0 obj) not found at offset 3262
Language                        : en-GB
Tagged PDF                      : Yes
XMP Toolkit                     : 3.1-701
Producer                        : Microsoft® Word for Microsoft 365
Creator                         : Jeong Sangsoo
Creator Tool                    : Microsoft® Word for Microsoft 365
Create Date                     : 2023:03:09 21:49:28+09:00
Modify Date                     : 2023:03:09 21:49:28+09:00
Document ID                     : uuid:84D01404-CD88-48AE-93F1-41967F54B148
Instance ID                     : uuid:84D01404-CD88-48AE-93F1-41967F54B148
Author                          : Jeong Sangsoo
```

If we use `strings` command to check, we would see there’s two object 13. However, object 14 is not found and it goes to object 15.

I suspected that the 2nd object 13 should be object 14.

I opened it in hex editor, changed byte 33 to 34

Similarly, from the previous exiftool warning, we can go to offset 3262, which is 0xCBE, and will be able to see the duplicated object 13.

<figure><img src="../../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

Change byte 33 to 34, save and open

<figure><img src="../../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

The flag can be found on page 2 now.

<figure><img src="../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

Flag: 5b9f2f30e1abeeece18b4553ed23566b
