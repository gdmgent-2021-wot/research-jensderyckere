# Weather Station

## Samenvatting

Wat we zullen maken is een eigen weerstation. We zullen het weer eerst gaan ophalen met de API van OpenWeatherMap. Via deze API krijgen we een grote reeks aan data. Deze data bevat een weersvoorspelling voor de komende 5 dagen en een uitgebreid verslag voor het weer van vandaag. Het weer en de voorspelling zullen we gaan weergeven binnen de app en we gaan deze dan ook gaan vergelijken met een real-time temperatuur van binnen en van buiten aan de hand van de micro:bit. Deze app zal netjes worden vormgegeven aan de hand van een zelfgemaakt template waardoor enkel nog maar de data zal moeten worden ingevoerd.

De benodigheden:
- 2 micro:bits
- Batterijen
- 1 Raspberry PI
- Mu editor
- Visual Studio Code of andere IDE
- Python
- OpenWeatherMap API
- Flask Webserver

De GitHub-repo vind je terug via [deze link.](https://github.com/jensderyckere/weatherstation).

## Code on the pi

We gaan aan de slag met de volgende aangekregen **folder-structuur**:

```
- /app
---- /static
---- /templates
---- .env
---- app.py
```

Binnen de **app.py** gaan we aan de slag. Laten we starten met enkele imports van zeer belangrijke functionaliteiten die we kunnen toepassen in het vervolg van dit project.

```python
# Importeren van packages

## Urlllib2 gaan ge we gebruiken om de data binnen te halen
import urllib2

## Os maakt het mogelijk om door onze bestanden te bladeren
import os

## Hiermee gaan we de locatie gaan analyseren
from geopy.geocoders import Nominatim

## Beveiligde waarden kunnen we hiermee ophalen in dit bestand
from dotenv import load_dotenv

# Onze webserver
from flask import Flask, render_template

# Data leesbaar gaan maken
import json

# Versturen van micro:bit data naar onze computer/pi
import serial, time
```

We gaan binnen de **.env** bestand onze waarden gaan definiëren die we niet zichtbaar willen maken aan anderen. Denk maar aan je locatie, een API-key, ... Dit zijn gegevens die jouw privacy kunnen schaden of jouw project kunnen verstoren als deze zichtbaar zijn. Better be carefull!

Schrijf binnen de .env deze waarden:
```
GEO_USER=""
GEO_LOC=""
WEATHER_KEY=""
```
> Deze worden later nog ingevuld. Het is handig om nu al te weten dat we onze gevoelige waarden hier veilig kunnen bewaren.

We schakelen terug over naar de **app.py**. Hierbinnen gaan we nu de .env gaan ophalen en deze waarden gaan definiëren binnen onze app.py. Dit doen we als volgt:

```python
# Ophalen van het .env bestand, python weet automatisch 
# via deze functie dat het moet zoeken naar het eerste de beste .env file
load_dotenv()

# We slaan de waarden op met makkelijkere namen
api_key= os.getenv("WEATHER_KEY")
geo_loc = os.getenv("GEO_LOC")
geo_user = os.getenv("GEO_USER")
```

Deze velden moeten ingevuld worden. Laten we starten met de API-key. 

### OpenWeatherMap API
Navigeer naar de volgende link https://openweathermap.org/api. Eens we de website bereikt hebben moeten we kijken naar de optie "**One Call API**". Druk op de knop **Subscribe**. Ga naar de optie **Free** en druk op **Get API-key**. Eens we deze knop hebben ingedrukt krijgen we de mogelijkheid om ons te registeren. Registreer je zorgvuldig en dan word je doorgeleid naar jouw profiel. Daar vind je de knop API-keys. Kopieer de lange key. Vul binnen .env deze waarde in met jouw key:

```
WEATHER_KEY="jouw_superlange_key"
```

### Geopy
Binnen de volgende waarden vul je de naam van je app en jouw eigen locatie in. Dit kan zeer minimaal. De naam van een gemeente is al meer dan genoeg. Vul binnen .env deze waarden dan in:

```
GEO_LOC="Gent"
GEO_USER="jensdery"
```

Daarna word het tijd om met onze **locatie te gaan werken**. Het is belangrijk dat wij de locatie kunnen signaliseren en dit doen we het best door de naam van de gemeente te gaan omvormen tot 2 waarden. We spreken hier voornamelijk over de **longitude** en de **latitude**.

``` python
geolocator = Nominatim(user_agent=geo_user)
location = geolocator.geocode(geo_loc)
```

We moeten natuurlijk ook de data verkrijgen van onze **micro:bit**. We halen de temperatuur op via onderstaande configuratie. Deze noteren we ook in de app.py.

```python
port = "/dev/ttyACM0"
baud = 115200
s = serial.Serial(port)
s.baudrate = baud
```

En nu is het tijd voor het opzetten van een Flask server. Dit is een webserver waardoor we een eigen website lokaal kunnen maken. Deze website zal een dashboard voorstellen van verschillende waarden. We tonen het huidig weer en ook een voorspelling voor de komende dagen. In de code word alle toepassingen grondig uitgelegd:

```python
# We starten de server op
app = Flask(__name__)

# Te vinden op volgende route
@app.route('/')
def index():
    # We verkrijgen de data met onze eigen velden
    string = "https://api.openweathermap.org/data/2.5/onecall?lat={}&lon={}&appid={}".format(location.latitude, location.longitude, api_key)
    contents = urllib2.urlopen(string).read()

    # We zetten de data om tot JSON
    data = json.loads(contents)

    # De voorspelling
    forecast = data['daily']

    # Het huidig weer
    current = data['current']

    while True:
        # Verkrijg de indoor data
        indoor = s.readline()
        indoor = int(indoor[0:4])

        # Toon onze website binnen de webserver en verstuur de opgehaalde waarden naar de webpagina
        return render_template('index.html', forecast=forecast, current=current, indoor=indoor)

# De server zal zich herladen na elke wijzigingen
if __name__ == '__main__':
    app.run(debug=True)
```

> Let op! Er is nog geen data verstuurd vanuit de micro:bit.

## Code on the micro:bit

Tijd om de data vanuit de micro:bit te versturen naar de computer! We gaan dit simpelweg doen door een eindeloze loop aan te gaan waarbij de temperatuur om de 10 seconden word verzonden. Schrijf binnen de Mu editor de volgende code.

```python
import microbit from *

while True:
    print(temperature())
    sleep(10000)
```

Zo, nu word de code verstuurd naar de computer. Natuurlijk moet dit alles nog in werking treden!

## Run the code

We beginnen in onze Mu editor. Daar drukken we de knop **Flash** in. Dit zorgt ervoor dat de code van de Mu editor wordt geplaatst op onze micro:bit. Zo is die klaar om de data te gaan versturen naar onze Raspberry Pi.

![alt text](https://codewith.mu/img/en/tutorials/microbit_flash.gif "Mu editor")

In Visual Studio Code gaan we de code runnen binnen de terminal. 2 commands moeten in deze volgorde uitgevoerd worden:

```
cd app
python app.py
```

Dit zorgt ervoor dat de webserver opgestart zal worden. Als alles correct is verlopen zou je deze melding moeten krijgen.

![alt text](https://miro.medium.com/max/2704/1*0_T47qY8ClYdxtuAtABH1w.png "terminal")

De **running on** informatie is zeer belangrijk voor ons. Via deze url kan je de webpagina bezoeken. Als je deze link volgt, zou je volgend scherm moeten verkrijgen. Deze webpagina is opgemaakt uit **HTML, CSS en JS**. Dit zijn de basics voor webdevelopment. [Als je echt geïnteresseerd bent kan je binnen deze GitHub repositorie dan ook de HTML, CSS en JS files raadplegen.](https://github.com/jensderyckere/weatherstation)


![alt text](https://i.ibb.co/564dzNh/Schermafbeelding-2020-10-15-om-18-49-48.png "window")