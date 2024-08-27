Tässä [Linux Palvelimet 2024 alkusyksy](https://terokarvinen.com/linux-palvelimet/) -kurssin ensimmäisessä tehtävässä opiskelin hieman raportin kirjoittamista sekä vapaiden ohjelmistojen pääpiirteitä. Varsinaisena tehtävänä asensin Linux-virtuaalikoneen virtuaaliboksiin. Tein tehtävän maanantaina 26.8.2024. Aloitin klo 21, ja valmista tuli n. klo 24.

# Tehtävä 1: Oma Linux

## Lue ja tiivistä

### Tero Karvinen: Raportin kirjoittaminen 

Tero Karvisen Raportin kirjoittaminen -artikkelissa käsitellään tieteellisen kirjoittamisen perusteita. Karvinen kehottaa kirjoittamaan harjoitustöiden raportit niin, että ne ovat täsmällisiä ja helppolukuisia. Lähdeviitteiden on syytä löytyä, ja tulosten on oltava toistettavissa. Pahoina virheinä mainitaan muun muassa sepittäminen ja plagiointi.

Itseäni ohjeistuksessa yllätti sen yksityiskohtaisuus: eteneminen tehtävissä saattaa Karvisen mukaan olla tarpeen merkitä kellonajan tarkkuudella. En koe ehkä aivan näin suurta tarkkuutta tarpeellisena, mutta erityisesti virhetilanteet on toki syytä dokumentoida huolella. 

### Free Software Foundation: What is Free Software?

Free Software Foundation toteaa vapaista ohjelmistoista (engl. free software) seuraavaa:

 > Free software” means software that respects users' freedom and community. Roughly, it means that the users have the freedom to run, copy, distribute, study, change and improve the software. Thus, “free software” is a matter of liberty, not price.

Toisin sanoen vapaissa ohjelmistoissa keskeistä on käyttäjien oikeus a) käyttää, b) tutkia, muokata ja c) jakaa sekä d) uudelleenjakaa tai levittää (muokattua) ohjelmistoa haluamillaan tavoilla. Vapaa pääsy ohjelman lähdekoodiin on edellytys oikeuksien toteutumiselle.

Vapaat ohjelmistot voivat olla myös kaupallisia, edellyttäen että niihin liittyvät edellä mainitut neljä perusoikeutta toteutuvat.

## Asenna Linux virtuaalikoneeseen

