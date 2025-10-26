### h1 Sniff [Tehtävänanto](https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#h1-sniff)

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

## x)

### Wireshark
- Johtava verkkoliikenteen kuunteluun ja analysointiin tarkoitettu työkalu.
- Työkalun avulla voidaan tallentaa liikennettä ja tarkastella tietoja.
- Tallennetun liikenteen tietoja voidaan suodattaa Display filterien avulla.

### Network Interface
- Verkkoliitäntä on melkein kuin verkkokortti, joka ei välttämättä ole fyysinen.
- Verkkoliitäntöjen nimet määräytyvät systemd:n nimeämiskäytännön mukaan.
- Etuliite ilmaisee liitännän tyypin:
  - en - Wired Ethernet
  - wl - WLAN, wireless local area network, WiFi
  - lo - Loopback adapter

## a)

Kali Linux on tullut asennettua virtuaalikoneelle jo aiemmalla kurssilla.

Kalin latasin täältä: [Get Kali](https://www.kali.org/get-kali/#kali-installer-images).

<img width="384" height="223" alt="image" src="https://github.com/user-attachments/assets/d9821d2b-18b0-48d4-aeba-1edcac759a4b" />

## b)

### Tapa 1

Internet yhteyden katkaisu työpöydältä: Ethernet Network > Disconnect

<img width="252" height="174" alt="image" src="https://github.com/user-attachments/assets/8025e154-2982-47ac-b6ab-8925631bfe5d" />

Testasin verkkoyhteyttä Googlen DNS-palvelimeen. Pingit eivät menneet perille, joten verkkoyhteys ei ole käytössä.

<img width="341" height="64" alt="image" src="https://github.com/user-attachments/assets/140eee04-3b58-4e25-a0f5-31d4797c82a9" />

Palautin tämän jälkeen verkkoyhteyden valitsemalla Ethernet Network > Wired connection 1

<img width="253" height="191" alt="image" src="https://github.com/user-attachments/assets/1147967e-8a6f-4c53-8095-bdd5cfd3278d" />

Tämän jälkeen nimipalvelin vastasi taas pyyntöihin:

<img width="545" height="191" alt="image" src="https://github.com/user-attachments/assets/26307da1-8d4a-4728-abb0-02a7e1c59a8b" />

### Tapa 2

Verkkoasetuksista (Machine > Settings... > Network) voidaan valita 'Cable Connected' vaihtoehto päälle / pois.

<img width="759" height="471" alt="image" src="https://github.com/user-attachments/assets/26e3e8cd-f5e4-4b54-8ab3-6873c50bf390" />

Testasin internet yhteyttä ensin ilman täppää, ja tämän jälkeen muodostin yhteyden uudelleen valitsemalla tuon 'Cable Connected' täpän uudelleen:

<img width="540" height="258" alt="image" src="https://github.com/user-attachments/assets/7ae5a3e4-118e-44bd-bcc2-e2edc262a9cd" />

## c)

### Wireshark asennus

Wireshark oli jo valmiiksi asennettuna virtuaalikoneelleni. Wireshark tuli muistaakseni valmiiksi asennettuna Kalille.

Wiresharkin voi asentaa komennolla:

    sudo apt-get update
    sudo apt-get install wireshark

<img width="1074" height="384" alt="image" src="https://github.com/user-attachments/assets/4af93be9-802f-4354-b690-a2085ad3a3ea" />

## d)

Sieppasin tehtävää varten Wiresharkilla jonkin verran liikennettä:

<img width="1710" height="549" alt="image" src="https://github.com/user-attachments/assets/fab98653-d95e-442a-a4ac-73c48a6bbf03" />

TCP/IP -mallin neljä kerrosta valitusta (sinisellä pohjalla) paketista:

- Application layer: Hypertext Transfer Protocol (HTTP)
- Transport layer: Transmission Control Protocol (TCP)
- Internet layer: Internet Protocol Version 4 (IPv4)
- Link layer: Ethernet II

## e)

Latasin [surfing-secure.pcap](https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/surfing-secure.pcap) tiedoston ja tarkastelin ensin Capture file properties näkymää Wiresharkilla:

<img width="1096" height="506" alt="image" src="https://github.com/user-attachments/assets/c4754a65-b7e2-4cd1-9ef4-27d07ccfa0fd" />

Saadaan selville ainakin seuraavat:
- Ensimmäisen ja viimeisen paketin ajankohdat, kaappaus kestänyt ~7 sekuntia
- Paketit kaapattiin ethernet liitännästä
- Kaapattujen pakettien määrä: 283

<img width="1108" height="292" alt="image" src="https://github.com/user-attachments/assets/3f3bfe57-efca-47ce-9dca-22974cf6e62c" />

DNS-kyselyistä nähdään, että käyttäjä on vieraillut ainakin sivustoilla google.com ja terokarvinen.com

## g)

Verkkokortin löytää valitsemalla minkä tahansa paketin ja laajentamalla 'Ethernet source' osion:

<img width="560" height="250" alt="image" src="https://github.com/user-attachments/assets/3e54a8ed-9062-4d7e-a86c-41e5201b589a" />

Verkkokortin valmistaja näyttäisi olevan Realtek (RealtekU)

## h)

Tutustuin Wiresharkin asetuksiin ja löysin sieltä tämän kohdan:

<img width="826" height="605" alt="image" src="https://github.com/user-attachments/assets/f42817b8-19d9-4357-a88e-8174f81e023e" />

Laittamalla tuon asetuksen päälle voidaan sivustot löytää suoraan Statistics > Resolved Addressess:

<img width="621" height="475" alt="image" src="https://github.com/user-attachments/assets/a95cce34-3ef0-4a0e-8ca1-da248544c429" />

Hain tietoja myös hyödyntämällä display filteriä ja syötin kenttään 'dns' jolloin saadaan rajattua ainoastaan DNS protokollaa käyttäneet paketit. Sivustot näkyvät 'info' -otsikon alla:

<img width="1905" height="564" alt="image" src="https://github.com/user-attachments/assets/afbf3914-5dc6-4eeb-9d99-c8ad5d47dbee" />

## i)

Sieppasin liikennettä 11 paketin verran tehtävää varten:

<img width="1562" height="251" alt="image" src="https://github.com/user-attachments/assets/167223cf-df99-4849-beb8-1860d283925d" />

Capture File Properties -näkymä:

<img width="1156" height="874" alt="image" src="https://github.com/user-attachments/assets/064dd89f-64c3-4bbc-b05a-fa3673f58673" />

- Time otsikon alta nähdään ensimmäisen ja viimeisen paketin ajankohdat (eivät tässä tapauksessa vastaa tosin todellisuutta).

- Capture otsikon alta löytyy prosessorin tiedot, käyttöjärjestelmä sekä ohjelmiston tiedot.

- Statistics -osiosta näkyy mm. siepattujen pakettien määrä ja sieppaukseen käytetty aika.

<img width="623" height="482" alt="image" src="https://github.com/user-attachments/assets/1f416360-be25-4040-b700-f24690aa0268" />

- Resolved Addressess -näkymässä näkyy verkkokortin tietoja (valmistaja, MAC-osoitteen etuliite) sekä osoite www.goatcounter.com, joka näyttäisi olevan verkkosivuanalytiikka työkalu.

### Lähteet

Goatcounter. Open source web analytics. https://www.goatcounter.com/

Karvinen, T. 26.3.2025. Verkkoon tunkeutuminen ja tiedustelu. https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/

Karvinen, T. 28.3.2025. Wireshark - Getting Started. https://terokarvinen.com/wireshark-getting-started/

Karvinen, T. 28.3.2025. Network Interface Names on Linux. https://terokarvinen.com/network-interface-linux/

Wikipedia. Internet Protocol Suite. https://en.wikipedia.org/wiki/Internet_protocol_suite
