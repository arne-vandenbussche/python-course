# Inleiding

## Doel van dit hoofdstuk

Na het bestuderen van dit hoofdstuk heb je enig idee van wat Python is, wat de specifieke kenmerken van Python zijn.

Je weet ook welke tools we hanteren. Na het bestuderen van dit hoofdstuk heb je de nodige software geïnstalleerd en kan je in het volgende hoofdstuk volop aan de slag.

## Opzet van deze cursus

De bedoeling van deze cursus is een stevige inleiding in Python te geven. Een opleidingsonderdeel van drie studiepunten laat niet toe alle aspecten van Python te behandelen. Onze doelgroep is hier niet de full-stackontwikkelaar, maar elke IT-professional die Python kan gebruiken in zijn specialiteit. Onze focus ligt dus eerder op kleinere projecten.

* Scripts of kleine projecten om repititieve taken te automatiseren.
* Automatisering van servertaken en securitytaken.
* Data-analyse.

Topics die we dus niet of heel beperkt zullen behandelen, zijn:

* Full-stack web development met frameworks als Flask of Django.
* Desktop GUI-applicaties met tools als Tkinter, PyQt5, wxPython, enzovoort.
* API's ontwikkelen of gebruiken.

## Vereiste voorkennis

Dit is geen beginnerscursus programmeren. We verwachten dat elke student in deze cursus al een stevige basis heeft in objectgeoriënteerd programmeren, in gelijk welke programmeertaal. 

De cursus mag dan wel beginnen met de absolute basis van Python. Toch zullen we in deze cursus niet uitleggen wat een variabele is, hoe een iteratie in elkaar zit, wat een exceptie is, of wat klassen en objecten zijn. We veronderstellen dat deze concepten al bekend zijn.

## Kenmerken van Python

### Algemene taal met een breed scala aan mogelijkheden

Op zich is Python een oudere programmeertaal, gecreëerd door de Nederlander Guido Van Rossem in de late jaren 80 van de twintigste eeuw. De actieve versie op dit moment is Python3 met zijn varianten, ontstaan in 2008.

Python is een programmeertaal met een steeds groeiende populariteit en een grote gemeenschap. Python heeft een breed scala van toepassingen:

* Scripting om kleinere repititieve taken te automatiseren, in diverse domeinen.
* Webontwikkeling met frameworks als Flask, Django en nog vele andere.
* Dataverwerking en data-analyse met bibliothelen als Pandas, Numpy, Matplotlib.

- Desktopapplicaties met behulp van bibliotheken als Tkinter, PyQT en wxPython.
- Gameontwikkeling met bibliotheken als Pygame voor 2D-games.
- IoT: Python wordt vaak gebruikt om kleinere apparaten zoals een Rapsberry Pi te programmeren.
- Toepassingen van data science en artificiële intelligentie met bibliotheken en frameworks als skikit-learn, TensorFlow, Keras, PyTorch, NLTK.

### Platformonafhankelijk

Python is ook beschikbaar op een breed gamma aan platformen zoals Windows, macOS, Linux, BSD.

### Sterk in leesbaarheid

Guido van Rossum heeft Python ontwikkeld omdat hij in zijn job een scripttaal moest hanteren die erg lastig leesbaar was en moeilijk te hanteren. Een eenvoudige en leesbare syntax behoort tot de basisfilosofie van Python.

Python gebruikt ook geen accolates of andere symbolen om codeblokken te structureren, maar indendatie, het inspringen van code. Dit verplicht de programmeur om leesbare code te schrijven. Het onderstaande codevoorbeeld illustreert dit:

```python
def gemiddelde(lijst):
    som = 0
    teller = 0
    for getal in lijst:
        som += getal
        teller += 1
    gemiddelde = som / teller
    return gemiddelde

getallen = [10, 20, 30, 40, 50]
resultaat = gemiddelde(getallen)
print("Het gemiddelde is:", resultaat)
```

### Dynamische, maar strikte typering

**Dynamische typering** (dynamic typing) betekent dat je het datatype niet vooraf moet bepalen bij het declareren van een variabele zoals in C, C++, C# of Java gebuikelijk is. Het datatype wordt bepaald bij de eerste toekenning.

Voorbeeld:

```python
leeftijd = 25
```

Door de toekenning van een integer bepaalt Python op dat moment het datatype van de variabele "leeftijd". Daarin gelijkt Python op Javascript.

