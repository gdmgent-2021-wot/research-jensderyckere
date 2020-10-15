# Introduction

## Simple code

Code is voor velen een onderwerp waar men bang van word. Het ziet er vrij complex uit maar met ietwat inhoud kan code eenvoudig worden. Het lijkt me dan ook voordehands liggend dat we code gaan **vergelijken met situaties in het werkelijk leven**. Alle begrippen rond code moeten zorgvuldig worden uitgelegd voordat we deze kunnen toepassen. 

Zonder voorkennis is het algemeen duidelijk dat we een **rollercoaster** zullen berijden. In het begin mogen we **geen grootse doelen** stellen. Het begint met simpele dingen. Tictactoe is een voorbeeldje van wat je kan maken in het begin. De nieuwe Facebook lanceren zal nog niet voor direct zijn. Misschien lukt het je wel al binnen een jaar want tenslotte zijn alle grote social media platformen gemaakt in een slaapkamer, kot, …

Programmeren is natuurlijk **niet verbonden tot één medium**. Webdevelopment lijkt de grootste prioriteit te krijgen maar mobile development en **Internet of Things** zijn ook interessante topics om aan te kaarten. Verschillen moeten aangetoond worden tussen de verschillende doelen en programmeertalen maar ook tussen de verschillende developers.

We willen ervoor zorgen dat we met deze workshop studenten **goesting laten krijgen in code!** En hoe kan dat dan beter door een indrukwekkend projectje te maken?

## Goals

Het doel is dus om **mensen geïnteresseerd te krijgen in programmeren**. We moeten dus kijken om een project te maken waarbij mensen gestimuleerd worden om dit met project met volle goesting te volbrengen en daarnaast om zich in de toekomst te verdiepen. Als we onszelf doelen mogen stellen, dan zijn dat de volgende:

- Stimuleren van de goesting om te programmeren
- Inzichten verwerven
- Kunnen begrijpen wat de code doet
- Kunnen begrijpen waarvoor verschillende technologiën gebruikt worden

## Main purpose

We starten met inwerken. We gaan micro:bit gaan verkennen door enkele animaties te maken, de naam te laten verschijnen, ...

We zullen vandaag ook een kleine versie worden van Frank Deboosere. We gaan **het weer gaan ophalen** voor onze huidige locatie en we gaan deze dan ook gaan voorstellen op een klein LED-schermpje of eventueel een aparte webapp. Wat we precies gaan voorstellen is het volgende:

- Huidige temperatuur
- Gevoelstemperatuur
- Huidig situatie
- Windrichting
- Windsnelheid

Dit project geeft duidelijk weer hoe gemakkelijk het is om iets bruikbaars te maken in een korte tijd. 

Hieronder kan je al wat proeven van hoe het project er zal uitzien:
> Hier komt een voorbeeldvideo die beschikbaar zal zijn op YouTube

![alt text](https://focus.knack.be/medias/18801/9626177.jpg "Frank Deboosere - VRT")

## What's needed

We kunnen dit natuurlijk niet maken zonder enkele **handige technologieën**. Dit zowel fysiek als digitaal. Hieronder maken we een korte samenvatting van de nodige verplichtingen. Laten we starten met de digitale benodigdheden.

### Digitals 

#### Microsoft MakeCode

Microsoft MakeCode maakt het mogelijk om studenten eenvoudig code te leren. Via een online platform kan men gaan werken met een micro:bit. Men kan kleurtjes gaan toepassen, geluiden gaan instellen, rekenoefeningen gaan uitvoeren, ...

![alt text](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE2Nd2Q?ver=ef06&q=90&m=6&h=405&w=720&b=%23FFFFFFFF&l=f&o=t "MakeCode")

[Klik hier om meer te weten te komen over Microsoft MakeCode](https://makecode.microbit.org/)

#### Code Editor

Heel belangrijk om te programmeren is natuurlijk jouw eigen code-editor. Deze zullen we gebruiken na het oefenen in Microsoft MakeCode. Je hebt er heel wat. Ik som er een aantal op:

- Visual Studio Code
- Atom 
- Sublime Text
- ...

Wij kiezen voor **Visual Studio Code**. Visual Studio Code is een code-editor gemaakt door Microsoft en kan gebruikt worden op zowel MacOS, Windows als Linux.

> **Let op!** Maak geen gebruik van Visual Studio. Visual Studio is gemaakt voor het bouwen en debuggen van moderne web en cloud applicaties.

![alt text](https://code.visualstudio.com/opengraphimg/opengraph-home.png "Visual Studio Code")

[Klik hier om meer te weten te komen over Visual Studio Code of om het te installeren](https://code.visualstudio.com/)

#### Mu

Daarnaast moeten we voor de micro:bit ook gebruik maken van de Mu editor. Deze editor is zeer eenvoudig en gemaakt voor de beginnende programmeur. Het is beknopt en doet wat het moet doen. Handig hier is dat de code die opgeslagen word, direct gecompileerd en verstuurd word naar de micro:bit.

![alt text](https://codewith.mu/img/en/mu.gif "Mu editor")

[Klik hier om meer te weten te komen over Mu of om het te installeren](https://codewith.mu/)

#### Python

Wij gaan een aantal programmeertalen gebruiken maar we zullen vooral gebruik maken van **Python** om onze code te schrijven. Python is ontworpen in de jaren 90 door de Nederlander Guido van Rossum en staat nog steeds hoog aangeschreven als programmeertaal. Het grote voordeel van Python is dat het **zeer eenvoudig te leren is**. Ze is zeer populair en word vaak gezien als een basis binnen Internet of Things. Binnen Python gaan we gebruik maken van een **Flask-server** om de data te gaan visualiseren.

> Momenteel word er gebruik gemaakt van 3.8.5 welke gereleased is op 20 juli 2020.

[Klik hier om meer te weten te komen over Python of om het te installeren](https://python.org/)

#### OpenWeatherMap API

Als we fysiek de data niet kunnen gaan ophalen, gaan we gebruik maken van een API. Via een API kunnen wij eigenlijk alle data gaan ophalen die noodzakelijk is voor ons. Deze data is real-time waardoor we altijd correcte gegevens verkrijgen. Binnen deze data gaan we vooral gaan kijken naar de temperatuur, de weersomstandigheden en de wind. We gaan deze real-time gaan visualiseren maar ook de voorspelling voor komende dagen. Dit per uur of per dag. Daarnaast kunnen we ook historische data gaan waarnemen en eventuele meldingen over gevaarlijke weersomstandigheden. 

[Klik hier om meer te weten te komen over OpenWeatherMap API of om het te gebruiken](https://openweathermap.org/api)

### Physical

#### Raspberry PI

Wij gaan gebruik maken van een **Raspberry PI**. Er zijn meerdere versies van deze. Momenteel zitten we al aan de 4e generatie van Raspberry PI. 

![alt text](https://www.raspberrypi.org/homepage-9df4b/images/opengraph/pi-4-og-image.png "raspberry pi")

#### micro:bit

Micro:bit is een systeem ontworpen door BBC en word ingezet binnen het Brits onderwijs. Dit is een kleine computer ontworpen om kinderen te leren programmeren maar ook om de mogelijkheden binnen technologie te ontdekken. 

![alt text](https://jaar1microbit.files.wordpress.com/2018/04/bbc-microbit.png?w=736 "micro:bit")