Valmistauduin Linux-koneen asentamiseen perustamalla [GitHub-tilin](https://github.com/)  sekä opiskelemalla MarkDown-ohjelmointikielen perusteita. Totesin GitHubin artikkelin [Basic writing and formatting syntax](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax) varsin toimivaksi pikakurssiksi aiheeseen.

Seuraavaksi asensin [VirtualBoxin](https://www.virtualbox.org/wiki/Downloads), jota PC:lläni ei ollut ennestään. Käytössäni on Windows 11 Home -käyttöjärjestelmällä varustettu jokusen vuoden vanha HP:n PC, jossa on 16 GB RAMia, 450 GB SSD-levytilaa ja prosessorina AMD Ryzen 7 3700U with Radeon Vega Mobile Gfx  2.30 GHz.

Am ilmoitus hieman hämmensi, mutta päätin palata asiaan tarvittaessa myöhemmin.

![image](https://github.com/user-attachments/assets/82d1d60d-e039-4a10-9626-e19c2c6d32cd)

VirtualBox tuli asennettua onnistuneesti.

![image](https://github.com/user-attachments/assets/0dc3160a-3597-4420-bf6e-dd798fde7955)

VirtualBoxin asennuksen jälkeen siirryin asentamaan Linuxin Debian-levityspakettia (distroa). Käytin hyväkseni Karvisen kattavaa ohjetta [Install Debian on Virtualbox](https://terokarvinen.com/2021/install-debian-on-virtualbox/), jonka luin kokonaisuudessaan ennen etenemistä.

Latasin levykuvan debian-live-12.6.0-amd64-xfce.iso koneelleni Karvisen ohjeiden mukaan, osoitteesta https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/ . Lataus kesti viitisen minuuttia. Pistin muistiin Karvisen huomiot sopivasta kuvasta:

> The correct image is
> - live - Can boot from image and use Linux even without installing. Some Linux distributions call live images desktop images.
> - 12.x.x - The distribution version, which locks major versions of most software, while providing security updates.
> - amd64 - Most regular desktops, laptops and servers are amd64. Also Intel processors use amd64 architecture.
> - xfce - my favourite desktop environment. Obvious and simple, but also easy to configure if you want. The other ones work fine, too.

Levykuvan latauduttua käynnistin VirtualBoxin, ja aloin asentamaan uutta virtuaali-Linuxiani.

Asennustapa oli hieman muuttunut Karvisen ohjeen päivittämisen jälkeen, ’Skip unattended Installation’ ei pystynyt valitsemaan. Valitsin kuitenkin Expert Mode.

![image](https://github.com/user-attachments/assets/8458b192-eaf4-4bf5-9ad1-ebde4716f78a)
 
![image](https://github.com/user-attachments/assets/c7281cba-a622-41c6-8e2c-90cdd0304990)

![image](https://github.com/user-attachments/assets/24ced394-ae97-48cb-81e8-656ec72652e9)
 
Lisäsin RAMia ja CPU:ita (aloitusarvo oli 1).

![image](https://github.com/user-attachments/assets/e93dddb3-4443-4ed5-bdfb-5e873c9b203b)
 
Toisin kuin ohjeissa, vaihtoehtoa ’Storage on physical hard disk: Dynamically allocated’ ei ollut saatavilla, mutta oletin että jättämällä vaihtoehdon ’Pre-allocate Full Size’ tyhjäksi, asia tulee hoidettua.

![image](https://github.com/user-attachments/assets/890a40b7-e81b-4b67-ab17-903fed1e0c59)

![image](https://github.com/user-attachments/assets/7ad38d44-b903-4583-8d40-f5f8c1f6ece0)
 
Seuraavaksi aloin asentamaan käyttöjärjestelmää virtuaalikoneeseen. Asensin virtuaalisen CDROMin jossa on  levykuva, ja buuttasin Debian-koneen tuplaklikkaamalla konetta.

![image](https://github.com/user-attachments/assets/07f0ac53-8013-4a9f-ae9f-2ad7959d59d6)
 
![image](https://github.com/user-attachments/assets/df6a4ce4-9ff9-42ae-a7d0-2f278dca3e51)

Testasin konetta avaamalla nettiselaimen.

![image](https://github.com/user-attachments/assets/883e801b-95ec-4a2b-924d-ea9c6d6585ea)

Seuraavaksi käynnistin Debianin asennusohjelman. Tein määritykset Karvisen ohjeiden mukaan.

![image](https://github.com/user-attachments/assets/898332c2-c5c1-4962-9ad6-1bc1edcca02e)

![image](https://github.com/user-attachments/assets/8fda7a9f-4338-4275-9cb7-47469266709e)

Asennus kesti noin varttitunnin. Sen päätyttyä yritin kirjautua sisään, mutta järjestelmä väitti salasanan olevan väärä. Uudelleenkäynnistin, ja tällä kertaa järjestelmä antoi kirjautua.

![image](https://github.com/user-attachments/assets/61baae89-01ba-4a53-9a9c-78687cdcd062)

![image](https://github.com/user-attachments/assets/297feb61-d25e-458f-92dc-aa3ca1be2d81)

Kokeilin taas nettiä, toimi. 

Seuraavaksi avasin terminaali-emulaattorin ja tein päivitykset Karvisen ohjeiden mukaan, sekä asensin palomuurin.

>$ sudo apt-get -y dist-upgrade

>Upgrade everything. Everything? Latest versions for this Debian? Security updates? Command line apps? Desktop apps? Servers? Yes.

![image](https://github.com/user-attachments/assets/8460f68d-573b-485b-af6b-c54de76cdec9)
 
![image](https://github.com/user-attachments/assets/2e35ea4f-81e5-4bb1-9875-0a4450d0611b)

Päivitysten ja palomuurin asentamisen jälkeen lisäsin VirtualBox Guest Additions -lisiä, joilla virtuaali-Debianin käytöstä saadaan hieman mukavampaa.

Virtuaalikoneen työpöytä alkoi näkymään.

Lopuksi tallensin työn tulokset (VirtualBox, Machine, Take Snapshot). 

Virtuaali-Debianin asennukseen esitöineen kului ensikertalaiselta noin kolme tuntia (kirjoitin raporttia samanaikaisesti).

![image](https://github.com/user-attachments/assets/b9ad9f7a-6cf6-4561-b7aa-ba0952d21033)

## Suosikkiohjelmani Linuxilla

Uutena Linux-käyttäjänä minulle ei ole ehtinyt kertyä suosikkiohjelmia, mutta pidän taulukkolaskennasta, joten kokeilin LibreOffice Calcia. Alla kuvakaappaus kaavalla lasketusta laskutoimenpiteestä 1+1. Kaava toimi vastaavasti kuin Excelissä. 

![image](https://github.com/user-attachments/assets/f0b4d0a6-36f7-4c25-8a12-04ed3ca3cedc)

## Lähteet

Free Software Foundation, Inc. 1.1.2024. What is Free Software? Luettavissa: https://www.gnu.org/philosophy/free-sw.html . Luettu: 26.8.2024

GitHub Inc. 2024. Basic writing and formatting syntax. Luettavissa: https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax . Luettu 26.8.2024

Karvinen, T. 2023. Install Debian on Virtualbox - Updated 2023. Tero Karvinen – Learn Free Software with me. Luettavissa: https://terokarvinen.com/2021/install-debian-on-virtualbox/ . Luettu: 26.8.2024

Karvinen, T. 2024. Linux Palvelimet 2024 alkusyksy. Tero Karvinen – Learn Free Software with me. Luettavissa https://terokarvinen.com/linux-palvelimet/  . Luettu: 26.8.2024

Karvinen, T. 4.6.2006. Raportin kirjoittaminen. Tero Karvinen – Learn Free Software with me. Luettavissa: https://terokarvinen.com/2006/raportin-kirjoittaminen-4/ . Luettu: 26.8.2024

Oracle. 2024. VirtualBox. Luettavissa: https://www.virtualbox.org/wiki/Downloads . Luettu 26.8.2024
