# h5 Nimekäs

[Linux Palvelimet 2024 alkusyksy](https://terokarvinen.com/linux-palvelimet/) –kurssin viidennen viikon tunnilla vuokrasimme  domainin eli verkkotunnuksen edellisellä viikolla hankitulle pilvipalvelimellemme. Vuokrasin verkkotunnuksen [holmroos.me]( http://www.holmroos.me/) [Name Cheapilta]( https://www.namecheap.com/) GilHub Educationilta saaduilla krediiteillä.

Kurssin viidennessä tehtävässä vuokrasin kaksi uutta alidomainia sekä loin kolmen erillisen weppisivun kotisivun, jonka laitoin osoittamaan pilvipalvelimen IP-osoitteeseen käyttäen name based hosting -tekniikkaa (viikko 3). Lisäksi automatisoin kirjautumisen virtuaali-debianiini julkisella SSH-avaimella. Lopuksi tutkin muutaman weppipalvelun DNS-tietoja host- ja dig-komennoilla. 

Tein tehtävän osiot a) ja b) torstaina 19.9.2024. Aloitin klo 16, ja valmista tuli klo 22. Loppuosan tehtävästä tein perjantain 20.9.2024 klo 15-18.

## Laitteisto

### Host

Käytössäni on Windows 11 Home -käyttöjärjestelmällä varustettu jokusen vuoden vanha HP:n kannettava kone, jonka tiedot ovat seuraavat: 

- HP:n kannettava Envy x360
- 64-bittinen käyttöjärjestelmä: Windows 11 Home Edition
- CPU ja näytönohjain: AMD Ryzen 7 3700U with Radeon Vega Mobile Gfx 2.30 GHz (4 ydintä, 8 säiettä)
- RAM: 16,0 GB (käytettävissä 13,9 GB)
- Levytila: 476 GB SSD, vapaana 202 GB

### Guest

- Virtualisointiympäristönä Oracle VM VirtualBox 7.0.20
- Virtuaalikoneena Debian GNU/Linux 12.6.0 (”Bookworm”)
- CPU 4 ydintä
- RAM: 4 GB
- Levytila: 30 GB

## b) Alidomain

Tee kaksi uutta alidomainia, jotka osoittava omaan koneeseesi. Esimerkiksi palvelu on example.com -> linuxkurssi.example.com. Tee toinen alidomain A-tietueella ja toinen CNAME-tietueella. Alidomainit ovat tyypillisesti ilmaisia, kun sinulla on päädomain (example.com).

Päätin tehdä b-tehtävän ennen a-tehtävää, jotta voisin käyttää a-tehtävässä oikeita domaineja local hostien sijasta.

