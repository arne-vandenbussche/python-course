# Functies

## Doelstellingen

Na dit hoofdstuk moet je in staat zijn om:

- modules en functies te importeren en die functies te gebruiken,
- functies toe te kennen aan een variabele of als argument in een andere functie gebruiken,
- zelf functies te definiëren,
- anonieme of lambda-funties te definiëren en te gebruiken,
- functies met default-argumenten te definiëren en te gebruiken,
- een script te schrijven met functies waarbij je een onderscheid maakt tussen de direct uitvoerbare code en de importeerbare functies (`if __name__ == "__main__:`")
- de functie `dir()` te gebruiken.

## Uit de documentatie van Python

[functies](https://docs.python.org/3/reference/compound_stmts.html#function)

[modules](https://docs.python.org/3/tutorial/modules.html)

[top-level code environment](https://docs.python.org/3/library/__main__.html?highlight=__name__%20__main__)


## Functies en modules

### Ingebouwde functies

We hebben in eerdere hoofdstukken al gebruikt gemaakt van ingebouwde functies en functies uit de *math*-library. We hebben functies aangeroepen met de naam van de functies, met de parameters tussen haakjes. De functie geeft dan een waarde terug.

```python
maximum = max(1, 3, 5, 6) # 6
```

### Functies uit modules

Als de functie niet ingebouwd is, maar behoort tot een bepaalde module, dan moeten we die module of de functie zelf importeren.

In onderstaand voorbeeld importeren we de module *math* en gebruiken we de functie die de vierkantswortel berekent.

```python
import math
vierkantswortel = math.sqrt(2)
```

We kunnen ook de functie zelf importen:

```python
from math import sqrt
vierkantswortel = sqrt(4)
```

Bij het importeren kunnen we de functie ook een eigen naam geven:

```python
from math import sqrt as squareroot
vierkantswortel_honderd = squareroot(100)
```

### Functies als variabele of parameter

Een functie kan ook aan een variabele worden toegekend:

```python
fnc = my_function
fnc()
```

   Op die manier kan je ook een functie als argument doorgeven aan een andere functie:

```
def minmax(x, y, z, func):
  return func(x, y, z)
```

```
print(minmax(1, 2, 3, min))
print(minmax(1, 2, 3, max))
```

We zullen van deze mogelijkheid nog gebruik maken bij het filteren, opbouwen of sorteren van lijsten.

## Functies definiëren

### Zelf een functie definiëren

In Python kan je ook zelf functies definiëren door gebruik te maken van het keyword "def". Bijvoorbeeld:

```python
def my_function():
  print("Hello from a function!")
```

```python
my_function() # output: Hello from a function!
```

 Python maakt geen gebruik van accolades of het keyword "end" om het  einde van de functie aan te geven. In Python is het inspringen van code  (Engels: indentation) onderdeel van de syntax, wat in het geval van een  functie betekent dat alle ingesprongen code na de dubbele punt deel  uitmaakt van de functie!  
In het volgende voorbeeld verklaart dit waarom de derde print statement eerst wordt uitgevoerd:

```
def my_function_2():
  print("First print is inside function")
  print("Second print is inside function")
print("Third print is outside function")
my_function_2()
```

Om je code te laten inspringen maak je gebruik van de tab-toets. Editors zetten die om naar vier spaties. Editors die het coderen van Python ondersteune, laten de code na een dubbele punt automatisch inspringen.

### Default-argumenten

Bij het definiëren van een functie kan je ook default-argumenten meegeven. Deze argumenten hoeven bij het aanroepen niet gedefinieerd te zijn. Als ze niet gedefinieerd zijn, dan krijgen de de defaultwaarde. Als we één defaultargument hebben, dan plaatsen we die aan het einde aangezien argumenten normaal gezien van links naar rechts geëvalueerd worden.

```python
def display_info(name, age, country="Unknown"):
    print(f"Name: {name}")
    print(f"Age: {age}")
    print(f"Country: {country}")

# Call the function providing all arguments
display_info("Alice", 30, "USA")
# Outputs:
# Name: Alice
# Age: 30
# Country: USA

# Call the function without providing the country
display_info("Bob", 25)
# Outputs:
# Name: Bob
# Age: 25
# Country: Unknown
```

Wanneer er meerdere defaultargumenten zijn, dan moeten we wij het aanroepen van de functie expliciet de naam van het argument vermelden. We noemen dit *keyword argumentst*. Dat kunnen we ook doen bij gewone argumenten, trouwens.

```python
def display_info(name="Unknown", age=0, country="Unknown"):
    print(f"Name: {name}")
    print(f"Age: {age}")
    print(f"Country: {country}")

# Call the function providing all arguments using keyword arguments
display_info(name="Alice", age=30, country="USA")
# Outputs:
# Name: Alice
# Age: 30
# Country: USA

# Call the function providing only the country
display_info(country="Canada")
# Outputs:
# Name: Unknown
# Age: 0
# Country: Canada

# Call the function providing age and country, but out of order
display_info(country="UK", age=40)
# Outputs:
# Name: Unknown
# Age: 40
# Country: UK
```

### Eigen ontwikkelde modules

We kunnen ook functies gebruiken uit eigen ontwikkelde modules. Elk Pythonbestand is een module. Als we bijvoorbeeld een Pythonbestand mijnfuncties.py hebben met de volgende code:

```python
# mijnfuncties.py
def welkom(naam):
  print(f"Welkom {naam}")
        
def goedemorgen(naam):
	print(f"Goedemorgen {naam}")
```

Dan kunnen we in dezelfde map een ander bestand begroeting.py ontwikkelen die er dan zo uitziet:

```python
# begroeting.py
from mijnfuncties import welkom, goedemorgen
naam = input("Geef je naam: ")
welkom(naam)
goedemorgen(naam)
```

We zullen in een later hoofdstuk zien hoe we complexere structuren van modules kunnen definiëren met *packages*.

### if \_\_name\_\_ == " \_\_main\_\_" 

Wanneer we een script schrijven dat functies bevatten, moeten we er rekening mee houden dat er een moment kan komen dat andere stukken code dit script als module kunnen importeren om gebruik te kunnen maken van die functie. In dat geval is het de bedoeling dat de functies gebruikt worden, maar niet dat het script bij het importeren onmiddellijk uitgevoerd wordt. 

We moeten dus in ons script een onderscheid maken tussen top-level code, dat is code die direct in het aangeroepen script staat en daar uitgevoerd wordt, en code die in functies verpakt zit. Wanneer we Pythonbestand met functies én met top-level code hebben, dan zullen we de top-level code laten voorafgaan door `if __name__ == '__main__':`. 

De variabele `__name__` bevat de naam van de actieve module. Als het script direct aangeroepen wordt (en niet vanuit een import), dan krijgt dia variabele de waarde `"__main__"`. Het bovenstaade statement betekent dus: voer deze code enkel uit wanneer dit bestand rechtstreeks aangeroepen wordt en voer dit niet uit bij een import. Je kan om die manier een script definiëren dat op zichzelf kan uitgevoerd worden, maar waarvan de functies ook bij een import gebruikt kunnen worden.

```python 
def greet(name):
    return f"Hello, {name}!"

def main():
    user_name = input("Enter your name: ")
    message = greet(user_name)
    print(message)

if __name__ == '__main__':
    main()
```

Als het script op zichzelf (stand-alone) uitgevoerd wordt, dan wordt de functie `main()` aangroepen, maar je kan ook in een ander script een import doen. `main()` wordt dan niet automatisch aangeroepen bij het uitvoeren van het import-statement, maar je kan de functie `greet()` en `main()` in dat andere script aangroepen op een moment dat je dat zelf wil.

### Anonieme functies (lambda)

Wanneer de code binnen een functie kort is, dan definiëren we deze graag als een anonieme functie of een lambda-functie. Een lambda-functie kunnen we dan toekennen aan een variabele of meegeven als argument aan een andere functie.

Een lambda-functie bestaat uit de volgende onderdelen:

- het sleutelwoord *lambda* (naar de Griekse letter 'l'),
- de lijst van argumenten
- een dubbelepunt, 
- het returnstatement (zonder het sleutelwoord *return*).

```python
som = lambda x, y: x + y
print(som(1, 2)) # output: 3
```

In onderstaand voorbeeld definiëren we een functie `minmax()` die zelf een functie als één van zijn argumenten heeft. We kunnen dit argument als een lambdafunctie definiëren.

```python
def minmax(x, y, z, func):
  return func(x, y, z)

mijn_functie = lambda x, y, z: (x + y + z) # lambda-functie toekennen aan een variabele
print(minmax(2, 3, 4, mijn_functie)) # output: 9
      
# lambdafunctie direct definiëren in de aanroep
print(minmax(2, 3, 4, lambda x, y, z: (x * y * z))) # output: 24
      
# idem, maar met expliciete benoeming van de argumenten
print(minmax(x=2, y=3, z=4, func=lambda x, y, z: ((x + y) ** z))) # output: 625
```

We zullen bij de filter en sorteerfunctie graag gebruik maken van lambda-functies.

## De functie dir()

Wanneer we een module gebruiken, willen we graag weten welke attributen of functies die module bevat. Dat kunnen we met de dir-functie. 

Willen we bijvoorbeeld weten welke functies de module random heeft, dan kunnen we dat als volgt doen:

```python
>>> import random
>>> dir(random)
['BPF', 'LOG4', 'NV_MAGICCONST', 'RECIP_BPF', 'Random', 'SG_MAGICCONST', 'SystemRandom', 'TWOPI', '_ONE', '_Sequence', '_Set', '__all__', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', '_accumulate', '_acos', '_bisect', '_ceil', '_cos', '_e', '_exp', '_floor', '_index', '_inst', '_isfinite', '_log', '_os', '_pi', '_random', '_repeat', '_sha512', '_sin', '_sqrt', '_test', '_test_generator', '_urandom', '_warn', 'betavariate', 'choice', 'choices', 'expovariate', 'gammavariate', 'gauss', 'getrandbits', 'getstate', 'lognormvariate', 'normalvariate', 'paretovariate', 'randbytes', 'randint', 'random', 'randrange', 'sample', 'seed', 'setstate', 'shuffle', 'triangular', 'uniform', 'vonmisesvariate', 'weibullvariate']
```

Dit kunnen we op elk object toepassen: een ingebouwde module, een geïnstalleerde module, een eigen geschreven module, een variabele, een object van een klasse, enzovoort.

