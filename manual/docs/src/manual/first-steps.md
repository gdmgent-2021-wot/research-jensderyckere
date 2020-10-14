# First steps

## Kennismaking micro:bit

De micro:bit is een kleine computer. Op de micro:bit vind je knopjes op de bediening met een 5x5 LED matrix dat gebruikt word als beeldscherm. Deze kan gebruikt worden met 4 verschillende programmeertalen. 

We kunnen gebruik maken van de blocks editor. Dit is het laagste niveau maar wel perfect voor de beginners om de essentie te snappen achter programmeren. De code word zo een op grafische manier voorgesteld waardoor het veel gemakkelijker te begrijpen is. 

De micro:bit bevat een aantal sensoren voor:
- Temperatuur
- Licht
- Trillingen
- Oriëntatie
- Magneetvelden

Het handige aan een micro:bit is dat men draadloos kan connecteren. Micro:bits kunnen met andere micro:bits connecteren maar ook met smartphones, tablets en pc's.

De programmeertalen die voornamelijk gebruikt worden zijn **JavaScript** en **Python**.

### Connecteer de micro:bit met Mu

Je kan de micro:bit connecteren aan de hand van **Bluetooth** of een **USB-kabel**. Eens deze geconnecteerd is, hoef je geen extra zaken meer te doen. De code zal bij elke save op Mu automatisch gecompileerd worden naar de micro:bit.

### Display the name

We kunnen starten met het tonen van je eigen naam op de micro:bit. Let op! Bij elke code moeten we een import doen van Micro:bit. Anders zal de code niet werken.

```python
from microbit import *

while True:
    display.scroll('Jane Doe')
    sleep(2000)
    display.clear()
```

<iframe width="100%" height="315" src="https://www.youtube.com/embed/mQqsKH67wc4" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Wat zal er hier gebeuren?
- We importeren microbit om zo alles te laten functioneren.
- De while-statement zorgt voor een eindeloze lus. Dit zorgt ervoor dat de tekst zal blijven lopen.
- Om de tekst niet aan elkaar te sluiten, laten we ze 2seconden sluiten na afronden
- We zorgen ook voor dat de vorige tekst dan verdwijnt

### Press the button

We kunnen er natuurlijk ook voor zorgen dat de naam enkel en alleen maar getoond word bij het indrukken van een knop. Dit doen we als volgend:

```python
from microbit import *

while True:
    if button_a.is_pressed() :
        display.scroll('Jane Doe')
        sleep(2000)
        display.clear()
    if button_b.is_pressed() :
        display.scroll('Jane Foo')
        sleep(2000)
        display.clear()
```

<iframe width="100%" height="315" src="https://www.youtube.com/embed/1CPZjh_OrKE" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Wat zal er hier gebeuren
- We houden dezelfde systematiek aan van de vorige oefening.
- Nu zullen we de naam tonen vanaf het moment een knop word ingedrukt

### Hot or cold? 

Binnenin het micro:bit pakket vinden we ook een thermometer. Met de thermometer kunnen we de temperatuur gaan aflezen. Dit geeft de perfecte aanloop naar ons eindproject. Dan zullen we het weer gaan ophalen en aantonen op het web. Hieronder vind je hoe we dit kunnen doen:

```python
from microbit import *

# Een eindeloze loop maken
while True:
    # Bekijk of de knop word ingedrukt en toon dan de temperatuur
    if button_a.was_pressed():
        display.scroll(temperature())
```

<iframe width="100%" height="315" src="https://www.youtube.com/embed/UVdorjyfP8Y" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Outside/inside

Met het volgende geven we al een klein beetje van het eindproject weer. Nu gaan we de temperatuur van binnen en buiten gaan ophalen. We hebben hiervoor 2 micro:bits nodig en wat batterijen. Deze keer zullen we werken met verzending via bluetooth. 

We moeten rekening houden met de volgende onderverdeling:
- De micro:bit die buiten ligt zal werken als **verzender**.
- De micro:bit die binnen ligt zal werken als **ontvanger**.

Hoe gaan we te werk voor de **verzender**:
```python
from microbit import *

# Dit is de package die ons zal helpen met het verzenden
import radio

# We configureren de radio op zender 23
radio.config(group=23)
radio.on()

# We gaan een eindeloze loop gaan gebruiken om de data te versturen om de 2 seconden
while True:
    radio.send(str(temperature()))
    sleep(2000)
```

Hoe gaan we te werk voor de **ontvanger**:
```python
from microbit import *

# Dit is de package die ons zal helpen met het verzenden
import radio

# We configureren de radio op zender 23
radio.config(group=23)
radio.on()

# Een eindeloze loop
while True:
    # Bekijk of we de radiosignalen ontvangen
    outdoor = radio.receive()
    # Toon de buiten-temperatuur bij het drukken van knop A
    if button_a.was_pressed():
        display.scroll(outdoor)
    # Toon de binnen-temperatuur bij het drukken van knop B
    if button_b.was_pressed():
        display.scroll(str(temperature()))
```

<iframe width="100%" height="315" src="https://www.youtube.com/embed/yvVpibBBNNQ" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>