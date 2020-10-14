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

De GitHub-repo vind je terug via deze link.

## Set-up op de Pi

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

    # het huidig weer
    current = data['current']

    # We zenden deze waarden naar de webpagina
    return render_template('index.html', forecast=forecast, current=current)

# De server zal zich herladen na elke wijzigingen
if __name__ == '__main__':
    app.run(debug=True)
```