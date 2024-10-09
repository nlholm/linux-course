# h7 Maalisuora

[Linux Palvelimet 2024 alkusyksy](https://terokarvinen.com/linux-palvelimet/) –kurssin seitsemännessä ja viimeisessä kotitehtävässä harjoittelin ohjelmointikielien alkeita Linuxilla sekä kokeilin muutaman skriptin kirjoittamista. Tein myös vanhan arvioitavan laboratorioharjoituksen soveltuvin osin. Lopuksi asensin uuden tyhjän virtuaalikoneen oman kurssini arvioitavaa labraa varten, mutta tätä kohtaa ei käsitellä raportissa.  

Tein tehtävän useammassa osassa. Aloitin lukemalla taustamateriaaleja perjantaina 4.10. klo 11.30-14.00. Seuraavaksi tein ohjelmointiharjoitukset klo 14.00-17.00. Vanhaa arvioitavaa laboratoriotehtävää en ehtinyt tehdä raportin palauttamisen määräaikaan mennessä, mutta palautin raportin ensin tiistaina 8.10 klo 17.30, ja aloin sen jälkeen tekemään tehtävää. Täydensin raporttia myöhemmin tämän tehtävän osalta. 

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

## a) Hei maailma kolmella kielellä 

_Kirjoita ja aja "Hei maailma" kolmella kielellä._

Tehtävän a-osassa tukena toimi Karvisen artikkeli [Hello World Python3, Bash, C, C++, Go, Lua, Ruby, Java – Programming Languages on Ubuntu 18.04](https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/). Lisäksi kyselin Chat-GPT:ltä apuja kielien asentamiseen Linuxille, sekä perusasioita kustakin kielestä; koodauskokemukseni on toistaiseksi hyvin rajoittunutta. Chat-GPT auttoikin am kommenteissa ja tulkinnoissa.

### Python3

Ennen kunkin kielen kokeilua, se täytyy asentaa Linuxiin. Pythonin osalta tämä oli jo tehty  edellisellä viikolla (`sudo apt-get install python3`, `python3 –version`), joten etenin luomaan kotihakemistooni code-kansion, sen alle python-kansion, ja sen alle heipy-kansion (`mkdir heipy`). Siirryin kansioon cd-komennolla. Seuraavaksi loin microlla tiedoston, johon python-koodi tallennettaisiin (`micro hello.py`), ja kirjoitin itse koodin, `print (”Hello, world!”)`. Koodi ajettiin komennolla`python3 hello.py`. Pelkkä cat puolestaan näyttää tiedoston sisällön, ajamatta koodia. 

![image](https://github.com/user-attachments/assets/bd53e3cb-ec42-4c29-9c1e-53ace9bc0d26)

### Bash

Bash on Debianin sisäänrakennettu oletusympäristö (komentotulkki), joten sitäkään ei tarvitse yleensä erikseen asentaa tai käynnistää. Tarkistin version:

![image](https://github.com/user-attachments/assets/fded7855-c68b-4ad8-9f6c-dc9f3fec61cd)

![image](https://github.com/user-attachments/assets/ed0b28a4-5ad7-42b8-a960-3af43542e737)
 
Kooditiedosto on muotoa .sh, ja se ajetaan komennolla `bash`.

### Ruby

Ruby asennetaan `sudo apt-get update`, `sudo apt-get upgrade`, `sudo apt-get install ruby-full`.

![image](https://github.com/user-attachments/assets/4aa6b17d-796a-4700-9e68-8f80e20bd3ee)

Kooditiedosto on muotoa .rb, ja se ajetaan komennolla `ruby`.

### Java

Bonuksena Java.

![image](https://github.com/user-attachments/assets/f3662518-c565-4888-93ea-6a30fbf15173)

Tässä olennaista on, että tiedoston nimi on sama kuin luokan nimi. Tiedostopääte on .java.  `javac Hello.java`kääntää koodin, `java Hello`suorittaa sen. Ensimmäisessä yrityksessä oli kirjoitusvirhe (”system” pienellä).

## b) Uusi komento skriptinä

_Laita Linuxiin uusi komento niin, että kaikki käyttäjät voivat ajaa sitä._

B-tehtävän ohjeistuksena toimi Karvisen (varsin niukkasanainen) artikkeli [Shell Scripting](https://terokarvinen.com/2007/12/04/shell-scripting-4/). Kyselin jälleen tekoälyltä, että mitä tässä oikein ollaankaan tekemässä. Yleisissä tietoteknisissä kysymyksissä Chat-GPT on mielestäni aloittelijalle oikein oiva apu, vaikka eriäviäkin mielipiteitä kurssilla on esitetty.

![image](https://github.com/user-attachments/assets/8c0e6abc-533a-46de-a19f-96e6781e81d4)
 
![image](https://github.com/user-attachments/assets/67fc420b-8939-4279-b159-4e22fdb9061f)

Ei kun luomaan skriptiä. Otin hieman vinkkiä aiemmista kurssitoteutuksista, ja päätin luoda skriptin `hello.sh`, joka tulostaa käyttäjän nimen, nykyhakemiston polun, sisällön, päivämäärän sekä koneen käynnissäoloajan.   

![image](https://github.com/user-attachments/assets/72b4c36a-c8c5-4462-86be-fce22bcfec1c)

![image](https://github.com/user-attachments/assets/6aee7352-7883-45a4-b7a4-6d1bbee4aed9)

Tässä `#!/usr/bin/bash` määrittti, että skripti ajetaan bashilla kansiosta /usr/bin/bash (olisin voinut kirjoittaa myös /bin/bash). Sitten listattiin komennot. `bash hello.sh`ajoi skriptin.

![image](https://github.com/user-attachments/assets/b2d04705-1aca-487b-b649-884a50eea237)

`chmod a+x hello.sh` antoi kaikille käyttäjille oikeuden ajaa komento. 

![image](https://github.com/user-attachments/assets/d74424af-a318-4698-9390-39ed01de3c6f)

`sudo cp hello.sh /usr/local/bin/` kopioi skriptin kaikkien käyttäjien käytettäväksi ilman ./ kansioon /usr/local/bin.

## c) Vanha arvioitava laboratorioharjoitus

_Ratkaise vanha arvioitava laboratorioharjoitus soveltuvin osin._

Tein harjoitustehtävänä kevään 2024 Linux-kurssin labratehtävän, https://terokarvinen.com/2024/arvioitava-laboratorioharjoitus-2024-linux-palvelimet/.  Harjoitusta varten asensin uuden tyhjän virtuaali-Debianin. Tein koneelle päivitykset, asensin palomuurin ja micron. Aloitin harjoituksen keskiviikkona 9.10. klo 11.30, ja lopetin klo 16.00. 

Kirjoitan raportit Windows-koneella Wordissa, mutta labraharjotusta varten loin uudelle koneelle kansion reports, ja sinne index.md-tiedoston, johon labraharjoituksen eteneminen tulisi tositilanteessa merkitä. Testasin myös näyttökuvien ottamista Linuxilla sekä kuviin viittaamista raportissa (tähän asti olen copy-peistannut näyttökuvat GitHubissa luotuihin .md-tiedostoihin linkkeinä)

![image](https://github.com/user-attachments/assets/75a28921-8d15-4c0b-917b-5a71abac86b8)

### aa) Taustatiedot

-	_Oma nimi_
-	_Opiskelijanumero_
-	_Linkki omaan kotitehtäväpakettiin_

### bb) Tiivistelmä työstä

- _Vastaa tähän kohtaan aivan viimeisenä_
- _Mikä toimii, mikä ei_
- _Tämä toimii: toimivien palveluiden osoitteet tai polut komentoihin_
- _Tämä ei vielä toimi: luettelo kohdista, joita ei ratkaistu._
-   _Huomaa, että nopeimpienkin viihdyttämiseksi tässä tehtävässä on enemmän kohtia kuin mitä muutamassa tunnissa ehtii ratkoa._

Sain tehtyä viimeistä lukuunottamatta kaikki labran harjoitukset. Weppisivuja ja Djangoa en saanut toimimaan yhtä aikaa localhostista.

### cc) Ei kolmea sekoseiskaa

- _Suojaa raportti Linux-oikeuksilla niin, että vain oma käyttäjäsi pystyy katselemaan raporttia_

En tehnyt tätä vielä, siltä varalta, että raportille tulisi harjoituksessa lisäkäyttöä, mutta komento olisi `chmod u=r, go= index.md`.

Tällä erää oikeuksia oli enemmän:

![image](https://github.com/user-attachments/assets/aabe82a5-b8fc-4808-b8ca-5f20283ce043)

### dd) howdy

- _Tee kaikkien käyttäjien käyttöön komento 'howdy'_
-  _Tulosta haluamaasi ajankohtaista tietoa, esim päivämäärä, koneen osoite tms_
-   _Pelkkä "hei maailma" ei riitä_
- _Komennon tulee toimia kaikilla käyttäjillä työhakemistosta riippumatta_

Tämä tehtävä oli toisinto kohdan b) skriptaus-tehtävästä. 

![image](https://github.com/user-attachments/assets/c2b29d45-0256-45a3-95b9-20db7893a896)
 
![image](https://github.com/user-attachments/assets/2e2602a3-35de-44e7-a4be-62a61f7086c9)

Hups, komennon nimeksi tuli epähuomiossa hello howdyn sijasta. No, virallisemmalla linjalla jatketaan.

### ee) Etusivu uusiksi

- _Asenna Apache-weppipalvelin_
- _Tee yrityksellemme "AI Kakone" kotisivu_
- _Kotisivu tulee näkyä koneesi IP-osoitteella suoraan etusivulla_
- _Sivua pitää päästä muokkaamaan normaalin käyttäjän oikeuksin (ilman sudoa). Liitä raporttiisi listaus tarvittavien tiedostojen ja kansioiden oikeuksista._

![image](https://github.com/user-attachments/assets/8683eaf7-88ff-443f-afac-01a3931f140f)
 
Asensin Apachen ja loin uuden name based virtual hostin alkakone.com, joka vastaa locaslhostista.

![image](https://github.com/user-attachments/assets/c6fdc186-f3eb-42d4-87c3-41f697afcd4e)

Sivun muokkaukseen tarvittavan kansion alkakone.com oikeudet:

![image](https://github.com/user-attachments/assets/899e05c1-1670-4d81-92e2-439786f2d03b)
 
### gg) Salattua hallintaa

- _Asenna ssh-palvelin_
- _Tee uusi käyttäjä omalla nimelläsi, esim. minä tekisin "Tero Karvinen test", login name: "terote01"_
- _Automatisoi ssh-kirjautuminen julkisen avaimen menetelmällä, niin että et tarvitse salasanoja, kun kirjaudut sisään. Voit käyttää kirjautumiseen localhost-osoitetta_

Asensin OpenSSH-palvelimen tämän [artikkelin]( https://phoenixnap.com/kb/how-to-enable-ssh-on-debian) ohjeilla, tein uuden käyttäjän, loin uuden avainparin ja kopioin julkisen avaimen uudelle käyttäjälle.  Lopuksi otin yhteyden SSH:lla.

![image](https://github.com/user-attachments/assets/64bf7f1d-6b91-40c1-bc01-7ffa09d903d3)

### h) Djangon lahjat

- _Asenna omalle käyttäjällesi Django-kehitysympäristö_
- _Tee tietokantaan lista tekoälyistämme, jossa on nämä ominaisuudet_
-  _Kirjautuminen salasanalla_
-  _Tietokannan muokkaus wepissä Djangon omalla ylläpitoliittymällä (Django admin)_
-  _Käyttäjä Erkille, jossa ei ole ylläpito-oikeuksia_
-  _Taulu Assistants, jossa jokaisella tietueella on nimi (name)_
-  _Jos haluat, voit lisäksi bonuksena laittaa mukaan kentän koko (size)_

Asensin Djangon, ja aloitin testiprojektin.

![image](https://github.com/user-attachments/assets/d15b3726-3046-41c3-b2bb-59cb5debdf80)

Kaikki muut localhostit, mukaan lukien äsken luodut Al Kakosen weppisivut piti ottaa pois päältä, jotta Djangon testiliittymä lähti pyörimään. /etc/apache2/sites-available/, `sudo a2dissite 000-default.conf`, `sudo a2dissite alkakone.com.conf`.

![image](https://github.com/user-attachments/assets/aa372004-d875-44e7-b8a9-d1b746bce483)

Loin admin-liittymässä käyttäjän Erkki ilman ylläpitooikeuksia (superuserin on luonut jo aiemmin).

![image](https://github.com/user-attachments/assets/c4d26a5a-1c1d-485d-b7c4-09d8a04c4a5f)

Loin sovelluksen aiassistants, ja loin hallintaliittymässä sille muutaman tietueen.

![image](https://github.com/user-attachments/assets/afc0ce68-8410-432b-b1cf-6b4a85ae6685)
 
![image](https://github.com/user-attachments/assets/a16de314-4b0d-410e-a3d7-fcbcfa28c597)

### hh) Tuotantopropelli

- _Jos olet tässä kohdassa, olet kyllä työskennellyt todella nopeasti (tai sitten teet tätä tehtävää huviksesi kurssin jälkeen). Mutta älä huoli, tässä haastetta, jotta et joudu pyörittelemään peukaloita._
- _Tee tuotantotyyppinen asennus Djangosta_
- _Laita Django-lahjatietokanta tuotantotyyppiseen asennukseen_
- _Voit vaihtaa tämän sivun näkymään etusivulla staattisen sivun sijasta_

Tätä kohtaa harjoituslabrasta en ajanpuutteen vuoksi tehnyt.

# Lähteet

Karvinen, T. 12.3.2024. Final Lab for Linux Palvelimet 2024 Spring. Tero Karvinen – Learn Free Software with me.  Luettavissa: https://terokarvinen.com/2024/arvioitava-laboratorioharjoitus-2024-linux-palvelimet/ .

Karvinen, T. 27.9.2018. Hello World Python3, Bash, C, C++, Go, Lua, Ruby, Java – Programming Languages on Ubuntu 18.04. Tero Karvinen – Learn Free Software with me. Luettavissa: https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/

Karvinen, T. 2024. Linux Palvelimet 2024 alkusyksy. Tero Karvinen – Learn Free Software with me. Luettavissa https://terokarvinen.com/linux-palvelimet/ .

Karvinen, T. 4.12.2007. Shell Scripting. Tero Karvinen – Learn Free Software with me. Luettavissa: https://terokarvinen.com/2007/12/04/shell-scripting-4/ .

PhoenixNAP. 20.3.2024. Hoe to Enable SSH on Debian 12. Luettavissa: https://phoenixnap.com/kb/how-to-enable-ssh-on-debian