Kirjauduin sisään nimipalvelu Namecheapin sivuille, ja etsin tietoa alidomainin lisäämisestä. Seurasin löytyneen [artikkelin](https://www.namecheap.com/support/knowledgebase/article.aspx/9776/2237/how-to-create-a-subdomain-for-my-domain/) ohjeita.  

 

Alidomainit ohjeistettiin lisäämällä päädomainin alle Advanced DNS-kohdassa lisäämällä uusia tietueita.

 

Tehtävänannon mukaisesti loin yhden A Record -tyyppisen alidomainin ja toisen CNAME Record-tyyppisen. Tavoittelemani alidomainit olivat siis n.holmroos.me ja info.n.holmroos.me. Sivuja käytetään tässä vaiheessa vain harjoitusmielessä, joten en halunnut niiden viittaavan liian ilmeisesti koko nimeeni.

## a) Kotisivu

Tee vähintään kolmen erillisen weppisivun kotisivu ja kopioi se näkymään palvelimellesi. Jos sinulla on oikea palvelin Internetissä, kannattaa käyttää sitä. Käytä name based virtual hosting tekniikkaa. Sivujen muokkaamisen pitää onnistua ilman pääkäyttäjän oikeuksia, niiden kopioiminen pääkäyttäjänä testisivun paikalle ei käy. Kotisivujen ei tarvitse olla hienoja, mutta niiden tulee olla validia HTML:ää ja linkittää toisiinsa.

Html-kokemukseni rajoittuu Johdanto digitaalisiin palveluihin -kurssin varsin vajavaiseen toteutukseen edeltävältä keväältä, joten päätin tässä tehtävässä tyytyä mahdollisimman yksinkertaisiin sivuihin, jotka kuitenkin vastaisivat omista domaineistaan ja linkkaisivat toisiinsa.

Navigoin w3 schoolsin [HTML-tuoriaaliin](https://www.w3schools.com/html/default.asp) muistelemaan linkkien tekoa, muilta osin hyväksikäytin Karvisen  yksinkertaisen html-sivun [ohjetta](https://terokarvinen.com/2012/short-html5-page/).

Tein sivuille kansiot virtuaali-Debianissani, ajatuksena kopioida ne myöhemmin pilvi-Debianiini. Tein kansiot kotihahakemistoni alaiseen publicsites-hakemistoon.


 

 

 
¨
Loin kansioihin varsinaiset html-sivut microlla. Aloitin holmroos.me.sivusta.

 

Kopion sivun sivuksi n.holmroos.me ja siirsin sen hakemistoon n.holmroos.me. Polun oikein saaminen vaati muutamia yrityksiä, täytyy todeta, että tässä kohtaa graafinen käyttöliittymä on helppokäyttöisempi.

 

Muotoilin sivun n.holmroos.me sisällön microlla. Olin unohtanut tiedostopäätteen .html (sitä ei välttämättä Linuxissa tarvita), siksi näytti varsin harmaalta.

 

Muutin tiedoston nimen, `mv n.holmroos.me n.holmroos.me.html`. 

 

Luettavuus parani.

 

Seuraavaksi siirsin kolmannen weppisivunsa omaan kansioonsa ja muokkasin sen halutunlaiseksi.

Testasin sivut [w3-validatorissa](https://validator.w3.org/#validate_by_input). Suurempia ongelmia ei löytynyt.

 

holmroos.me

Näiden vaiheiden jälkeen avasin SSH-yhteyden pilvi-Debianini (delfiini), `ssh nlholm@holmroos.me `ja päivitin sen ohjelmistot.

 

Kirjauduin ulos delfiinistä, ja kokeilin kopioida äsken virtuaali-Debianiin luodut kansiot sisältöineen kerralla delfiiniin.

 

Eipä onnistunut.

 

Ei vieläkään. Luovutin ja tein kansiot ja tiedostot uudestaan pilvikoneessa.

 

 

 

 

Hmm, käyttäjä tarvitsi sudo-oikeudet pystyäkseen tekemään kansioita. Oikeuksissa oli jotain vikaa. Lisäsin käyttäjän adm-ryhmään, mutta se ei auttanut. Kysyin Chat-GPT:ltä apuja ja toimin ohjeiden mukaan. Oikeudet näyttivät korjausten jälkeen oikeilta.

 

Yritin luoda html-tiedoston uudestaan, mutta tarvitsin sudo-oikeudet sen tallentamiseen… 

 

Uusi yritys oikeuksien korjaamisessa. `sudo chown -R nlhom:nlholm /home/nlholm`

 

No niin, järjestelmä lopetti jatkuvan oikeuksien kyselemisen.

 

Kolmaskin weppisivu tuli tallennetua kansioonsa.

Seuraavaksi navigon kohteeseen /etc/apache2/sites-available, ja muokkasin tai loin konffitiedostot kullekin weppisivulle.


 

holmroos.me

 

n.holmroos.me

 

info.nholmroos.me

 

 

Ajoin sivuille yksi kerrallaan `sudo a2ensite holmroos.me`ja `systemctl reload apache2`

 

Hups, yhdessä konffissa oli kirjoitusvirhe, korjasin muuttamalla tiedoston nimen (mv vanha nimi uusi nimi).

 

Mutta nyt järjestelmä väitti edelleen, että sivua ei löydy. Konffitiedosto kuitenkin oli kunnossa. Samoin html-sivu löytyi.

 

Alkoi väsymys painaa. Tuijotin konffitiedoston alkua niin tiiviisti, että en huomannut, että nimen lopusta puutui .me. Ehkä opetus myös siitä, että ei kannata tehdä liian pitkiä ja monimutkaisia domain-nimiä.

 

Sivut tulivat lopulta enabloiduiksi ja Apache uudelleenkäynnistetyksi.

 

Asennusten jälkeen jälkeen kokeilin sivuja, mutta ne eivät toimineet.

 

Vaihdoin kunkin nettisivun nimen index.html:äksi, Chat-GPT:n mukaan Apachen on helpompi löytää ne näin.

 

 

Pääsivu holmroos.me  alkoi viimein toimimaan. Korjasin vielä väärin näkyvät lainausmerkit. 

 

 

Muutaman uudelleenkäynnistyksen jälkeen alisivut alkoivat myös toimimaan. Sivut ovat todella karut, mutta näkyvissä.

Sivut eivät tosin toimineet, jos ne aloitti www:llä. Ilmeisesti Namecheapin www-tietue ei riitä kattamaan alidomaineja (konffitiedostoista alias löytyy). Yritin etsiä tutorialia Namecheapin sivuilta, mutta en tahtonut löytää sopivaa. Niinpä päädyin jälleen kyselemään neuvoja Chat-GPT:ltä. Kokeilin lisätä kaksi uutta CNAME-tietuetta tekoälyn ohjeistuksen mukaan. Näissä www osoittaa uusiin alidomaineihin.

 

Neuvosta ei kuitenkaan ollut apua, alidomainit eivät edelleenkään toimineet kera www:n. Päätin palata ongelman ratkomiseen myöhempänä ajankohtana.

 

## c) Pubkey

Automatisoi kirjautuminen julkisella SSH-avaimella.

Hain tietoa epäsymmetrisistä avaimista mm. seuraavista artikkeleista: https://en.wikipedia.org/wiki/Public-key_cryptography , https://en.wikipedia.org/wiki/Secure_Shell , https://en.wikipedia.org/wiki/Ssh-keygen , https://ifixlinux.com/post/how-to-generate-ssh-key-on-mac-linux/ . 

Lopulta päädyin kuitenkin pyytämään Chat-GPT:ltä ohjeet avainparin asettamiseksi, ja sainkin mielestäni hyvät ja havainnolliset ohjeet. Etenin niiden mukaan.

 

Prompti.

 

Loin RSA-tyyppisen avaimen, bitit spesifioitu. Tallensin sen ehdotettuun lokaatioon. Jätin tunnuslauseen tyhjäksi.

Yksityinen avain sijaitsee täällä: ~/.ssh/id_rsa
Julkinen avain joka jaetaan kotha pilvipalvelimelle, sijaitsee täällä: ~/.ssh/id_rsa.pub

 

 

Käytin ssh-copy-id -komentoa kopioidakseni julkisen avaimen pilvipalvelimen tiedostoon ~/.ssh/authorized_keys.

 

ssh nlholm@ip. Sisäänkirjautuminen onnistui ilman salasanaa. Sama onnistui käyttämällä domain-nimeä nlholm@holmroos.me.

 

 

Varmistin luvituksen, koska sen kanssa on ollut ongelmia pilvipalvelimella.

## d) Nimien DNS-tiedot sekä host ja dig-komennot

Tutki jonkin nimen DNS-tietoja 'host' ja 'dig' -komennoilla. Käytä kumpaakin komentoa kaikkiin nimiin ja vertaa tuloksia. Katso man-sivulta, miten komennot toimivat - esimerkiksi miten 'dig' näyttää kaikki kentät. Analysoi tulokset. Etsi tarvittaessa uusia lähteitä haastaviin kohtiin. Sähköpostin todentamiseen liittyvät SPF- ja DMARC -tietojen yksityiskohdat on jätetty vapaaehtoiseksi lisätehtäväksi. Tutkittavat nimet:
-	Oma domain-nimesi. Vertaa tuloksia nimen vuokraajan (namecheap.com, name.com...) weppiliittymässä näkyviin asetuksiin.
-	Jonkin pikkuyrityksen, kerhon tai yksittäisen henkilön weppisivut. (Ei kuitenkaan kurssikaverin tällä viikolla vuokrattua nimeä).
-	Jonkin suuren ja kaikkien tunteman palvelun tiedot.

Host:

 

Dig:

 

### Oma domain-nimeni

Domain-nimeni on holmroos.me. Host-komennolla saan siitä esiin lähinnä ulkoisen ip-osoitteen. Tämä oli ilmeisesti tarkoituskin.

Host:

 

Dig-komennolla tietoja tuli vastaan hieman enemmän.

Dig:

 

 

Uutena tietona tässä oli lähinnä DNS-palvelin, joka vastasi omasta paikallisen Windows-koneen reitittimestä.

### Yksittäisen henkilön weppisivut

Tutkin pilvipalveluopettajamme Pekka Korpi-Tassin sivuja osoitteessa pekkakorpi-tassi.fi.

Host:

 

Pekan sivuilla on näemmä useita IP-osoitteita. Yleensä asia menee toisin päin; useita sivuja yhden IP-osoitteen takana. Pekan sivut on kuitenkin rakennettu Amazonin AWS-alustan päälle, joten Chat-GPT:n arvailut mm. load balancingista ja redundanssista osunevat kohdalleen.

 

Dig: 

 

A tarkoittaa A-tietuetta eli IPv4-osoitetta.

### Suuren palvelun sivut

Tutkin sivuja www.nvidia.com/en-us/ . 

Host:

 

Dig:

 

En nähnyt komentojen välillä olennaisia eroja. Argumenteilla tai kommenteilla olisi varmastikin saanut esille lisää tietoja. Tässä vaiheessa minulla ei kuitenkaan ollut enempää aikaa käytettävissäni, koska olin jälleen edellisenä päivänä käyttänyt tuntikausia vianselvittelyyn. Kurssin työmäärä tuntui jälleen ylisuurelta aloittelijalle, joka joutuu tekemään paljon taustatyötä.

# Lähteet

Fix Linux. 14.9.2022. How to Generate SSH Key And Connect to The Server Without Password. Luettavissa: https://ifixlinux.com/post/how-to-generate-ssh-key-on-mac-linux/ .

Namecheap. 2024. Luettavissa: https://www.namecheap.com/ .

Namecheap. 25.9.2023. How to Create a Subdomain for my Domain. Luettavissa: https://www.namecheap.com/support/knowledgebase/article.aspx/9776/2237/how-to-create-a-subdomain-for-my-domain/ .

Holmroos, N. 2024. Holmroos.me. Luettavissa: http://www.holmroos.me/ .

Karvinen, T. 2024. Linux Palvelimet 2024 alkusyksy. Tero Karvinen – Learn Free Software with me. Luettavissa https://terokarvinen.com/linux-palvelimet/ .

Karvinen, T. 12.2.2012. Short HTML5 page. Tero Karvinen – Learn Free Software with me. Luettavissa https://terokarvinen.com/2012/short-html5-page/  .

W3 schools. sa. HTML Tutorial. Luettavissa: https://www.w3schools.com/html/default.asp .

W3C.2024. Marup Validation Service. Luettavissa: https://validator.w3.org/ . 

Wikipedia. 2024. Public-key cryptography. Luettavissa: https://en.wikipedia.org/wiki/Public-key_cryptography .

Wikipedia. 2024. Secure Shell. Luettavissa: https://en.wikipedia.org/wiki/Secure_Shell .

Wikipedia. 2024. ssh-keygen, Luettavissa: https://en.wikipedia.org/wiki/Ssh-keygen .
