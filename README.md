# IoT Workshop PXL-Digital Electronic Engineering

![overview banner](/media/banner_IoTWorkshop.png)

Steeds meer dingen – auto’s, deurbellen, rookmelders, koelkasten, noem maar op – zijn via een ‘embedded systeem’ verbonden met het internet. Internet of Things (IoT) noemen we dat. Hoe werken die systemen en wat zijn de elementaire bouwstenen om een volwaardig IoT-device te maken? In deze workshop bouwen we een eerste IoT-device. We bouwen een koppeling tussen sociale media (Discord) en een “thing” met behulp van een Raspberry Pi-computertje verbonden met een temepratuur en luchtvochtigheid sensor, een bewegingssensor en een camera. Dit alles doen we op een laagdrempelige manier. Alles is beschikbaar zodat je thuis - met je eigen Raspberry Pi – het werk kan voortzetten, als je dat wil.

## Deel 1: Installeren en configureren Raspberry PI
Om de Raspberry PI 3 te kunnen gebruiken voor het IOT project moet eerst het Raspberry Pi operating system geïnstaleerd worden (1.1). Daarna moet de wifi op de PI geconfigureerd worden en het IP genoteerd worden zodat vanaf een andere pc ingelogd kan worden op de PI via SSH (1.2). **Als je de workshop volgt tijdens de demo kan je Deel 1 volledig overslaan. Wil je het project bij je thuis nabouwen, dan moet je eerst stap 1.1 doornemen om het project te kunnen opbouwen.**

### 1.1: Installeren Raspberry Pi OS