Python verschilt op dat punt ook enigszins van Javascript. In Javascript zal men bij het combineren van variabelen met een verschillend type (bijv. bij een bewerking of een toekenning), de bewerking te laten doorgaan door één van de variabelen te converteren. Pyhton doet dit niet. Python geeft dan een `TypeError`. 

### Geïnterpreteerd, niet gecompileerd

Talen als C, C++, C# en Java zijn gecompileerde talen, terwijl een taal als Python net als Javascript en PHP beschouwd wordt als een geïnterpreteerde talen. Een gecompileerde taal wordt eerst door een compiler omgezet in machinetaal en is dan uitvoerbaar terwijl een geïnterpreteerde taal lijn per lijn uitgevoerd wordt  door een 'interpreter'.

Het grootste verschil zit in het volgende voorbeeld. Als je in de laatste regel een syntactische fout maakt, dan zal de compiler bij een gecompileerde taal als Java een foutmelding geven en het programma niet willen compileren. Je ontdekt de fout dus onmiddellijk vooralleer je het programma zelfs maar kan uitvoeren. In het geval van Python zal het programma uitgevoerd worden tot het op de fout stuit en dan zal de uitvoering onderbroken worden. Het programma is onmiddellijk uitvoerbaar.

We moeten echter toegeven dat het onderscheid niet zo strikt is. Python wordt ook achter de schermen eerste gecompileerd naar bytecode en het is die bytecode die door de interpreter uitgevoerd wordt. De gecompileerde bytecode vind je in de mysterieuze map `__pycache__`. Dit proces is heel vergelijkbaar met wat er in Java en C# gebeurt, met dat verschil dat er in die twee talen een expliciete compileerstap uitgevoerd moet worden vooralleer je 

### Objectgeoriënteerd én functioneel

In een functionele programmeertaal ligt de nadruk op functies die "stateless" zijn, die geen waarde wijzigen, die geen neveneffecten hebben, maar op basis van een input een output berekenen en teruggeven. Een objectgeoriënteerde taal is gebaseerd op klassen, waarbij objecten een instantie zijn van een klasse. Aspecten als overerving en polymorfisme zijn typische eigenschappen van een objectgeoriënteerde taal.

Python ondersteunt beide paradigma's.

## Tools

### Python

Onze eerste tool is natuurlijk de Python interpreter. Die kan je best installeren van de officiële site van Python: https://www.python.org/downloads/. Het is mogelijk dat je al de juiste versie op je computer staan heb. Je kan de versie testen met het volgende commando

```bash
$ python --version
```

en je krijgt de versie terug:

```bash
$ Python 3.11.4
```

