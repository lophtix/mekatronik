# Programmera LEGO Mindstomrms EV3 med Python via webbläsare

Denna guide visar (när den blir klar) hur flera i en grupp (familj, förening, skolklass etc) kan programmera och turas om att köra program på samma EV3-robot. 

## I korthet

### Internet- och hårdvarukrav
* EV3-roboten behöver tillgång till internet antingen via bluetooth eller USB-sladd (genom en lämplig dator eller mobiltelefon) eller via wifi (genom att man stoppar in ett lämpligt USB-nätverkskort i USB-porten på EV3). Det går att programmera EV3 utan internettillgång, men inte om man vill följa hur vi gör i denna guide.
* Man behöver ett micro-SD-kort som man förbereder och sedan stoppar in i SD-kortplatsen på EV3.

### Den som förbereder (räcker att en gör)
* Man behöver ladda ner linux-varianten ev3dev på en dator och ladda in det på ett micro-SD-kort som man sedan stoppar in i SD-kortplatsen på EV3.
* För att kunna ställa in saker behöver någon även lära sig lite om Linux och Git samt kunna logga in till EV3 via "SSH"

### De som vill programmera
* De som vill programmera använder sig av versionshanteringssystemet Git för att hålla reda på sina program. Vi visar hur man gör det med "gitlab" via webbläsare (funkar t.ex. även på chromebooks) - Gitlab innehåller även en "editor" där man kan skriva sina program.
* När man vill hämta programmet använder man knapparna och den lilla skärmen på EV3 för att starta ett script som laddar ner senaste versionen av det man programmerat. Sedan använder man knapparna för att starta programmet.

---------------

## Den långa versionen

### Förbereda ev3dev (admin)
Kräver dator med kortläsare m.m.
Fullständiga beskrivningar finns på https://www.ev3dev.org/ (på engelska)
...

### Koppla upp ev3 mot internet (admin)  
ev3 + wifi-USB-nätverkskort eller internetansluten dator/telefon med bluetooth/USB)
Fullständiga beskrivningar finns på https://www.ev3dev.org/ (på engelska)
...

### Skapa gitlab-konto och projekt (alla)
Gå till https://gitlab.com
* Skapa ett eget konto (mitt exempel https://gitlab.com/ErikSundvall)
* Skapa ett projekt (mitt exempel https://gitlab.com/ErikSundvall/ev3dev-test1) kryssa gärna för att du vill att filen readme.md ska skapas.
* Visa adressen som står under "clone via https" för den i er grupp som är "admin" så att hen kan förbereda ett filbibliotek till dig. (Adressen i mitt exempel https://gitlab.com/ErikSundvall/ev3dev-test1.git)
![Skärmdump som visar clone via https](/images/gitlab-clone-1.png)
* Redigera gärna filen readme.md för att testa redigering, skriv t.ex. något om ditt projekt
* Skapa din första python-fil (TODO: berätta hur) Fyll med programkod, t.ex. genom att kopiera in följande
```python
...
```

### Förbereda bibliotek, git och script på ev3 (admin)
* Logga in via ssh till EV3, se till att du står i hembiblioteket för användaren "robot"
* Skapa underbibliotek med samma namn som dina användare och projekt exempelvis `mkdir ErikSundvall`


### Ladda ner och testa ditt program, ändra, ladda ner och testa igen (alla)
* ...