Om het project te kunnen bouwen moet het Raspberry PI operating system geïnstalleerd worden (op een SD-kaart van minstens 16GB die volledig geformateerd mag worden). **Bij de PI die tijdens de workshop gebruikt wordt is dit reeds uitgevoerd. Om dit thuis ook te kunnen doen moet dit eerst nog op de SD-kaart geïnstalleerd worden.** Via de [Raspberry Pi Imager](https://www.raspberrypi.org/software/) kan het Raspberry PI OS geïnstalleerd op de SD-kaart. 

Raadpleeg voor meer informatie over hoe de image te installeren de [website van Raspberry](https://www.raspberrypi.org/blog/raspberry-pi-imager-imaging-utility/). 

Wanneer je de melding krijgt dat het schrijven van de image succesvol afgerond is mag je de kaart verwijderen uit je PC en in de Raspberry 3 plaatsen. Sluit vervolgens het toetsenbord, muis, camera, HDMI scherm aan.

Stap 1.1 is nu succesvol afgerond. Je kan nu verder gaan met stap 1.2.

### 1.2: Raspberry Pi 3 verbinden met wifi en noteren IP-adres

Start de Raspberry 3 op en klik recht boven op het wifi icoontje (1), controleer vervolgens of de wifi ingeschakeld is (2) en selecteer daarna het gewenste netwerk (3). Er zal nu een melding komen om een wachtwoord in te geven (4). Kies na het ingeven van het wachtwoord ten slotte voor OK (5).

De Raspberry is nu verbonden met het wifi netwerkt en er werd door de router een IP-adres toegewezen aan de Raspberry. Beweeg met de cursor over het wifi icoontje (1), er zal nu een text vlak verschijnen met daarin het IP-adres (2). Noteer dit IP_adres ergens wat je zal het later nodig hebben om via de PC te verbinden met de Raspberry.

Als je de workshop volgt tijdens de demo of als je in Stap1.1 voor een image gekozen hebt mag je nu naar Deel2 gaan. Heb je in Stap1.1 gekozen om met het script te werken, ga dan verder met Stap1.3.

### 1.3: Raspberry Pi 3 Sense Hat
Details over de [Sense Hat](https://www.raspberrypi.com/products/sense-hat/) vindt u op de website. De sense hat is origineel ontworpen voor de [Astro Pi](https://astro-pi.org/) challange op het ISS voor de ESA. De Sense hat is uitgerust met:   
- 8×8 RGB LED matrix
- five-button joystick
- Gyroscope
- Accelerometer
- Magnetometer
- Temperature
- Barometric pressure
- Humidity
- Colour and brightness

Er is een Python3 library beschikbaar voor deze sense hat. Een uitgebreide tutorial vindt u [hier](https://projects.raspberrypi.org/en/projects/getting-started-with-the-sense-hat/).
Zorg ervoor dat deze geïnstalleerd is, dit kan via het volgende command in de terminal:
```bash
sudo apt-get install sense-hat
```

## Deel 2: Aanmaken Discord BOT
Om met de Raspberry te comuniceren moet op het Discord profiel eerst een BOT aangemaakt worden die gebruikt kan worden op de Raspberry PI. Deze moet vervolgens gekopeld worden aan een server. 

Surf naar de [Discord Developer Console](https://discordapp.com/developers/applications/me) en log in met het Discord account waarop de BOT moet werken of maak een nieuw account aan. Kies nu voor New Application (1), geef de applicatie een naam naar keuze (2) en kies voor Create (3).

![Deel2_1](/media/Deel2_1.jpg)

Nu de applicatie aangemaakt is kies je voor Bot (1), dan voor Add Bot (2) en ten slotte voor Yes, do it! (3).

![Deel2_2](/media/Deel2_2.jpg)

Kies de volgende instellingen voor de bot:

![Deel2_2b](/media/Deel2_2b.png)

Nu de bot aangemaakt is kan je de Token kopiëren (1). Bewaar deze ergens want we hebben deze straks nodig om toegang te krijgen tot de bot met de Raspberry PI (sla deze bevoorbeeld op in een text bestand op je pc).

![Deel2_3](/media/Deel2_3.jpg)

Ga nu terug naar Genaral Information (1) en kies voor Copy bij de Client ID (2). 

![Deel2_4](/media/Deel2_4.jpg)

Surf naar https://discordapp.com/oauth2/authorize?client_id=!CLIENTID!&scope=bot&permissions=0 **en vervang !CLIENTID! door jouw client id** (voorbeeld: is je client id 123 dan ziet je link er als volgt uit:  https://discordapp.com/oauth2/authorize?client_id=123&scope=bot&permissions=0). Kies op deze pagina aan welke server de Bot toegevoegd mag worden (1) en kies voor Autoriseren (2). Je moet wel beheersrechten heben tot deze server. (Het beste kan je voor deze test even een [nieuwe server aanmaken](https://support.discord.com/hc/nl/articles/204849977-Hoe-kan-ik-een-server-cre%C3%ABren-) op je [Discord account](https://discord.com/app).)

![Deel2_5](/media/Deel2_5.jpg)

Je moet eventueel nog bevestigen dat je geen Robot bent. Als je dit gedaan hebt zie je normaal op de server nu de Bot staan (ga hiervoor naar je [Discord account](https://discord.com/app)) die je hebt toegevoegd. Het enige wat we nu nog nodig hebben is het channel-ID. Ga hiervoor eerst naar de gebruikersinstellingen (1).

![Deel2_6](/media/Deel2_6.jpg)
  
Scrol nu in de linkerbalk naar beneden en kies voor weergave (1). Activeer nu de ontwikkelaarsmodus (2). Staat je Discord ingesteld in het Engels, kies dan eerst voor Advanced (1) en activeer daarna Developer Mode (2).

![Deel2_7](/media/Deel2_7.jpg)
![Deel2_8](/media/Deel2_8.jpg)

Klik ten slotte rechts op de kanaalnaam (1) en Kopieer ID (2).

![Deel2_9](/media/Deel2_9.jpg)

Bewaar deze ID ergens want we hebben deze straks nodig om te comuniceren met de server vanaf de Raspberry PI (sla deze bevoorbeeld op in een text bestand op je pc). Deel2 is nu volledig afgerond en je kan verder gaan met Deel3.

## Deel 3: Schrijven code
Nu alles ingesteld is kan begonnen worden met het schrijven van de code. Om dit te doen gebruiken we een laptop met daarop de code editor [nothepad++](https://notepad-plus-plus.org/downloads/), [WinSCP](https://winscp.net/eng/download.php) om de code te kunnen bewerken die op de Raspberry geplaatst is en [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) om de commando's door te sturen naar de Raspberry (dan is een scherm, toetsenbord en muis op de Raspberry niet meer nodig). Volg je de workshop van thuis? Installeer de programma's dan door op de namen van de programma's hierboven te klikken. Tijdens de workshop demo zijn de programma's reed geïnstalleerd en kan je dus direct verder gaan.

Wanneer je nu Putty opent kijg je normaal een scherm te zien zoals hieronder weergegeven. Geef eerst het IP-adres in (1). Dit is het adres waarop de Raspberry zit binnen het netwerk. Als je de workshop van thuis volgt is dit het adres wat je onder stap 1.2 genoteerd hebt. Volge je de workshop tijdens de demo? Gebruik dan het IP adres wat tijdens de demo vermeld wordt. Als je dit adres hebt ingegeven kies je voor Open (2).

![Deel3_1](/media/Deel3_1.jpg)

In de terminal zal je nu moeten inloggen. Als je niets aangepast hebt aan de inloggegevens zijn deze standaard als volgt:
- login as: **workshop**
- password: **pxl**

Als je na het inloggen een veiligheidsmeling krijgt, beantwoordt deze dan met "Ja". Als nu onderstaand bericht in de terminal verschijnt ben je succescol ingelogd.
```bash
pi@raspberrypi:~ $
```

Het is nu de bedoeling om de start code de downloaden op de Raspberry zodat hier verder aan gewerkt kan worden. Kopieer het commando hier en plak dit in de de putty terminal (in Putty kan je iets plakken door op je rechter muisknop te klikken).
```bash
wget -q https://raw.github.com/PXLDigital/EAI-Workshop-IoT-met-RPi/main/Code/Workshop.py -O ~/Desktop/IOT_Workshop/Workshop.py
```

Ga nu naar WinSCP en log in met en start een nieuwe sessie (1) en kies voor Nieuwe site (2). Gebruik nu dezelfde inloggegevens als de gegevens om in te loggen op Putty. Plaatst het IP adres (3), de gebruikersnaam (4) en het wachtwoord (5). Kies ten slotte voor inloggen (6).
![Deel3_2](/media/Deel3_2.jpg)

Als je de eerste keer inlogt op de Raspberry zal er een veiligheidsmelding komen. Antwoord hierop met Ja (1).

![Deel3_3](/media/Deel3_3.jpg)

Aan de rechterzijde worden nu de systeemmappen van de Raspberry weergegeven. Navigeer nu naar "/home/pi/Desktop/IOT_Workshop/" (1) en selecteer klik met de rechter muisknop op de file Workshop.py (2). Kies voor Bewerken (3) en Nothepad++(4) (Staat Nothepad++ er niet tussen? Voeg deze dan toe met Configureren.). Nu zal de code openen in Nothepad++ en deze kan nu vanaf hier bewerkt worden.

![Deel3_4](/media/Deel3_4.jpg)

Ga nu in de code opzoek naar de TOKEN (1) en de Channel_ID (2) en pas deze aan door de gegevens die genoteerd zijn tijdens het uitvoeren van Deel 2.  Elke keer dat je iets aanpast in de code moet je deze opslaan in Nothepad++. Als je dit gedaan hebt is de code ook meteen opgeslagen op de 
Raspberry en kan deze hier uitgevoerd worden.

![Deel3_5](/media/Deel3_5.jpg)

Om de code nu uit te voeren gaan we terug naar Putty. In Putty navigeren we naar de IOT_Workshop map met onderstaand commando. (Dit moet enkel gebeuren als Putty opnieuw opgestart is of als je van map verandert bent.)
```bash
cd Desktop/IOT_Workshop/
```

Nu we in de juiste map zitten kunnen we de code als volgt starten:
```bash
python3 Workshop.py
```

Als je nu een melding krijgt in de terminal zoals hieronder is de bot correct gestart.

![Deel3_6](/Documentatie/Afbeeldingen/Deel3_6.jpg)

Probeer nu in je [Discord kanaal](https://discord.com/app) ```?help``` te sturen. Als je nu een info blok als reactie teruggestuurd krijgt is de code succesvol uitgevoerd. Druk nu in putty ```ctrl+c``` in om de code te laten stoppen met uitvoeren.

Alles is nu klaar om verder te programmeren. Lees nu de [wiki pagina's](https://github.com/PXLDigital/EAI-Workshop-IoT-met-RPi/wiki) waar de Workshop opgedeeld is in verschillende deel programmeer opdrachten.

## Referenties
1. „Introducing Raspberry Pi Imager, our new imaging utility” RaspberryPi, 5 Maart 2020. [Online]. Available: https://www.raspberrypi.org/blog/raspberry-pi-imager-imaging-utility. [Geopend 30 Maart 2021].
2. „Python: Create a Discord Bot on Your Raspberry Pi Using Discord.py” The Ginger Ninja, 3 Mei 2017. [Online]. Available: https://www.gngrninja.com/code/2017/3/24/python-create-discord-bot-on-raspberry-pi. [Geopend 28 Februari 2021].
3. „DHT11 Temperature and Humidity Sensor and the Raspberry Pi” The Ginger Ninja, 21 September 2017. [Online]. Available: https://www.raspberrypi-spy.co.uk/2017/09/dht11-temperature-and-humidity-sensor-raspberry-pi. [Geopend 28 Februari 2021].
4. „Getting started with the Camera Module” Projects RaspberryPi. [Online]. Available: https://projects.raspberrypi.org/en/projects/getting-started-with-picamera. [Geopend 10 Maart 2021].
5. „The parent detector” Projects RaspberryPi. [Online]. Available: https://projects.raspberrypi.org/en/projects/parent-detector/3. [Geopend 15 Maart 2021].
6. „Discordpy Readthedoc” Discord. [Online]. Available: https://discordpy.readthedocs.io/en/stable. [Geopend 9 April 2021].


based on: https://github.com/PXLDigital/EAI-Workshop-IoT-met-RPi

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are greatly appreciated. 

Check out our [contributing page](/contributing.md) for how to add issues, features and make pull requests.

## People

- **CONTRI BUTOR1** - _CONTRIBUTOR_ - [CONTRI BUTOR1](https://github.com/CONTRIBUTOR1)
- **Dieter Vanrykel** - _TEACHER_ - [Dieter Vanrykel](https://github.com/Vanrykel)
