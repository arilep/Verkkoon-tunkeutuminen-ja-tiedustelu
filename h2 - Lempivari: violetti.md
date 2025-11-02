### h2 Lempiväri: Violetti [Tehtävänanto](https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#h2-lempivari-violetti)

## Tehtävissä käytetty ympäristö

### PC

- Käyttöjärjestelmä: Windows 11 Home 64-bit
- Suoritin: AMD Ryzen 7 5800X 8-Core Processor
- Muisti: 32GB RAM
- Näytönohjain: NVIDIA GeForce RTX 3080
- Virtualisointiohjelmisto: Oracle VM VirtualBox 7.0

- Internet yhteys: DNA Netti 600 M

### Virtuaalikone

- Kali Linux [Get Kali](https://www.kali.org/get-kali/#kali-installer-images)
- Base Memory: 8192 MB
- Processors: 1
- Virtual HD: 60 GB
- Video Memory: 128 MB

## x) Tuskan pyramidi ja timanttimalli

### Tuskan Pyramidi (Pyramid of Pain)

- Pyramidi kuvaa eri indikaattorien yhteyksiä, joita voidaan käyttää hyökkääjää vastaan, ja kuinka paljon ne vaikeuttavat hyökkääjän toimia, kun kyseiset indikaattorit estetään.
- Tavoitteena tehdä hyökkäyksestä niin vaikeaa, että hyökkääjä luovuttaa.

### Timanttimalli (Diamond Model)

- Viitekehys ulkoisten ja sisäisten hyökkäysten analysointiin ja torjuntaan.
- Malli kuvaa hyökkäysten eri vaiheet tapahtumaketjuna, joissa tutkaillaan neljän ydintoiminnon välisiä suhteita: hyökkääjä (adversary), uhri (victim), kyvykkyys (capability) ja infrastruktuuri (infrastructure).

## a) Apache log. Asenna Apache-weppipalvelin paikalliselle virtuaalikoneellesi. Surffaa palvelimellesi salaamattomalla HTTP-yhteydellä, http://localhost . Etsi omaa sivulataustasi vastaava lokirivi. Analysoi yksi tällainen lokirivi, eli selitä sen kaikki kohdat.

Ajoin Apache asennusta varten seuraavat komennot. Apache oli Kaliin valmiiksi asennettuna ja sain ilmoituksen "apache2 is already the newest version (2.4.65-3+b1)".

    sudo apt-get update
    sudo apt-get install apache2

Tämän jälkeen käynnistin Apachen:

    sudo systemctl start apache2

Menin selaimella osoitteeseen 'http://localhost' ja tarkistin että Apache oletussivu näkyy:

<img width="807" height="653" alt="image" src="https://github.com/user-attachments/assets/f08c5a4b-6341-4526-9c0c-5b6d9c5038f4" />

Tämän jälkeen tarkistin lokin komennolla: `sudo tail -F /var/log/apache2/access.log`:

```
127.0.0.1 - - [02/Nov/2025:19:25:53 +0200] "GET / HTTP/1.1" 200 3383 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0"
127.0.0.1 - - [02/Nov/2025:19:25:54 +0200] "GET /icons/openlogo-75.png HTTP/1.1" 200 6040 "http://localhost/" "Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0"
127.0.0.1 - - [02/Nov/2025:19:25:54 +0200] "GET /favicon.ico HTTP/1.1" 404 487 "http://localhost/" "Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0"
```

Perehdyin [Apachen dokumentaatio](https://httpd.apache.org/docs/2.4/logs.html#accesslog) sivustoon, jossa käydään access login rakenne läpi. Avasin sen pohjalta ensimmäisen rivin:

`127.0.0.1` Asiakkaan (client) ip-osoite

`-` Asiakkaan identiteetti. Ei käytössä, jolloin merkitään '-'.

`-` Käyttäjätunnus jos http-autentikointi on käytössä. Ei käytössä, jolloin merkitään '-'.

`[02/Nov/2025:19:25:53 +0200]` Aika ja päivämäärä jolloin pyyntö vastaanotettu.

`GET` Pyynnön metodi.

`/` Pyydetty resurssi.

`HTTP/1.1` Käytetty HTTP-protokolla.

`200` Statuskoodi. 200 = onnistunut pyyntö.

`3383` Vastauksen sisällön koko tavuina.

`"-"` Viittaus, joka kertoo miltä sivulta käyttäjä tuli. Sivu avattiin suoraan selaimelta = ei viittausta, joten merkitään '-'.

`"Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0"` User-Agent. Tunnistetieto jonka asiakkaan selain ilmoittaa (käyttöjärjestelmä ja selain).


## b) Nmapped. Porttiskannaa oma weppipalvelimesi käyttäen localhost-osoitetta ja 'nmap -A' päällä. Selitä tulokset. (Pelkkä http-portti 80/tcp riittää)



Aloitin katkaisemalla verkkoyhteyden siirtymällä virtuaalikoneen verkkoasetuksiin (Machine > Settings... > Network) ja poistin valinnan 'cable connected'. Tämän jälkeen tarkistin ettei virtuaalikoneella ole yhteyttä verkkoon:

<img width="348" height="131" alt="image" src="https://github.com/user-attachments/assets/cd6cb9fa-4671-4645-a2af-817d6a28228c" />

Varmistuttuani ettei virtuaalikoneessa ole verkkoyhteyttä, tein porttiskannauksen localhost-osoitteeseen ja porttiin 80.

    sudo nmap -T4 -vv -A -p 80 localhost

Skannauksen tulos:

```
Starting Nmap 7.95 ( https://nmap.org ) at 2025-11-02 20:27 EET
NSE: Loaded 157 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 20:27
Completed NSE at 20:27, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 20:27
Completed NSE at 20:27, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 20:27
Completed NSE at 20:27, 0.00s elapsed
Warning: Hostname localhost resolves to 2 IPs. Using 127.0.0.1.
mass_dns: warning: Unable to determine any DNS servers. Reverse DNS is disabled. Try using --system-dns or specify valid servers with --dns-servers
Initiating SYN Stealth Scan at 20:27
Scanning localhost (127.0.0.1) [1 port]
Discovered open port 80/tcp on 127.0.0.1
Completed SYN Stealth Scan at 20:27, 0.01s elapsed (1 total ports)
Initiating Service scan at 20:27
Scanning 1 service on localhost (127.0.0.1)
Warning: Hit PCRE_ERROR_MATCHLIMIT when probing for service http with the regex '^HTTP/1\.1 \d\d\d (?:[^\r\n]*\r\n(?!\r\n))*?.*\r\nServer: Virata-EmWeb/R([\d_]+)\r\nContent-Type: text/html; ?charset=UTF-8\r\nExpires: .*<title>HP (Color |)LaserJet ([\w._ -]+)&nbsp;&nbsp;&nbsp;'
Completed Service scan at 20:27, 6.06s elapsed (1 service on 1 host)
Initiating OS detection (try #1) against localhost (127.0.0.1)
NSE: Script scanning 127.0.0.1.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 20:27
Completed NSE at 20:27, 0.11s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 20:27
Completed NSE at 20:27, 0.01s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 20:27
Completed NSE at 20:27, 0.00s elapsed
Nmap scan report for localhost (127.0.0.1)
Host is up, received localhost-response (0.000024s latency).
Other addresses for localhost (not scanned): ::1
Scanned at 2025-11-02 20:27:47 EET for 8s

PORT   STATE SERVICE REASON         VERSION
80/tcp open  http    syn-ack ttl 64 Apache httpd 2.4.65 ((Debian))
|_http-server-header: Apache/2.4.65 (Debian)
| http-methods: 
|_  Supported Methods: OPTIONS HEAD GET POST
|_http-title: Apache2 Debian Default Page: It works
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Linux 2.6.X|5.X
OS CPE: cpe:/o:linux:linux_kernel:2.6.32 cpe:/o:linux:linux_kernel:5 cpe:/o:linux:linux_kernel:6
OS details: Linux 2.6.32, Linux 5.0 - 6.2
TCP/IP fingerprint:
OS:SCAN(V=7.95%E=4%D=11/2%OT=80%CT=%CU=37270%PV=N%DS=0%DC=L%G=N%TM=6907A2AB
OS:%P=x86_64-pc-linux-gnu)SEQ(SP=108%GCD=1%ISR=109%TI=Z%CI=Z%II=I%TS=A)OPS(
OS:O1=MFFD7ST11NW7%O2=MFFD7ST11NW7%O3=MFFD7NNT11NW7%O4=MFFD7ST11NW7%O5=MFFD
OS:7ST11NW7%O6=MFFD7ST11)WIN(W1=FFCB%W2=FFCB%W3=FFCB%W4=FFCB%W5=FFCB%W6=FFC
OS:B)ECN(R=Y%DF=Y%T=40%W=FFD7%O=MFFD7NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=
OS:S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q
OS:=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A
OS:%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y
OS:%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T
OS:=40%CD=S)

Uptime guess: 39.651 days (since Wed Sep 24 05:49:57 2025)
Network Distance: 0 hops
TCP Sequence Prediction: Difficulty=264 (Good luck!)
IP ID Sequence Generation: All zeros

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 20:27
Completed NSE at 20:27, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 20:27
Completed NSE at 20:27, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 20:27
Completed NSE at 20:27, 0.00s elapsed
Read data files from: /usr/share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 7.90 seconds
           Raw packets sent: 23 (1.822KB) | Rcvd: 44 (3.068KB)
```

Mielenkiintoisimmat tulokset:

`NSE: Loaded 157 scripts for scanning.` NSE = Nmap Scripting Engine [lähde](https://nmap.org/book/man-nse.html). 157 skriptiä ladattu skannausta varten.

`Warning: Hostname localhost resolves to 2 IPs. Using 127.0.0.1.` Varoitus, että localhost kääntyy kahdeksi osoitteeksi (IPv4 ja IPv6) ja käytettiin osoitetta 127.0.0.1

`mass_dns: warning: Unable to determine any DNS servers. Reverse DNS is disabled. Try using --system-dns or specify valid servers with --dns-servers` DNS palvelimia ei löytynyt. Käänteishaku (Reverse DNS) ei päällä.

`Discovered open port 80/tcp on 127.0.0.1` Tunnistettu avoin portti 80 osoitteessa 127.0.0.1

`|_http-server-header: Apache/2.4.65 (Debian)` HTTP-header, tunnistettu palvelin Apache 2.4.65

`OS details: Linux 2.6.32, Linux 5.0 - 6.2` Tunnistettu käyttöjärjestelmän tiedot (Linux 2.6.32)

`Network Distance: 0 hops` Etäisyys = 0 hops = paikallinen kohde (ei reitittimiä välissä) 

`TCP Sequence Prediction: Difficulty=264 (Good luck!)` TCP sekvenssin ennustaminen. TCP:n kolmivaiheinen kädenpuristus aloitetaan SYN-paketilla jota seuraa alkusekvenssinumero. Difficulty kertoo kuinka vaikea tämän numeron ennustaminen on. [lähde](https://www.opensourceforu.com/2011/01/advanced-nmap-fin-scan-and-os-detection/)

## c) Skriptit. Mitkä skriptit olivat automaattisesti päällä, kun käytit "-A" parametria? (Näkyy avoimien porttinumeroiden alta, http-blah, http-blöh...).

Kävin komennon parametreja läpi näillä sivuilla https://nmap.org/book/port-scanning-options.html ja https://hackviser.com/tactics/tools/nmap. Komento avattuna näiden pohjalta:

`sudo` Aja root-oikeuksilla

`nmap` Skanneri

`-T4` Timing. Skannauksen nopeus väliltä T0 - T5, jossa T0 hitain ja T5 nopein.

`-vv` Verbosity level. Kuinka paljon tietoa tulostetaan skannauksesta. Vaihtoehtoina -v, -vv, -vvv (-v pienin, -vvv suurin).

`-A` Aggressiivinen skannaus. Sisältää seuraavat skriptit: OS detection, version detection, script scanning ja traceroute.

`-p 80` Portin valinta (portti 80).

`localhost` Lopuksi skannattava kohde (= localhost).


## d) Jäljet lokissa. Etsi weppipalvelimen lokeista jäljet porttiskannauksesta (NSE eli Nmap Scripting Engine -skripteistä skannauksessa). Löydätkö sanan "nmap" isolla tai pienellä? Selitä osumat. Millaisilla hauilla tai säännöillä voisit tunnistaa porttiskannauksen jostain muusta lokista, jos se on niin laaja, että et pysty lukemaan itse kaikkia rivejä?

Lokeista löytyi useita jälkiä porttiskannauksesta, Nmap Scripting Engine toistuu usealla lokin rivillä `cat /var/log/apache2/access.log`:

<img width="1442" height="522" alt="image" src="https://github.com/user-attachments/assets/b18a15ca-73cc-4acd-8191-58914902eb78" />

- Riveillä näkyy localhost osoite: 127.0.0.1
- Pyyntojen päivämäärät ja kellonajat
- HTTP metodit: GET, POST, PROPFIND, OPTIONS, TAIS
- Statuskoodit: 200 (OK), 404 (Not Found), 405 (Method Not Allowed), 501 (Not Implemented). Statuskoodit tarkistin [Wikipediasta](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).
- User Agent: "Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)"

Helpoin tapa etsiä ja suodattaa tuloksia on hyödyntää grep komentoa.

Grep [man -sivulta](https://www.man7.org/linux/man-pages/man1/grep.1.html) poimittua:

    -i, --ignore-case
    Ignore case distinctions in patterns and input data, so
    that characters that differ only in case match each other."

Eli `grep -i` avulla voidaan hakea tulokset huolimatta siitä sisältävätkö ne isoja tai pieniä kirjaimia. Ajoin komennon `cat /var/log/apache2/access.log | grep -i nmap`:

<img width="1451" height="433" alt="image" src="https://github.com/user-attachments/assets/b2b92230-584f-4649-8d80-fae0d471ab42" />

## e) Wire sharking. Sieppaa verkkoliikenne porttiskannatessa Wiresharkilla. Huomaa, että localhost käyttää "Loopback adapter" eli "lo". Tallenna pcap. Etsi kohdat, joilla on sana "nmap" ja kommentoi niitä. Jokaisen paketin jokaista kohtaa ei tarvitse analysoida, yleisempi tarkastelu riittää.

Avasin Wiresharkin toiselle työpöydälle terminaalista komennolla `wireshark` ja valitsin sieppauskohteeksi tehtävänannon mukaan Loopback: lo.

<img width="1237" height="582" alt="image" src="https://github.com/user-attachments/assets/0a99f83e-af08-4975-a6c1-7fed6d36497c" />

Tämän jälkeen siirryin takaisin ensimmäiselle työpöydälle, avasin selaimesta http://localhost ja ajoin jälleen skannaus komennon `sudo nmap -T4 -vv -A -p 80 localhost`.

Skannauksen päätyttyä palasin takaisin toiselle työpöydälle ja pysäytin wiresharkin sieppauksen.

Tämän jälkeen kirjoitin wiresharkin display filteriin `frame contains "nmap"`, jolla saadaan suodatettua kohdat joissa esiintyy 'nmap':

<img width="1261" height="481" alt="image" src="https://github.com/user-attachments/assets/d844a095-665a-44da-8abb-caac5e03a820" />

Paketteja tutkiessani löysin nmap:in User-Agent:in sisältä:

<img width="1195" height="778" alt="image" src="https://github.com/user-attachments/assets/9a577c18-ac31-4347-a182-69282f484ec2" />

Yhden paketin info -kentästä löytyy myös suoraan nmap maininta:

<img width="1118" height="93" alt="image" src="https://github.com/user-attachments/assets/4f473e23-dc67-4a3b-9629-3a86ab135bd6" />

## f) Net grep. Sieppaa verkkoliikenne 'ngrep' komennolla ja näytä kohdat, joissa on sana "nmap".

Avasin terminaalin toisella työpöydällä ja aloin sieppaamaan liikennettä komennolla `sudo ngrep -d lo -i nmap`.

ngrep parametrit [(lähde)](https://linux.die.net/man/8/ngrep):
- -d lo = pakotetaan (force) ngrep kuuntelemaan tiettyä liitäntää (tässä tapauksessa Loopback lo)
- -i = Jätä kirjainkoko huomioimatta
- nmap = etsittävä sisältö

Tämän jälkeen siirryin takaisin ensimmäiselle työpöydälle. Avasin jälleen selaimella http://localhost ja ajoin terminaalissa komennon `sudo nmap -T4 -vv -A -p 80 localhost`.

Skannauksen päätteeksi palasin toiselle työpöydälle tarkastamaan mitä liikennettä ngrep oli onnistunut sieppaamaan:

```
T 127.0.0.1:58882 -> 127.0.0.1:80 [AP] #356
  GET / HTTP/1.1..Host: localhost..Connection: close..User-Agent: Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.o
  rg/book/nse.html)....                                                                                                         
#####
T 127.0.0.1:58892 -> 127.0.0.1:80 [AP] #361
  GET /nmaplowercheck1762116594 HTTP/1.1..Host: localhost..Connection: close..User-Agent: Mozilla/5.0 (compatible; Nmap Scriptin
  g Engine; https://nmap.org/book/nse.html)....                                                                                 
#####
T 127.0.0.1:58894 -> 127.0.0.1:80 [AP] #366
  POST / HTTP/1.1..Connection: close..Content-Length: 88..Host: localhost..User-Agent: Mozilla/5.0 (compatible; Nmap Scripting E
  ngine; https://nmap.org/book/nse.html)..Content-Type: application/x-www-form-urlencoded....<methodCall> <methodName>system.lis
  tMethods</methodName> <params></params> </methodCall>                                                                         
#####
T 127.0.0.1:58896 -> 127.0.0.1:80 [AP] #371
  PROPFIND / HTTP/1.1..Host: localhost..Connection: close..User-Agent: Mozilla/5.0 (compatible; Nmap Scripting Engine; https://n
  map.org/book/nse.html)..Depth: 0....                                                                                          
#######
T 127.0.0.1:58898 -> 127.0.0.1:80 [AP] #378
  OPTIONS / HTTP/1.1..Host: localhost..Connection: close..User-Agent: Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nm
  ap.org/book/nse.html)....                                                                                                     
#####
T 127.0.0.1:58900 -> 127.0.0.1:80 [AP] #383
  POST /sdk HTTP/1.1..Host: localhost..Connection: close..User-Agent: Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nm
  ap.org/book/nse.html)..Content-Length: 441....<soap:Envelope xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://ww
  w.w3.org/2001/XMLSchema-instance" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/"><soap:Header><operationID>00000001-00
  000001</operationID></soap:Header><soap:Body><RetrieveServiceContent xmlns="urn:internalvim25"><_this xsi:type="ManagedObjectR
  eference" type="ServiceInstance">ServiceInstance</_this></RetrieveServiceContent></soap:Body></soap:Envelope>                 
#####
T 127.0.0.1:58914 -> 127.0.0.1:80 [AP] #388
  PROPFIND / HTTP/1.1..Host: localhost..Connection: close..User-Agent: Mozilla/5.0 (compatible; Nmap Scripting Engine; https://n
  map.org/book/nse.html)..Depth: 0....                                                                                          
####
T 127.0.0.1:58926 -> 127.0.0.1:80 [AP] #392
  GET /robots.txt HTTP/1.1..Host: localhost..Connection: close..User-Agent: Mozilla/5.0 (compatible; Nmap Scripting Engine; http
  s://nmap.org/book/nse.html)....                                                                                               
##
T 127.0.0.1:58928 -> 127.0.0.1:80 [AP] #394
  GET /.git/HEAD HTTP/1.1..Host: localhost..Connection: close..User-Agent: Mozilla/5.0 (compatible; Nmap Scripting Engine; https
  ://nmap.org/book/nse.html)....                                                                                                
##
T 127.0.0.1:58934 -> 127.0.0.1:80 [AP] #396
  OPTIONS / HTTP/1.1..Connection: close..Access-Control-Request-Method: HEAD..Host: localhost..Origin: example.com..User-Agent: 
  Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)....                                           
##
T 127.0.0.1:58946 -> 127.0.0.1:80 [AP] #398
  OPTIONS / HTTP/1.1..Host: localhost..Connection: close..User-Agent: Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nm
  ap.org/book/nse.html)....                                                                                                     
###########################################################
T 127.0.0.1:58952 -> 127.0.0.1:80 [AP] #457
  GET /HNAP1 HTTP/1.1..Host: localhost..Connection: close..User-Agent: Mozilla/5.0 (compatible; Nmap Scripting Engine; https://n
  map.org/book/nse.html)....                                                                                                    
#####
T 127.0.0.1:58962 -> 127.0.0.1:80 [AP] #462
  WXDN / HTTP/1.1..Host: localhost..Connection: close..User-Agent: Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.
  org/book/nse.html)....                                                                                                        
#####
T 127.0.0.1:58978 -> 127.0.0.1:80 [AP] #467
  OPTIONS / HTTP/1.1..Connection: close..Access-Control-Request-Method: GET..Host: localhost..Origin: example.com..User-Agent: M
  ozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)....                                            
#####
T 127.0.0.1:58986 -> 127.0.0.1:80 [AP] #472
  PROPFIND / HTTP/1.1..Connection: close..Content-Length: 0..Host: localhost..User-Agent: Mozilla/5.0 (compatible; Nmap Scriptin
  g Engine; https://nmap.org/book/nse.html)..Depth: 1....                                                                       
#####
T 127.0.0.1:58992 -> 127.0.0.1:80 [AP] #477
  GET /evox/about HTTP/1.1..Host: localhost..Connection: close..User-Agent: Mozilla/5.0 (compatible; Nmap Scripting Engine; http
  s://nmap.org/book/nse.html)....                                                                                               
#####################
T 127.0.0.1:58994 -> 127.0.0.1:80 [AP] #498
  GET /favicon.ico HTTP/1.1..Host: localhost..Connection: close..User-Agent: Mozilla/5.0 (compatible; Nmap Scripting Engine; htt
  ps://nmap.org/book/nse.html)....                                                                                              
#####
T 127.0.0.1:59008 -> 127.0.0.1:80 [AP] #503
  OPTIONS / HTTP/1.1..Connection: close..Access-Control-Request-Method: POST..Host: localhost..Origin: example.com..User-Agent: 
  Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)....                                           
###############
T 127.0.0.1:59022 -> 127.0.0.1:80 [AP] #518
  GET / HTTP/1.1..Host: localhost..Connection: close..User-Agent: Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.o
  rg/book/nse.html)....                                                                                                         
#####
T 127.0.0.1:59038 -> 127.0.0.1:80 [AP] #523
  OPTIONS / HTTP/1.1..Connection: close..Access-Control-Request-Method: PUT..Host: localhost..Origin: example.com..User-Agent: M
  ozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)....                                            
############
T 127.0.0.1:59052 -> 127.0.0.1:80 [AP] #535
  OPTIONS / HTTP/1.1..Connection: close..Access-Control-Request-Method: DELETE..Host: localhost..Origin: example.com..User-Agent
  : Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)....                                         
##########
T 127.0.0.1:59056 -> 127.0.0.1:80 [AP] #545
  OPTIONS / HTTP/1.1..Connection: close..Access-Control-Request-Method: TRACE..Host: localhost..Origin: example.com..User-Agent:
   Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)....                                          
##########
T 127.0.0.1:59060 -> 127.0.0.1:80 [AP] #555
  OPTIONS / HTTP/1.1..Connection: close..Access-Control-Request-Method: OPTIONS..Host: localhost..Origin: example.com..User-Agen
  t: Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)....                                        
##########
T 127.0.0.1:59062 -> 127.0.0.1:80 [AP] #565
  OPTIONS / HTTP/1.1..Connection: close..Access-Control-Request-Method: CONNECT..Host: localhost..Origin: example.com..User-Agen
  t: Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)....                                        
##########
T 127.0.0.1:59074 -> 127.0.0.1:80 [AP] #575
  OPTIONS / HTTP/1.1..Connection: close..Access-Control-Request-Method: PATCH..Host: localhost..Origin: example.com..User-Agent:
   Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)....                                          
##########################################^Cexit
617 received, 25 matched
```

## g) + h) Agentti. Vaihda nmap:n user-agent niin, että se näyttää tavalliselta weppiselaimelta. Pienemmät jäljet. Porttiskannaa weppipalvelimesi uudelleen localhost-osoitteella. Tarkastele sekä Apachen lokia että siepattua verkkoliikennettä. Mikä on muuttunut, kun vaihdoit user-agent:n? Löytyykö lokista edelleen tekstijono "nmap"?

Aloitin avaamalla wiresharkin toiselle työpöydälle ja aloitin sieppauksen.

Sitten selaimesta localhost sivusto uudelleen auki.

Hyödynsin tehtävänannossa annettua ohjetta ja ajoin skannausta varten komennon `sudo nmap -A localhost --script-args http.useragent="BSD experimental on XBox350 alpha (emulated on Nokia 3110)"`

Palasin wiresharkin ääreen tutkimaan oliko User-Agent tiedot muuttuneet paketin tiedoissa, valitsin sattumanvaraisesti paketin:

<img width="1192" height="556" alt="image" src="https://github.com/user-attachments/assets/02f44a47-f951-4255-8e4a-33566a851b40" />

Ainakin kyseisessä paketissa tiedot olivat muuttuneet.

Tarkistin vielä löytyykö nmap -mainintaa paketeista syöttämällä display filteriin `frame contains "nmap"`. Tuloksia löytyi enää vain yksi kappale:

<img width="1170" height="803" alt="image" src="https://github.com/user-attachments/assets/b71028bd-3451-406e-8aa9-e16595fe87ca" />

Tarkistin Apache acccess lokista `sudo tail -F /var/log/apache2/access.log` miltä muutokset siellä näyttivät:

<img width="1137" height="243" alt="image" src="https://github.com/user-attachments/assets/f6e01516-4dab-40df-9089-f0289d4d7cb0" />

Riveillä toistuu "BSD experimental on XBox350 alpha (emulated on Nokia 3110)"

Lopuksi tarkistin vielä `sudo cat /var/log/apache2/access.log | grep -i nmap` löytyykö mainintaa 'nmap'

<img width="1134" height="36" alt="image" src="https://github.com/user-attachments/assets/be15240f-33ea-4285-b602-40746accb01c" />

Löytyi enää yksi kappale, jossa siinäkin user-agent nimi muuttunut.

## i)  Hieman vaikeampi: LoWeR ChEcK. Poista skritiskannauksesta viimeinenkin "nmap" -teksti. Etsi löytämääsi tekstiä /usr/share/nmap -hakemistosta ja korvaa se toisella. Tee porttiskannaus ja tarkista, että "nmap" ei näy isolla eikä pienellä kirjoitettuna Apachen lokissa eikä siepatussa verkkoliikenteessä. (Tässä tehtävässä voit muokata suoraan lua-skriptejä /usr/share/nmap alta, 'sudoedit'. Muokatun version paketoiminen siis rajataan ulos tehtävästä.)

Edellisessä tehtävässä wiresharkissa ainoa maininta joka sisälsi merkkijonon 'nmap' oli muotoa `/nmaplowercheck1762115059`, joten päätin aloittaa etsinnät hakusanalla `nmaplowercheck`.

Tekstiä tulee tehtävänannon mukaan etsiä polusta /usr/share/nmap , joten siirryin tähän polkuun ja ajoin komennon `grep -irn "nmaplowercheck"`

grep parametrit [(lähde)](https://linux.die.net/man/1/grep):

- -i = Jätä kirjainkoko huomioimatta
- -r = Rekursiivinen haku
- -n = Näyttää millä tiedoston rivillä sisältö esiintyy 
- nmaplowercheck = etsittävä sisältö

Ei löytynyt kuin yksi osuma nselib -kansiosta http.lua -tiedostosta riviltä 2625:

<img width="679" height="66" alt="image" src="https://github.com/user-attachments/assets/cea6cc6a-6c84-4a60-88b5-90f10e29f655" />

Menin muokkaamaan tiedostoa komennolla `sudo micro http.lua` ja etsimään tuota kyseistä riviä:

<img width="585" height="77" alt="image" src="https://github.com/user-attachments/assets/d2e1b0c4-7c9b-4e48-b3c9-6dd4bf1cb50a" />

Sieltä löytyikin kolme riviä jossa nmap esiintyy, joten päätin nimetä ne kaikki uudelleen:

<img width="594" height="78" alt="image" src="https://github.com/user-attachments/assets/67d563bb-7391-4ba3-a577-241ccad09c3e" />

Tämän jälkeen lähdin testaamaan tuottiko muokkaukset tulosta.

Avasin toiselle työpöydälle wiresharkin ja aloin sieppaamaan liikennettä: Loopback lo.

Sitten avasin ensimmäisellä työpöydällä jälleen selaimeen localhost ja ajoin terminaalissa saman skannaus komennon jota käytin aiemmin: `sudo nmap -A localhost --script-args http.useragent="BSD experimental on XBox350 alpha (emulated on Nokia 3110)"`

<img width="865" height="197" alt="image" src="https://github.com/user-attachments/assets/23d7fa46-c5e3-4d20-978c-096999286689" />

Wireshark ei löytänyt enää nmap -merkkijonoa. Myöskään `sudo cat /var/log/apache2/access.log | grep -i nmap` ei tuottanut enää uusia tuloksia.

### Lähteet

Apache. Log Files. https://httpd.apache.org/docs/2.4/logs.html#accesslog

Bianco, D. 17.1.2013. The Pyramid of Pain. https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html

Caltagirone, S., Pendergast, A. & Betz, C. Diamond Model. https://www.threatintel.academy/wp-content/uploads/2020/07/diamond-model.pdf

die.net. ngrep(8) - Linux man page. https://linux.die.net/man/8/ngrep

die.net. grep(1) - Linux man page. https://linux.die.net/man/1/grep

Hackviser. NMAP. https://hackviser.com/tactics/tools/nmap

Hutchins, E., Cloppert, M. & Amin, R. Cyber Kill Chain. https://lockheedmartin.com/content/dam/lockheed-martin/rms/documents/cyber/LM-White-Paper-Intel-Driven-Defense.pdf

Karvinen, T. 26.3.2025. Verkkoon tunkeutuminen ja tiedustelu. https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/

Mitre. ATT&CK. https://attack.mitre.org/

Nmap.org. Command-line Flags. https://nmap.org/book/port-scanning-options.html

Nmap.org. Nmap Scripting Engine. https://nmap.org/book/man-nse.html

Deodhar, R. Advanced Nmap: FIN Scan & OS Detection. https://www.opensourceforu.com/2011/01/advanced-nmap-fin-scan-and-os-detection/

Wikipedia. List of HTTP status codes. https://en.wikipedia.org/wiki/List_of_HTTP_status_codes
