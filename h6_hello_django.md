# Hello Django

[Linux Palvelimet 2024 alkusyksy](https://terokarvinen.com/linux-palvelimet/) –kurssin kuudennessa
tehtävässä asensin Django-sovelluskehyksen virtuaali-Debianiini ja harjoittelin kehyksen käyttöä tekemällä testi- ja tuotantotyyppiset asennukset. 

Testityyppisen asennuksen pääohjeena toimi Karvisen artikkeli [Django 4 Instant Customer Database Tutorial]( https://terokarvinen.com/2022/django-instant-crm-tutorial/) ja tuotantotyyppisen asennuksen pääohjeena puolestaan Karvisen artikkeli [Deploy Django 4 - Production Install](https://terokarvinen.com/2022/deploy-django/). Tehtävä oli haastava, joten selailin lisäksi usean aiemman kurssitoteutuksen oppilaiden raportteja asiaan liittyen. 

Tein tehtävän useammassa osassa. Aloitin lukemalla Karvisen artikkelit sekä aiempia raportteja perjantaina 27.9.2024 klo 16-19 ja maanantain 30.9.2024 klo 8-9.30. Itse tehtävän tekemisen aloitin maanantaina 30.9. klo 16.30. Valmista tuli n. klo 23.00 käytyäni välissä toisen kurssin luennolla.

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

## a) Yksinkertainen esimerkkiohjelma Djangolla

_Tee yksinkertainen esimerkkiohjelma Djangolla._
- _Voit käyttää testipalvelinta, kunhan se ei näy Internetiin._
- _Riittää, kun ohjelmasi näkyy esimerkiksi Django Adminsissa._
- _Voit halutessasi tehdä aivan samanlaisen kuin Teron CRM-esimerkissä. Jos olet jo taitavampi, voit hieman soveltaa._
- _Karvinen 2021: [Django 4 Instant Customer Database Tutorial]( https://terokarvinen.com/2022/django-instant-crm-tutorial/)_

Kuten Django-projekti (https://www.djangoproject.com/) kertoo, Django on web-kehys Pyhton-ohjelmointikielelle. Django on helppo- ja nopeakäyttöinen kehys, joka sisältää useita valmiita komponentteja ja työkaluja ohjelmointiprojektien helpottamiseksi.

Aloitin oman projektini luomalla virtuaali-Debianinin kotikansioon kansion 'django', asentamalla virtualenv-paketin ja luomalla testiympäristön kansion env/, joka käyttää Pythonin versiota 3.

![image](https://github.com/user-attachments/assets/ea3f2570-994d-4138-aaf1-9ef76037cdfb)

`sudo apt-get -y install virtualenv` luo virtuaaliympäristön.
`virtualenv --system-site-packages -p python3 env/` asentaa hakemiston.
`source env/bin/activate` ottaa käyttöön virtuaaliympäristön. `Env` tulee näkymään alkuun. Olennaista on olla siinä kansiossa, josta enviä ajetaan (tässä tapauksessa django, myöhemmin publicwsgi).

![image](https://github.com/user-attachments/assets/8840e6e8-69be-43db-ad6b-d3b86a5a9c1c)

`which pip` -komennolla varmistetaan, että ollaan env-ympäristössä. Pip-asennuksia ei tule tehdä env-ympäristön ulkopuolella, eikä etenkään sudolla. 

![image](https://github.com/user-attachments/assets/43b9868a-bba6-4bd1-b10a-80a5e7d2ab75)

Loin tekstitiedoston `requirements.txt` Python-paketteja varten:

![image](https://github.com/user-attachments/assets/3a7ffb85-e61a-42b1-bad4-9cd5e2c41eb5)

Tiedoston sisältö on lyhyt ja ytimekäs:

![image](https://github.com/user-attachments/assets/fa3288c5-0934-40ac-b193-35b72b03db42)

Tarkistus catilla:

![image](https://github.com/user-attachments/assets/5a4f93ac-8b84-46ed-8329-0dd11d8e4149)

Komento `pip install -r requirements.txt` asensi tiedoston. Lopuksi tarkistin version komennolla `django-admin –version`.

![image](https://github.com/user-attachments/assets/e4d92f21-438f-4716-9a3a-867dab9481f9)

Kun asennus oli valmis, oli aika aloittaa uuden projektin tekeminen.

`django-admin startproject project1`
`cd project1`
`./manage.py runserver` 

Viimeinen komento käynnistää kehitysympäristön palvelimella. Tätä kehitysympäristöä ei tule koskaan laittaa julkisesti esiin internetiin.

![image](https://github.com/user-attachments/assets/6ebfac4b-6edf-4dd7-aba9-b84a4fcf8130)
 
![image](https://github.com/user-attachments/assets/173b3dc0-e35e-453e-b690-c7b3cea60bfd)

Ilmoituksen mukaan testipalvelin oli toiminnassa osoitteessa http://127.0.0.1:8000/. Sammutus onnistuisi näppäinyhditelmällä Ctrl+C. Punaisessa tekstissä mainitut tietokantamigraatiot tekisin seuraavassa vaiheessa.

![image](https://github.com/user-attachments/assets/e2f676a5-3b41-431f-a903-a948fbe016ed)

Toistaiseksi asennus eteni suunnitelmien mukaan. Djangon etusivu näkyi localhostin portissa 8000.

Seuraavaksi loin adminin ko URL:ään http://127.0.0.1:8000/admin/. 

`./manage.py makemigrations` ja `./manage.py migrate` päivittävät tietokannat.

![image](https://github.com/user-attachments/assets/afa24eea-9bad-4042-a591-160c51016ef0)

Asensin salasanageneraattorin, `sudo apt-get install pwgen` ja loin satunnaisen 20-merkkisen salasanan, `pwgen -s 20 1`.

Komennolla `./manage.py createsuperuser` loin admin-käyttäjän.

Törmäsin ensin  unable to connect -ongelmaan yrittäessäni ottaa yhteyttä palvelimeen. Hetken asiaa pähkäiltyäni totesin, että tämä johtui siitä, että olin sulkenut palvelimen Ctrl+C:llä aiemmin, kun ajoin muita komentoja. Käynnistin palvelimen uudestaan komennolla `./manage.py runserver`, ja etusivu sekä admin-sivu tulivat näkyviin. 

 ![image](https://github.com/user-attachments/assets/df146d67-d5e0-4906-934f-c9fccf599db5)

![image](https://github.com/user-attachments/assets/f2813624-ebc2-4c1a-ab69-5362b70086f7)

Kirjauduin sisään äsken luoduilla superuserin tunnuksilla.
 
![image](https://github.com/user-attachments/assets/c6b572e2-bc70-4c13-9a84-563e114d2f34)

Loin hallintasivun kautta uuden käyttäjän djangouser1, ja annoin tälle staff- sekä superuser-oikeudet.

![image](https://github.com/user-attachments/assets/40da1f19-b4e9-400d-87dc-d7b5a85c289f)

Kirjauduin ulos hallintasivulta adminina ja uudestaan sisään user1:senä. Loin kolmannen käyttäjän, user2, ollessani kirjautuneena user1:senä. Tälle käyttäjälle annoin vain tavallisen käyttäjän oikeudet. Totesin, että user2:sen superoikeudet toimivat, koska niillä pystyi luomaan uuden käyttäjän.

![image](https://github.com/user-attachments/assets/bbfee523-3c5f-4c11-aec8-c5191e23cfba)

Seuraavaksi lähdin luomaan ensimmäistä sovellusta Djangoon. Päätin seurata Karvisen esimerkkiä, ja luoda vastaavanlaisen asiakashallintatietokantasovelluksen kuin hänen ohjeessaan.

Komento `./manage.py startapp crm` luo uuden kansion crm/ CRM-sovellusta varten.

Sovellus tulee lisätä kohtaan INSTALLED_APPS tiedostossa settings.py, ts.projektin asetuksia tulee muokata.

`micro project1/settings.py`

![image](https://github.com/user-attachments/assets/78c32f61-20f1-46d1-b8b6-c36ae714ba24)
 
![image](https://github.com/user-attachments/assets/265358d0-e870-4faa-bb80-94be9b8ac51c)

Seuraavaksi lisäsin mallin tiedostoon crm/models.py, jonka avulla Django loi tietokannan.

![image](https://github.com/user-attachments/assets/dec5d263-1bbc-4c12-a076-af0d5620dd31)

Kopioin tekstin suoraan Terolta, sillä tutkiessani asiaa aiemmin, olin oppinut, että tabuloinnin saaminen oikein on olennaista Pythonissa, mutta että micro saattaa sekoittaa tabulointia.

Tässä Customer-luokka loi ”customer”-taulun tietokantaan ja siihen ”nimi”-tietueen.
__str__  palauttaa objektin nimen (tässä tapauksessa asiakas). Ilman tätä funktiota tietueen nimenä olisi 'Customer object 1' jne, nyt vain 'Customer xx'.

![image](https://github.com/user-attachments/assets/999a7e9e-1834-4520-a2c4-c574d83a27bf)
 
Tein migraatiot, jotta muutokset tulisivat voimaan. `./manage.py makemigrations` ja `./manage.py migrate`.

![image](https://github.com/user-attachments/assets/1a15f392-8cad-4224-97c5-ff96dddfa0e7)
 
Rekisteröin uuden tietokannan admin/-tiedostoon, jotta se tulisi näkyviin hallintapaneeliin. `micro crm/admin.py`.

![image](https://github.com/user-attachments/assets/914a4f9c-c0a0-470e-8d18-753258cba527)

Käynnistin testipalvelimen (`./manage.py runserver`) ja kirjauduin sisään hallintapaneeliin (127.0.0.1:8000/admin). Loin kaksi asiakasta.

![image](https://github.com/user-attachments/assets/56e2caab-fd8f-48cd-8427-32700f48713f)
 
![image](https://github.com/user-attachments/assets/f10e43cd-3525-4e9b-9b17-9503d3923778)

Testiympärisössä oli nyt asennettuna asiakastietokanta, web admin -hallintanäkymä sekä lisättynä muutama käyttäjä.

## b) Djangon tuotantotyyppinen asennus

_Tee Djangon tuotantotyyppinen asennus_
- _Voit halutessasi tehdä asennuksen omalle, paikalliselle virtuaalikoneelle. Sen ei tarvitse näkyä Internetiin._
- _Karvinen 2021: Deploy Django 4 - Production Install](https://terokarvinen.com/2022/deploy-django/)_

Testiasennuksen tultua valmiiksi, aloin työstämään Djangon tuotantotyyppistä asennusta. Tämän olisi voinut tehdä pilvi-Debianissa näkyville internetiin (virtual private server), mutta päätin kokeilla asennusta virtuaali-Debianissani localhostina.

Navigoin kotihakemistooni ja loin uuden hakemiston ` mkdir -p publicwsgi/project1/static/` sekä sille hieman testisisältöä.

![image](https://github.com/user-attachments/assets/2b920671-f34e-42c7-b8e9-3559840369d9)
 
![image](https://github.com/user-attachments/assets/f9328671-54ce-4747-97e9-2ee2b8e75c79)

Komennolla `sudoedit /etc/apache2/sites-available/project1.conf` määritin uuden virtuaali-isännän.

![image](https://github.com/user-attachments/assets/fd181f56-4f08-4b36-ac7f-1a2f9e6ff3ad)
 
Komento `sudo a2ensite project1.conf` ottaa käyttöön project1.conf -tiedoston määrittelyt. 
`sudo a2dissite 000-default.conf` poistaa käytöstä oletuskonfiguraatiot.
`/sbin/apache2ctl configtest` testaa, että määritykset ovat oikein. Virheilmoitus ei haittaa jos lopussa on ilmoitus "Syntax OK".
`sudo systemctl restart apache2` käynnistää palvelimen uudestaan. 
`curl http://localhost/static/` tulostaa aiemmin määritellyn sivun sisällön.

![image](https://github.com/user-attachments/assets/3667eeb7-d0e0-4f5d-8473-9ccf65d365a1)
 
![image](https://github.com/user-attachments/assets/a8bbeec0-72f0-4862-a0ac-d507c7cd948e)

Sivu lähti pyörimään muutaman uudelleenkäynnistyksen jälkeen.

Seuraavaksi hieman dynaamisempaa otetta. Loin uuden virtualenv-ympäristön kansioon publicwsgi.

![image](https://github.com/user-attachments/assets/01d8eef3-f86f-4f6f-8160-22f56951e793)

Asensin ympäristöön Djangon, vastaavasti kuin testipalvelimella.

![image](https://github.com/user-attachments/assets/1efcf96c-3e3d-45a6-8332-8b8d24bb424f)
 
Kopion aiemmin tehdyn projektin testikansiosta tuotantokansioon.

![image](https://github.com/user-attachments/assets/57790d98-6b73-4803-a67b-78240d0570d5)

Seuraavassa vaiheessa yhdistin Apache-palvelimen Python-ohjelmiin (joihin Djangokin lukeutuu). Tämä tehtiin hyödyntämällä Apachen moduulia WSGI (web server gateway interface); komponenttia joka ajaa Pythonia.

Karvisen tuotantotyylisen asennuksen ohjeissa (https://terokarvinen.com/2022/deploy-django/ ) kohdataan tässä kohtaa useita tärkeitä kohtia:

“To set up Apache to serve Python programs, including Django, we need to know three absolute paths:
- Our Django project main dir, the one containing manage.py: "/home/tero/publicwsgi/teroco/" (TDIR variable in config file below)
- Path to wsgi.py: "/home/tero/publicwsgi/teroco/teroco/wsgi.py" (TWSGI)
- Virtualenv site-packages directory: "/home/tero/publicwsgi/env/lib/python3.9/site-packages" (TVENV)

Whenever paths are needed, use `ls` and tab to write the paths on the shell, then copy-paste them to config file. Less typos means less need for debugging.

WSGI module runs code as the user we specify. It will be the same user we used for testing (`whoami`). Because the code gets input from anonymous web users, it makes sense to create a Django user that does not have sudo privileges, i.e. is not a member of sudo group. This is left as an exercise for the reader. Here, the user is "tero" (TUSER below).”

Pohdin, että jos olisin tekemästä asennusta pilvipalvelimelle, ”teroa” vastaavaksi käyttäjäksi olisi varmaankin hyvä asettaa peruskäyttäjä user2. Tässä kohtaa pitäydyin kuitenkin pääkäyttäjässäni nlholm.

Kopioin ym polut talteen sekä konffitiedoston sisällön Karviselta. Muutin tiedostoon omat tietoni.

`sudoedit /etc/apache2/sites-available/project1.conf`

![image](https://github.com/user-attachments/assets/d48bfeca-885b-4fa8-b819-0a2b848015ed)

Asensin Apachen WSGI-moduulin, ajatuksena on opettaa Apachelle, mitä WSGI-komentoni tarkoittavat. `sudo apt-get -y install libapache2-mod-wsgi-py3`.

Tarkistin syntaksin, `/sbin/apache2ctl configtest`.

Lopuksi käynnistin Apachen uudestaan uudella konfiguraatiolla, `sudo systemctl restart apache2`.

![image](https://github.com/user-attachments/assets/7d5dcf0b-a9f5-4156-ab6b-7acba1166cce)
 
Testasin toiminnan, tuotantoversio Djangosta vastasi Apachen kautta localhostista onnistuneesti.

![image](https://github.com/user-attachments/assets/5e80c5c8-7362-4feb-a688-6b786d3c64aa)
 
![image](https://github.com/user-attachments/assets/cc52500a-be2c-4984-aa14-3c909f9ee27b)

Selaimella Djangon tuotantosivu näkyi tosin vasta kun sekä selain että teminaaliohjelma oli suljettu ja käynnistetty kertaalleen uudestaan (toistuva teema selainten kanssa).

Otin Debug-ominaisuuden pois päältä. `cd publicwsgi/project1/ ja `micro project1/settings.py`. 

Tiedostossa muokattiin näitä kahta kohtaa:

![image](https://github.com/user-attachments/assets/61d51b3e-75d4-4838-87cc-e3e7c043cc74)
 
![image](https://github.com/user-attachments/assets/73d1eb77-1829-45b1-90c8-354bc266cfbc)

Tässä Apache käynnistettiin uudelleen. Vähäisempien muutosten jatkoksi olisi riittänyt peruskäyttäjän komento `touch project1/wsgi.py`.

Totesin että käynnistettyäni terminaalin uudelleen, env oli unohtunut. No, ehkä asiasta ei virtuaalikoneella ole suurta haittaa.

![image](https://github.com/user-attachments/assets/1eb200ab-4f9c-4d95-91cc-f0da9e2c7b4f)

Etusivu on nyt odotetusti tyhjä:

![image](https://github.com/user-attachments/assets/119ce1f7-f029-47d2-94c6-493a4bf5b81a)
 
Ja admin-sivu näytti karulta: 

![image](https://github.com/user-attachments/assets/83ea738c-fc38-4a8c-9d98-966186892d2c)
 

Lisäsin tyylitiedostoja: 

`cd`
` cd publicwsgi/project1/`
`micro project1/settings.py`, tähän tiedostoon päivitettiin tiedot 'import os' ja STATIC ROOT:

![image](https://github.com/user-attachments/assets/b8bd163e-b625-4812-bc16-10e61c214a50)

`./manage.py collectstatic` `yes` .

![image](https://github.com/user-attachments/assets/82873e31-fc39-4a97-bccc-109296dc57fa)
 
![image](https://github.com/user-attachments/assets/a17bc211-7735-4915-a882-34206f655e65)

Tyylisivut tulivat käyttöön ja tehtävä valmiiksi.

# Lähteet

Django Software  Foundation. sa. Django makes it easier to build better web apps more quickly and with less code. Luettavissa: https://www.djangoproject.com/ .

Karvinen, T. 2021. Deploy Django 4 - Production Install. Tero Karvinen – Learn Free Software with me. Luettavissa https://terokarvinen.com/2022/deploy-django/ .

Karvinen, T. sa. Django 4 Instant Customer Database Tutorial. Tero Karvinen – Learn Free Software with me. Luettavissa https://terokarvinen.com/2022/django-instant-crm-tutorial/ .

Karvinen, T. 2024. Linux Palvelimet 2024 alkusyksy. Tero Karvinen – Learn Free Software with me. Luettavissa https://terokarvinen.com/linux-palvelimet/ .