Het is mogelijk dat je het commando `python3 moet gebruiken.

``` bash
$ python3 --version
```

Je hoeft voor deze cursus niet per se de laatste versie van Python te hebben. Een versie vanaf 3.8 zou moeten volstaan.

Python kan je op verschillende manieren uitvoeren:

- Interactief
- Commandolijn
- Jupyter notebooks

De **interactieve manier** krijgt je door in je terminal het command `python` of `python3`in te tikken, zonder andere argumenten. Je kan dan pythoncommando's één voor één uitvoeren. Het onderstaande voorbeeld illustreert dit:

![python op een interactieve manier](./afbeeldingen/python-interactive.png)

**Jupyter notebooks** zijn een omgeving, een soort document, waarin je zowel tekst (in de vorm van markdown) als Pythoncode kunt schrijven. De Pythoncode kan je binnen het document uitvoeren en het resultaat is ook onmiddellijk in het document zichtbaar. Jupyter notebooks zijn interessant bij een data-analyse. Je kan onmiddellijk de gegevens verkennen en het resultaat bekijken.

Een derde manier is de uitvoering via de commandolijn. Je schrijft je Pythoncode in een tekstbestand met de extensie *.py. Je voert het script onmiddellijk uit in een terminal met het commando ```python your_script.py```. Dit is de manier die wij zullen hanteren.

### Teksteditor en terminal

Een ervaren ontwikkelaar die complexe Pythonprogramma's ontwikkelt, zal gebruik maken van een IDE, een intergrated development environment, zoals PyCharm of VSCode. Deze omgevingen bieden een ruime ondersteuning zoals code completion, AI-tools om code te schrijven, een geïntegreerde debugger, het automatisch opzetten van een virtuele omgeving, de automatische intallatie van geïmporteerde bibliotheken, enzovoort.

Wij zullen gebruik maken van een eenvoudige IDE, Spyder. Die is geschreven in Python en vooral nuttig voor data-analyse en om Python te leren.

We kiezen voor Spyder omdat Spyder de essentiële kenmerken van een IDE heeft, zoals syntax highlighting, auto-completion en debugging, maar voor de rest eenvoudig in gebruik is. Spyder bevat ook geen AI-module. Alhoewel AI een ontwikkelaar zeker kan helpen bij het coderen, is het voor een student beter om de nodige vaardigheden te trainen zonder gebruik te maken van AI.

Het staat iedereen vrij om een andere editor zoals Vim, Neovim, Atom, Sublime Text, PyCharm of VSCode te gebruiken, maar op het examen is het gebruik van Spyder zonder plug-ins verplicht.

Je kan Spyder als stand-alone programma installeren via [deze link](https://www.spyder-ide.org/download)

### SQLite en Db Browser for SQLite

Vanaf hoofdstuk zes maken we ook gebruik van een relationele database. Om de overhead minimaal te houden maken we gebruik van SQLite3. SQLite3 heeft alle kenmerken van een relationele database, maar de installatie is heel eenvoudig. 

Er is ook geen overhead. Een SQLite-database bestaat uit één bestand. Je hoeft geen server te installeren, geen services te installeren, enzovoort. Alle functionaliteit zit vervat in je Pythoncode.

SQLite is ook standaard in Python. Je hoeft geen extra packages te installeren.

SQLite is dé standaardoplossing op kleine devices zoals IoT-devices en je eigen smartphone, maar kan toch heel grote hoeveelheden gegevens aan. Wanneer oplossingen en Excel te kort schieten, dan is SQLite een uitstekend alternatief.

Je zou SQLite kunnen downloaden en installeren van de [officiële homepagina](https://www.sqlite.org), maar wij zullen een andere aanpak hanteren. SQLite kan je benaderen vanuit programmacode of via de terminal, maar er ook een gebruiksvriendelijke grafische tool waarmee je een SQLite-database kunt beheren: [DB Browser for SQLite](https://sqlitebrowser.org/). We raden aan DB Browser for SQLite te installeren en dan heb je SQLite op zich er zomaar bij.

### Cursus

De cursus bestaat uit losse delen die in pdf-formaat beschikbaar gesteld zullen worden. Elk hoofdstuk zal uit minstens drie delen bestaan:

* Een theoriegedeelte met de uitleg en voorbeelden.
* Oefeningen.
* Oplossingen van oefeningen.

### Extra filmpjes

In de Toledocursus vullen we het cursusmateriaal aan met filmpjes, eigen opnames, maar ook heel wat fimpjes van YouTube of andere kanelen. We verwijzen graag naar de filmpjes van het [Socraticakanaal](https://www.youtube.com/watch?v=bY6m6_IIN94&list=PLi01XoE8jYohWFPpC17Z-wWhPOSuh8Er-). Zij leggen heel wat Pythonconcepten op een boeiende en duidelijke manier uit.

Ook de YouTubecursussen van [Tech with Tim](https://www.youtube.com/watch?v=sxTmJE4k0ho&t=3629s) of [Programming with Mosh](https://www.youtube.com/watch?v=_uQrJ0TkZlc) zijn prima.

### Officiële documentatie

Er bestaan heel wat uitstekende tutorials over Python, en massa's fora waar je vragen kunt stellen. Toch is het nuttig om in de [officiële documentatie](https://docs.python.org/3/index.html) je weg te vinden. In de cursus zullen we ook geregeld naar deze documentatie verwijzen.

## Aanpak
Hoe pas je deze cursus het beste aan? Daar bestaan geen grote geheimen over. 
Bestudeer eerste de voorbeelden in de theorie en probeer de uitleg erbij goed te begrijpen. 

De volgende stap is dan om enkele oefeningen te maken. Het is zeker niet altijd nodig alle oefeningen te maken. Het hangt van je eigen voorkeur en tempo af hoeveel oefeningen je maakt. Zorg er wel voor dat je alle concepten geoefend hebt. Verzin zelf eigen voorbeelden om de leerstof naar een andere context te transfereren.

Gebruik de doelstellingen bij het begin van elk hoofdstuk als checklist om na te gaan of je alles beheerst.

Gebruik de basisprincipes die voor elke cursus gelden:
* Gespreide herhaling.
* Oefenen.
* Test jezelf.

## Opdracht

Bij deze cursus hoort ook een opdracht. Die wordt in de Toledocursus toegelicht.

## Dank

Bij het samenstellen van dit cursusmateriaal heb ik dankbaar gebruik gemaakt van het uitstekende werk van mijn voorgangers, Andy Louwyck, Yves Sagaert en Karim Gabsi.

