### h5 Laboratorio- ja simulaatioympäristöt hyökkäyksissä [Tehtävänanto](https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#h5-laboratorio--ja-simulaatioymparistot-hyokkayksissa)

## Tehtävissä käytetty ympäristö

### PC

- Käyttöjärjestelmä: Windows 11 Home 64-bit
- Suoritin: AMD Ryzen 7 5800X 8-Core Processor
- Muisti: 32GB RAM
- Näytönohjain: NVIDIA GeForce RTX 3080
- Virtualisointiohjelmisto: Oracle VM VirtualBox 7.0

- Internet yhteys: DNA Netti 600 M

## a) Tutustu seuraavaan työkaluun https://github.com/kgretzky/evilginx2 . Vastaa seuraaviin kysymyksiin
- Asensitko työkalun, jos asensit niin kirjoita miten sen teit.
- Mitä teit työkalun kanssa?
- Onnistuitko huijaamaan liikennettä

Aloitin lataamalla päivitykset ja kloonasin evilginx2 -repon

    sudo apt-get update
    git clone https://github.com/kgretzky/evilginx2

Tämän jälkeen siirryin kloonattuun kansioon ja käänsin ohjelman

    cd evilginx2
    make

Mutta `make` komennon jälkeen sain herjan

    make: go: No such file or directory
    make: *** [Makefile:8: build] Error 127

Tarkistin, että oliko go asennettuna `go version`

<img width="436" height="98" alt="image" src="https://github.com/user-attachments/assets/2ebf6801-5ac8-4ed1-9017-cbe6439445d5" />

Ei löytynyt Kalista valmiina, joten asensin sen ajamalla komennon `sudo apt install golang-go`

Tämän jälkeen `make` meni läpi. Siirryin build -kansioon ja ajoin ohjelman `./evilginx`

<img width="1087" height="562" alt="image" src="https://github.com/user-attachments/assets/f88c48f0-728d-4d83-ab69-e1e55420366c" />

Ohjelma pyytää polkua phishlets -tiedostoja varten, asetin sen ajamalla `./evilginx -p /home/ap/evilginx2/phishlets`

<img width="1126" height="627" alt="image" src="https://github.com/user-attachments/assets/7c4effb3-b283-4c6e-81f3-ae75a510101e" />

[Quickstart](https://help.evilginx.com/community/getting-started/quickstart) ohjeilla pitäisi onnistua paikallinen testaus:

    Esimerkki:
    
    config domain not-a-phish.com
    config ipv4 127.0.0.1
    phishlets hostname linkedin totally.legit.linkedin.not-a-phish.com
    phishlets enable linkedin
    lures create linkedin # Antaa lure ID:n
    lures get-url [Lure ID]

    --> Tulostuu linkki huijaussivustolle
    

Muutamien testailujen jälkeen harjoituksen työstäminen tyssäsi toistaiseksi kuitenkin tähän: "too many failed authorizations (5) for "academy.not-a-phish.evilginx-testi.com" in the last 1h0m0s"

Testasin kuitenkin vielä huijaussivusto -linkkiä ja evilginx alkoi tulostamaan lokia:

<img width="1138" height="144" alt="image" src="https://github.com/user-attachments/assets/45645dfe-c2ae-47ad-9add-1546d79e2c82" />

Täytyy palata tähän harjoitukseen myöhemmin TLS ongelman takia. Aikaa on ollut todella rajallisesti muuttokiireistä johtuen.

## b) Sinulla on käytössäsi mininet-ympäristö. Luo ympäristö, jossa voit tehdä TCP SYN-Flood hyökkäyksen. Kirjoita miten loit mininet ympäristön ja miten toteutit hyökkäyksen.

Aloitin asentamalla mininetin ja xtermin kalille

    sudo apt-get update
    sudo apt-get install -y mininet xterm

Mininetin käynnistys

    sudo mn --topo single,3 --mac --switch ovsk --controller remote

<img width="829" height="278" alt="image" src="https://github.com/user-attachments/assets/1a5c97fe-f93e-4555-afae-ec700002b241" />

Tulee herjaa openvswitchistä. Ajoin komennon `sudo service openvswitch-switch start` jonka jälkeen starttasi.

Tämän jälkeen avasin xtermillä koneet h1-h3 `xterm h1 h2 h3`:

<img width="1294" height="855" alt="image" src="https://github.com/user-attachments/assets/25c68a9b-d74f-4bc1-ab1c-8140bd50781a" />

`dump` -komennolla saadaan hostien ip-osoitteet näkyviin:

<img width="642" height="144" alt="image" src="https://github.com/user-attachments/assets/c952b9bd-a463-4b79-bd22-0043b842032c" />

Aika loppui kesken, enkä saanut ryu-manageria toimimaan. Kuitenkin hyökkäys hostilta h1 -> h2 olisi tapahtunut ajamalla `hping3 -S --flood 80 10.0.0.2`.

hostin h1 näkymä:

<img width="488" height="109" alt="image" src="https://github.com/user-attachments/assets/05952d01-b9dc-4608-b919-eaa556e07b3c" />

## Lähteet

Evilginx. Building. https://help.evilginx.com/community/getting-started/building

Evilginx. Quickstart Guide. https://help.evilginx.com/community/getting-started/quickstart

Iso-Anttila, L. s.a. Verkkoon tunkeutuminen ja tiedustelu -opintojakson esitysmateriaali Moodlessa. Haaga-Helia ammattikorkeakoulu.

Karvinen, T. 26.3.2025. Verkkoon tunkeutuminen ja tiedustelu. https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/

NCCS. Hping3 & Traffic/Attack Generator. https://nccs.gov.in/public/events/DDoS_Presentation_17092024.pdf
