# Werken met bestanden

## Doelstellingen

Na dit hoofdstuk ben je in staat:

- een tekstbestand te openen en de informatie in te lezen (in zijn geheel of regel per regel) en te verwerken;
- tekst in een tekstbestand weg te schrijven (in zijn geheel of regel per regel);
- informatie aan een bestaand tekstbestand toe te voegen (op het einde);
- het lezen en schrijven van tekstbestanden uit te voeren met de `with`-structuur;
- fouten op te vangen met exeption handling;
- zelf excepties op te gooien;
- zelf excepties te definiëren;
- csv-bestanden in de lezen en te verwerken;
- informatie weg te schrijven naar een csv-bestand;
- bestanden en mappen te manipuleren (toevoegen, verwijderen, hernoemen, verplaatsen, ...);
- te navigeren in mappen;
- te testen of iets een bestand of een map is;
- gecomprimeerde bestanden in zip- of tar-formaat te maken;
- gecomprimeerde bestanden uit te pakken.

##  Bestanden lezen en verwerken

Om een bestand te kunnen lezen, gebruiken we de ingebouwde functie `open()`. Je creëert hiermee een object. Dat object moeten we achteraf ook wee sluiten met het commando `close()`.

De functie `open()` verwacht altijd een argument met  daarin de verwijzing naar de bestandsnaam. Als tweede optionele  parameter is er de 'mode' waarin je het bestand wil openen. De  verschillende modi zijn:

- 'r': openen voor enkel lezen (default).
- 'w': openen om te schrijven, maar eerst alle inhoud wissen.
- 'x': probeert het bestand aan te maken en geeft een fout als het bestand reeds bestaat.
- 'a': openen om te schrijven, inhoud op het einde toevoegen.

Je kan ook meegeven dat je het bestand als tekst ('t') of binaire  data ('b') wil openen. Standaard wordt een bestand als tekst geopend.

Als laatste optie is er het '+'-teken. Als je dat bij de modus plaatst, kan je zowel lezen als schrijven naar het bestand.

