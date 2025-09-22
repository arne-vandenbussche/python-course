# Een eenvoudig script schrijven

## Doel van dit hoofdstuk

Op het einde van dit hoofdstuk zal je:

- een eenvoudig script kunnen schrijven,
- de basisdatatypes int, float, string, list kunnen hanteren,
- basisoperaties kunnen uitvoeren met deze datatypes,
- de controlestructuur `if` kunnen hanteren,
- een iteratie kunnen uitvoeren met `for` of `while`,
- testen of een variabele van een bepaald datatype is,
- gegevens kunnen omzetten naar een ander datatype,
- input van de gebruiker kunnen opvragen,
- output op een formatteerde manier kunnen teruggeven,
- argumenten in een script kunnen hanteren,
- stringoperaties kunnen uitvoeren (slicing, ...)

## Extra documentatie

### Uit de officiële documentatie

- [Using Python as a Calculator](https://docs.python.org/3/tutorial/introduction.html): in deze voorbeelden worden de basisdatatypes en hun bewerkingen gedemonstreerd.
- [Numeric Types](https://docs.python.org/3/library/stdtypes.html#typesnumeric): beschrijving van alle numerieke datatypes (int, float, complex) en hun bewerkingen.
- [Boolean operations](https://docs.python.org/3/library/stdtypes.html#boolean-operations-and-or-not)
- [Tekst](https://docs.python.org/3/library/stdtypes.html#text-sequence-type-str)
- [Wiskundige functies die behoren tot de module math](https://docs.python.org/3/library/math.html#math.trunc)
- [Built-in Functions](https://docs.python.org/3/library/functions.html?highlight=input#input)
- [More Control Flow Tools](https://docs.python.org/3/library/functions.html?highlight=input#input): in dit onderdeel worden statements en functions zoals if, for, range(), break, continue, pass, match (vanaf Python 3.10).
- [Custom String Formatting](https://docs.python.org/3/library/string.html#custom-string-formatting)

## Variabelen en datatypes

Zoals we eerder aangaven is Python dynamisch getypeerd. We moeten dus het datatype niet vooraf bepalen. Het datatype wordt bepaald door de eerste toekenning.

### Getallen

We kennen twee datypes die over getallen gaan:

- `int`: integer of gehele getallen
- `float`: kommagetallen

Kommagetallen worden aangeduid met een punt. Bekijk de volgende voorbeelden:

```python
leeftijd = 23
gewicht = 78.5
```

De variabele leeftijd zal van het type `int` zijn en de variabele gewicht zal van het type `float` zijn.

Python heeft de volgende **rekenkundige operatoren** die je op numerieke datatypes kan toepassen:

*   Optelling: +
*   Aftrekking: -
*   Vermenigvuldiging: *
*   Machtsverheffing: **
*   Deling: /
*   Geheeltallige (integer) deling: //
*   Module (rest): %

De volgende functies op getallen ook interessant:

- `abs(x)` geeft de absolute waarde van x terug.
- `max(x,y)`: geeft het grootste getal van x en y terug.
- `min(x,y)`: geeft het kleinste getal van x en y terug.

Als we de ingebouwde module *math* importeren, en dan doen we door het statment `import math` bij het begin van ons script te plaatsen, dan hebben we nog een aantal intessante functies.

- `math.ceil(x)`: geeft het kleinste geheel getal groter dan of gelijk aan x terug.
- `math.floor(x)`: geeft het grootste geheel getal kleiner dan of gelijk aan x terug.

Voorbeelden:

```python
import math
print(math.ceil(2.3)) # 3
print(math.floor(2.3)) # 2
print(abs(-5)) # 5
print(max(5,7)) # 7
```

### Booleaanse waarden

Zoals je weet is een booleaanse waarde waar (`True`) of onwaar (`False`).

We kennen de klassieke operaties op booleaanse waarden. In Python zien die er zo uit: `or`, `and` en `not`.

De vergelijkingsoperatoren zien er in Python zo uit:

| Operatie | Betekenis                 |
| -------- | ------------------------- |
| `<`      | kleiner dan               |
| `<=`     | kleiner dan of gelijk aan |
| `>`      | groter dan                |
| `>=`     | groter dan of gelijk aan  |
| `==`     | gelijk aan                |
| `!=`     | niet gelijk aan           |
| `is`     | objectgelijkheid          |
| `is not` | objectongelijkheid        |

### Tekst 

Tekst of `str` kunnen we tussen enkele of dubbele aanhalingstekens zetten. De volgende statements zijn dus gelijk:

```python
print("Hello world")
print('Hello world')
```

Als je dus in een stukje tekst ook aanhalingstekens wil gebruiken, dan kan dat door af te wisselen tussen enkele en dubbele aanhalingstekens:

```python
print('En de vader zei: "Jongen, je moet op tijd beginnen te studeren."')
```

Om strings aan elkaar te plakken (**concatenate**) gebruiken we de plus-operator (+) gebruiken om twee strings aan elkaar te “plakken” (concateneren). Je kan de ster operator (\*) gebruiken met een string en een integer om een string te maken die een herhaling van de originele string bevat.

Het commando:

```python
print("Hogeschool" + " VIVES")
```

zal de volgende output geven: Hogeschool VIVES.

Het commando:

```python
print(3 * "ai")
```

zal de volgende output geven: aiaiai.

Enkele interessante **stringfuncties** zijn:

- `str.lower()`: geeft str in kleine letters.
- `str.upper()`: geeft str in hoofdetters.
- `str.title()`: laat elk woord in de string met een hoofdletter beginnen.
- `len(str)`: geeft het aantal tekens in een string
- `str.count(sub [,start [,end]])`: telt hoe vaak een niet-overlappend stuk tekst voorkomt in een string.
- `str.find(sub, [, start [,end]])`: geeft -1 als sub niet in str voorkomt en ander de laagste index (beginnend bij 0).
- `sub in str`: geeft True als sub in str voorkomt, anders False.
- `str.replace(str1, str2)`: vervangt, str1 met str2

Bedenk dat strings **onwijzigbaar** zijn. Een gewijzigde string druk je af of ken je toe aan een nieuwe variabele.

Voorbeelden:

```python 
print("Vives Hogeschool").lower() # vives hogeschool
print("Vives Hogeschool").upper() # VIVES HOGESCHOOL
print("vives hogeschool").title() # Vives Hogeschool
print(len("Dit is tekst")) # 12
boodschap = "Dit is tekst"
print(boodschap.count('i')) # 2
print(boodschap.count('t')) # 3
print(boodschap.count('t', 4)) # 2 (ik begin maar te tellen vanaf de vierde positie)
print(boodschap.find('t', 4)) # 7
print("tekst" in "Dit is tekst.") # True
print("text" in "Dit is tekst.") # False
nieuweboodschap = boodschap.replace("tekst", "een boodschap.") # Dit is een boodschap
```

In een stuk tekst val `\t` een tab voorstellen en `\n` een nieuwe regel. Let wel, in Windows is een nieuwe regel een combinatie van nieuwe regel en "carriage return", dus `\n\r`'.

Wanneer een teken dat een andere betekenis heeft, letterlijk moet genomen worden, dan moet je er een backslash voor zetten, het zogenaamde **escapeteken**.

```python
print("We gebruiken het teken \", of aanhalingstekens bij citaten.")
print("De directory is C:\\Windows\\System32.")
```

Wanneer je een teken uit een stuk tekst wil **selecteren**, dan kan je de index gebruiken. De index begint bij 0.

```python
boodschap = "Hello, World!"
print(boodschap[1]) # resultaat: e
```

Met de **slice-operator**, kan je een substring selecteren. Let wel, de startindex wordt meegerekend, de slotindex niet.

```python
boodschap = "Hello, World!"
print(boodschap[2:5]) # resultaat: llo
```

 De start `i1` van de slice `i1:i2` mag je echter         weglaten als `i1` de eerste index is, en `i2`         mag je weglaten als `i2` de laatste index is:      

```python
print(boodschap[:5]) # resultaat: Hello
print(boodschap[7:]) # resultaat: World!
```

### Conversie van datatypes

We ontvangen niet altijd waarden in het juiste datatype. Daarom moeten we vaak aan type casting, of het omzetten naar een andere datatype doen.

- `int(x)`: omzettennaar geheel getal.

- `float(x)`: omzetten naar kommagetal.
- `str(x)`: omzetten naar string.

### Testen of iets van een bepaald datatype is

De meest algemene functie om te testen of een waarde van een bepaald type is, is de functie `isinstance(object, type)`.

Je kan hierbij één type of een lijst van types weergeven.

```python
x = isinstance("Hello", str) # x is True
x = isinstance(2, str) # x is False
x = isinstance(2.5, int) # is is False
x = isinstance(2.5, (int, float)) # x is True
```

Een andere methode is de functie `type()`.

```python
x = 5
y = type(x) == int # y is True
```



De functie `str.isnumeric()` test of alle tekens in een string cijfers zijn.

```python
x = "122343".isnumeric() # x is True
x = "2.5".isnumeric() # x is False
```

Met de module numbers kan je echts testen of iets een getal is:

```python
import numbers

x = 5
print(isintance(x, numbers.Number)) #resultaat True
```

### Meervoudige toekenning

Je kan ook meerdere variabelen toekennen op één en dezelfde lijn (ook al is dat omwille van de leesbaarheid niet altijd aan te raden):

```python
x, y, z = 10.0, 20.0, 30.0
print(x + y + z) # 60.0
```


##  Input inlezen

Een script heeft vooral zin als we input aan de gebruiker kunnen opvragen. Dat doen we met de functie `input()`. Deze kan een prompt bevatten, een stukje tekst dat aan de gebruiker als boodschap meegegeven wordt. Let wel, input wordt altijd in string-formaat ontvangen. Het kan zijn dat je een omzetting moet doen naar een ander dataype.

```python
voornaam = input("Geef je voornaam: ")
print("Welkom " + voornaam)
```

```python
getal = input("Geef een geheel getal: ")
print("Het kwadraat van dit getal is " + int(getal)**2)
```



## Beslissingen nemen (if)

Python kent ook de gewone if-structuur. De onderstaande voorbeelden illustreren de werking van if:

```python
speed = 31.54
if speed <= 30:
    print("Flying allowed.")
else:
    print("Flying not allowed, due to strong winds.")
```

```python
age = 14
if (age <= 12):
    print("Free entrance.")
elif (age < 18):
    print("Ticket price: €5.")
else:
    print("Ticket price: €8.")
```

```python
voltage = 3.9
temperature = 36
if voltage > 3.7 and temperature < 49:
    print("All ok.")
else:
    print("Warning, check parameters!")
```

Voor korte statements is deze notatie ook mogelijk:

```python
cost = 24.54
revenue = 93.01
profit = revenue - cost
print("Nice, keep going!") if profit > 0 else print("Watch out for bankruptcy.")
```

Indien je een leeg statement wil zetten om eventueel later nog iets mee te doen, kan je `pass` plaatsen. Zo vermijd je een error.

```python
height = 150
if height < 300:
    pass
else:
    print("Too high.")
```

In plaats van pass kan je ook drie puntjes zetten, het zogenaamde Ellipsis object:

```python
naam = 'KULeuven'
if naam.lower() == 'vives':
  print('Hogeschool')
else:
  ...
```

## Commentaar en indentatie

Zoals je in voorgaande voorbeelden hebt opgemerkt, werkt Python niet met accolades of puntkomma om code te structureren, maar wel met inspringen of indexatie. Je sprint vier tekens in om een blok code op te geven. In de meeste text editors kan je hiervoor de tabtoets gebruiken. Deze wordt omgezet naar vier tekens.

Commentaar geef je aan met het teken `#`. Alle code achter dit teken wordt niet meer geïnterpreteerd.

Commentaar van meerdere regels laat je starten en beginnen met `'''` of `"""`.

## Meerdere regels

Soms gebeurt het dat een commando over meerdere regels loopt. In dat geval eindig je de regel met een backslash `\` 

```python
if school1[1] == school2[1] 
        and school1[2] == school2[2] \
        and school1[3] == school2[3] \
        and school1[4] == school[4]: 
        return True
else:
        return False
```

Een alternatieve methode is om de code in ronde haakjes, vierkante haakjes of accolades in te sluiten:

```python
 if (school1[1] == school2[1]
        and school1[2] == school2[2]
        and school1[3] == school2[3]
        and school1[4] == school2[4]): 
        return True
    else:
        return False
```

Als je een stuk tekst, een string over meerdere regels wil laten lopen, kan je dezelfde methode toepassen als hierboven, of werken met een opeenvolging van drie aanhalingstekens. Het overgaan van een nieuwe regel wordt in dat laatste geval ook letterlijk genomen. 

```python
my_text = """Python is 
a very readable
programming language
"""
print(my_text)
```

Deze code zal de volgende output opleveren:

```
Python is 
a very readable
programming language
```

## Lists

In een later hoofdstuk gaan we uitgebreid op lijsten in, maar we bespreken graag het basistype, de list of array. Je kan een list op twee manieren declareren:

```python
myList = ["car", "bike", "airplane", "step"]
myUnimportantList = list(("a", "b", "c"))
```

Om één specifiek element te bereiken, kan je via de index werken, net zoals bij strings. Zo'n index is eigenlijk een gewoon volgnummer (zero based). Gebruik vierkante haakjes om de index tussen te noteren.

```python
myList = ["car", "bike", "airplane", "step"]
print(myList[1]) # bike
```

In tegenstelling tot strings zijn lists wel veranderlijk. Daardoor kan je dat element wel wijzigen:

```python
myList[1] = "e-bike"
print(myList[1]) # e-bike
```

Als je slechts een deel van een list wil opvragen, kan je ook bij lists een 'slice' meegeven. In feite bekom je dan een nieuwe (kortere) lijst. Vergeet niet dat het element van het tweede getal (index) niet tot de nieuwe lijst behoort (exclusive boundary).

```python
myList = ["car", "bike", "airplane", "step"]
print(myList[1:3]) # ['bike', 'airplane']
```


Items toevoegen op het einde van de (geordende) lijst, kan via de methode `append()`.
```python
my_list = ['bike', 'car']
my_list.append("boat") # ['bike', 'car', 'boat']
```

Meer details over lijsten volgt nog later.

## Iteratie of herhaling 

Wanneer een elementer "iterable" is, dat bekent dat het als een lijst doorlopen kan worden, dan is de `for`-lus de meest aangewezen manier om dat te doen. Zowel strings als lists zijn iterable.

```python
myList = ["car", "bike", "airplane", "step"]
for item in myList:     
    print(item)
```

Omdat je geen 'lusvariabele' hebt in de for-lus, moet je een andere manier bedenken om een 'vast aantal' iteraties uit te voeren. Meestal wordt hiervoor de `range()` functie gebruikt.

```python
for i in range(10):
    print(i*2)
```

Daarnaast heb je ook de `while`-lus om een herhaling te doen tot een voorwaarde is vervuld.

```python
i = 0;
while i < 5:
    i += 1
    print("i has the value of: " + str(i))
```

Een iteratie onderbreken kan je met het statement `break`. Een iteratie voortzetten kan je met het statement `continue`.

## Geformatteerde String output

We hebben al gezien dat de functie `print()` een output naar de terminal print. Het statement kan ook meerdere argumenten bevatten, die dan aan elkaar geplakt worden.

```python
getal = input("Geef een getal: ")
if isinstance(getal, (float, int)):
  print("Het kwadraat van dit getal is", getal**2)
```

In vele gevallen willen we echter dat onze output op een verzorgde manier gepresenteerd wordt en mengen we ook variabelen met letterlijke tekst. 

De eenvoudigste manier om dit aan te pakken is om de letter 'f' voor de dubbele aanhalingstekens te zetten. Als je dan binnen dit tekst een variabele wil gebruiken, dan zet je die tussen accolades.

```python
naam = "Saïd"
leeftijd = 23
print(f"Dag {naam}, ik heb vernomen dat je {leefijd} jaar oud bent.")
```

Eigenlijk is dit een verkorte notatie van de functie `format()`. Je zou dit kunnen herschrijven als:

```python
naam = "Saïd"
leeftijd = 23
begroeting = "Dag {}, ik heb vernomen dat je {} jaar oud bent."
print(begroeting.format(naam,leefijd))
```

De lege accolades zijn plaatsaanduidingen (placeholders). Je vult die dan concreet in met de format-functie.

Naast het eenvoudigweg invoegen van waarden in een string, kun je met de `format()`-functie ook formattering toevoegen aan de ingevoegde waarden. Hier zijn enkele  veelvoorkomende manieren om tekst te formatteren in Python.

**Centreren:** Je kunt tekst centreren in een bepaald aantal tekens met behulp van het `^`-teken in de plaatsaanduiding, gevolgd door een getal dat de breedte van de velden aangeeft. Hier is een voorbeeld:

```python
tekst = "Python"
gecentreerde_tekst = "{:^10}".format(tekst)
print(gecentreerde_tekst)
```

Deze code zal het woord 'Python' centreren in een veld van 10 tekens breed.

**Links uitlijnen:** Je kunt tekst links uitlijnen met behulp van het `<`-teken in de plaatsaanduiding, gevolgd door de breedte van het veld. Hier is een voorbeeld:

```python
tekst = "Python"
links_uitgelijnde_tekst = "{:<10}".format(tekst)
print(links_uitgelijnde_tekst)
```

**Rechts uitlijnen:** Je kunt tekst rechts uitlijnen met behulp van het `>`-teken in de plaatsaanduiding, gevolgd door de breedte van het veld. Hier is een voorbeeld:

```python
tekst = "Python"
rechts_uitgelijnde_tekst = "{:>10}".format(tekst)
print(rechts_uitgelijnde_tekst)
```

**Aantal decimalen:** Je kunt het aantal decimalen in een drijvende-kommagetal regelen met behulp van `.2f` (of een ander gewenst aantal decimalen). Hier is een voorbeeld:

```python
getal = 3.14159265
afgerond_getal = "{:.2f}".format(getal)
print(afgerond_getal)
```

Deze output zal het getal presenteren met twee decimalen: `3.14`.

Je kunt de `f`-notatie gebruiken om hetzelfde resultaat te  bereiken met de f-string syntaxis in Python. Hier is het voorbeeld met  de f-string notatie:

```python
getal = 3.14159265
print(f"Het getal pi is {getal:.2f}.")"
```

De output zal zijn: Het getal pi is 3.14.

## Argumenten

Scripts vragen niet alleen input van een gebruiker, maar je kan ook argumenten meegeven met een script. Neem bijvoorbeeld een script dat de omtrek van een rechtshoek berekent. Je roept het script als volgt aan:

```bash
python3 omtrek.py 5 10
```

Waarbij 5 de breedte en 10 de lengte van de rechthoek is. 

Je verwerkt dergelijke argumenten als volgt. In de module `sys` heb je de lijst `sys.argv`. Deze lijst bevat alle argumenten die zijn doorgegeven aan het script, inclusief de scriptnaam zelf als het eerste element (index 0) in de lijst.

Hier is een voorbeeld van hoe je `sys.argv` kunt gebruiken om argumenten te verwerken:

```python
import sys

# Het eerste element is de naam van het script zelf
script_naam = sys.argv[0]

# De rest van de elementen zijn de argumenten
argumenten = sys.argv[1:]

# Je telt het aantal argumenten als volgt
aantal_argumenten = len(sys.argv) - 1

# Je kunt de argumenten nu gebruiken
print("Scriptnaam:", script_naam)
print("Argumenten:", argumenten)
```

In het bovenstaande voorbeeld van de omtrek van een rechthoek, zou dit er als volgt uitzien:

```python
import sys

script_naam, breedte, lengte = sys.argv

omtrek = int(lengte) * int(breedte)
print(f"De omtrek is {omtrek}.")
```

We gaan dit script nog wat robuuster maken, door ook te testen op het aantal argumenten.

```python
import sys

if len(sys.argv) -1 != 2:
	print("Je moet twee argumenten geven, een lengte en een breedte.")
	sys.exit(1)

script_naam, breedte, lengte = sys.argv

omtrek = int(lengte) * int(breedte)
print(f"De omtrek is {omtrek}.")
```

Als het aantal argument verschillend is van twee, dan wordt er een foutbericht gegeven en wordt het script verlaten met foutcode 1, wat gelijk is aan een niet-succesvolle beëindiging (0 is succesvol).
