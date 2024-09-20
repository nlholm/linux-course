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

_Tee kaksi uutta alidomainia, jotka osoittava omaan koneeseesi. Esimerkiksi palvelu on example.com -> linuxkurssi.example.com. Tee toinen alidomain A-tietueella ja toinen CNAME-tietueella. Alidomainit ovat tyypillisesti ilmaisia, kun sinulla on päädomain (example.com)._

Päätin tehdä b-tehtävän ennen a-tehtävää, jotta voisin käyttää a-tehtävässä oikeita domaineja local hostien sijasta.

Kirjauduin sisään nimipalvelu Namecheapin sivuille, ja etsin tietoa alidomainin lisäämisestä. Seurasin löytyneen [artikkelin](https://www.namecheap.com/support/knowledgebase/article.aspx/9776/2237/how-to-create-a-subdomain-for-my-domain/) ohjeita.  

![image](https://github.com/user-attachments/assets/e1be9814-4c6f-4631-add9-ca4034c17ec6)

Alidomainit ohjeistettiin lisäämällä päädomainin alle Advanced DNS-kohdassa lisäämällä uusia tietueita.

![image](https://github.com/user-attachments/assets/9a733d08-b8a2-4d76-985e-0fed20f44c11)

Tehtävänannon mukaisesti loin yhden A Record -tyyppisen alidomainin ja toisen CNAME Record-tyyppisen. Tavoittelemani alidomainit olivat siis n.holmroos.me ja info.n.holmroos.me. Sivuja käytetään tässä vaiheessa vain harjoitusmielessä, joten en halunnut niiden viittaavan liian ilmeisesti koko nimeeni.

## a) Kotisivu

_Tee vähintään kolmen erillisen weppisivun kotisivu ja kopioi se näkymään palvelimellesi. Jos sinulla on oikea palvelin Internetissä, kannattaa käyttää sitä. Käytä name based virtual hosting tekniikkaa. Sivujen muokkaamisen pitää onnistua ilman pääkäyttäjän oikeuksia, niiden kopioiminen pääkäyttäjänä testisivun paikalle ei käy. Kotisivujen ei tarvitse olla hienoja, mutta niiden tulee olla validia HTML:ää ja linkittää toisiinsa._

Html-kokemukseni rajoittuu Johdanto digitaalisiin palveluihin -kurssin varsin vajavaiseen toteutukseen edeltävältä keväältä, joten päätin tässä tehtävässä tyytyä mahdollisimman yksinkertaisiin sivuihin, jotka kuitenkin vastaisivat omista domaineistaan ja linkkaisivat toisiinsa.

Navigoin w3 schoolsin [HTML-tuoriaaliin](https://www.w3schools.com/html/default.asp) muistelemaan linkkien tekoa, muilta osin hyväksikäytin Karvisen yksinkertaisen html-sivun [ohjetta](https://terokarvinen.com/2012/short-html5-page/).

Tein sivuille kansiot virtuaali-Debianissani, ajatuksena kopioida ne myöhemmin pilvi-Debianiini. Tein kansiot kotihahakemistoni alaiseen publicsites-hakemistoon.

![image](https://github.com/user-attachments/assets/02d4e1d7-b76a-477b-bdd4-9c83ff4fe9ec)

![image](https://github.com/user-attachments/assets/3f64111d-8a5b-4db8-be5f-1e8f2057527d)
 
![image](https://github.com/user-attachments/assets/6d075e50-a563-4fe4-8d60-33aedde9fd00)

Loin kansioihin varsinaiset html-sivut microlla. Aloitin holmroos.me.sivusta.

![image](https://github.com/user-attachments/assets/b502eda4-8a82-4408-8962-ac310d0de19a)

Kopion sivun sivuksi n.holmroos.me ja siirsin sen hakemistoon n.holmroos.me. Polun oikein saaminen vaati muutamia yrityksiä, täytyy todeta, että tässä kohtaa graafinen käyttöliittymä on helppokäyttöisempi.

![image](https://github.com/user-attachments/assets/3714520b-3317-4484-874a-9a7e4da06cc5)

Muotoilin sivun n.holmroos.me sisällön microlla. Olin unohtanut tiedostopäätteen .html (sitä ei välttämättä Linuxissa tarvita), siksi näytti varsin harmaalta.

![image](https://github.com/user-attachments/assets/bda5a803-db70-4ad8-a27f-a0c256c725dc)
 
Muutin tiedoston nimen, `mv n.holmroos.me n.holmroos.me.html`. 

![image](https://github.com/user-attachments/assets/d6472e78-0183-4709-b2c0-ad114e4a6e56)

Luettavuus parani.

![image](https://github.com/user-attachments/assets/edf9fc73-542f-4ba7-b8a6-ce3153c5b191)

Seuraavaksi siirsin kolmannen weppisivunsa omaan kansioonsa ja muokkasin sen halutunlaiseksi.

Testasin sivut [w3-validatorissa](https://validator.w3.org/#validate_by_input). Suurempia ongelmia ei löytynyt.

![image](https://github.com/user-attachments/assets/df7ce1c7-7c45-4a65-9568-77ba273f0d03)
 
holmroos.me

Näiden vaiheiden jälkeen avasin SSH-yhteyden pilvi-Debianini (delfiini), `ssh nlholm@holmroos.me `ja päivitin sen ohjelmistot.

![image](https://github.com/user-attachments/assets/b7d61233-9f36-4599-98ad-8c88a20f1cb9)

Kirjauduin ulos delfiinistä, ja kokeilin kopioida äsken virtuaali-Debianiin luodut kansiot sisältöineen kerralla delfiiniin.

![image](https://github.com/user-attachments/assets/a0616ee3-4ff0-468e-a636-e8599cadaaf7)

Eipä onnistunut.

![image](https://github.com/user-attachments/assets/f246806e-e223-4af1-95de-ed34f276ef0e)

Ei vieläkään. Luovutin ja tein kansiot ja tiedostot uudestaan pilvikoneessa.

![image](https://github.com/user-attachments/assets/a422ab63-bec2-4eb1-a6ff-9742f2a5c1dd)

![image](https://github.com/user-attachments/assets/9e9397da-6407-401f-97a9-ac9ce24ea2b8)
 
![image](https://github.com/user-attachments/assets/80a5e7ba-6dc3-42b9-922d-ac6292dc7303)

![image](https://github.com/user-attachments/assets/ba677c65-5585-4127-96d3-582bb92c765f)
 
Hmm, käyttäjä tarvitsi sudo-oikeudet pystyäkseen tekemään kansioita. Oikeuksissa oli jotain vikaa. Lisäsin käyttäjän adm-ryhmään, mutta se ei auttanut. Kysyin Chat-GPT:ltä apuja ja toimin ohjeiden mukaan. Oikeudet näyttivät korjausten jälkeen oikeilta.

![image](https://github.com/user-attachments/assets/4e3b5b3c-30ad-40d6-abc9-1ba5ec09d3a2)

Yritin luoda html-tiedoston uudestaan, mutta tarvitsin edelleen sudo-oikeudet sen tallentamiseen… 

![image](https://github.com/user-attachments/assets/3b242072-2922-4714-86f3-cd3c7f7db0bd)

Uusi yritys oikeuksien korjaamisessa. `sudo chown -R nlhom:nlholm /home/nlholm`

![image](https://github.com/user-attachments/assets/62206c4d-d210-4542-92a9-0216bbc65006)

No niin, järjestelmä lopetti jatkuvan oikeuksien kyselemisen.

![image](https://github.com/user-attachments/assets/e8ffcf07-af40-4cdb-965c-7b708cdaaca6)

Kolmaskin weppisivu tuli tallennetua kansioonsa.

Seuraavaksi navigon kohteeseen /etc/apache2/sites-available, ja muokkasin tai loin konffitiedostot kullekin weppisivulle.

![image](https://github.com/user-attachments/assets/fecefadf-d811-455a-bb96-d62c98591b28)

holmroos.me

![image](https://github.com/user-attachments/assets/3b768970-d735-47fa-a9ad-107629b350c9)

n.holmroos.me

![image](https://github.com/user-attachments/assets/eadc3eea-7e62-4d3e-b8a1-f398a4788030)

info.n.holmroos.me

![image](https://github.com/user-attachments/assets/626c8a9a-c814-44da-84f0-4ac7b4a75059)
 
![image](https://github.com/user-attachments/assets/5f4309ed-b11a-42db-8bee-d212f85d0b00)

Ajoin sivuille yksi kerrallaan `sudo a2ensite holmroos.me`ja `systemctl reload apache2`

![image](https://github.com/user-attachments/assets/69071fcb-1b35-49cf-a7ff-fae79ed967d0)
 
Hups, yhdessä konffissa oli kirjoitusvirhe, korjasin muuttamalla tiedoston nimen (mv vanha nimi uusi nimi).

![image](https://github.com/user-attachments/assets/7f8cc8f8-5717-4e5f-8acb-f55a773e544b)

Mutta järjestelmä väitti edelleen, että sivua ei löydy. Konffitiedosto kuitenkin oli kunnossa. Samoin html-sivu löytyi.

![image](https://github.com/user-attachments/assets/cd3eab6b-ed4b-423d-9105-ac1b1aeca50e)

Alkoi väsymys painaa. Tuijotin konffitiedoston alkua niin tiiviisti, että en huomannut, että nimen lopusta puutui .me. Ehkä opetus myös siitä, että ei kannata tehdä liian pitkiä ja monimutkaisia domain-nimiä.

![image](https://github.com/user-attachments/assets/69caecc6-e871-4b12-be01-4240735d6dd8)

Sivut tulivat lopulta enabloiduiksi ja Apache uudelleenkäynnistetyksi.

![image](https://github.com/user-attachments/assets/c4b638e1-6560-4e61-a258-924edef793a1)

Asennusten jälkeen jälkeen kokeilin sivuja, mutta ne eivät toimineet.

![image](https://github.com/user-attachments/assets/ebe053ee-a9ba-4eb6-883e-01f6eb96c5c7)

Vaihdoin kunkin nettisivun nimen index.html:äksi, Chat-GPT:n mukaan Apachen on helpompi löytää ne näin.

![image](https://github.com/user-attachments/assets/f4cc43e5-3478-4c24-b4bd-03becbdc5fcf)
 
![image](https://github.com/user-attachments/assets/41a79df9-6033-416f-8ac3-c9c8dd5746ac)

Pääsivu holmroos.me  alkoi viimein toimimaan. Korjasin vielä väärin näkyvät lainausmerkit. 

![image](https://github.com/user-attachments/assets/e872e76a-d3ea-44e4-945e-3a9efbed0ec5)
 
![image](https://github.com/user-attachments/assets/a9062b11-4d74-42f5-aa2d-6dadf6ced780)

Muutaman uudelleenkäynnistyksen jälkeen alisivut alkoivat myös toimimaan. Sivut ovat todella karut, mutta näkyvissä.

Sivut eivät tosin toimineet, jos ne aloitti www:llä. Ilmeisesti Namecheapin www-tietue ei riitä kattamaan alidomaineja (konffitiedostoista alias löytyy). Yritin etsiä tutorialia Namecheapin sivuilta, mutta en tahtonut löytää sopivaa. Niinpä päädyin jälleen kyselemään neuvoja Chat-GPT:ltä. Kokeilin lisätä kaksi uutta CNAME-tietuetta tekoälyn ohjeistuksen mukaan. Näissä www osoittaa uusiin alidomaineihin.

![image](https://github.com/user-attachments/assets/e59b8a3b-d903-40c7-b096-6024d355fbcc)

Neuvosta ei kuitenkaan ollut apua, alidomainit eivät edelleenkään toimineet kera www:n. Päätin palata ongelman ratkomiseen myöhempänä ajankohtana.

![image](https://github.com/user-attachments/assets/913e9e19-4643-4c00-a4ae-22ba5c7f8e59)
 
## c) Pubkey

_Automatisoi kirjautuminen julkisella SSH-avaimella._

Hain tietoa epäsymmetrisistä avaimista mm. seuraavista artikkeleista: https://en.wikipedia.org/wiki/Public-key_cryptography, https://en.wikipedia.org/wiki/Secure_Shell, https://en.wikipedia.org/wiki/Ssh-keygen, https://ifixlinux.com/post/how-to-generate-ssh-key-on-mac-linux/. 

Lopulta päädyin kuitenkin pyytämään Chat-GPT:ltä ohjeet avainparin asettamiseksi, ja sainkin mielestäni hyvät ja havainnolliset ohjeet. Etenin niiden mukaan.

![image](https://github.com/user-attachments/assets/86ea00f7-ed37-4816-ab4e-3bcc47346ee0)
 
Prompti.

![image](https://github.com/user-attachments/assets/87c14646-69ef-44ba-b5ae-7ffb21a852ad)

Loin RSA-tyyppisen avaimen, bitit spesifioitu. Tallensin sen ehdotettuun lokaatioon. Jätin tunnuslauseen tyhjäksi.

Yksityinen avain sijaitsee täällä: ~/.ssh/id_rsa

Julkinen avain joka jaetaan kotha pilvipalvelimelle, sijaitsee täällä: ~/.ssh/id_rsa.pub

![image](https://github.com/user-attachments/assets/44fd4278-666c-4a6a-8fde-c34eefca006a)
 
![image](https://github.com/user-attachments/assets/2914502d-d687-41ca-a5f3-e39d541894ec)

Käytin ssh-copy-id -komentoa kopioidakseni julkisen avaimen pilvipalvelimen tiedostoon ~/.ssh/authorized_keys.

![image](https://github.com/user-attachments/assets/c9f70328-f05c-442b-b218-f65f880601a8)

ssh nlholm@ip. Sisäänkirjautuminen onnistui ilman salasanaa. Sama onnistui käyttämällä domain-nimeä nlholm@holmroos.me.

![image](https://github.com/user-attachments/assets/fa72343c-2e35-4440-94f9-58346832d80c)
 
![image](https://github.com/user-attachments/assets/7a75f279-5aad-406f-abcd-2d2e3234e699)

Varmistin luvituksen, koska sen kanssa on ollut ongelmia pilvipalvelimella.

## d) Nimien DNS-tiedot sekä host ja dig-komennot

_Tutki jonkin nimen DNS-tietoja 'host' ja 'dig' -komennoilla. Käytä kumpaakin komentoa kaikkiin nimiin ja vertaa tuloksia. Katso man-sivulta, miten komennot toimivat - esimerkiksi miten 'dig' näyttää kaikki kentät. Analysoi tulokset. Etsi tarvittaessa uusia lähteitä haastaviin kohtiin. Sähköpostin todentamiseen liittyvät SPF- ja DMARC -tietojen yksityiskohdat on jätetty vapaaehtoiseksi lisätehtäväksi. Tutkittavat nimet:_
-	_Oma domain-nimesi. Vertaa tuloksia nimen vuokraajan (namecheap.com, name.com...) weppiliittymässä näkyviin asetuksiin._
-	_Jonkin pikkuyrityksen, kerhon tai yksittäisen henkilön weppisivut. (Ei kuitenkaan kurssikaverin tällä viikolla vuokrattua nimeä)._
-	_Jonkin suuren ja kaikkien tunteman palvelun tiedot._

Host:

![image](https://github.com/user-attachments/assets/296e847d-6f9b-49fc-a33d-5ac5ad4c0ae4)

Dig:

![image](https://github.com/user-attachments/assets/ced49d2a-d744-4d0b-a2ca-e4501e423873)

### Oma domain-nimeni

Domain-nimeni on holmroos.me. Host-komennolla saan siitä esiin lähinnä ulkoisen ip-osoitteen. Tämä oli ilmeisesti tarkoituskin.

Host:

![image](https://github.com/user-attachments/assets/7b413fda-d48a-4c4e-a5dd-fb0565715b0c)

Dig-komennolla tietoja tuli vastaan hieman enemmän.

Dig:

![image](https://github.com/user-attachments/assets/e5d475a9-9514-4883-98b4-db3554029e62)

![image](https://github.com/user-attachments/assets/e68d4c31-cb9f-4dbe-a94f-bb9eadf62e49)

Uutena tietona tässä oli lähinnä DNS-palvelin, joka vastasi omasta paikallisen Windows-koneeni reitittimestä.

### Yksittäisen henkilön weppisivut

Tutkin pilvipalveluopettajamme Pekka Korpi-Tassin sivuja osoitteessa pekkakorpi-tassi.fi.

Host:

![image](https://github.com/user-attachments/assets/3b4a6f62-1ace-4eee-82e7-26d3258a9a8f)

Pekan sivuilla on näemmä useita IP-osoitteita. Yleensä asia menee toisin päin; useita sivuja yhden IP-osoitteen takana. Pekan sivut on kuitenkin rakennettu Amazonin AWS-alustan päälle, joten Chat-GPT:n arvailut mm. load balancingista ja redundanssista osunevat kohdalleen.

![image](https://github.com/user-attachments/assets/3132fc44-8b84-47ed-a649-b86582ee1da4)
 
Dig: 

![image](https://github.com/user-attachments/assets/1ade2fb4-4a8a-4fc6-af92-8c13229abdf4)
 
A tarkoittaa A-tietuetta eli IPv4-osoitetta.

### Suuren palvelun sivut

Tutkin sivuja www.nvidia.com/en-us/ . 

Host:

![image](https://github.com/user-attachments/assets/507d20a8-7a29-4ae9-8438-2f1d2c0277df)

Dig:

![image](https://github.com/user-attachments/assets/ca9a171f-5406-4f7e-9b3b-ca6aa1e118f8)
 
En nähnyt komentojen välillä olennaisia eroja. Argumenteilla tai kommenteilla olisi varmastikin saanut esille lisää tietoja. Tässä vaiheessa minulla ei kuitenkaan ollut enempää aikaa käytettävissäni, koska olin jälleen edellisenä päivänä käyttänyt tuntikausia vianselvittelyyn. Kurssin työmäärä tuntui jälleen jokseenkin ylisuurelta aloittelijalle, joka joutuu tekemään paljon taustatyötä.

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
