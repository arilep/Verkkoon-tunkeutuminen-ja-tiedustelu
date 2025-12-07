### h4 NFC ja RFID

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

## a) Tarkastele käytössäsi olevia RFID tuotteita, mieti miten hyvin olet suojautunut RFID urkinnalta?

Mielestäni olen melko hyvin varautunut urkinnan varalta. Tällä hetkellä päivittäin mukana kulkevia RFID tuotteita, joita kannan mukanani ovat ainoastaan puhelin, plussa-kortti, ajokortti ja pankkikortti. Avaimissa ei ole RFID tekniikkaa, eikä minulla ole kulkulätkiä tai muita älylaitteita.

Kaikkia kortteja ja puhelinta säilytän puhelinkotelossa, jossa on RFID-suojaus. Puhelimeni NFC ominaisuutta käytän todella harvoin, ja tällöinkin otan sen pois käytöstä heti kun en tarvitse sitä enää.

## b) Tutustu APDU komentojen rakenteeseen (voit käyttää tekoälyä tutustumiseen)

APDU on lyhenne sanoista (smart card) Application Protocol Data Unit. APDU jaetaan kahteen kategoriaan: Command- ja Response APDU:un. Command APDU:lla tarkoitetaan lukijalta kortille lähetettäviä komentoja, Response APDU:lla taas kortilta lukijalle.

### Command APDU rakenne

| Kentän nimi | Pituus tavuina | Kuvaus |
| ---------- | ---------- | ---------- |
|  CLA | 1 | Käskyluokka |
| INS | 1 | Käskykoodi |
| P1-P2 | 2 | Komennon parametrit |
| Lc | 0, 1 tai 3 | Komennossa lähetettävän datan tavujen määrä |
| Command Data | 0-n  | 0-n tavua dataa |
| Le | 0, 1, 2 tai 3 | Vastausdatan odotettu pituus |

### Response APDU rakenne

| Kentän nimi | Pituus tavuina | Kuvaus |
| ---------- | ---------- | ---------- |
|  Response Data | Vaihteleva | Vastauksen data |
| SW1-SW2 | 2 | Komennon käsittelyn tila |


## c) Tutki ja kerro minkä mielenkiintoisen RFID hakkerointi uutiset löysit. (Vinkki, useimmat liittyvät henkilökortteihin)

### Hardware Backdoor Discovered in RFID Cards Used in Hotels and Offices Worldwide. [(linkki uutiseen)](https://thehackernews.com/2024/08/hardware-backdoor-discovered-in-rfid.html)

Tietyistä MIFARE Classic contactless -korteista löydetty laitteistotakaportti, jolloin korttien avaimet on pystytty murtamaan ja kortit kloonaamaan. Väärennetyillä korteilla on onnistuttu siten avaamaan hotelli- ja toimistohuoneiden ovia.

### Rfid Theft Statistics. [(linkki uutiseen)](https://zipdo.co/rfid-theft-statistics/)

Mielenkiintoisia tilastoja RFID varkauksista ja haavoittuvuuksista.

<img width="792" height="55" alt="image" src="https://github.com/user-attachments/assets/18ef1471-0ef8-4b03-801f-75ca60a80fd2" />

<img width="749" height="79" alt="image" src="https://github.com/user-attachments/assets/5afe0d6e-95c9-4a69-a20e-30549ef2c0bf" />

<img width="831" height="82" alt="image" src="https://github.com/user-attachments/assets/bbe711be-8fe7-4122-b77d-60219d3cf954" />

<img width="773" height="44" alt="image" src="https://github.com/user-attachments/assets/11d054b5-6ce6-4aaf-b514-ee7ddcf86144" />

<img width="794" height="55" alt="image" src="https://github.com/user-attachments/assets/e31261f9-ac4b-4ba4-b542-bf72040ed148" />

<img width="713" height="42" alt="image" src="https://github.com/user-attachments/assets/9c56d070-8605-457c-9a04-29ae83d1ecdf" />

<img width="819" height="75" alt="image" src="https://github.com/user-attachments/assets/3e80a016-ba6c-43b8-a236-5aeef0f3a0e0" />

<img width="783" height="82" alt="image" src="https://github.com/user-attachments/assets/b6ea50c1-4e5d-4a7b-b7e5-f471a74e42ec" />

## Lähteet

Eser, A. 30.5.2025. Rfid Theft Statistics. https://zipdo.co/rfid-theft-statistics/

Iso-Anttila, L. s.a. Verkkoon tunkeutuminen ja tiedustelu -opintojakson esitysmateriaali Moodlessa. Haaga-Helia ammattikorkeakoulu.

Karvinen, T. 26.3.2025. Verkkoon tunkeutuminen ja tiedustelu. https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/

The Hacker News. Hardware Backdoor Discovered in RFID Cards Used in Hotels and Offices Worldwide. https://thehackernews.com/2024/08/hardware-backdoor-discovered-in-rfid.html

Wikipedia. Smart card application protocol data unit. https://en.wikipedia.org/wiki/Smart_card_application_protocol_data_unit

