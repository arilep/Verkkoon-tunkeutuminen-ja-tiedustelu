### h7 Aaltoja harjaamassa [tehtävänanto](https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#h7-aaltoja-harjaamassa)

## Tehtävissä käytetty ympäristö

### PC

- Käyttöjärjestelmä: Windows 11 Home 64-bit
- Suoritin: AMD Ryzen 7 5800X 8-Core Processor
- Muisti: 32GB RAM
- Näytönohjain: NVIDIA GeForce RTX 3080
- Virtualisointiohjelmisto: Oracle VM VirtualBox 7.0

- Internet yhteys: DNA Netti 1000 M

### Virtuaalikone

- Kali Linux [Get Kali](https://www.kali.org/get-kali/#kali-installer-images)
- Base Memory: 8192 MB
- Processors: 1
- Virtual HD: 60 GB
- Video Memory: 128 MB

## x) Lue ja tiivistä.

### Hubacek 2019: [Universal Radio Hacker SDR Tutorial on 433 MHz radio plugs](https://www.youtube.com/watch?v=sbqMqb6FVMY&t=199s)

- Universal Radio Hacker (URH) -työkalu radioliikenteen sieppaamiseen ja analysointiin.
- Modulaatiomenetelmät ASK, FSK, PSK.
- Autodetect parameters -toiminnolla voidaan yrittää tunnistaa automaattisesti signaalin keskipiste (center), bittipituus (bit length) ja toleranssi (tolerance).

### Cornelius 2022: [Decode 433.92 MHz weather station data](https://www.onetransistor.eu/2022/01/decode-433mhz-ask-signal.html)

- rtl_433 -työkalulla voidaan dekoodata 433 MHz laitteiden lähettämiä radiosignaaleja.
- Artikkelissa avattiin lisää URH-työkalun käyttötarkoitusta ja toimintaa.
- Saatavilla [tietokanta](https://triq.org/explorer/) kaikista tunnetuista signaaleista ja linkit rtl_433 lähdekoodiin.

## a) WebSDR. Etäkäytä WebSDR-ohjelmaradiota, joka on kaukana sinusta ja kuuntele radioliikennettä. Radioliikenne tulee siepata niin, että radiovastaanotin on joko eri maassa tai vähintään 400 km paikasta, jossa teet tätä tehtävää. Käytä esimerkkinä julkista, suurelle yleisölle tarkoitettua viestiä, esimerkiksi yleisradiolähetystä. Kerro löytämäsi taajuus, aallonpituus ja modulaatio. Kuvaile askeleet ja ota ruutukaappaus. (Tehtävässä ei saa ilmaista sellaisen viestin sisältöä tai olemassaoloa, joka ei ole tarkoitettu julkiseksi. Voit sen sijaan kuvailla, miten sait julkisen radiolähetyksen kuulumaan kaiuttimistasi. Julkisten, esimerkiksi yleisradiolähetysten sisältöä saa tietysti kuvailla.)

Menin WebSDR [sivustolle](http://websdr.org/), valitsin sivulta ensimmäisen vastaanottimen ja avasin sen selaimessa.

<img width="1105" height="63" alt="image" src="https://github.com/user-attachments/assets/4d90591e-375d-4001-82fa-3f6020503eab" />

Sivuston avatessani valitsin "start audio":

<img width="707" height="225" alt="image" src="https://github.com/user-attachments/assets/93300725-2db2-42e8-8098-428191502400" />

Etsiskelin radiolähetyksiä hetken aikaa, alkuun kuului pelkkää kohinaa. Lopulta löysin radiokanavan CHN China Radio Int. [China Radio International](https://en.wikipedia.org/wiki/China_Radio_International)

<img width="1100" height="605" alt="image" src="https://github.com/user-attachments/assets/99ab01c0-c43c-41a2-9bfe-3b85f2e908bd" />

| Taajuus | Aallonpituus | Modulaatio |
| --- | --- | --- |
| 7265.00 kHz | 41m | AM |

Kanavalta kuului enimmäkseen musiikkia ja välillä lyhyitä pätkiä puhetta, jotka olivat luultavasti mainoksia. Kohinaa jäi hieman taustalle hienosäädöstä huolimatta, mutta puheesta sai kuitenkin selvää.

## b) rtl_433. Asenna rtl_433 automaattista analyysia varten. Kokeile, että voit ajaa sitä. './rtl_433' vastaa "rtl_433 version 25.02 branch..."

Asensin rtl_433 ajamalla seuraavat komennot:

    sudo apt-get update
    sudo apt-get install -y rtl-433

Tarkistin vielä että asennus onnistui ja ohjelma vastaa:

<img width="592" height="149" alt="image" src="https://github.com/user-attachments/assets/134d1a48-f917-4709-bfb3-871e8693fd80" />

## c) Automaattinen analyysi. Mitä tässä näytteessä tapahtuu? Mitä tunnisteita (id yms) löydät? Converted_433.92M_2000k.cs8. Analysoi näyte 'rtl_433' ohjelmalla.

Latasin tiedoston ja ajoin sen komennolla `rtl_433 Converted_433.92M_2000k.cs8`

<img width="976" height="872" alt="image" src="https://github.com/user-attachments/assets/d1e16bfb-4aee-433d-88f2-b26c0f6e189d" />

Tunnisteet:

    time
    model
    Unit
    Channel
    Group Call
    id
    Command
    Dim
    Dim Value
    State
    House Code
    Group

Modeleista löytyvät KlikAanKlikUit-Switch, Proove-Security ja Nexa-Security.

Tein googlehaun tuolla 'klikaaanklikuit-switch' hakusanalla ja silmäilin tuloksia:

<img width="689" height="743" alt="image" src="https://github.com/user-attachments/assets/2edd9328-ba58-40dc-97bd-7c5774147090" />

Tämän perusteella kyseessä on jonkinlainen kodin älylaitteisiin liittyvä langaton seinäkytkin. AI Overview tuloksissa mainitaan älyvalaistus, johon tulokset 'dim' ja 'dim value' viittaavat myös.

Vastaava haku 'proove-security':

<img width="872" height="435" alt="image" src="https://github.com/user-attachments/assets/f2548228-a546-4d26-86bc-f3d40c7f4082" />

Kyseessä voisi olla jonkinlainen IP kamera.

Nexa-security:

<img width="436" height="325" alt="image" src="https://github.com/user-attachments/assets/9345ae20-ed38-4155-a2b2-47e7ca97d619" />

Ilmeisesti kyseessä jokin turva-alan yritys, joka tarjoaa kodin hälytysjärjestelmiä.

## d) Too compex 16? Olet nauhoittanut näytteen 'urh' -ohjelmalla .complex16s-muodossa. Muunna näyte rtl_433-yhteensopivaan muotoon ja analysoi se. Näyte Recorded-HackRF-20250411_183354-433_92MHz-2MSps-2MHz.complex16s

rtl_433 github sivulta kävin tutkimassa mitkä tiedostomuodot ovat tuettuja:

<img width="586" height="104" alt="image" src="https://github.com/user-attachments/assets/1982289c-27b4-4cd3-950a-8741deb07868" />

Nimesin tiedoston .cu8 -päätteiseksi, mutta se ei tuottanut tulosta:

<img width="1058" height="195" alt="image" src="https://github.com/user-attachments/assets/82052b18-0f7e-4093-a00f-e27268a7c197" />

"Jonosta seuraava" -periaatteella testasin seuraavaksi .cs8 -päätteellä ja sillä lähti toimimaan:

<img width="1007" height="816" alt="image" src="https://github.com/user-attachments/assets/6adca976-8332-4f6a-bb82-19b7633b1e90" />

Tulokset näyttäisivät olevan vastaavia kuin edellisessä tehtävässä.

## e) Ultimate. Asenna URH, the Ultimate Radio Hacker.

Aloitin asennuksen ohjeiden mukaan:

    Helppo asennus, sopii valmiiksi kaapattujen signaalien analyysiin
    $ sudo apt-get update
    $ sudo apt-get -y install pipx
    $ pipx install urh
    $ pipx ensurepath
    sulje ja avaa terminaali
    $ urh
    URH graafinen käyttöliittymä aukeaa

`pipx install urh` komennon jälkeen tuli kuitenkin ongelmia:

<img width="609" height="228" alt="image" src="https://github.com/user-attachments/assets/dd13a22e-8e5d-4551-ba1f-2178245b7620" />

Lokit:

<img width="712" height="421" alt="image" src="https://github.com/user-attachments/assets/879ea98b-4c16-4156-b412-5580708959ea" />

"You need Cython to build URH's extensions!
You can get it e.g. with python3 -m pip install cython."

Koitin seuraavaksi ajaa tuon komennon `python3 -m pip install cython`, mutta vastaan tuli seuraava herja:

<img width="1072" height="412" alt="image" src="https://github.com/user-attachments/assets/6328e8a3-1f01-4afb-812c-d1549fa82fe9" />

Hetken googlettelun tuloksena päädyin [tänne](https://medium.com/@martia_es/pip-vs-pipx-the-definitive-guide-to-python-package-management-a7039a5c62fa)

Löysin vastauksen ongelmaan:

"pipx is a specialized tool designed for installing and running Python applications that provide command-line interfaces (CLI). Unlike pip, which focuses on managing project dependencies, pipx creates isolated environments for each installed application, ensuring no conflicts arise between their dependencies."

Uusi komento `python3 -m pipx install cython`

<img width="533" height="142" alt="image" src="https://github.com/user-attachments/assets/0e14177c-f12f-4fa6-8e65-6bdf8f5a23f9" />

Tästä huolimatta `pipx install urh` ei mennyt läpi ja sain samaa herjaa. Päätin ajan säästämiseksi kokeilla ajaa komennot toisella virtuaalikoneellani (debian-live-12.9.0-amd64-xfce).

     $ sudo apt-get update
    $ sudo apt-get -y install pipx
    $ pipx install urh
    $ pipx ensurepath
    sulje ja avaa terminaali
    $ urh

Komennot menivät läpi ilman ongelmia ja sain ohjelman asennettua:

<img width="1278" height="546" alt="image" src="https://github.com/user-attachments/assets/357c359c-edc0-4bbb-a871-dee60ba6ad24" />

## Tarkastele näytettä 1-on-on-on-HackRF-20250412_113805-433_912MHz-2MSps-2MHz.complex16s. Siinä Nexan pistorasian kaukosäätimen valon 1 ON -nappia on painettu kolmesti. Käytä Ultimate Radio Hacker 'urh' -ohjelmaa.

## f) Yleiskuva. Kuvaile näytettä yleisesti: kuinka pitkä, millä taajuudella, milloin nauhoitettu? Miltä näyte silmämääräisesti näyttää?

Avasin tiedoston URH:lla ja klikkasin 'Autodetect parameters':

<img width="1212" height="679" alt="image" src="https://github.com/user-attachments/assets/7b976c0b-2cfe-4431-8b59-3a5a0430fd0a" />

Tämän jälkeen valitsin koko alueen klikkaamalla näytettä (ylempi ikkuna) ja pikavalinnalla Ctrl+A:

<img width="1197" height="589" alt="image" src="https://github.com/user-attachments/assets/f085c631-7ba7-420d-8f28-95950139ae23" />

Kuinka pitkä? 5,49s

Millä taajuudella ja milloin nauhoitettu? Tiedoston nimestä päätellen 433_912MHz ja nauhoitettu 12.4.2025 klo 11:38:05 (kuva alla)

<img width="698" height="224" alt="image" src="https://github.com/user-attachments/assets/29145b85-44d9-4a42-8f17-043e42d45516" />

Muita tietoja joita näytteestä saadaan:

    Noise (kohina): 0,0000
    Center (keskipiste): 0,1439
    Samples/Symbol (näytteet/symboli): 500
    Error tolerance (virhe toleranssi): 2
    Modulation (modulaatio): ASK
    Bits/Symbol (bitit/symboli): 1

## g) Bittistä. Demoduloi signaali niin, että saat raakabittejä. Mikä on oikea modulaatio? Miten pitkä yksi raakabitti on ajassa? Kuvaile tätä aikaa vertaamalla sitä johonkin. (Monissa singaaleissa on line encoding, eli lopullisia bittejä varten näitä "raakabittejä" on vielä käsiteltävä)

Demodulaatio tulikin tehtyä jo edellisen tehtävän alussa, eli klikkaamalla Autodetect parameters -painiketta.

Päättelisin että oikea modulaatio on ASK bittien perusteella:

Ensimmäinen bitti (1) maalattuna ASK modulaatiossa:

<img width="1129" height="496" alt="image" src="https://github.com/user-attachments/assets/e00b70e0-db24-4811-967c-19a5e12c25d9" />

Toinen bitti (0) maalattuna:

<img width="1210" height="506" alt="image" src="https://github.com/user-attachments/assets/14f61c0c-7ff4-4953-b019-df1ad546f346" />

FSK modulaatiossa löytyi ainoastaan 0 bittejä ja PSK modulaatiossa 0 ja 1 bitit eivät vastanneet "aaltoja". Ensimmäiset kolme 0 bittiä maalattuna PSK modulaatiossa:

<img width="1218" height="490" alt="image" src="https://github.com/user-attachments/assets/40ce9960-0631-42aa-a376-46ec4a457ae5" />

Miten pitkä yksi raakabitti on ajassa?

<img width="310" height="136" alt="image" src="https://github.com/user-attachments/assets/3e0512ed-07fb-4151-a000-fd0986f80a58" />

Maalasin ensimmäisen bitin ja se näyttäisi olevan 522,00 µs (mikrosekuntia) [lähde](https://simple.wikipedia.org/wiki/Microsecond) eli sekunneissa 0,000522 sekuntia.

Otin vertailukohdaksi valonnopeuden, joka on 299 792 458 m/s [lähde](https://fi.wikipedia.org/wiki/Valonnopeus). Pyysin chatGPT:tä tekemään laskutoimituksen promptilla "valon nopeus: 299 792 458 m/s, kuinka pitkän matkan valo kulkee ajassa 522 µs?":

<img width="470" height="338" alt="image" src="https://github.com/user-attachments/assets/d2ce3713-4628-4ab6-9316-1a8971ba199c" />

## Lähteet

chatGPT. promptilla: "valon nopeus: 299 792 458 m/s, kuinka pitkän matkan valo kulkee ajassa 522 µs?"

Cornelius. 4.1.2022. Decode 433.92 MHz weather station data. https://www.onetransistor.eu/2022/01/decode-433mhz-ask-signal.html

García, M. pip vs pipx: The Definitive Guide to Python Package Management. https://medium.com/@martia_es/pip-vs-pipx-the-definitive-guide-to-python-package-management-a7039a5c62fa

hubmartin. 18.1.2019. Universal Radio Hacker SDR Tutorial on 433 MHz radio plugs. https://www.youtube.com/watch?v=sbqMqb6FVMY&t=199s

Iso-Anttila, L. s.a. Verkkoon tunkeutuminen ja tiedustelu -opintojakson esitysmateriaali Moodlessa. Haaga-Helia ammattikorkeakoulu.

Karvinen, T. 26.3.2025. Verkkoon tunkeutuminen ja tiedustelu. https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/

Merbanan. rtl_433. https://github.com/merbanan/rtl_433

Wikipedia. Microsecond. https://simple.wikipedia.org/wiki/Microsecond

Wikipedia. Valonnopeus. https://fi.wikipedia.org/wiki/Valonnopeus
