# Hello Web Server

[Linux Palvelimet 2024 alkusyksy](https://terokarvinen.com/linux-palvelimet/) -kurssin kolmannessa tehtävässä asensin Apache-weppipalvelimen Debianiini ja testasin sen käyttöä. Olin jälleen kerran uuden äärellä. 

Tein tehtävän torstaina 5.9.2024.

## Laitteisto

### Host

Käytössäni on Windows 11 Home -käyttöjärjestelmällä varustettu jokusen vuoden vanha HP:n kannettava kone, jonka tiedot ovat seuraavat: 

- HP:n kannettava Envy x360
- 64-bittinen käyttöjärjestelmä: Windows 11 Home Edition
- CPU ja näytönohjain: AMD Ryzen 7 3700U with Radeon Vega Mobile Gfx 2.30 GHz (4 ydintä, 8 säiettä)
- RAM: 16,0 GB (käytettävissä 13,9 GB käytettävissä)
- Levytila: 476 GB SSD, vapaana 202 GB

### Guest

- Virtualisointiympäristönä Oracle VM VirtualBox 7.0.20
- Virtuaalikoneena Debian GNU/Linux 12.6.0 (”Bookworm”)
- CPU 4 ydintä
- RAM: 4 GB
- Levytila: 30 GB

## x) Lue ja tiivistä

Ennen varsinaisen tehtävän aloittamista luin hieman teoriaa nimiperusteisista virtuaali-isännistä Apache Software Foundationin artikkelista [Name-based Virtual Host Support]( https://httpd.apache.org/docs/2.4/vhosts/name-based.html) sekä Karvisen artikkelista [Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address[(https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/). 

Apache Software Foundationin artikkelissa kerrotaan yleisiä periaatteita nimiperusteisille virtuaali-isännille. Artikkelissa vastattiin mm. kysymyksiin, kuinka nimiperusteiset virtuaali-isännät eroavat IP-perusteisista; kuinka palvelin valitsee oikean nimiperusteisen virtuaali-isännän; ja kuinka isäntä tai isännät tulisi perustaa.

Karvisen artikkelissa annetetaan yksityiskohtaisempia ohjeita nimiperusteisen virtuaali-isännän konfigurointiin.

## a) Apache-weppipalvelin

_Asenna Apache-weppipalvelin, jos se ei ole jo asennettuna. Testaa, että weppipalvelimesi vastaa localhost-osoitteesta. _

Debianiini ei ollut ennestään asennettu Apachea, joten aloitin tehtävän tekemisen asennustöillä.

Aloitustilanne:

![image](https://github.com/user-attachments/assets/5bcddb22-efbf-4605-8e4f-cc39edef902b)
 
![image](https://github.com/user-attachments/assets/4bcbce50-b111-4ad1-8ff2-622de1ca21f1)

![image](https://github.com/user-attachments/assets/dcf28efc-0210-4d1b-863d-6756128e1e28)
 
Web-palvelinohjelmistoa ei vielä ollut.

Asensin Apachen:

![image](https://github.com/user-attachments/assets/32aba7c5-7b0f-43ee-ab7e-536a99eaf770)
 
![image](https://github.com/user-attachments/assets/ad7d2502-7358-4e25-92c6-561609dbcc0f)

Asennus onnistui, ja pääsin lukemaan Apache2 Debian Default Pagea. Tämä kehotettiin muuttamaan.

![image](https://github.com/user-attachments/assets/d720eecf-b370-4344-a64c-21cc20e14dfe)
 
Käynnistin Apachen `sudo systemctl enable –now apache2`:

![image](https://github.com/user-attachments/assets/0d729423-ed06-4754-baca-1b8ee7970c03)
 
Testailin kertaalleen, tällä kertaa IP-osoitteella:

![image](https://github.com/user-attachments/assets/abb3671a-6fc5-4206-a26f-a4632adb532b)
 
![image](https://github.com/user-attachments/assets/36168b67-774a-4912-9eba-cba16e2ab795)

Muutin aloitussivun sisällön:

`echo "Tervehdys!" | sudo tee /var/www/html/index.html`

![image](https://github.com/user-attachments/assets/27762c79-bd13-475b-9b42-057bc6e5d128)

![image](https://github.com/user-attachments/assets/34a6c843-a8f7-4ce8-8ae4-4a41d893102b)
 
Toesin, että web-palvelin vastaa localhost-osoitteesta.

Seuraavaksi annoin pääkäyttäjänä tavallisille käyttäjille oikeuden luoda web-sivuja.

Lähtötilanne:

![image](https://github.com/user-attachments/assets/79a15c82-e215-460e-9d95-4e6362c80fe8)

![image](https://github.com/user-attachments/assets/cad1f114-ae85-4b2f-a353-b527480cdae8)

Virhe 404, webpage not found.

Oikeudet annoin am käskyllä, jota varten siirryin ensin Apache2-kansioon (ei olisi ollut tarpeen):

```
sudo a2enmod userdir
```

![image](https://github.com/user-attachments/assets/716c6d1b-e1f5-4242-a50c-eb07201dfd77)
 
Oikeuksien antamisen jälkeen käynnistin Apache2:sen eli ”potkaisin demonia”.

![image](https://github.com/user-attachments/assets/0a8d8ec3-9e89-4268-afea-2ab7a4ae1643)
 
Virheilmoitus muuttui 404:sta 403:seen.

Selitys löytyi logista; nlholm/public_html-kansiota ei ole (en kylläkään olisi itse osannut tulkita virhettä, mutta se käytiin tunnilla läpi):

![image](https://github.com/user-attachments/assets/2eeeef45-66d9-4516-bbe4-48eef5ec887e)

![image](https://github.com/user-attachments/assets/adcb6cad-7c24-4b64-b724-441161e7a0f7)
 
Loin siis kansion /nlholm/public_html/:

![image](https://github.com/user-attachments/assets/30bafdba-5a75-4a67-9234-22a2f5095b50)
 
![image](https://github.com/user-attachments/assets/10491a65-4675-491f-90ac-93faf5366919)

Nyt kansio löytyi. Sisältö listattuna vielä curlilla:

![image](https://github.com/user-attachments/assets/a7c26a37-2ca1-46c4-917b-44b3d26d3318)

Mikäli kotisivu olisi ollut kielletty (virhe 403), asia  olisi hoitunut käskyllä

```
chmod ugo+x $HOME $HOME/public_html/', 'ls -ld $HOME $HOME/public_html/
```

tai lyhyemmin 

```
chmod ugo+x /home/nlholm/
```

Tästä oli esimerkki tunnilla:

![image](https://github.com/user-attachments/assets/007474b3-999b-4b0d-9149-cc34d0aa8bd4)

Perusasennuksen lopuksi säädin palomuurin asetuksia Karvisen [ohjeilla](https://terokarvinen.com/2016/instant-firewall-sudo-ufw-enable/):

```
sudo ufw allow 22/tcp
```
Tämä käsky avaa portin 22 SSH-liikennettä varten, ts jos palvelimeeni olisi tarvetta ottaa SSH-yhteys.

```
sudo ufw allow 80/tcp
```
Tämä käsky avaa portin 80 web-palvelimen HTTP-liikennettä varten, ts tekee palvelimesta julkisen.

```
sudo ufw allow 443/tcp
```
Tämä käsky puolestaan avaa portin 443 web-palvelimen TLS-salattua HTTP-liikennettä varten.

En ollut varma, oliko säätöjä tarpeen tehtävänannon puitteissa tehdä, mutta tulipahan tehtyä.

![image](https://github.com/user-attachments/assets/ea498d22-a8cb-4603-88b7-dcd7e51b1971)

## b) Lokit

_Etsi lokista rivit, jotka syntyvät, kun lataat omalta palvelimeltasi yhden sivun. Analysoi rivit (eli selitä yksityiskohtaisesti jokainen kohta ja numero, etsi tarvittaessa lähteitä)._

![image](https://github.com/user-attachments/assets/6a761ef0-69c5-4276-a9f1-6b5ac9fb08d0)
 
Latasin uudelleen localhost-indeksisivuni, ja lähdin tutkimaan Apachen access-lokia (jonka | nl laittaa riveille).

Vaihdoin rivinäkymän 50:neen, ja sain seuraavan tuloksen. 

![image](https://github.com/user-attachments/assets/378df124-4f49-48ca-a1c1-a10a2b69f336)
 
Rivit 26-29 näyttivät kellonajan perusteella liittyvän localhost-sivun päivitykseen. Tutkin mitä näkymästä voidaan todeta, osittain Chat-GPT:n avulla.

-	**127.0.0.1**. “127.0.0.1 is called the loopback address, and is the IP a computer uses to refer to itself. A server running on your local PC will be accessible at 127.0.0.1, or you can force internet traffic to connect to 127.0.0.1 instead of accessing a website to block access to that site.”, kertoo Lewisin artikkeli [What Is the 127.0.0.1 IP Address, and How Do You Use It? ](https://www.howtogeek.com/789017/what-is-the-127.0.0.1-ip-address-and-how-do-you-use-it/). “It is also possible you just want to run a service that is only accessible to you, on your local device. This is relatively common in the self-hosting community --- it doesn't make sense to unnecessarily expose a service to outside devices and threats.”
-	**Päivämäärä- ja kellonaikatietoja**.
-	**“GET /~nlholm/ HTTP/1.1”**. GET on HTTP-metodi, jolla pyydetään dataa resurssilta, /~nlholm/ on resurssin osoite, HTTP/1.1 on HTTP-protokollan yleisesti käytetty versio 1. 
-	**200 499/490**. 200 tarkoittaa status ok, 490 on vastauksen pituus bitteinä.
-	**"Mozilla/5.0 (X11; Linux x86_64; rv:109-0) Gecko/20100101 Firefox/115.0"."** This User-Agent string is telling the server that the request is coming from a Firefox browser (version 115.0) running on a 64-bit Linux system using the Gecko rendering engine, with revision 109.0.”

ChatGPT:n promptit ja vastaukset, jotka olivat mielestäni hyvin havainnolliset:

 ![image](https://github.com/user-attachments/assets/7e3975de-5757-42b0-bc2d-eaf53b1d563f)

![image](https://github.com/user-attachments/assets/ad982114-cf71-4f50-81b9-0affcef1cc38)

![image](https://github.com/user-attachments/assets/9480fb00-c1e2-4d48-9230-7abdea74b891)

## c) Etusivu uusiksi

_Tee uusi **name based virtual host**. Sivun tulee näkyä suoraan palvelimen etusivulla http://localhost/. Sivua pitää pystyä muokkaamaan normaalina käyttäjänä, ilman sudoa. Tee uusi, laita vanhat pois päältä. Uusi sivu on **hattu.example.com**, ja tämän pitää näkyä: asetustiedoston nimessä, asetustiedoston ServerName-muuttujassa sekä etusivun sisällössä (esim title, h1 tai p)._

Tämän osatehtävän onnistumisesta en ollut lainkaan varma, mutta lähdin kokeilemaan nimiperusteisen virtuaali-isännän luomista Karvisen [ohjeiden]( https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/) perusteella.

``
$ sudoedit /etc/host
``

![image](https://github.com/user-attachments/assets/b74e5313-7c15-4312-86f3-b70862a2ad10)

 ![image](https://github.com/user-attachments/assets/8e150c79-0eea-4068-89b8-b68891878943)

Totesin että en tiedä yhtään mitä olen tekemässä, tähän kohtaan olisin kaivannut huomattavasti selkeämpiä ohjeita. Onko ajatus, että tällä tekstitiedostolla luodaan hakemisto /debian/publicsites? Sellaista ei nimittäin ennestään ollut.

![image](https://github.com/user-attachments/assets/de1976c4-53a0-49af-9dfb-14b4164789a9)

![image](https://github.com/user-attachments/assets/9d5ae05b-e138-4c88-ab18-01cb0465887f)

![image](https://github.com/user-attachments/assets/055c65e3-3b96-49cf-b7ee-8b7bac68b53d)

Jotain meni pieleen, mutta en tiedä mitä (Directoryn kirjoitusvirheen lisäksi).

![image](https://github.com/user-attachments/assets/7fe5dd0e-34f9-43b5-9077-5babff48a7c0)

Hakemistopolussa taisi olla jotain vikaa. Kokeilin muuttaa hakemistoa kuten yllä.

![image](https://github.com/user-attachments/assets/fdefa582-7c5b-4b37-b464-7ed06448c5d7)

Mikään ei toiminut edelleenkään. Olin lisäksi onnistunut rikkomaan yhteyden palvelimelleni. Tässä kohtaa täytyy todeta, että Karvisen ohjeet olivat aloittelijalle aivan riittämättömät.

Kysyin tarkempia ohjeita Chat-GPT:ltä, ja etenin niiden mukaan.

![image](https://github.com/user-attachments/assets/d63b73df-2745-4cd7-bd87-03fd125c11c7)
 
Lopputulos oli että Apache ei käynnistynyt edelleenkään:

![image](https://github.com/user-attachments/assets/4c00de23-b768-403f-b606-ea1d27d10646)
 
En keksinyt enää muuta keinoa, kuin apoistaa Apache2 ja aloittaa alusta (`sudo apt-get purge apache2`).

Uusi yritys VirtualHost configuration filen kanssa:

![image](https://github.com/user-attachments/assets/8fa270c6-c34f-4789-ac31-b4a77675aa18)
 
Totesin että web-palvelimessa on edelleen vikaa. Tässä kohtaa aikaa oli kulunut tuntikausia, luovutin. 

![image](https://github.com/user-attachments/assets/b0edee27-8d2e-4c33-adfe-bfe654fff0aa)

Sekä localhost-sivu että http://hattu.example.com tulostivat /var/www/html/index.html -tiedostoon tallennetun tervehdystekstin.

![image](https://github.com/user-attachments/assets/a6cd0487-c4dc-4ece-b896-9d8ff91ea015)
 
Olin luonut kohdassa e) mainitun html-sivun localhostin alle jo aiemmin, mutta enää en päässyt siihen selaimella käsiksi.

Poistin tervehdystekstin komennolla ` sudo a2dissite 000-default.conf`. Nyt alkoi localhostin alle luotu weppisivu taas näkymään, mutta hattu.example lopetti toimimisen.

![image](https://github.com/user-attachments/assets/ec9587f8-bee7-4797-b49c-7027f9dd7d08)
 
Kaeiken kaikkiaan voidaan todeta, että epäonnistuin nimiperusteisen virtuaali-isännän luomisessa, enkä osannut omin voimin korjata tilannetta.

![image](https://github.com/user-attachments/assets/04967a90-5885-4c06-9e54-06bb61b07ed0)
 
## e) HTML5-sivu

_Tee validi HTML5 sivu._

Tein tämän osatehtävän ilman ongelmia, ennen kuin asiat alkoivat mennä pieleen kohdassa d).

Kirjoitin hyvin lyhyen HTML-sivun microlla Karvisen [ohjeiden]( https://terokarvinen.com/2012/short-html5-page/) mukaan. Tallensin sivun public_html-hakemistooni nimellä index.html.

![image](https://github.com/user-attachments/assets/1c268f34-d7b8-4557-ae4b-765d59d25aba)
 
![image](https://github.com/user-attachments/assets/301be0c2-6569-4b1d-9333-2bceb4d82043)

## f) ’curl -l’ ja ’curl’

_Anna esimerkit 'curl -I' ja 'curl' -komennoista. Selitä 'curl -I' muutamasta näyttämästä otsakkeesta (response header), mitä ne tarkoittavat._

Curl ja curl -i -komennoilla voi etsiä tietoa URL-osoitteista. -i-komento antaa enemmän tietoa response headereista. Alla esimerkki komennon käytöstä.

![image](https://github.com/user-attachments/assets/dc327c20-2a79-49c0-a2aa-ef05348f1c89)

Esimerkki response headerista: Palvelimeksi on nimetty Apache/2.4.62 (Debian).

## m) GitHub Education

_Vapaaehtoinen, suosittelen tekemään: Hanki GitHub Education -paketti._

Hankin paketin [Git Hub Education-linkin](https://github.com/education) ohjeiden mukaan. Säätämistä oli senkin kanssa, koska enää ei ole saatavilla perinteisiä opiskelijakortteja.

## Lähteet 

Apache Software Foundation, The. 2024. Name-based Virtual Host Support. Luettavissa: https://httpd.apache.org/docs/2.4/vhosts/name-based.html .

Karvinen, T. 8.9.2016. Instant Firewall – sudo ufw enable. Tero Karvinen – Learn Free Software with me. Luettavissa https://terokarvinen.com/2016/instant-firewall-sudo-ufw-enable/ .

Karvinen, T. 2024. Linux Palvelimet 2024 alkusyksy. Tero Karvinen – Learn Free Software with me. Luettavissa https://terokarvinen.com/linux-palvelimet/ .

Karvinen, T. 10.4.2018. Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address. Tero Karvinen – Learn Free Software with me. Luettavissa https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/ .

Karvinen, T. 12.2.2012. Short HTML5 page. Tero Karvinen – Learn Free Software with me. Luettavissa https://terokarvinen.com/2012/short-html5-page/  .

Lewis, Nick. 14.3.2022. What Is the 127.0.0.1 IP Address, and How Do You Use It? How-To Geek. Luettavissa: https://www.howtogeek.com/789017/what-is-the-127.0.0.1-ip-address-and-how-do-you-use-it/ .  

