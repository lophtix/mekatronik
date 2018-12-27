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
Den här biten kan vara krånglig första gångerna man försöker, så detta görs lämpligast i lugn och ro i god tid innan någon ivrigt vill kasta sig över robotprogrammering...

Målet i den här beskrivningen är ju att många ska kunna programmera roboten från sina egna datorer och att man som "admin" inte ska behövas när man väl riggat upp användare+projektinställningar. Därför vill vi att EV3 själv ska kunna ta sig ut på internet och hämta ner användarnasn nya/ändrade program. 

* Följ beskrivningarna länkade på https://www.ev3dev.org/docs/networking/ (på engelska), de bör vara tillräckliga för att få kontakt mellan EV3 och din admin-dator med någon metod...
* Nu bör det gå att med beskrivningen på https://www.ev3dev.org/docs/tutorials/connecting-to-ev3dev-with-ssh/ ansluta med SSH till din EV3... 
   * Om det inte funkar att med SSH ansluta till namnet ev3dev som i de ovan länkade instruktionerna, pröva då 
   istället med IP-adressen som man kan hitta via knappar+skärm på EV3 under: Wireless and networks > 
   All Network Connections > {välj din anslutning} > IPv4
* Kontrollera (via din SSH-session) om EV3 kommer åt internetadresser t.ex. genom att pinga www.sunet.se  eller någon ip-adress, t.ex. googles nameserver på 8.8.8.8 kolla även att du kan nå gitlabs webisdor, när vi körde `curl https://gitlab.com/` såg det ut så här:
```
robot@ev3dev:~$ curl https://gitlab.com/
<html><body>You are being <a href="https://about.gitlab.com/">redirected</a>.</body></html>robot@ev3dev:~$ 
```
   * Om det går fint att nå fram så är detta admin-steg klart och du kan gå vidare till nästa avsnitt
   * Om det _inte_ funkade får du läsa vidare och ta fram tyngre verktyg:

Vi har haft problem med att (t.ex. via EV3s skärm+knappar) ställa in vissa nätverk på ett sätt så att man kommer åt internet _från_ EV3.  Man kan ibland komma åt EV3 via SSH frpån sin USB-sladds-anslutna eller bluetooth-anslutna dator men EV3 kanske ändå inte komemr åt DNS och internet. Då kan man göra vidare inställningar beskrivna på https://www.ev3dev.org/docs/tutorials/setting-up-wifi-using-the-command-line/

Programemt "ifconfig" som vanligen finns på linux, finns inte på EV3, därför används kommandot `connmanctl` istället. Mer info om det connmanctl finns på t.ex. https://wiki.archlinux.org/index.php/ConnMan - där finns bl.a. tips om man har problem att ansluta till Eduroam som finns på många skolor, universitet m.m.) Om man exempelvis tröttnar på att försöka knappa in wifi-lösenord etc via knapparna på EV3 så kan man via SSH skapa/redigera en config-fil med nätverksuppgifter:
* gå till rätt bibliotek med `cd /var/lib/connman/`
* För hemmanätverket skapade jag där en fil `sudo nano hemma.config` med följamnde innehåll (byt till rätt nätverksanamn och lösen på de didts två raderna)
```
[service_home_wifi]
Type = wifi
Name = bahnhof2_4Ghz-123456
Passphrase = yourWifiPasswordGoesHere
```

Lite nätverksverktyg att använda via SSH:
* Kommandot `hostname -I` visar EV3s adresser, i mitt fall fick jag svaret `192.168.1.10 169.254.192.141` när det kördes. Första adressen i detta fall var adressen EV3 fått via wifi (usb-wifi-nätverkskortet) andra adressen var den adress som min windows-dator tilldelat EV3 via bluetooth.
* Vill man se vilken adress datorer ute på internet tyckar att man har så kan man använda `curl ifconfig.me`. Sitter du på ett hemmanät eller liknande som gömmer din EV3 bakom sig så är detta troligen din routers adress ut mot internet

Innan du går vidare ska du ha fått `curl https://gitlab.com/` att funka som beskrivet ovan.

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
*

Så här såg den första hämtningen ut när projektet /ErikSundvall/ev3dev-test1 var "privat" så att inmatninga v användarnamn+lösenord krävdes:

```bash
robot@ev3dev:~$ cd
robot@ev3dev:~$ pwd
/home/robot
robot@ev3dev:~$ ls
ErikSundvall
robot@ev3dev:~$ cd ErikSundvall/
robot@ev3dev:~/ErikSundvall$ git clone https://gitlab.com/ErikSundvall/ev3dev-test1.git
Cloning into 'ev3dev-test1'...
Username for 'https://gitlab.com': ErikSundvall
Password for 'https://ErikSundvall@gitlab.com':
remote: Enumerating objects: 14, done.
remote: Counting objects: 100% (14/14), done.
remote: Compressing objects: 100% (8/8), done.
remote: Total 14 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (14/14), done.
robot@ev3dev:~/ErikSundvall$ ls
ev3dev-test1
robot@ev3dev:~/ErikSundvall$ cd ev3dev-test1/
robot@ev3dev:~/ErikSundvall/ev3dev-test1$ ls
README.md  images
robot@ev3dev:~/ErikSundvall/ev3dev-test1$
```



### Ladda ner och testa ditt program, ändra, ladda ner och testa igen (alla)
* ...

