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
### 1.4: Python Library voor Discord
Een gedetaileerde uitleg over de library vindt u [hier](https://discordpy.readthedocs.io/en/stable/intro.html#installing)
```bash
pip3 install discord.py
```

## Deel 2: Aanmaken Discord BOT

![Deel2_1](/media/discord-server.jpg)


Om met de Raspberry te comuniceren moet op het Discord profiel eerst een BOT aangemaakt worden die gebruikt kan worden op de Raspberry PI. Deze moet vervolgens gekopeld worden aan een server. 

Surf naar de [Discord Developer Console](https://discordapp.com/developers/applications/me) en log in met het Discord account waarop de BOT moet werken of maak een nieuw account aan. Kies nu voor New Application (1), geef de applicatie een naam naar keuze (2) en kies voor Create (3).

![Deel2_1](/media/Deel2_1.jpg)

Nu de applicatie aangemaakt is kies je voor Bot (1), dan voor Add Bot (2) en ten slotte voor Yes, do it! (3).

![Deel2_2](/media/Deel2_2.jpg)

Kies de volgende instellingen voor de bot:

![Deel2_2b](/media/Deel2_2b.png)

Nu de bot aangemaakt is kan je de Token kopiëren (1). Bewaar deze ergens want we hebben deze straks nodig om toegang te krijgen tot de bot met de Raspberry PI (sla deze bevoorbeeld op in een text bestand op je pc).

![Deel2_3](/media/Deel2_3.jpg)

Ga nu terug naar Genaral Information (1) en kies voor Copy bij de APPLICATION ID (2). 

![Deel2_4](/media/deel2_4_update23.png)

Surf naar:<br /> https://discordapp.com/oauth2/authorize?client_id=!APPLICATIONID!&scope=bot&permissions=0 <br />**en vervang !APPLICATIONID! door jouw APPLICATION ID** <br />(voorbeeld: is je APPLICATION ID 123 dan ziet je link er als volgt uit:<br />  https://discordapp.com/oauth2/authorize?client_id=123&scope=bot&permissions=0).<br /> Kies op deze pagina aan welke server de Bot toegevoegd mag worden (1) en kies voor Autoriseren (2). Je moet wel beheersrechten heben tot deze server. (Het beste kan je voor deze test even een [nieuwe server aanmaken](https://support.discord.com/hc/nl/articles/204849977-Hoe-kan-ik-een-server-cre%C3%ABren-) op je [Discord account](https://discord.com/app).)

![Deel2_5](/media/Deel2_5.jpg)

Je moet eventueel nog bevestigen dat je geen Robot bent. Als je dit gedaan hebt zie je normaal op de server nu de Bot staan (ga hiervoor naar je [Discord account](https://discord.com/app)) die je hebt toegevoegd. Het enige wat we nu nog nodig hebben is het channel-ID. Ga hiervoor eerst naar de gebruikersinstellingen (1).

![Deel2_6](/media/Deel2_6.jpg)
  
Scrol nu in de linkerbalk naar beneden en kies voor weergave (1). Activeer nu de ontwikkelaarsmodus (2). Staat je Discord ingesteld in het Engels, kies dan eerst voor Advanced (1) en activeer daarna Developer Mode (2).

![Deel2_8](/media/Deel2_8.jpg)

Klik ten slotte rechts op de kanaalnaam (1) en Kopieer ID (2).

![Deel2_9](/media/Deel2_9.jpg)

Bewaar deze ID ergens want we hebben deze straks nodig om te comuniceren met de server vanaf de Raspberry PI (sla deze bevoorbeeld op in een text bestand op je pc). Deel2 is nu volledig afgerond en je kan verder gaan met Deel3.

## Deel 3: Schrijven code 'Hello World'
Nu alles ingesteld is kan begonnen worden met het schrijven van de code.

- login as: **workshop**
- password: **pxl**

***Python editor***

![Thonny](/media/thonny_ide_start.png)

***Start code***
```
from sense_hat import SenseHat
import discord
from discord.ext import commands

TOKEN = 'token'
CHANNEL_ID = ch_id
intents = discord.Intents.all()

sense = SenseHat()

#Toegang token voor discord server
description = '''IOT Workshop - Discord Bot'''
bot = commands.Bot(command_prefix='?', intents = intents)

@bot.event
async def on_ready():
    print('Bot opgestart en ingelogd als:')
    print(bot.user.name)
    print(bot.user.id)
    print('------')

@bot.command()
async def hello(ctx):
    await ctx.send("hello world")

bot.run(TOKEN)
```

## Deel 4: Schrijven code 'Opdrachten'

### Opdracht 1: tekst afspelen op de RGB matrix
Met deze code toon je 'hello world' op de rgb matrix, voeg ze toen aan de code zodat je dit kan tonen via het discord commando '?hello'.

```
sense.show_message("Hello world")
```

### Opdracht 2: Voeg een nieuw commando toe om de temperatuur uit te lezen.
Maak een nieuw commando ?temp aan dat de temperatuur terug weergeeft:
```
temp = sense.get_temperature()
await ctx.send(temp)
```

### Opdracht 3: maak een nieuw commando om de omgevingssensoren uit te lezen.

De onderstaande code leeste de sensoren:
```
temp = sense.get_temperature()
hum = sense.get_humidity() 
pres = sense.get_pressure() 
```

Dit zou het resultaat moeten zijn:
![Opdracht 3](/media/Opdracht3.png)


- 8×8 RGB LED matrix
- five-button joystick
- Gyroscope
- Accelerometer
- Magnetometer
- Temperature
- Barometric pressure
- Humidity
- Colour and brightness

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
