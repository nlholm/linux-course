# h2 Komentaja Pingviini

[Linux Palvelimet 2024 alkusyksy](https://terokarvinen.com/linux-palvelimet/) -kurssin toisessa tehtävässä opiskelin komentokehotteiden käyttöä sekä paketinhallintaa. Olin uuden äärellä, sillä ennen tätä viikkoa en ollut käyttänyt komentoriviä tai terminaali-emulaattoreita juuri ollenkaan.

Aloitin tehtävän tekemisen perjantaina 30.8.2024, ja jatkoin lauantaina 31.8.2024.

## Laitteisto

### Host

Käytössäni on Windows 11 Home -käyttöjärjestelmällä varustettu jokusen vuoden vanha HP:n kannettava kone, jonka tiedot ovat seuraavat: 

- HP:n kannettava Envy x360
- 64-bittinen käyttöjärjestelmä: Windows 11 Home Edition
- CPU ja näytönohjain: AMD Ryzen 7 3700U with Radeon Vega Mobile Gfx 2.30 GHz (4 ydintä, 8 säiettä)
- RAM: 16,0 GB (13,9 GB käytettävissä)
- Levytila: 476 GB SSD, vapaana 202 GB

### Guest

- Virtualisointiympäristönä Oracle VM VirtualBox 7.0.20
- Virtuaalikoneena Debian GNU/Linux 12.6.0 (”Bookworkm”)
- Muisti: 4000 MB

## x) Lue ja tiivistä

Karvisen artikkeli [Command Line Basics Revisited]( https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited) on hyvä ja tiivis esitys tärkeimpiin komentokehotteisiin sekä paketinhallintaan. Artikkelissa komentokehotteet on jaoteltu alaryhmiin kuten liikkuminen, tiedostojen käsittely, avut, historia, SSH. Myös tärkeimmistä hakemistoista puhutaan. Lisäksi Karvinen käsittelee paketinhallintaa ja sen tarjoamia mahdollisuuksia, kuten sovellusten asentamista.

Harjoittelin komentojen käyttöä virtuaali-Debianillani. Lisäksi opiskelin hieman lisää perusteita sivustoilta [LinuxCommand.org](https://www.linuxcommand.org/index.php) sekä [Komentorivin perusteet](https://www.linux.fi/wiki/Komentorivin_perusteet).

Totesin, että tulee kulumaan hetki, ennen kuin olen sujut komentokehotteiden kanssa. Esimerkiksi absoluuttiset ja suhteelliset kansioviittaukset eivät tahtoneet mennä kerralla oikein.

![image](https://github.com/user-attachments/assets/638abaee-9551-4f8a-993b-8e59286e5816)

## a) Micro 

_Asenna micro-editori_

Suoritin ensin `apt-get update`, mutta ajo tuntui jäävän kesken. Aloin asentamaan seuraavaksi micro-editoria suorittamalla ensin `apt-cache search micro`ja ajamalla sitten `apt-get -y install micro`. Haku tuntui tässä yhteydessä varsin tyhjänpäiväiseltä, vaikka kokeilin putkittaa lessillä; en ymmärtänyt, mitä olin etsimässä.

Haku:

![image](https://github.com/user-attachments/assets/aaa7d508-cbff-4e13-8bdd-516b68040a67)

Asennus:

![image](https://github.com/user-attachments/assets/f2fdf503-2aec-4429-b31b-b53a3bb4e8ca)
 
Ensimmäinen yritys ei näyttänyt onnistuvan:

![image](https://github.com/user-attachments/assets/b3050cf6-ed8e-4f6f-9c68-b10b20d1911e)

Ajoin apt-get update loppuun ensi, ja kokeilin uudestaan, nyt asennus näytti onnistuvan:

![image](https://github.com/user-attachments/assets/33aed7fc-1779-434d-9e4d-1f4f8fbb52c9)
 
## b) Apt

_Asenna kolme itsellesi uutta komentoriviohjelmaa. Kokeile kutakin ohjelmaa sen pääasiallisessa käyttötarkoituksessa. Ota ruutukaappaus. Kaikki terminaaliohjelmat kelpaavat, TUI (text user interface) ja CLI (command line interface). Osaatko tehdä apt-get komennon, joka asentaa nämä kolme ohjelmaa kerralla?_

Tämän osatehtävän edessä olin hieman hämmentynyt. Mistä tiedän, mitä ohjelmia Linuxilleni on jo asennettu? Selailu /bin-hakemistossa ei juuri auttanut. Löysin graafisesta kansionäkymästä (File System) kyllä äsken asennetun micro-editorin, mutta komentoliittymän käskystä `apt-cache search micro `en ymmärtänyt juuri mitään. 

Googlailin hieman mahdollisia komentoriviohjelmia. Niitä esiteltiinkin erilaisilla sivustoilla, mutta päätin asentaa hyötyohjelmien sijaan hupia: cowsay, fortune ja nsnake. Kokeilin asentaa ohjelmat yhdellä käskyllä 

```
sudo apt-get -y install cowsay fortune nsnake
````

![image](https://github.com/user-attachments/assets/f631f655-f748-4212-bfe9-cca12d6e28d8)
 
![image](https://github.com/user-attachments/assets/9e66167f-2f38-4a56-bb12-0bcadfd783ff)

Cowsay taisi olla jo asennettuna, mutta toimii:

![image](https://github.com/user-attachments/assets/bc0d7a2e-ddd5-4fff-aa08-16f9bc35a55e)

Fortune toimii, mutta puhuu italiaa…

![image](https://github.com/user-attachments/assets/341af56f-e8ff-4a7c-bced-124d9bc8664d)

Matopelikin toimii:

![image](https://github.com/user-attachments/assets/d0a8aef1-9155-459c-b7eb-4b3b11b17c24)
 
## c) FHS

_Esittele kansiot, jotka on listattu "Command Line Basics Revisited" kappaleessa "Important directories". Näytä kuvaava esimerkki kunkin tärkeän kansion sisältämästä tiedostosta tai kansiosta. Jos kyseessä on tiedosto, näytä siitä kuvaava esimerkkirivi. Työskentele komentokehotteessa ja näytä komennot, joilla etsit esimerkit._

Karvisen [Command Line Basics]( https://terokarvinen.com/2020/command-line-basics-revisited/) -artikkelissa kerrotaan seuraavista olennaisista kansioista.

![image](https://github.com/user-attachments/assets/19e4683e-3c8d-448f-9daf-a6fdf9fbe43a)

Tutkin kansioita komentokehotteessa lähtemällä liikkeelle juuresta.

### l eli juuri

![image](https://github.com/user-attachments/assets/e04dc073-fcfa-4bc4-b82a-6172c10ce1c3)

Kaikki alakansiot sijaitsevat juuren alla.

### /home/

![image](https://github.com/user-attachments/assets/8baf7d37-9989-47c7-b46f-33d36abf0103)

Linuxillani on vain yksi käyttäjä, joten /home/:n alla on vai yksi alakansio, nlholm.

### /home/nlholm/

![image](https://github.com/user-attachments/assets/147fe0eb-b332-41ef-8eaf-cff2c5a7ebbc)

Kotikansiostani löytyvät yllä listatut alakansiot.

### /etc/

![image](https://github.com/user-attachments/assets/6200e717-cdbe-403a-bba0-8d063eabe99d)
 
![image](https://github.com/user-attachments/assets/034ff58f-f527-47ec-85c5-f55328e82fa2)

/etc/-kansio on varsin täynnä tavaraa. Ei ihme, koska tänne kuuluvat järjestelmätiedostot.

Tutkin saisinko modules-tiedoston näkymään:

![image](https://github.com/user-attachments/assets/d1d52897-757e-4b1b-8225-12d59098c8f4)
 
### /media/

![image](https://github.com/user-attachments/assets/2e4f149b-9e0b-471f-9c40-c1adef576d2b)

Media-kansiossa näkyy siirrettävä media, kuten esim. USB-tikku, joten se on nyt tyhjä.

### /var/log/

![image](https://github.com/user-attachments/assets/18e8f13d-6554-4928-83fb-afbce07a139a)

/var/log/-kansioon tulee lokitiedostoja. 

![image](https://github.com/user-attachments/assets/2b4d44cc-1348-433b-acb1-929e6cd7cc7d)

Boot.log-tiedostoa en päässyt äkkiseltään lukemaan, mutta kokeilin README-tiedostoa.

Kokeilin ehdotettua journalctl-komentoa, mutta kovin paljoa en tulostuksesta ymmärtänyt.

![image](https://github.com/user-attachments/assets/b6c4acd3-cc83-40c7-80cd-928a523f13e4)

## d) The Friendly M 

_Näytä 2-3 kuvaavaa esimerkkiä grep-komennon käytöstä. Ohjeita löytyy 'man grep' ja tietysti verkosta._

[Digital Ocean](https://www.digitalocean.com/community/tutorials/grep-command-in-linux-unix) -sivusto kertoo, että ”Grep, short for “global regular expression print”, is a command used for searching and matching text patterns in files contained in the regular expressions.” Tutustuin komentoon ym sivustolla, sekä lukemalla artikkelin https://www.geeksforgeeks.org/grep-command-in-unixlinux/ . 

Seuraavaksi kokeilin komennon käyttöä muutamalla komennolla.

![image](https://github.com/user-attachments/assets/23e99e0e-d5c3-4cc9-97bf-4e0fe37f8543)

Yritin etsiä matopelin sijainnin:

![image](https://github.com/user-attachments/assets/4b12ce07-ce00-46d8-a387-d61ae3130578)
 
![image](https://github.com/user-attachments/assets/dc09af80-4407-4fff-821e-f4d7b3e7f870)

Eipä löytynyt.

Kokeilin etsiä tekstinpätkää esimerkkitiedostosta (ilman case sensitiivisyyttä, -i):

![image](https://github.com/user-attachments/assets/7b194b89-4ab3-45d1-8b1c-64d5d297e388)

Tämä onnistui.

## e) Pipe 

_Näytä esimerkki putkista (pipes, "|")._

Putkitin lehmän puhumaan ikivihreitä italiaksi:

![image](https://github.com/user-attachments/assets/ff79c8b4-9bd9-46b8-b3d6-0d1e472e20aa)

## f) Rauta 

_Listaa testaamasi koneen rauta (‘sudo lshw -short -sanitize’). Asenna lshw tarvittaessa. Selitä ja analysoi listaus._

Asensin lshw:n ja listasin koneeni raudan.

![image](https://github.com/user-attachments/assets/2646b844-0baa-4f12-aac4-f8bb9ebec5e8)
 
![image](https://github.com/user-attachments/assets/b789f483-b3d1-4486-8744-9556e29fa926)

Raudasta voidaan tehdä muun muassa seuraavia huomioita: Järjestelmää ajetaan VirtualBoxissa. Muistia on 4 GB (kuten konetta asennettaessa määrittelin), tallennustilaa 32  GB, ja prosessorina toimii host OS:än AMZ  Ryden 7 3700U.

## Lähteet 

Digital Ocean. 3.8.2022. Grep Command in Linux/UNIX. Luettavissa: https://www.digitalocean.com/community/tutorials/grep-command-in-linux-unix .

Geeks for geeks. 12.7.2024. grep command in Unix/Linux. Luettavissa: https://www.geeksforgeeks.org/grep-command-in-unixlinux/ . 

Karvinen, T. 3.2.2020. Command Line Basics Revisited. Tero Karvinen – Learn Free Software with me. Luettavissa: https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited . 

Karvinen, T. 2024. Linux Palvelimet 2024 alkusyksy. Tero Karvinen – Learn Free Software with me. Luettavissa https://terokarvinen.com/linux-palvelimet/  .

Linux.fi. 2022. Komentorivin perusteet. Luetttavissa: https://www.linux.fi/wiki/Komentorivin_perusteet .

Shotts, W.E. s.a. Learning the Shell. LinuxCommand.org. Luettavissa: https://www.linuxcommand.org/lc3_learning_the_shell.php .
