# h4 Maailma kuulee

[Linux Palvelimet 2024 alkusyksy](https://terokarvinen.com/linux-palvelimet/) -kurssin neljännessä tehtävässä vuokrasin virtuaalipalvelimen, tein sille alkutoimet, ja asensin sille weppipalvelimen. 

Tein tehtävän torstaina 12.9.2024. Aloitin klo 15, ja valmista tuli klo 20.

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

## x) Lue ja tiivistä

Ennen varsinaisen tehtävän aloittamista luin hieman teoriaa virtuaalipalvelimista Karvisen artikkelista [First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS](https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/). Artikkelissa esitetään tiiviisti toimenpiteet, joiden avulla virtuaalipalvelin saadaan pystyyn:
•	Perusta tili palveluntarjoajalle (esimerkkinä Digital Ocean) ja luo uusi virtuaalipalvelin.
•	Kirjaudu koneelle etänä SSH:ta hyödyntäen. Luo käyttäjä ja anna käyttäjälle sudo-oikeudet.
•	Pystytä palomuuri, tee reikä SSH:ta varten.
•	Lukitse root-tili.
•	Päivitä ohjelmistot ja asenna web-palvelin kuten Apache.
•	Hanki palvelimellesi domain-nimi julkiselta DNS-palveluntarjoajalta.

Susanna Lehdon erinomaisesta raportista [Teoriasta käytäntöön pilvipalvelimen avulla (h4)]( https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/) löysin puolestaan tervetulleet, yksityiskohtaiset ohjeet siitä, miten virtuaalipalvelimen perustaminen kannattaa käytännössä tehdä vaihe vaiheelta. Tämän tasoiset ohjeet ovat minulle aloittelijana arvokkaita; edellisen tehtävän kanssa käytin tuntikausia aikaa virheiden selvittelyyn, koska en tahtonut ymmärtää osaamistasooni verrattuna turhan ylimalkaisia ohjeita.

## a) Virtuaalipalvelimen vuokraus

_Vuokraa oma virtuaalipalvelin haluamaltasi palveluntarjoajalta. (Vaihtoehtona voit käyttää ilmaista kokeilujaksoa, GitHub Education krediittejä; tai jos mikään muu ei onnistu, voit kokeilla ilmaiseksi vagrant:ia paikallisesti. Suosittelen kuitenkin harjoittelemaan oikeilla, tuotantoon kelpaavilla julkisilla palveluilla)._

Edellisellä viikolla jättämäni GitHub Education -hakemukseni oli lisätietojen antamisen jälkeen hyväksytty, ja pääsin tutkimaan [Student Developer Pack -sivuston]( https://education.github.com/pack#digitalocean) tarjoamaa, josta kurssikaveri ystävällisesti vinkkasi (oikeaa sivua en onnistunut löytämään Git Hub Educationin sivustolta muuten lainkaan).

Navigoin sivun keskivaiheille kohtaan All offers ja valitsin DigitalOceanin tarjouksen.

![image](https://github.com/user-attachments/assets/464e133d-fc21-4c66-be63-365b227679a3)

![image](https://github.com/user-attachments/assets/96a6087e-92ec-4f06-8225-f3ef3c80b225)

Kirjauduin Digital Oceaniin GitHub-tunnuksillani, ja käytin Student Pack -tarjouksen.

![image](https://github.com/user-attachments/assets/e1c03b54-227d-4168-9985-04d2823b30ad)
 
Seuraavaksi loin virtuaalipalvelimen (Create Droplet).

![image](https://github.com/user-attachments/assets/66901188-b2e6-4804-a8df-603e17a04f4a)

Valinnat:

![image](https://github.com/user-attachments/assets/422eace1-31d3-4d97-bfc6-9d094aa6299c)
 
![image](https://github.com/user-attachments/assets/ba31c162-78e5-4f54-a616-d12815c104dd)

![image](https://github.com/user-attachments/assets/12354768-8d70-4428-8e3a-07e3bfd71efd)
 
![image](https://github.com/user-attachments/assets/015c92cd-dc49-4b89-a6fc-e309cf2abc6f)

Valitsin palvelimeeni regioonan läheltä itseäni, OS Debian 12, shared  regular CPU, min. 1 GB RAM, 25 GB SSD, 1000 GB transfer. En valinnut lisäpalveluja. Hintaa kombinaatiolle tuli 6 USD/kk.

Kone  luotiin n. 30 sekunnissa. Otin talteen koneen IP-osoitteen ja tiedot. Tein itselleni kalenterimerkinnän poistaa kone, jos en tarvitse sitä enää vuoden jälkeen.

![image](https://github.com/user-attachments/assets/e25d6c40-0fc9-4666-be8a-89b2c12b4518)

## b) Alkutoimet virtuaalipalvelimella

_Tee alkutoimet omalla virtuaalipalvelimellasi: tulimuuri päälle, root-tunnus kiinni, ohjelmien päivitys._

Käynnistin VirtualBoxissa sijaitsevan virtuaali-Debianini (niina-virtualbox) ja avasin terminaalin. Otin SSH-yhteyden virtuaalipalvelimeeni osoitteessa 167.71.76.115. Ensimmäisen yhteyden ollessa kyseessä, komento oli 

```
ssh root@167.71.76.115
```
![image](https://github.com/user-attachments/assets/db8ab920-a6c5-4de9-973d-06f6d449957c)

Yhteys tuli luotua onnistuneesti.

![image](https://github.com/user-attachments/assets/23c8fdef-79ba-4e30-8af0-76b6c3604157)

Lisäsin käyttäjän nlholm (`sudo adduser nlholm`), ja annoin käyttäjälle sudo-oikeudet (`sudo adduser nlholm sudo`).

![image](https://github.com/user-attachments/assets/57ae70e1-a5cf-4262-8280-9c498425e301)

Asensin palomuurin (`sudo apt-get install ufw`), tein siihen reiän SSH:ta varten (`sudo ufw allow 22/tcp`) ja laitoin palomuurin päälle (`sudo ufw enable`).

![image](https://github.com/user-attachments/assets/91a3285b-d04f-49a5-a914-ba01f314a7ca)

Testasin toisella terminaaliyhteydellä, että yhteys verkkopalvelimen käyttäjään löytyy. Onnistuin toisella yrittämällä.

![image](https://github.com/user-attachments/assets/eb8d0f98-4eda-487d-b427-05d096134c30)

Palasin ensimmäiseen terminaaliin, lukitsin juuritilin (`sudo usermod --lock root`), ja vaihdoin käyttäjäksi nlholm (`su nlholm`).

```
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt-get dist-upgrade
````
![image](https://github.com/user-attachments/assets/40a8edcf-9b36-4995-9152-1e5745f0bdfc)

Lopuksi päivitin virtuaalipalvelin delfiinin ohjelmistot.

## c) Weppipalvelin virtuaalipalvelimelle

_Asenna weppipalvelin omalle virtuaalipalvelimellesi. Korvaa testisivu. Kokeile, että se näkyy julkisesti. Kokeile myös eri koneelta, esim kännykältä._

![image](https://github.com/user-attachments/assets/c1b5752b-6988-4f89-be91-aa8cf0096950)

Olin avannut palomuurin portin 80 samalla kuin 22:sen, mutta tarkistin vielä palomuurin tilan.

![image](https://github.com/user-attachments/assets/925967d3-6f84-4235-bbe9-76c8505ee8e0)

![image](https://github.com/user-attachments/assets/104cdde5-8930-4bb5-b6e3-b23d440f88c3)

![image](https://github.com/user-attachments/assets/021aaa61-c324-4072-a332-bac125df5f70)

Asensin web-palvelin Apache2:sen edellisen viikon oppien mukaan.

![image](https://github.com/user-attachments/assets/7a3170cc-f356-4325-aedc-ba7d90fb1d8a)

Testisivu toimi.
 
![image](https://github.com/user-attachments/assets/a9975a16-69aa-483e-8bc8-1a6157b69ee7)

![image](https://github.com/user-attachments/assets/2a173b67-5c7f-4728-87eb-6b838ed21ce5)
 
![image](https://github.com/user-attachments/assets/cd7cccbf-6e31-4c7b-88b3-8f6f0c13345f)

Korvasin testisivun tervehdyksellä.

![image](https://github.com/user-attachments/assets/3f9a4e6b-984a-4ea7-a36b-77a90cd5c865)

Loin käyttäjän nlholm kotikansioon kansiot public_html ja publicsites.

![image](https://github.com/user-attachments/assets/0c2a652b-a2be-46c4-98ea-0cc826ad05ba)

Asensin micron ja loin lyhyen HTML-sivun käyttäjän nlholm public_html-kansioon.

![image](https://github.com/user-attachments/assets/addb9cc0-4611-4fb0-84e8-beedc259bb0a)

Hmm, sain 403-virheen. Tarkistin kertaalleen, että userdir oli käynnissä, ja käynnistin Apachen uudelleen. Tämäkään ei auttanut.

![image](https://github.com/user-attachments/assets/cbaf26fb-3ea8-41a1-9be0-1c6fa5cb3df7)

Annoin käyttäjän oikeudet uudestaan edellisellä tunnilla sivutulla komennolla.

![image](https://github.com/user-attachments/assets/44d176d3-6f4a-4fc7-acdb-b808bafb6f3c)
 
![image](https://github.com/user-attachments/assets/e5d20676-188e-4a93-b43e-2d129e02bf9b)

Kotisivut lähtivät käyntiin.

![image](https://github.com/user-attachments/assets/1daf3049-2707-40fb-91e3-bcdef255a5dd)

Ja toimivat myös Windows-koneen Chrome-selaimessa, ts. julkisen verkon yli.

![image](https://github.com/user-attachments/assets/b15627fc-5555-42d0-bad1-9acaf05ef292)

Lopuksi kokeilin luoda nimiperusteisen virtuaali-isännän dolphin.example.com, mutta hosts-tiedosto näyttikin erilaiselta virtuaalipalvelimella. En tehnyt tässä vaiheessa muutoksia.

![image](https://github.com/user-attachments/assets/c753a789-a853-41ac-b00d-03e341cd9c4d)
 
Asennustyöt tuli onnistuneesti tehtyä. Kirjauduin ulos SSH-istunnosta komennolla `exit`.

## Lähteet 

GitHub.com. 2024. GitHub Student Developer Pack. Luettavissa: https://education.github.com/pack#digitalocean .

Karvinen, T. 19.9.2017. First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS. Tero Karvinen – Learn Free Software with me. Luettavissa https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/ .

Karvinen, T. 2024. Linux Palvelimet 2024 alkusyksy. Tero Karvinen – Learn Free Software with me. Luettavissa https://terokarvinen.com/linux-palvelimet/ .

Leino, Susanna. 14.2.2022. Teoriasta käytäntöön pilvipalvelimen avulla (h4). Susanna Leino – Blogi. Luettavissa: https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/ .
