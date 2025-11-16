### h6 WiFi [Tehtävänanto](https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#h6-wifi)

## Tehtävissä käytetty ympäristö

### PC

- Käyttöjärjestelmä: Windows 11 Home 64-bit
- Suoritin: AMD Ryzen 7 5800X 8-Core Processor
- Muisti: 32GB RAM
- Näytönohjain: NVIDIA GeForce RTX 3080
- Virtualisointiohjelmisto: Oracle VM VirtualBox 7.0

- Internet yhteys: DNA Netti 600 M

### Virtuaalikone
 
Virtualisoitu Wi-Fi pentestauslaboratorio, jonka latasin [täältä](https://lab.wifichallenge.com/README)

<img width="711" height="181" alt="image" src="https://github.com/user-attachments/assets/cc0b14c3-afd4-4da3-9a2c-54cf5408c171" />

## a) Tutustu wifi challenge lab 2.1 harjoitus ympäristöön ja käytä tarvittaessa hyväksesi jo olemassa olevia ohjeita.

Harjoituksissa käyttämäni ohjeet löytyivät [täältä](https://r4ulcl.com/posts/walkthrough-wifichallenge-lab-2.0/)

Suoritetut tehtävät:

<img width="1333" height="748" alt="image" src="https://github.com/user-attachments/assets/05df6bb0-179f-4889-bfab-68c4388df212" />

## b) Kirjoita raportti siitä mitä opit ja mitkä asia yllättivät sinut kun tutustuit harjoitukseen.

Sain aika hyvän käsityksen siitä, miten paljon tietoa langattomista verkoista voidaan siepata ja analysoida ilman kirjautumistietoja ja miten näitä tietoja voidaan käyttää hyökkäystarkoituksessa hyödyntäen eri haavoittuvuuksia.

Mielenkiintoisimmat ja yllättävimmät havainnot, jotka tulivat harjoituksissa esille:

- Piilotettu ESSID (Extended Service Set Identifier) on mahdollista saada nopeasti selville esimerkiksi brute force -hyökkäyksellä.
- Oletus käyttäjätunnukset/salasanat tekevät kohteesta erittäin helpon maalin, joka on murrettavissa sekunneissa.
- Siepatusta ja analysoidusta liikenteestä voi paljastua arkaluontoista dataa selkokielisenä (kuten käyttäjätunnus ja salasana).
- MAC-osoitteen vaihtaminen ja sen hyödyntäminen hyökkäyksessä oli helposti ja nopeasti toteutettavissa.

## c) Miten suhtautumisesi WLanin turvallisuuteen muuttui sen jälkeen kun teit harjoitukset?

Olen aina ollut hieman skeptinen WLanin turvallisuudesta. Harjoituksissa selvisi monenlaisia riskejä ja jatkossa mietin sen käyttöä hyvin tarkkaan (missä verkossa, millä laitteilla ja onko välttämätöntä tarvetta).

Oman WLanin turvallisuuteen tulee varmasti kiinnitettyä enemmän huomiota ja pohdittua mitä laitteita siihen tulee liitettyä.

## Lähteet

Iso-Anttila, L. s.a. Verkkoon tunkeutuminen ja tiedustelu -opintojakson esitysmateriaali Moodlessa. Haaga-Helia ammattikorkeakoulu.

Karvinen, T. 26.3.2025. Verkkoon tunkeutuminen ja tiedustelu. https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/

Laorden, R. 9.8.2023. Walkthrough WiFiChallenge Lab v2.0. https://r4ulcl.com/posts/walkthrough-wifichallenge-lab-2.0/

WiFiChallenge Lab. https://lab.wifichallenge.com/
