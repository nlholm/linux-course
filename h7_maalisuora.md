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

## a) ”Hei maailma kolmella kielellä” 

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

## c) Vanha arvioitava laboratiorioharjoitus

_Ratkaise vanha arvioitava laboratorioharjoitus soveltuvin osin._

Täydennän tätä tehtävää myöhemmin.

# Lähteet

Karvinen, T. 27.9.2018. Hello World Python3, Bash, C, C++, Go, Lua, Ruby, Java – Programming Languages on Ubuntu 18.04. Tero Karvinen – Learn Free Software with me. Luettavissa: https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/

Karvinen, T. 2024. Linux Palvelimet 2024 alkusyksy. Tero Karvinen – Learn Free Software with me. Luettavissa https://terokarvinen.com/linux-palvelimet/ .

Karvinen, T. 4.12.2007. Shell Scripting. Tero Karvinen – Learn Free Software with me. Luettavissa: https://terokarvinen.com/2007/12/04/shell-scripting-4/ .