Zie ook de [officiële documentatie over open()](https://docs.python.org/3/library/functions.html#open).

We kunnen dit het beste illustreren met enkele voorbeelden:

```python
# Bestand openen om te schrijven. 
# Het bestand hoeft niet te bestaan
# Bestaat het wel, dan wordt de bestaande inhoud gewist! 
myFile = open("myTestFile.txt", 'w')
print(f"Het type van 'myFile' is: {type(myFile)}.")

# Een beetje tekst opslaan in het bestand.
myFile.write("Vives University of Applied Sciences")

# Bestand correct afsluiten
myFile.close()

# De inhoud lezen.
myFile = open("myTestFile.txt", 'r')
print(myFile.read())
myFile.close()  # niet vergeten opnieuw af te sluiten!
```

Python zoekt naar een bestand in de huidige map. Zoek je naar een bestand in een andere map, dan moet je het pad opgeven.

Wanneer de tweede keer de `read()` methode wordt aangeroepen  zonder argumenten, dan wordt de rest van het bestand ingelezen. Was de  methode nogmaals aangeroepen dan zou een lege string geretourneerd  worden. Dit betekent dat het einde van het bestand bereikt was. Je kan echter ook een beperkt aantal karakters inlezen.

```
myFile = open("myTestFile.txt", 'r')
print(myFile.read(20))  # Lees enkel de eerste 20 karakters.
print(myFile.read())  # Lees de rest van de file
myFile.close()
```

Zijn er meerdere lijnen om weg te schrijven, dan kan je één lange string wegschrijven die newline karakters bevat tussen de lijnen, of je kan  per lijn een nieuw write statement uitvoeren waarbij de string wordt  afgesloten met een newline. Bemerk dat de `write()` methode het aantal weggeschreven karakters retourneert.

```python
brief = open("brief.txt", 'w')
print(brief.write("Beste,\n"))  # vergeet de newline niet!
print(brief.write("Gelieve mij te contacteren.\n"))
print(brief.write("Vriendelijke groet,\nJos"))
brief.close()
```

Let er wel op dat wanneer een file in ‘write’ mode geopend wordt,  alle content van dat bestand wordt gewist. Indien er enkel iets  toegevoegd moet worden aan het bestand kan dit via twee wijzen aangepakt worden.

1. Het bestand wordt eerst ingelezen en de content wordt vervolgens  opgeslagen in een variabele. Aan die variabele wordt dan de extra tekst  toegevoegd. Vervolgens wordt die variabele weggeschreven naar het  bestand.
2. Het tekstbestand wordt in ‘append’ mode geopend. Op dezelfde wijze  als ‘write’ mode kan er data weggeschreven worden. Deze data wordt  automatisch toegevoegd op het einde van het bestand.

Indien het niet gewenst is om de content van een bestand in grote stukken te lezen, kan de methode `readlines()` gebruikt worden. Deze methode maakt een list waarvan elk element overeenkomt met een ingelezen lijn. Een voorbeeld:

```python
# tekstbestand creëren met meerdere lijnen
monty_python = open("monty_python.txt", 'w')

tekst = ("Monty Python is een Britse komediegroep.\n" + 
         "De groep staat bekend om het doorbreken van de toen conventionele komedieregels.\n" + 
         "De groep bestaat uit de volgende leden:\n" +  
         "\t- Graham Chapman\n" + 
         "\t- John Cleese\n" + 
         "\t- Terry Gilliam\n" + 
         "\t- Eric Idle\n" + 
         "\t- Terry Jones\n" + 
         "\t- Michael Palin")

monty_python.write(tekst)
monty_python.close()
```

```python 
# tekstbestand inlezen en inhoud uitprinten
monty_python = open("monty_python.txt", 'r')
tekst = monty_python.readlines()  # list van strings
monty_python.close()

print("".join(tekst))
```

Er is ook een methode `readline()` om de lijnen één voor één in te lezen, of je kan zelfs eenvoudig itereren over het `TextIOWrapper` object:

```python
monty_python = open("monty_python.txt", 'r')
read_next = True
while read_next:
  line = monty_python.readline()
  read_next = line != ""
  if read_next:
    print(line, end="")
monty_python.close()
```

```python
monty_python = open("monty_python.txt", 'r')
for line in monty_python:
  print(line, end="")  # end op lege string zetten omdat line al \n bevat
monty_python.close()
```

## Werken met excepties

[Python documentatie: errors and exceptions](https://docs.python.org/3/tutorial/errors.html)

[Overzicht van alle ingebouwde excepties in Python](https://docs.python.org/3/library/exceptions.html)

Tot nu toe hebben we telkens code geschreven waarbij we ervan uit gaan  dat de input correct is. Natuurlijk zou dit naïef zijn van ons moesten  we inderdaad geloven dat een gebruiker altijd de juiste input zal geven. Daarom bestaat er in Python en ook in andere programmeertalen een  manier om exceptions (uitzonderingen) en errors op te vangen.

We kennen natuurlijk de klassieke syntaxfout. Wanneer we een fout maken tegen de syntax van Python, zal het de interpreter zelf een exceptie opgooien, meer bepaald een syntaxfout.

```python
if False:
  print("onbereikbaar")
else
  print("enig uitvoerbaar statement")
```

Bij uitvoering zullen we de volgende fout krijgen:

```bash
File "<ipython-input-1-c85e64124321>", line 3
    else
        ^
SyntaxError: invalid syntax
```

Er kunnen ook andere redenen zijn waardoor een fout optreedt: we willen een bestand openen dat niet bestaat, we willen een variabelen met verschillende types combineren, we proberen te delen door 0, enzovoort. Al die zeken geven een uitvoeringsfout. Er wordt van een *exceptie* opgegooid. 

Python heeft heel wat [ingebouwde excepties](https://docs.python.org/3/library/exceptions.html). Voorbeelden van **ingebouwde excepties** zijn:

- `NameError`: wanneer een variabele niet is gedefinieerd;
- `TypeError`: wanneer een bewerking of functie wordt uitgevoerd op ongeldig datatype;
- `ValueError`: wanneer een functie argument een ongeldige waarde heeft;
- `ImportError`: wanneer een import statement niet lukt;
- `KeyboardInterrupt`: wanneer de gebruiker een programma onderbreekt, bijvoorbeeld met CTRL+C;
- `FloatingPointError`: wanneer een berekening met kommagetallen mislukt;
- `IndexError`: wanneer een opgegeven index niet bestaat in bijvoorbeeld een list;
- `KeyError`: wanneer een opgegeven key niet bestaat in de dictionary;
- `IOError`: wanneer een i/o bewerking faalt;
- `OSError`: een algemene fout van eht besturingssysteem, zoals een volle schijf, foute rechten, bestand niet gevonden, ...;
- `FileNotFoundError`: wanneer een file niet wordt teruggevonden;
- `ZeroDivisionError`: fout bij deling door 0.

De kunst bestaat erin dergelijke uitzonderlijke fouten te voorzien en ermee om te gaan. Dit doen we in een try-except-blok.

```python
try:
  result = 7/0
  print(result)
except:
  print("Oeps, jouw berekening liep fout... Maar je programma 'crasht' niet!")
```

In het **try**-block proberen we een handeling die potentieel fout kan lopen. In het **except**-blok definiëren we wat er moet gebeuren als het fout loopt. Je kan ook een specifieke soort fout opvangen en eventueel ook de oorspronkelijke boodschap weergeven. Dit doen we in het onderstaande voorbeeld:

```python
try:
  result = 7/0
  print(result)
except ZeroDivisionError as err:
  print(f"Error: {err}!")
```

Je kan **verschillende types excepties tegelijk opvangen**, en met een **algemeen except-blok** bepalen wat er moet gebeuren als er nog een ander type fout optreedt: 

```python
def division():
  try:
    numerator = int(input("Geef de teller van een breuk: "))
    denominator = int(input("Geef de noemer van een breuk: "))
    result = numerator / denominator
    print(f"De breuk heeft als resultaat: {result:.2f}.")
  except ZeroDivisionError as err:  # noemer is nul
    print(f"Error 1: {err}!")
  except ValueError as err:  # gebruiker geeft verkeerde input op
    print(f"Error 2: {err}!")
  except:  # onverwachte fout
    print("Error 3: unknown error at this moment...")
```

Als voor verschillende types excepties dezelfde handeling uitgevoerd moet worden, dan kan dit korter:

```python
except (RuntimeError, TypeError, NameError):
    pass
```



Met een **else**-blok bepalen we wat er moet gebeuren als er geen fout optreedt.

```python
try:
  result = x / y
except ZeroDivisionError as err:
  print(f"Error: {err}.")
else:
  print(f"Het resultaat van de deling is: {result:.2f}.")
```

Er bestaat ook een **finally**-block dat altijd uitgevoerd wordt. Dit wordt gewoonlijk gebruikt om externe bronnen zoals database- of netwerkverbindingen, zeker af te sluiten, wat er ook gebeurt.

```python
try:
    result = x / y
except ZeroDivisionError as err:
  print(f"Error: {err}.")
else:  # wordt uitgevoerd indien er geen exception was
  print(f"Het resultaat van de deling is: {result:.2f}.")  
finally:  # wordt altijd uitgevoerd
  print("Ik ben het finally gedeelte en word altijd uitgevoerd.")
```

Zelf een exeptie opgooien, doe je met het commando **raise**:

```python
if speed > 120:
  raise SpeedError("Speed too high!")
else:
  print("All cool.")
```

Een patroon dat we vaak zien, is excepties opvangen en dan toch een algemene exceptie opgooien die dan opgevangen wordt door een ander deel van het programma:

```python
import sys

try:
    f = open('myfile.txt')
    s = f.readline()
    i = int(s.strip())
except OSError as err:
    print("OS error:", err)
except ValueError:
    print("Could not convert data to an integer.")
except Exception as err:
    print(f"Unexpected {err=}, {type(err)=}")
    raise
```

We kunnen tenslotte ook **zelf excepties definiëren**. Dat doe je door een nieuwe klasse aan te maken die erft van `Exception`. Dat kan direct of indirect via een subklasse van `Exception`. Het volstaat om de naam van de superklasse mee te geven als 'parameter' bij de definitie de subklasse om die  laatste te laten erven van de eerste. Het is een goed idee om al jouw  eigen exceptions een naam te geven die eindigt met `Error`.

```python
class SpeedError(Exception):  # erft van klasse Exception
  def __init__(self, message):
    self.message = message


speed = 125
if speed > 120:
  raise SpeedError("Speed too high!")
else:
  print("All cool.")
```

## With

Het openen, uitlezen en sluiten van een bestand kan eigenlijk nog eleganter en veiliger met het statement `with`. 

Onderstaande voorbeelden gebruiken geen `with`: 

```
# file handling
```

 

```python
file = open('file_path', 'w')
file.write('hello world !')
file.close()
```

 We lopen hier een risico. Als er een exeptie optreedt, dan zal het bestand niet gesloten worden en dat kan nare neveneffecten geven. Om dat te vermijden zouden we een blok try-finally moeten gebruiken.

```python
file = open('file_path', 'w')
try:
  file.write('hello world')
finally:
  file.close()
```

Met `with` kan dit korter en eleganter.

```python
# using with statement
with open('file_path', 'w') as file:
  file.write('hello world !')
```

Je merkt op dat er geen `close()` gebeurt. Dit gebeurt nu automatisch, ongeacht of er een exceptie optreedt of niet.

## Bestanden verwerken

### Tekst in een bestand verwerken

Wanneer we tekstbestanden verwerken, is het goed om nog eens te wijzen op een aantal functies voor springmanipulatie:



`str.strip()`: de lege ruimte (spaties, tabs, ...) aan het begin en het einde worden verwijderd. We hebben ook `str.rstrip()` en `str.lstrip()` om enkel lege ruimte aan het einde of aan het begin te verwijderen.



`str.find(key_str, [start], [end])`: geeft -1 als key_str niet gevonden werd, en anders de laagste index waar die gevonden werd (binnen start en end).

Voorbeeld:

```python
s = '/test/in.txt'
waar_gevonden = s.find('in') # waar_gevonden is 6
```



`str.replace(old, new, [count])`: geeft een kopie terug waar *old* vervangen werd door *new*. Het argument _count_ beperkt het aantal keer dat de vervanging gebeurt.

```python
s = 'hello hello hello, world'
nieuwe_string = s.replace('ll', '**') #'he**o he**o he**o, world'
nieuwe_string = s.replace('ll', '**', 2) # 'he**o he**o hello, world'
```



`s.split([sep], [maxsplit=-1])`: geeft een lijst van woorden terug met *sep* als scheidingsteken. Als je hiervoor niets invult, neemt hij de spatie als scheidingsteken. Het argument *maxsplit* beperkt het aantal splits. Standaard is dit -1, dus onbeperkt.

```python
lijst = 'apple, orange, pear'.split()       # ['apple,', 'orange,', 'pear']
lijst = 'apple, orange, pear'.split(', ')   ['apple', 'orange', 'pear']
lijst = 'apple, orange, pear'.split(', ', maxsplit=1)  # ['apple', 'orange, pear']
```



`sep.join([str])`: doet het omgekeerde van een split. Dit zal de lijst van strings samenvoegen met *sep* als scheidingsteken. 

```python
', '.join(['apple', 'orange, pear']) # 'apple, orange, pear'
```

### CSV-bestanden verwerken

Een vaak gebruikt type tekstbestand is het csv-bestand. CSV staat voor "comma separated value". CSV-bestanden. Deze bestanden zijn vaak het resultaat van een export uit een Excelbestand of een tabel in een database. We gebruiken hiervoor in Python de [csv-module](https://docs.python.org/3/library/csv.html).

De functie `csv.reader(csv-bestand, dialect='excel', **fmtparams)` geeft een object terug waarmee we over de lijnen van een csv-bestand kunnen itereren. Het standaarddialect is *excel*, en dat is voor de meeste cases OK. Zogenaamd *fmtparams* zijn bijvoorbeeld:

- `delimiter`: het scheidingsteken. Dat is standaard een komma, meer bij sommige csv-bestanden kan dat ook iets anders zijn, zoals een puntkomma.
- `doublequote`: geeft aan hoe een de escape van dubbele aanhalingstekens gebeurt. Als dit *True* is, dan gebeurt dat door de dubbele aanhalingstekens te herhalen, anders wordt het escapesymbool gebruikt.
- `escape`: definieert het escapesymbool.
- `quoting`: definieert of de velden tussen aanhalingstekens staan. Dat gebeurt met een quotingconstante. De defaultwaarde is csv.QUOTE_MINIMAL.
  - csv.QUOTE_ALL: alles tussen aanhalingstekens
  - csv.QUOTE_MINIMAL: enkel velden met speciale tekens worden tussen aanhalingstekens gezet.
  - csv.QUOTE_NONNUMERIC: de niet-numerieke velden worden tussen aanhalingstekens gezet. De reader zal de velden die niet tussen aanhalingstekens staan als *float* inlezen.
  - csv.QUOTE_NONE: zet de velden nooit tussen aanhalingstekens.


In het onderstaande voorbeeld wordt een csv-bestand verwerkt met covidgegevens. Het scheidingsteken is een puntkomma.

```python
import csv

#  Ter info: 'with' is een compacte 'try-finally met close()'.
with open('covid.csv', newline='') as myCovidFile:
  
  myReader = csv.reader(myCovidFile, delimiter=';')
  print("The current delimiter is: " + myReader.dialect.delimiter) # ;

  # Merk op: next() geeft de volgende rij als list 
  # net als itereren met for over myReader 
  print("First row: " + str(next(myReader)))  # header
  largestNumberOfCases = 0
  for row in myReader:
    print(row)
    if int(row[4]) > largestNumberOfCases:
      largestNumberOfCases = int(row[4])

  print("The day with most COVID-cases in the list is: " + str(largestNumberOfCases))
```

We maken eerste een reader-object. De bestandsnaam is 'myCovidFile' en het scheidingsteken is een puntkomma. Met `next()` lezen we de eerste rij in en plaatsen we de pointer op de tweede rij. Daarna itereren we met een for-lus. De output zou er als volgt uitzien:

```text
The current delimiter is: ;
First row: ['dateReported', 'day', 'month', 'year', 'cases', 'deaths', 'country']
['6/10/2020', '6', '10', '2020', '314', '13', 'Belgium']
['5/10/2020', '5', '10', '2020', '748', '14', 'Belgium']
['4/10/2020', '4', '10', '2020', '1252', '14', 'Belgium']
['3/10/2020', '3', '10', '2020', '3222', '11', 'Belgium']
['2/10/2020', '2', '10', '2020', '3272', '15', 'Belgium']
...
['4/01/2020', '4', '1', '2020', '0', '0', 'Belgium']
['3/01/2020', '3', '1', '2020', '0', '0', 'Belgium']
['2/01/2020', '2', '1', '2020', '0', '0', 'Belgium']
['1/01/2020', '1', '1', '2020', '0', '0', 'Belgium']
['31/12/2019', '31', '12', '2019', '0', '0', 'Belgium']
The day with most COVID-cases in the list is: 3272
```

Op gelijkaardige wijze kan je ook data naar een csv-file wegschrijven met behulp van de csv-module. Die data kan je best structureren als een list van rijen, waarbij elke rij ook een list is.

Hieronder worden willekeurig gegenereerde neerslagwaarden per dag van een week opgeslagen als tabel:

```python
import random

days = ["monday", "tuesday", "wednesday", "thursday", "friday", "saturday", "sunday"]

table = []  # tabel is een list van rijen
for day in days:
  row = [day, random.randint(0, 100)]  # elke rij is een list van attributen
  table.append(row)
```

Vervolgens schrijven we de data weg naar een CSV-bestand. Kan je dat bestand openen in Excel om een grafiek van te maken?

```python
import csv

# Op een 'veilige' manier een CSV-bestand openen om te schrijven.
with open('rain.csv', 'w', newline='') as myRainyFile:
  myWriter = csv.writer(myRainyFile, delimiter=';')

  # Via een lus alle rijen in de tabel overlopen en wegschrijven naar het CSV-bestand.
  for row in table:
    myWriter.writerow(row)  
```

We zullen later zien dat we csv-bestanden op een nog krachtiger manier kunnen verwerken met de module *pandas*.

## Bestanden en mappen manipuleren

Om bestanden te manipuleren maken we gebruik van de modules `os`, `os.path` en `shutil`.

De module `os` bevat functies die eigen zijn aan het besturingssysteem, inclusief functies om bestanden te manipuleren.

### Over paden en bestandsnamen

Om bestandsnamen en paden te manipuleren hebben we de module `os.path` (zie [documentatie](https://docs.python.org/3/library/os.path.html)). Laten we enkele nuttige functies van `os.path` bekijken.

- `os.path.abspath(path)`: geeft het volledig pad van de gegeven directory .
- `os.path.basename(path)`: zal het laatste deel van het absolute pad geven. 
- `os.path.dirname(path)`: geeft alles van het pad behalve het laatste deel.
- `os.path.exists(path)`: geeft `True` als het pad van die map of het bestand bestaat.
- `os.path.join(path, *paths)`: plakt paden of onderdelen van paden aan elkaar, op een intelligente manier.
- `os.path.isdir(path)`: is `True` als het pad een map is.
- `os.path.isfile(path)`: is `True` als het pad een bestand is.



```python
# We zitten in de map /Users/pythonuser/
print(os.path.abspath(os.getcwd())) # getcwd() geeft het huidige pad. 
# resultaat van bovenstaand commando: /Users/pythonuser

print(os.path.basename(os.getcwd())) # pythonuser
print(os.path.dirname(os.getcwd())) # /Users
```

De functie `os.path.join()` verdient wel een speciale vermelding. De functie is intelligent op verschillende manieren:

- Hij filtert de directory separators (backslash (Windows) of slash (unixsystemen)) zodat er geen twee na elkaar komen in het resultaat.
- Hij zet een directory separator op het einde als dat nodig is.
- Als één element een absoluut pad is, worden de elementen ervoor weggegooid en begint het pad vanaf dat absolute pad.

```python
pad = os.path.join(os.getcwd(), 'file.txt'))
```

Bovenstaand stelt een correcte padnaam samen, bijv. `/Users/pythonuser/file.txt` ongeacht het besturingssysteem. De schuine streep zal in een Windowssysteem vervangen worden door een backslash.

### Bestanden kopiëren, verwijderen en verplaatsen

De shutil-module (shell utilities) biedt een aantal bewerkingen op  een hoger niveau dan de os-module aan voor bestanden en verzamelingen  van bestanden. In het bijzonder worden functies aangeboden die het  kopiëren en verwijderen van bestanden ondersteunen.

Met `shutil.copy()` kan je bijvoorbeeld een bestand kopiëren, zoals in onderstaand stukje code. Met `os.rename()` wordt de file hernoemd en `path.exists()` checkt of het te kopiëren bestand effectief bestaat.

```python
import os
from os import path
import shutil

if path.exists("myShUtilsTestFile.txt"):  # bestaat bestand?
  
  source = "myShUtilsTestFile.txt"  # te kopiëren bestand
  destination = "./temp/myShUtilsTestFile.txt"  # gekopieerd bestand
  
  if not path.exists("./temp"): os.mkdir("temp")  # maak directory "temp" als die nog niet bestaat
  file = shutil.copy(source, destination)  # kopieer bestand
  
  newname = "./temp/test.txt"
  os.rename(file, newname)  # hernoem bestand
```

### Mappen manipuleren
Een specifieke type bestand is een map of directory. De bestanden in een map **oplijsten** kan je met de functie `scandir()`
```python
import os

with os.scandir('my_directory/') as entries:
    for entry in entries:
        print(entry.name)
```

De functies `os.scandir()` geeft een lijst van objecten terug, één object per bestand of map in 'my_directory'. We hebben die lijst hier 'entries' genoemd. Met het `with`-statement creëren we een context waarin we gaan itereren over de elementen van `entries`. Door `with` garanderen we dat de systeembronnen na de iteratie automatisch vrijgegeven worden. We itereren over de lijst van elementen in de map en we drukken de naam van elk element af. Het resultaat is vergelijkbaar met wat een commando `ls` of `dir` zou doen.

Elk object `entry` in dit voorbeeld bevat meer dan alleen de naam van de bestanden of mappen. We hebben ook allerlei andere eigenschappen van het object. We kunnen bijvoorbeeld testen of het een bestand is met `entry.is_file()`. Vergelijkbaar is de functie `entry.isdir()`.

Een **map maken** doe je met de functie `os.mkdir('naam_map')`. Pas op, als de map al bestaat, wordt de exceptie `FileExistsError` opgegooid. Je kan een map met submappen maken met `os.mkdirs('map/submap/subsubmap')`.

Een **map verwijderen** doe je met het commando `os.rmdir('naam_map')`. Als een map niet leeg is, zal er een `OSError` optreden. Met os.removedirs() zal je een map en alle onderliggende mappen verwijderen, maar dit werkt enkel met lege mappen. In de module `shutil` heb je wel een functie `shutil.rmtree` waarmee je een map en alle onderliggende bestanden en mappen in één keer kan verwijderen.

Je kan de **huidige map opvragen** met `os.getcwd()`.

**Wijzigen van map**: `os.chdir()`.

## Gecomprimeerde bestanden

De module `shutil` bevat ook functies om met gecomprimeerde bestanden te werken. Dat kunnen zip-bestanden of tar-bestanden zijn.

```python
from shutil import make_archive
make_archive("sample_data_archive", "zip", "./sample_data")  # De hele map 'sample_data' zippen.
```

In feite maakt de functie `make_archive()` achter de schermen gebruik van de modules "zipfile" en "tarfile":

```python
from zipfile import ZipFile
with ZipFile("file.zip", "w") as newzip:
  newzip.write("myShUtilsTestFile.txt")  # Voeg bestand toe aan Zip.
```

```python
with ZipFile('file.zip', 'r') as zipObj:
   # unzip de zip-file en plaats de inhoud in folder 'temp'
   # geef je geen folder op, dan komt de inhoud in de huidige directory terecht
   zipObj.extractall('temp')  # 'temp' hoeft nog niet te bestaan
```
