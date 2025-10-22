# Collecties : list, tuples, sets, dictionaries

## Doelstellingen

Na dit hoofdstuk kan je omgaan met lists, tuples, sets en dictionaries:

* elementen opvragen, toevoegen, verwijderen, wijzigen (waar mogelijk),
* de in-operator correct toepassen,
* collecties samenvoegen,
* de set-operaties (union, intersect, difference, ...) toepassen,
* de collectie kopiëren,
* lists en tuples sorteren,
* filteren en opzetten naar een gewijzigde collectie (map()),
* gebruik maken van comprehensions,
* de json-module gebruiken om een dictionary of een lijst van dictionaries om te zetten naar json en omgekeerd.

## Lists

Lists hebben we al in een vorige les besproken. Dit hoofdstuk is dus voor het grootste deel herhaling van wat we al gezien hebben.

### Kenmerken

Lists hebben de volgende eigenschappen:

- ze zijn **geordend**;
- ze zijn **heterogeen**, wat betekent dat de elementen niet van hetzelfde datatype hoeven te zijn;
- ze zijn **veranderlijk** (Engels: mutable), wat wil zeggen dat hun elementen kunnen worden gewijzigd, en dat je elementen kan toevoegen of verwijderen.

### Lists creëren

Lists worden gecreëerd met behulp van **vierkante haakjes**:

```python
lst0 = []  # lege list
lst91 = list() # lege list
lst1 = [1, 2, 3, 4]  # kan getallen bevatten
lst2 = ["Jan", "Piet", "Joris", "Korneel"]  # kan strings bevatten
lst3 = [3.1415, "pi", True, lst1]  # kan elementen van verschillende datatypes bevatten
```

### Het aantal elementen opvragen

De lengte van een list vraag je op met de functie **len()**:

```python
print(len(lst2)) # 4
```

### Elementen selecteren en vervangen

Je kan gebruik maken van de **slice** operator om elementen te selecteren of te vervangen:

```python
print(lst1[0])  # let op! het eerste element heeft 0 als index!
print(lst1[1:3]) # [2, 3], bij slicing is laatste element niet ingebrepen
lst3[1] = lst3[1].upper()  # [3.1415, 'PI', True, [1, 2, 3, 4]]
print(lst3)
```

Een variable waaraan een list is toegekend bevat de **referentie** naar deze list:

```python
lst1[-1] = 10  # laatste element vervangen [1, 2, 3, 10]
print(lst1) # [1, 2, 3, 10]
print(lst3[-1])  # [1, 2, 3, 10] laatste element in lst3 is lst1 en is dus ook gewijzigd!
```

### Een lijst doorlopen en zoeken in een lijst

Met een **for**-lus en de **in**-operator kan je de verschillende elementen van een list overlopen:

```python
for num in lst1:
  print(num, end="\t")
```

Met de **in**-operator kan je ook checken of een list een bepaald element bevat:

```python
if "Piet" in lst2:
  print("Piet is een man met baard!")
else:
  print("Piet heeft geen baard...")
```

Je kan ook de index van een element opvragen:

```python
lst2.index("Victor") # 0
lst2.index("Alice") # ValueError. 'Alice' is not in list
```
### De functie `enumerate()`

Wanneer je over een lijst iterereert, heb je vaak zowel de **index**
(positie) als de **waarde** van elk element nodig.\
Je *zou* zelf een teller kunnen bijhouden, maar Python biedt een veel
elegantere manier: de ingebouwde functie **`enumerate()`**.

#### Voorbeeld zonder `enumerate()`

``` python
fruits = ["appel", "banaan", "kers"]

index = 0
for fruit in fruits:
    print(index, fruit)
    index += 1
```

#### Voorbeeld met `enumerate()`

``` python
fruits = ["appel", "banaan", "kers"]

for index, fruit in enumerate(fruits):
    print(index, fruit)
```

Uitvoer:

    0 appel
    1 banaan
    2 kers

Standaard begint `enumerate()` te tellen vanaf `0`, maar je kunt ook een
andere startindex opgeven:

``` python
for index, fruit in enumerate(fruits, start=1):
    print(index, fruit)
```

Uitvoer:

    1 appel
    2 banaan
    3 kers

Dit maakt je code overzichtelijker, meer "Pythonic", en minder
foutgevoelig wanneer je zowel de index als de waarde van elk element in
een lijst nodig hebt.

### Elementen toevoegen

Met de **extend()**, **append()** en **insert()** methodes kan je element toevoegen:

```python
lst1.extend([5, 6, 7, 8, 9, 10])  # voegt lists samen
print(lst1)
lst2.append("Bernard")  # element wordt achteraan de list toegevoegd
lst2.insert(0, "Norbert")  # element wordt toegevoegd op positie 0
print(lst2)
```

### Elementen verwijderen

Met de methode **pop()** kan je een element uit de list halen, en dat element wordt geretourneerd:

```python
print(lst3.pop())  # laatste element uit de lijst halen
print(lst3)
print(lst3.pop(0))  # element op positie 0 uit de lijst halen
print(lst3)
```

Met methode **remove()** kan je een gegeven waarde uit een list verwijderen, en met **del** kan je elementen verwijderen aan de hand opgegeven indices:

```python
lst2.remove("Norbert")  # element "Norbert" verwijderen
del lst2[-1]  # laatste element verwijderen
print(lst2)
```

### Enkele nuttige methodes en functies

Een list kan je omdraaien op de volgende manieren:

```python
lst2.reverse()
print(lst2) # ['Korneel', 'Joris', 'Piet', 'Jan']
lst2 = lst2[::-1]
print(lst2) # ['Jan', 'Piet', 'Joris', 'Korneel']
```

 Op een list met numerieke waarden kan je volgende functies toepassen:

```python
print(sum(lst1))  # retourneert de som van alle elementen
print(max(lst1))  # retourneert het element met de maximale waarde
print(min(lst1))  # retourneert het element met de minimale waarde
print(lst1)
```

Methodes count() en index() zijn ook heel praktisch:

```python
lst = [1, 2, 3, 4, 5, 4, 3, 2, 1]
print(lst.count(3))  # telt hoeveel keer het element 3 voorkomt in de list (2)
print(lst.index(2))  # geeft de (eerste) index weer van het element 2 (1)
```

### Lists samenvoegen

Samenvoegen van twee of meer lists kan met de plus-operator:

```python
abc = ["a", "b", "c"]
de = ["d", "e"]
fghi = ["f", "g", "h", "i"]
print(abc + de + fghi)
# ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i']
```

### Lists kopiëren

Wanneer je dezelfde list aan verschillende variabelen toekent, dan  wordt de referentie naar die list gekopieerd. M.a.w. de variabelen  verwijzen of refereren naar dezelfde list. Wil je echter de waarden  kopiëren naar een nieuwe list, dan gebruik je de methode **copy()**:

```python
abc1 = ["a", "b", "c"]
abc2 = abc1  # abc1 en abc2 verwijzen naar dezelfde list
abc2.append("d")
print("abc1:", abc1) # abc1: ['a', 'b', 'c', 'd']
print("abc2:", abc2) # abc2: ['a', 'b', 'c', 'd']
```

```python
abc3 = abc1.copy()  # abc3 is een nieuwe list met dezelfde waarden als abc
abc3.append("e")
print("abc1:", abc1) # abc1: ['a', 'b', 'c', 'd']
print("abc3:", abc3) # abc3: ['a', 'b', 'c', 'd', 'e']
```

 In dat verband is het ook interessant om het verschil tussen  operators "==" en "is" uit te leggen: de eerste checkt of de inhoud van  twee variabelen gelijk is (Engels: value equality), de tweede checkt of  de referenties gelijk zijn, m.a.w. of de variabelen naar hetzelfde  object verwijzen (Engels: reference equality):

```python
abc3.pop()  # "e" opnieuw verwijderen
print("abc1:", abc1)
print("abc3:", abc3)
print("abc1 == abc2:", abc1 == abc2)  # zelfde inhoud, dus True
print("abc1 is abc2:", abc1 is abc2)  # zelfde object, dus True
print("abc1 == abc3:", abc1 == abc3)  # zelfde inhoud, dus True
print("abc1 is abc3:", abc1 is abc3)  # verschillende objecten, dus False
```

Let op! Omdat lists geordend zijn, zijn lists niet alleen gelijk (==) als ze dezelfde waarden hebben, maar de waarden moeten ook in dezelfde  volgorde staan!

```python
abc4 = ['d', 'c', 'b', 'a']
print("abc1:", abc1) # abc1: ['a', 'b', 'c', 'd']
print("abc4:", abc4) # abc4: ['d', 'c', 'b', 'a']
print("abc1 == abc4:", abc1 == abc4) # abc1 == abc4: False
```

## Tuples

### Kenmerken

Tuples hebben de volgende eigenschappen:

- ze zijn **geordend**;
- ze zijn **heterogeen**, wat betekent dat de elementen niet van hetzelfde datatype hoeven te zijn;
- ze zijn **onveranderlijk** (Engels: immutable), wat wil zeggen dat hun elementen niet kunnen worden gewijzigd, en je kan geen  elementen toevoegen of verwijderen.


 Doordat ze onveranderlijk zijn, zijn tuples sneller om over te  itereren in vergelijking met lists. Bovendien is het omwille van die  eigenschap ook veiliger om voor een tuple te kiezen wanneer je met een  reeks constante waarden moet werken.

### Tuples creëren

Net als een list bestaat een tuple uit een aantal waardes die van  elkaar gescheiden zijn met komma’s. Meestal worden tuples geschreven met **ronde haakjes** eromheen, maar de haakjes zijn niet noodzakelijk (behalve in omstandigheden waar anders verwarring zou ontstaan). Bijvoorbeeld:

```python
t1 = ("appel", "mango")
t2 = "banaan", "kers"
print(t1, "is een object van", type(t1))
# ('appel', 'mango') is een object van <class 'tuple'>

print(t2, "is een object van", type(t2))
# ('banaan', 'kers') is een object van <class 'tuple'>
```

Je kan dus in een tuple verschillende data types mixen:

```python
t1 = ("appel", 3, 1.4)
t2 = ("appel", 3, 1.4, ("banaan", 5))
```

Een lege tuple creëer je als volgt:

```python
empty_tuple = ()
print(empty_tuple) # ()
print(type(empty_tuple)) # <class 'tuple'>
```

Maar let op, want een tuple met slechts één element definieer je als volgt:

```python
t = (2, )
print(t) # (2,)
print(type(t)) # <class 'tuple'>
```

Wanneer je zou schrijven `t = (2)`, dan zit in variabele t gewoon het getal 2, omdat je een getal met ronde haakjes mag omsluiten:

```python
t = (2)
print(t) # 2
print(type(t)) # <class 'int'>
```

### Tuples zijn onveranderlijk

Waar tuples verschillen van lists is dat ze **onveranderlijk** zijn. Dit commando geeft dus een foutmelding:

```python
fruit[-1] = "mango"
```

```
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-37-a16fa0115673> in <module>()
----> 1 fruit[-1] = "mango"

TypeError: 'tuple' object does not support item assignment
```

Omdat tuples onveranderlijk zijn, hebben ze geen methodes om elementen toe te voegen of te verwijderen.

```python
fruit.pop()
```

```
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-38-971343bd48cc> in <module>()
----> 1 fruit.pop()

AttributeError: 'tuple' object has no attribute 'pop'
```

Dit kan wel, maar denk eraan dat je in feite een nieuwe tuple toekent aan tuple_fruit:

```python
tuple_fruit = ("appel", "banaan", "kers", "mango")
print(tuple_fruit) # ('appel', 'banaan', 'kers', 'mango')
tuple_fruit = tuple_fruit[::-1]
print(tuple_fruit) # ('mango', 'kers', 'banaan', 'appel')
```

### Aantal elementen opvragen

Net als bij lists kan je de **len()** functie gebruiken om te bepalen hoeveel elementen een tuple bevat:

```python
t1 = ("appel", "mango")
t2 = ("appel", 3, 1.4)
t3 = ("appel", 3, 1.4, ("banaan", 5))
print(len(t1)) # 2
print(len(t2)) # 3
print(len(t3))  # 4
```

Merk op dat in dit voorbeeld de lengte van t3 gelijk is aan 4, en niet 5. Het laatste element van t3 is de tuple ("banaan", 5), wat telt als één element.

### De in-operator

Je kunt met de **in**-operator een **for**-lus gebruiken om de elementen van een tuple te doorlopen, net als bij een list:

```python
t1 = ("appel", 3, 1.4, ("banaan", 5))
for element in t1:
  print(element)
```

Met diezelfde **in**-operator kan je ook testen of een element onderdeel van een tuple is:

```python
t1 = ("appel", "banaan", "kers")
print("banaan" in t1) # True
print("mango" in t1) # False
```

### Tuples en het toekennen van variabelen

Zoals we eerder al gezien hebben staat Python toe om meerdere  variabelen links van de assignment operator te plaatsen (unpacking). In feite vormen die variabelen samen een tuple. Dit is een uitzondering op de regel dat slechts één variabele links van de assignment operator staat. De  waardes aan de rechterkant worden één voor één naar de linkerkant  gekopieerd, van links naar rechts.

```python
a, b = "appel", "banaan"
print(a) # appel
print(b) # banaan
```

Dit is equivalent, omdat we de elementen van een tuple tussen ronde haakjes mogen plaatsen:

```python
(a, b) = "appel", "banaan"
print(a) # appel
print(b) # banaan
```

Je kan dus haakjes om de variabelen aan de linkerkant zetten, maar je kan ook haakjes rond de waarden aan de rechterkant zetten; dat maakt  geen verschil. Als je meer variabelen aan de linkerkant zet dan waarden  aan de rechterkant, krijg je een runtime error. Hetzelfde geldt voor minder, met als uitzondering als je precies één variabele plaatst, maar  in dat geval wordt een tuple van de waarden aan de variabele toegekend:

```python
a = 1, 2, 3
print(a) # (1, 2, 3)
```

Hieronder is een voorbeeld waarin het plaatsen van ronde haakjes noodzakelijk is:

```python
t1, t2 = ("apple", "banaan"), "kers"
print(t1) # ('apple', 'banaan')
print(t2) # kers
```

 Tuples kan je trouwens ook 'unpacken':

```python
fruit = 'apple', 'banana', 'cherry'  # variabele fruit is een tuple met 3 elementen
print(fruit) # ('apple', 'banana', 'cherry')
fruit1, fruit2, fruit3 = fruit  # ken de 3 elementen van fruit toe aan 3 verschillende variabelen
print(fruit2) # banana
```

###  Tuples en functie output

Zoals we eerder hebben gezien kunnen functies slechts één variabele  retourneren. Willen we echter meerdere waarden retourneren, dan kunnen  we gebruik maken van een tuple:

```python
def stats(values):
    m = min(values)
    mx = max(values)
    mn = sum(values) / len(values)
    return m, mx, mn

out = stats([1, 3, 5, 10])  # list as input
print(out) # (1, 10, 4.75)
print(type(out)) # <class 'tuple'>
print()

out = stats((10, 30, 50, 100))  # tuple as input
print(out) # (10, 100, 47.5)
print(type(out)) # <class 'tuple'>
print()

m, mx, mn = stats((1, 2, 3))  # output toekennen aan 3 variabelen
print(m, mx, mn) # 1 3 2.0
```

De functie stats (afkorting voor statistics) kan als inputargument  een list of tuple van waarden krijgen omdat de functies min(), max() en  sum() voor beide datatypes zijn gedefinieerd. Dit noemt men "**duck typing**", wat betekent dat het datatype van de parameter niet belangrijk is  zolang de functies die op die parameter worden toegepast werken. Het  concept van "duck typing" is gerelateerd aan "**dynamic typing**" dat ervoor zorgt dat je het datatype niet moet declareren als je een variabele declareert.

### Elementen selecteren

Net als bij lists, kan je individuele elementen van een tuple benaderen via **indices**:

```python
fruit = ("appel", "banaan", "kers", "doerian")
print(fruit[2])  # derde element, want indices beginnen bij 0 (kers dus)
```

Door middel van **slicing** kan je ook sub-tuples maken, met dezelfde regels als bij lists. Een sub-tuple is ook weer een tuple:

```python
print(fruit[1:4]) # ('banaan', 'kers', 'doerian')
print(type(fruit[1:4])) # <class 'tuple'>
```

Het volgende statement is equivalent:

```python
print(fruit[1:]) # ('banaan', 'kers', 'doerian')
```

En ook bij tuples kan je gebruik maken van negatieve indices:

```python
print(fruit[1:3]) # ('banaan', 'kers')
print(fruit[1:-1]) # ('banaan', 'kers')
```

Gebruik makend van indices kan je ook op de volgende wijze door de elementen van een tuple gaan:

```python
for i in range(len(fruit)):
  print(fruit[i])

print()

i = 0
while i < len(fruit):
  print(fruit[i])
  i += 1
```

De versie met in-operator is echter eenvoudiger en meer leesbaar. We raden deze ook aan.

```python 
for piece_of_fruit in fruit:
    print(piece_of_fruit)
```

The functie **index()** wordt gebruikt om de index van een element te bepalen, maar bepaald van de eerste keer dat dit element voorkomt. Als het element niet bestaat, dan krijgen we een ValueError.


```python
my_tuple = (10, 20, 30, 40, 20)
index_of_20 = my_tuple.index(20)
print(index_of_20) # 1
```

Je ook een gebied afbakenen waarbinnen je wil zoeken. Je kan de startpositie en de eindpositie meegeven.

```python
index_of_20 = my_tuple.index(20, 2)  # Start searching from index 2
print(index_of_20) # 4
```

Tuples hebben ook een **count()**-methode:

```python
t = (1, 2, 3, 4, 3, 2, 1)
print(t.count(3))  # geeft aan hoeveel keer het element 3 in de tuple voorkomt (2)
```

Zoals we eerder al opmerkten, kan je testen of een element voorkomt in een tuple, met de in-operator. Deze operator geeft True als het element voorkomt in de tuple en False als dat niet zo is:


```python
my_tuple = (10, 20, 30, 40)

# ga na of 20 in het tuple voorkomt
is_present = 20 in my_tuple
print(is_present) # True

# Ga na of 50 in het tupe voorkomt
is_present = 50 in my_tuple
print(is_present) # False
```

Zoals eerder vermeld, gebruiken we `in` ook om te itereren door een tuple.

```python
my_tuple = (10, 20, 30, 40)

# Itereer door het tuple, druk de elementen af, gescheiden door tab.
for item in my_tuple
    print(item, end="\t")
```

### Rekenen met tuples

Net als bij lists kan je de **max()** en de **min()** functies gebruiken om het maximum respectievelijk het minimum te  bepalen van een tuple die bestaat uit getallen. Je kunt de elementen van een tuple met numerieke elementen bij elkaar optellen met de **sum()** functie:

```python
t1 = (327, 419, 101, 667, 925, 225)
print(max(t1)) # 925
print(min(t1)) # 101
print(sum(t1)) # 2664
```

### Tuples samenvoegen en elementen herhalen

Net als lists en strings, kan je tuples samenvoegen of concateneren met de plus-operator:

```python
a = (1, 2, 3)
b = (4, 5)
print(a + b) # (1, 2, 3, 4, 5)
```

Het resultaat van a + b is een nieuwe tuple.

Je kan de *-operator gebruiken om elementen te herhalen in een tuple.

```python
my_tuple = (1, 2, 3)

repeated_tuple = my_tuple * 3
print(repeated_tuple) # (1, 2, 3, 1, 2, 3, 1, 2, 3)
```

### Tuples sorteren en omkeren

Tuples zijn onveranderlijk. Dit betekent dat je een tuple niet zomaar kan sorteren, maar wat je wel kan doen, is een nieuw gesorteerd tuple creëren.


```python
print(sorted(fruit, reverse=True))
```

Een tuple omkeren kan op twee manieren: met slicing of met de functie `reversed()`.

```python
t = (1, 2, 3, 4)
reversed_t = t[::-1]
print(reversed_t)   # (4, 3, 2, 1)
```

Dit is de eenvoudigste en snelste methode. De slice [::-1] betekent: begin bij het einde, en keer terug met stapjes van -1.


```python
t = (1, 2, 3, 4)
reversed_t = tuple(reversed(t))
print(reversed_t)   # (4, 3, 2, 1)
```

De functie `reversed()` geeft een iterator terug, dus moeten we die verpakken in `tuple()` om een tuple te krijgen.

### Tuples kopiëren

Tuples hebben geen copy() methode zoals lists. Maar je kan een copy creëren door te concateneren met een lege tuple:

```python
a1 = (1, 2, 3)
a2 = a1  # a1 en a2 verwijzen naar dezelfde tuple
print("a1:", a1) # a1: (1, 2, 3)
print("a2:", a2) # a2: (1, 2, 3)
print("a1 == a2:", a1 == a2)  # a1 == a2: True (zelfde inhoud, dus True)
print("a1 is a2:", a1 is a2)  # a1 is a2: True (zelfde referentie, dus True)

a3 = a1 + ()  # creëert nieuwe tuple
print("a3: ", a3) # a3: (1, 2, 3)
print("a1 == a3: ", a1 == a3)  # a1 == a3: True (zelfde inhoud, dus True)
print("a1 is a3: ", a1 is a3)  # a1 is a3: False (verschillende referentie, dus False)
```

Omdat tuples geordend zijn, zijn twee tuples gelijk (==) als ze dezelfde elementen hebben in dezelfde volgorde!

```python
a4 = (3, 2, 1)
print("a4:", a4) # a4: (3, 2, 1)
print("a1 == a4:", a1 == a4)  # a1 == a4: False (verschillende inhoud, dus False)
```

### Tuples omzetten naar lists

Tuples kunnen omgezet worden naar een list en omgekeerd:

```python
list_fruit = list(tuple_fruit)
print(list_fruit) # ['mango', 'kers', 'banaan', 'appel']
tuple_fruit_2 = tuple(list_fruit) # ('mango', 'kers', 'banaan', 'appel')
print(tuple_fruit_2)
```

Doordat een tuple onveranderlijk is, kan je de elementen niet  rechtstreeks sorteren, maar via omzetten naar een list kan het wel:

```python
t = 1, 3, 5, 2, 6, 4
t2 = tuple(sorted(list(t))) # (1, 2, 3, 4, 5, 6)
```

## Sets

Sets zijn ongeordende data structuren die alleen unieke elementen  kunnen bevatten. Slechts weinig programmeertalen ondersteunen het  gebruik van sets, maar Python doet het wel. Sets worden niet vaak  gebruikt, maar kunnen soms een handige oplossing geven voor een  probleem.

Je kan bij sets denken aan wiskundige verzamelingen. In de wiskunde is een verzameling een collectie van elementen die alle uniek zijn, en  ieder element zit ofwel in de verzameling, ofwel niet in de verzameling. Er zijn bepaalde operatoren die toestaan sets te combineren.

### Kenmerken

Sets hebben de volgende eigenschappen:

- ze zijn **ongeordend**;
- ze zijn **heterogeen**, omdat hun elementen niet van hetzelfde datatype hoeven te zijn;
- ze zijn **veranderlijk** (Engels: mutable), omdat je elementen kan toevoegen of verwijderen, maar de elementen zelf moeten onveranderlijk zijn!

### Sets creëren

Om een set te creëren waarin al elementen zitten, plaats je die  elementen tussen accolades. Als alternatief kun je de set() functie  aanroepen en een list met de elementen als argument doorgeven.

```python
fruitset = {"appel", "banaan", "kers"}
print(fruitset)  # {'banaan', 'appel', 'kers'}
s = set([1, 2, 3])
print(s) # {1, 2, 3}
```

 Dat de elementen van een set uniek (moeten) zijn, kan je als volgt testen:

```python
s = {1, 1, 2, 2, 3, 3}
print(s) # {1, 2, 3}
```

 Als je een set wilt creëren bestaande uit de verschillende letters  van een string, dan kun je set() aanroepen met de string als argument.  Ook hier worden dubbele letters automatisch genegeerd:

```python
helloset = set("hello world")
print(helloset) # {'w', 'l', 'e', ' ', 'r', 'o', 'd', 'h'}
```

Merk op dat de spatie ook als element is opgenomen, omdat dit uiteraard ook een karakter is.

Python gebruikt dictionaries om sets te implementeren. Concreet  implementeert het de elementen van een set als keys van een dictionary.  Dictionaries gaan we verder nog uitvoerig bespreken. Omdat Python  dictionaries gebruikt om sets te implementeren, denk je misschien dat je een lege set kunt creëren door {} toe te kennen aan een variabele. Maar zoals we nog gaan zien creëert dat een lege dictionary, en niet een  lege set. In plaats daarvan creëer je een lege set door de retourwaarde  van de functie set() (zonder argumenten) toe te kennen aan een  variabele:

```python
lege_set = set()  # niet {}!!
print(lege_set) # set()
print(type(lege_set)) # <class 'set'>
```

 Het laatste voorbeeld toont aan dat in een set de elementen niet van hetzelfde datatype hoeven te zijn. De elementen moeten wel  onveranderlijk zijn. Daarom kan je een tuple als element opnemen, maar geen list of set.

```python
print({1, 2, "abc", True, False, (1, 2, 3)}) # {False, 1, 2, 'abc', (1, 2, 3)}

print({1, 2, "abc", True, False, {1, 2, 3}})
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-65-4cad94302ef0> in <module>()
----> 1 print({1, 2, "abc", True, False, {1, 2, 3}})

TypeError: unhashable type: 'set'
```

### Aantal elementen opvragen

De **len()** functie kan ook gebruikt worden bij sets om het aantal elementen op te vragen:

```python
print(len(fruitset)) # 3
print(len(set())) # 0
```

### De in-operator

Je kan de in-operator en een for-lus gebruiken om een set te  doorlopen. De variabele van de for-lus krijgt toegang tot alle element  van de set. Er is echter geen manier om te bepalen in welke volgorde je  de elementen te zien krijgt, omdat een set per definitie ongeordend is.

```python
fruitmand = { "appel", "banaan", "kers", "doerian", "mango" }
for fruit in fruitmand:
  print(fruit)
```

```
kers
mango
banaan
appel
doerian
```

Met de in-operator kan je ook nagaan of een element tot de set behoort:

```python
if "peer" in fruitmand:
  print("Er liggen peren in de fruitmand")
else:
  print("Er ligt geen peer in de fruitmand")
```

```
Er ligt geen peer in de fruitmand
```

De in-operator is de enige manier toegang te krijgen tot de elementen van een set. Een set is immers ongeordend, dus je kan geen indices  gebruiken om elementen te selecteren, want indexeren veronderstelt een  ordening:

```python
fruitmand[2]
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-70-f9ecc4e85d83> in <module>()
----> 1 fruitmand[2]

TypeError: 'set' object does not support indexing
```

### Elementen toevoegen en verwijderen

Met methode **add()** kan je elementen toevoegen aan een set:

```python
fruitmand = { "appel", "banaan", "kers", "doerian", "mango" }
fruitmand.add("peer")
print(fruitmand) # { "appel", "banaan", "kers", "doerian", "mango"i, "peer" }
```

En met methode **remove()** kan je elementen verwijderen:

```python
fruitmand.remove("doerian")
print(fruitmand) # { "appel", "banaan", "kers", "mango" }
```

Je kan ook methode **pop()** gebruiken als je wil dat het laatst toegevoegde element wordt verwijderd en geretourneerd:

```python
fruit = fruitmand.pop()
print(fruitmand) # {'mango', 'banaan', 'appel'}
```

Maar omdat een set ongeordend is, is het niet altijd duidelijk welk element er zal worden verwijderd door pop().

### Set bewerkingen

In deze sectie bespreken we kort enkele bewerkingen die we kennen uit de verzamelingenleer:

- unie,
- doorsnede,
- verschil,
- zijn disjunct,
- is deelverzameling van.

Met methode **union()** krijg je de unie van twee sets:

```python
set1 = {"a", "b" , "c"}
set2 = {1, 2, 3}

set3 = set1.union(set2)
print(set1)
print(set2)
print(set3)
```

```
{'b', 'a', 'c'}
{1, 2, 3}
{1, 'b', 'a', 2, 3, 'c'}
```

Je kan ook **update()** gebruiken, maar dan worden de elementen toegevoegd aan de set die de methode aanroept:

```python
set1 = {"a", "b" , "c"}
set2 = {1, 2, 3}

set1.update(set2)
print(set1)
print(set2)
```

```
{1, 'b', 'a', 2, 3, 'c'}
{1, 2, 3}
```

Duplicaten worden in beide gevallen uitgesloten:

```python
computers1 = {"HP", "Dell", "Asus", "Apple"}
computers2 = {"Lenovo", "HP", "Apple", "Acer"}
print(computers1.union(computers2))
```

```
{'Apple', 'Acer', 'Asus', 'HP', 'Dell', 'Lenovo'}
```

De doorsnede van twee (of meer) sets krijg je met methode **intersection()**:

```python
doorsnede = computers1.intersection(computers2)
print(computers1)
print(computers2)
print(doorsnede)
```

```python
{'Apple', 'Asus', 'HP', 'Dell'}
{'Apple', 'HP', 'Acer', 'Lenovo'}
{'Apple', 'HP'}
```

Om het verschil tussen twee (of meer) sets te krijgen, maak je gebruik van de methode **difference()**:

```python
verschil = computers1.difference(computers2)
print(computers1)
print(computers2)
print(verschil)
```

```python
{'Apple', 'Asus', 'HP', 'Dell'}
{'Apple', 'HP', 'Acer', 'Lenovo'}
{'Asus', 'Dell'}
```

Handig is ook de methode **isdisjoint** om te checken of twee sets disjunct zijn, d.w.z. geen gemeenschappelijke elementen hebben:

```python
print(computers1.isdisjoint(computers2))  # False want doorsnede is niet leeg
print({1, 2, 3}.isdisjoint({4, 5, 6}))  # True want doorsnede is leeg
```

```
False
True
```

En tot slot kan je ook checken of de ene set een subset of superset is van de andere set:

```python
A = {1, 2, 3}
B = {1, 2, 3, 4, 5}

print(A.issubset(B))  # True want A is deelverzameling van B
print(B.issuperset(A))  # True om dezelfde reden
```

```
True
True
```

### Sets kopiëren

Net als lists kan je sets kopiëren met de copy() methode:

```python
A1 = {1, 2, 3}
A2 = A1  # A1 en A2 verwijzen naar dezelfde set
print("A1 == A2:", A1 == A2)  # True want dezelfde waarden
print("A1 is A2:", A1 is A2)  # True want dezelfde referentie

A3 = A1.copy()  # A3 is een nieuwe set met dezelfde waarden als A1
print("A1 == A3:", A1 == A3)  # True want dezelfde waarden
print("A1 is A3:", A1 is A3)  # False want verschillende referenties
```

```
A1 == A2: True
A1 is A2: True
A1 == A3: True
A1 is A3: False
```

Omdat sets niet geordend zijn is A4 gelijk aan A1, ook al werden de elementen in een andere volgorde gedefinieerd:

```python
A4 = {3, 2, 1}
print("A1 == A4:", A1 == A4)
```

```
A1 == A4: True
```

### Sets omzetten naar lists

Je kan de elementen in een set niet sorteren zolang ze in de set  zitten. Je kan echter wel met een list casting de set omzetten in een  list, en die list dan sorteren. Op die manier weet je zeker in welke  volgorde de elementen worden doorlopen als je een lus toepast:

```python
fruitset = {"appel", "banaan", "kers", "doerian", "mango"}
for element in fruitset:  # worden ongeordend doorlopen
  print(element)

print()

fruitlist = list(fruitset)  # set omzetten naar list
fruitlist.sort()  # elementen sorteren
for element in fruitlist:  # worden geordend doorlopen
  print(element)
```

```bash
kers
mango
banaan
appel
doerian

appel
banaan
doerian
kers
mango
```

### Frozenset

Python kent als variant op het **set** type de **frozenset**. Je creëert een frozenset via de frozenset() constructor. Zoals de naam  laat vermoeden kunnen de elementen van een frozenset niet veranderd  worden. Je creëert dus een frozenset onmiddellijk als je de frozenset()  constructor aanroept, want zodra de frozenset bestaat kun je geen  elementen meer toevoegen of weghalen. Met andere woorden, frozensets  zijn, in tegenstelling tot gewone sets, **onveranderbaar**  (Engels: immutable).  Alle reguliere set methodes werken ook op frozensets, behalve de  methodes die proberen de set te veranderen (bijv. add() om elementen toe te voegen of remove() om elementen te verwijderen). Als je een  dergelijke methode probeert aan te roepen voor een frozenset krijg je  een syntax error.

```python
fruit1 = frozenset(["appel", "banaan", "kers"])
fruit2 = frozenset(["banaan", "kers", "doerian"])
print(fruit1.union(fruit2))
```

```python
frozenset({'banaan', 'appel', 'kers', 'doerian'})
```


```python
fruit1.add('peer')
```

```bash
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-83-88fc54476d6b> in <module>()
----> 1 fruit1.add('peer')

AttributeError: 'frozenset' object has no attribute 'add'
```

## Dictionaries

Tuples en lists (en ook strings) zijn geordende data structuren, wat  inhoudt dat ze via indices benaderd kunnen worden. Maar niet alle data  verzamelingen hebben een natuurlijke manier van numeriek geordend zijn,  en deze kunnen dus niet (gemakkelijk) geïndiceerd worden. Python biedt  “dictionaries” als een manier om ongeordende data te structureren.

### Kenmerken

Een “dictionary” (letterlijk: “woordenboek”, maar die vergelijking  loopt spaak in Python) is een ongeordende data structuur die een  verzameling elementen bevat. Om een element of waarde te vinden, moet je de “key” (“sleutel”) van het element kennen.


In de grond is een dictionary een verzameling van “keys” met  geassocieerde waardes. In andere programmeertalen kom je dictionaries  soms tegen als “associative memories” of “associative arrays”. Ieder  onveranderlijk atatype mag gebruikt worden als key. Een veelgebruikt  data type dat als key wordt ingezet is de string, die in Python  onveranderlijk is.

Samenvattend hebbn dictionaries de volgende eigenschappen:

- ze zijn **ongeordend**;
- ze zijn **heterogeen**, wat betekent dat de elementen niet van hetzelfde datatype hoeven te zijn;
- ze zijn **veranderlijk** (Engels: mutable), wat wil zeggen dat hun elementen kunnen worden gewijzigd, en dat je elementen kan toevoegen of verwijderen.
- ze bestaan uit **key/value** paren; de keys moeten onveranderlijke datatypen zijn.

### Dictionaries creëren

Dictionaries creëer je met accolades {}, vergelijkbaar met hoe je  lists creëert met vierkante haken. Je kunt een dictionary met inhoud  creëren door ieder element dat je erin wilt hebben tussen de accolades  te zetten, met als syntax \<key>:\<value>, en komma’s tussen de elementen.
  Hieronder bouwen we een dictionary fruitmand, met drie elementen,  namelijk de key "appel" met waarde 3, de key "banaan" met waarde 5, en  de key "kers" met waarde 50. De getallen kan je bijvoorbeeld  interpreteren als het aantal stukken van een bepaalde fruitsoort in de  mand:

```python
fruitmand = { "appel":3, "banaan":5, "kers":50 }
print(fruitmand)
```

```
{'appel': 3, 'banaan': 5, 'kers': 50}
```

Je kan ook de **dict()** constructor gebruiken. Let wel op dat je hier geen dubbele punt maar een = teken gebruikt.

```python
auto = dict(merk="Ford", model="Mustang", jaar=1964)
print(auto)
```

```
{'merk': 'Ford', 'model': 'Mustang', 'jaar': 1964}
```

Een lege dictionary maak je door een assignment aan een variabele te doen met {}:

```python
lege_dict = {}
print(lege_dict)
print(type(lege_dict))
```

```
{}
<class 'dict'>
```

Dictionaries zijn heterogeen, dus je kan er waarden van verschillende datatypen in stoppen, ook andere dictionaries:

```python
persoon = {'naam': "Jos",
           'leeftijd': 58,
           'auto': auto}
print(persoon)
```

```
{'naam': 'Jos', 'leeftijd': 58, 'auto': {'merk': 'Ford', 'model': 'Mustang', 'jaar': 1964}}
```

### Aantal elementen opvragen

De **len()** functie werkt ook voor dictionaries:

```python
print(len(auto)) # 3
```

### Elementen selecteren en vervangen

Om een waarde te vinden die hoort bij een specifieke sleutel, gebruik je dezelfde syntax als voor een list, behalve dat waar je bij een list  de index schrijft, je bij een dictionary de gezochte key schrijft:

```python
print(fruitmand["banaan"]) # 5
```

 Je kan ook de methode **get()** gebruiken:

```python
aantal_kersen = fruitmand.get("kers")
print(f"Er zijn {aantal_kersen} kersen in de fruitmand")
```

```
Er zijn 50 kersen in de fruitmand
```

Een element van een dictionary in een dictionary opvragen:

```python
print("{} rijdt met een {}".format(persoon["naam"],
                                   persoon["auto"]["merk"]))
```

```
Jos rijdt met een Ford
```

Als je een dictionary element probeert te benaderen met een key die niet voorkomt in de dictionary, krijg je een runtime error:

```python
fruitmand["peer"]
```

```
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
<ipython-input-97-a1f46f308e90> in <module>()
----> 1 fruitmand["peer"]

KeyError: 'peer'
```



Om elementen in een dictionary te wijzigen maak je ook gebruik van de vierkante haakjes:

```python
print(fruitmand)
fruitmand["banaan"] = 3  # 3 bananen ipv 5
fruitmand["appel"] += 1  # 1 appel toevoegen
print(fruitmand)
```

```
{'appel': 3, 'banaan': 5, 'kers': 50}
{'appel': 4, 'banaan': 3, 'kers': 50}
```

### De in-operator

Bij een dictionary gebruik je de in-operator om te checken of een gegeven key in de dictionary voorkomt:

```python
if "auto" in persoon:
  print("{} heeft een auto".format(persoon["naam"]))
```

```
Jos heeft een auto
```

Wanneer je de in-operator combineert met een for-lus, dan kan je alle keys overlopen:

```python
print("In de fruitmand ligt:")
for fruit in fruitmand:  # fruit is key
  print(fruit)
```

```
In de fruitmand ligt:
appel
banaan
kers
```

De waarden (in dit geval het aantal stukken fruit) kan je op de volgende manier meeprinten:

```python
print("In de fruitmand ligt:")
for fruit in fruitmand:
  aantal = fruitmand[fruit]
  print(aantal, fruit)
```

```
In de fruitmand ligt:
4 appel
3 banaan
50 kers
```

Maar het kan ook efficiënter met de methode **items()**:

```python
print("In de fruitmand ligt:")
for fruit, aantal in fruitmand.items():
  print(aantal, fruit)
```

```
In de fruitmand ligt:
4 appel
3 banaan
50 kers
```

De algemene syntax is dus:

```python
for key in dict:
  # do something with key

for key, value in dict.items():
  # do something with key and value
```

Dictionaries hebben trouwens ook methodes **keys()** en **values()** waarmee je respectievelijk sleutels en waarden kan opvragen:

```python
fruit = fruitmand.keys()
aantal = fruitmand.values()
print(fruit)
print(aantal)
```

```
dict_keys(['appel', 'banaan', 'kers'])
dict_values([4, 3, 50])
```

Zo kan je bijvoorbeeld ook de waarden zonder de sleutels doorlopen:

```python
for value in auto.values():
  print(value, end=" ")
```

```
Ford Mustang 1964
```

Maar let op! Omdat dictionaries ongeordend zijn, ligt de volgorde niet vast.

Geef je echter een dictionary door aan functie sorted(), dan krijg je een list van gesorteerde keys!

```python
print(sorted(auto))
```

```
['jaar', 'merk', 'model']
```

### Elementen toevoegen en verwijderen

We zagen eerder al dat wanneer je een dictionary element opvraagt met een key die niet voorkomt, je een runtime error krijgt. Maar als je een nieuw element wilt toevoegen, kun je dat eenvoudigweg doen door een  waarde toe te kennen aan een dictionary element met de nieuwe key.  Bijvoorbeeld, om een "mango" toe te voegen aan de fruitmand, doe je het  volgende:

```python
fruitmand['mango'] = 1
print(fruitmand)
```

```
{'appel': 4, 'banaan': 3, 'kers': 50, 'mango': 1}
```

Er zijn verschillende manieren om elementen uit een bestaande dictionary te verwijderen.

Met de **pop()** methode verwijder je een element die hoort bij de opgegeven key:

```python
os = dict(naam="Windows", versie=10, opensource=False)
print(os)
os.pop("versie")
print(os)
```

```
{'naam': 'Windows', 'versie': 10, 'opensource': False}
{'naam': 'Windows', 'opensource': False}
```

Je kan ook de **del** operator gebruiken:

```python
os = dict(naam="Windows", versie=10, opensource=False)
print(os)
del os["versie"]
print(os)
```

```
{'naam': 'Windows', 'versie': 10, 'opensource': False}
{'naam': 'Windows', 'opensource': False}
```

Met methode **clear()** maak je de volledige dictionary leeg:

```python
os.clear()
print(os)
```

```
{}
```

### Dictionaries samenvoegen

Met de methode **update()** kan je een dictionary aan een andere dictionary toevoegen:

```python
fruitmand.update({"peer": 5, "kiwi": 2})
print(fruitmand)
```

```
{'appel': 4, 'banaan': 3, 'kers': 50, 'mango': 1, 'peer': 5, 'kiwi': 2}
```

Wanneer de toegevoegde dictionary een element bevat met een key die  ook in de andere dictionary voorkomt, dan wordt het element vervangen:

```python
fruitmand.update({"banaan": 5})
print(fruitmand)
```

```
{'appel': 4, 'banaan': 5, 'kers': 50, 'mango': 1, 'peer': 5, 'kiwi': 2}
```

Bemerk dat in dit geval geen nieuwe (derde) dictionary wordt  gecreëerd. Wil je dat wel, dan kan je op de volgende manier te werk  gaan, gebruik makend van de + operator:

```python
d1 = {"naam" : "Jos", "leeftijd" :  56}
d2 = {"functie" : "systeembeheerder"}
d3 = dict(list(d1.items()) + list(d2.items()))
print(d3)
```

```
{'naam': 'Jos', 'leeftijd': 56, 'functie': 'systeembeheerder'}
```

### Dictionaries kopiëren

Dictionaries beschikken ook over een **copy()** methode. Merk op dat twee dictionaries gelijk zijn (==) als ze dezelfde  key/value paren hebben. Dictionaries zijn niet geordend, dus de volgorde waarin die paren gedefinieerd zijn, speelt geen rol.

```python
d1 = {'a': 1, 'b': 2, 'c': 3}
d2 = d1  # d1 en d2 verwijzen naar dezelfde dictionary
print("d1 == d2:", d1 == d2)  # d1 en d2 hebben dezelfde inhoud, dus True
print("d1 is d2:", d1 is d2)  # d1 en d2 verwijzen naar hetzelfde object, dus True

d3 = d1.copy()  # kopieer de inhoud van d1 in een nieuwe dictionary d3
print("d1 == d3:", d1 == d3)  # d1 en d3 hebben dezelfde inhoud, dus True
print("d1 is d3:", d1 is d3)  # d1 en d3 verwijzen naar verschillende objecten, dus False

d4 = {'c': 3, 'a': 1, 'b': 2}
print("d1 == d4:", d1 == d4)  # d1 en d4 hebben dezelfde inhoud, dus True
```

```
d1 == d2: True
d1 is d2: True
d1 == d3: True
d1 is d3: False
d1 == d4: True
```

## Wat meer over sorteren

Het is een goed moment om even in te gaan op het sorteren. Wat we hier vertellen over sorteren, geldt zowel voor list, tuples en strings. Sets en dictionaries kunnen we niet sorteren, want zij zijn niet geordend.

De functie sort() wijzigt de lijst. Standaard sorteren we in stijgende volgorde, maar het kan ook in dalende volgorde.

```python
fruitlist = ["appel", "aardbei", "banaan", "framboos",
             "kers", "banaan", "doerian", "mango"]
fruitlist.sort()
print(fruitlist)
# ['aardbei', 'appel', 'banaan', 'banaan', 'doerian', 'framboos', 'kers', 'mango']

numlist = [314, 315, 642, 246, 129, 999]
numlist.sort(reverse=True)
print(numlist)
# [999, 642, 315, 314, 246, 129]
```

Tuples zijn  *immutable* of onwijzigbaar. De kunnen deze functie dus niet gebruiken voor dat datatype, maar ook bij lijsten is het niet altijd een goed idee om de lijst te wijzigen. We bekijken straks een alternatief, maar eerste iets meer over de functi `sort()`.

In de interactieve versie van Python kunnen we meer informatie over de de functie `sort()` met de functie `help()`:

```python
>>> help(list.sort)
```

We krijgen de volgende info:

```
Help on method_descriptor:

sort(self, /, *, key=None, reverse=False)
    Sort the list in ascending order and return None.

    The sort is in-place (i.e. the list itself is modified) and stable (i.e. the
    order of two equal elements is maintained).

    If a key function is given, apply it once to each list item and sort them,
    ascending or descending, according to their function values.

    The reverse flag can be set to sort in descending order.
```

We kunnen dus, zoals het bovenstaande voorbeeld aantoonde, in stijgende of dalende volgorde laten sorteren.

We hebben in een vorige hoofdstuk gesproken over de lambda-functies. Het argument *key* verwacht een functie en daarvoor zijn lambdafunctie net heel geschikt. Stel dat we een lijst van tuples hebben, met personen en hun lengte in centimeter. We willen hen kunnen sorteren op alfabet of op lengte. Om dat ze kunnen doen moeten we een functie definiëren die bepaalt op welke sleutel we willen sorteren.

```python
personen = [ ("Jan", 172), ("Fatima", 165), ("Igor", 168), ("Rune", 176), ("Anja", 174)]
naam = lambda persoon: persoon[0]
lengte = lambda persoon: persoon[1]
personen.sort(key=naam) # sorteert de lijst van tupels op naam
personen.sort(key=lengte) # sorteeert de lijst van tupels op lengte
```

We willen echter onze oorpronkelijke lijst niet altijd wijzigen, maar een gesorteerde kopie maken. Daarvoor kunnen we de functie `sorted()`. Deze kan tuples, string en lijsten als argument krijgen. De zijn zogenaamde itereerbare, geordende objecten. De signatuur van de functie is: `sorted(iterable, key=None, reverse=False)`.

```python
personen = ["Jan", "Fatima", "Igor", "Rune", "Anja"]
gesorteerde_lijst_personen = sorted(personen)
# ["Anja", "Fatima", "Igor", "Jan", "Rune"]
```

Ook hier kunnen we de waarde voor *key* definiëren met een functie.

```python
personen = [ ("Jan", 172), ("Fatima", 165), ("Igor", 168), ("Rune", 176), ("Anja", 174)]
naam = lambda persoon: persoon[0]
lengte = lambda persoon: persoon[1]
personen_omgekeerd_gesorteerd_op_naam = sorted(personen, naam, reverse=True)
personen_gesorteerd_op_lengte = sorted(personen, lengte)
```

Let wel: de functie `sorted()` geeft een *list* terug. Als we een gesorteerde kopie van een tupel nodig hebben, dan moeten we lijst weer naar een tupel converteren.

```python
gewichten = (62, 81, 59, 78, 72, 63, 65)
gesorteerde_gewichten = tuple(sorted(gewichten))
# (59, 62, 63, 65, 72, 78, 81)
```

Hetzelfde geldt voor een string. `sorted()` geeft een lijst van karakters terug, dus moeten we list weer omzetten naar een string.

```python
letterbrij = "azertyuiopqsdfghjklm"
gesorteerde_letterbrij = sorted(letterbrij)
# ['a', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'o', 'p', 'q', 'r', 's', 't', 'u', 'y', 'z']
gesorteerde_letterbrij_als_string = ""
for letter in gesorteerde_letterbrij:
	gesorteerde_letterbrij_als_string += letter
print(gesorteerde_letterbrij_als_string)
# adefghijklmopqrstuyz
```

## Filter() en map() met lambda-functies

Lamba-functies komen ook tot hun recht bij de functie `filter()` en `map()`. De eerste functie creëert een nieuwe lijst die een subset is van de vorige lijst, gebaseerd op een voorwaarde. De functie `map()` creëert een nieuwe lijst met een gewijzigde versie van de elementen uit de oorspronkelijke lijst.

De functie `filter()` geeft die gegevens terug die voldoende aan een bepaalde voorwaarde. Die voorwaarde definiëren we in een functie. Nemen we opnieuw onze lijst van personen en hun lengte. We willen een nieuwe lijst met enkel personen die minstens 170 cm groot zijn. Met de functie `filter()` krijgen we een filterobject terug, we moeten dit object nog omzetten naar een lijst.

```python
personen = [ ("Jan", 172), ("Fatima", 165), ("Igor", 168), ("Rune", 176), ("Anja", 174)]
groter = lambda persoon: persoon[1] >= 170
grote_personen = list(filter(groter, personen))
print(grote_personen) # [('Jan', 172), ('Rune', 176), ('Anja', 174)]
```

Dit kan korter:

```python
personen = [ ("Jan", 172), ("Fatima", 165), ("Igor", 168), ("Rune", 176), ("Anja", 174)]
print(list(filter(lambda persoon: persoon[1] >= 170, personen)))
# [('Jan', 172), ('Rune', 176), ('Anja', 174)]
```

De functie `map()` heeft twee argumenten, een functie en een lijst. Het creëert een map-object waarbij de functie werd toegepaste op elk element van de lijst. Dit object converteren we opnieuw naar een lijst. Een voorbeeld maakt dit duidelijk:

```python
getallen = [1, 3, 5, 7, 8]
kwadraat = lambda x: x**2
getallen_in_kwadraat = list(map(kwadraat, getallen))
print(getallen_in_kwadraat) # [1, 9, 25, 49, 64]
```

Dit kan korter:

```python
getallen = [1, 3, 5, 7, 8]
print(list(map(lambda x: x**2, getallen))) # [1, 9, 25, 49, 64]
```

## Comprehensions

Python voorziet ons ook van de mogelijkheid om op een korte en  elegante manier reeksen zoals lists, sets en dictionaries te creëren met behulp van comprehensions. Die worden vaak gezien als meer "pythonic"  dan lussen, en ze zouden ook efficiënter zijn. Daarom nemen we ze op in  deze les, hoewel we er niet heel diep op in zullen gaan. We gaan enkel  kort bespreken hoe list, dictionary en set comprehensions werken.

### List comprehensions

De algemene syntax voor een list comprehension is:

```
new_list = [expression for element in iterable if (element satisfies condition)]
```

De conditie uitgedrukt door de `if` is niet verplicht.

Voorbeeldje: Stel dat we een list met elementen van 1 tot 10 willen. Met een for-lus doen we dat als volgt:

```python
lst = []
for i in range(1, 11):
  lst.append(i)
print(lst)
```

```
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

Met een list comprehension kan het in één lijn:

```python
lst = [i for i in range(1, 11)]
print(lst)
```

```
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

Willen we het kwadraat van de gehele getallen van 1 tot 10, dan ziet de list comprehension er als volgt uit:

```python
print([i**2 for i in range(1, 10)])
```

```
[1, 4, 9, 16, 25, 36, 49, 64, 81]
```

Een ander voorbeeld: Stel dat we een input list hebben met allemaal  gehele getallen en we willen daarmee een nieuwe list creëren die enkel  de even elementen bevat. Met een lus doen we dat zo:

```python
input = [1, 2, 3, 4, 4, 5, 6, 7, 7]
output = []
for i in input:
  if i % 2 == 0: output.append(i)
print(output)
```

```
[2, 4, 4, 6]
```

Met een list comprehension kan het opnieuw in één lijn:

```python
print([i for i in input if i % 2 == 0])
```

```
[2, 4, 4, 6]
```

Je kan ook geneste list comprehensions creëren. Stel dat je de volgende matrix wil definiëren:

```python
matrix = [[0, 1, 2, 3, 4],
          [0, 1, 2, 3, 4],
          [0, 1, 2, 3, 4],
          [0, 1, 2, 3, 4],
          [0, 1, 2, 3, 4]]
```

Met geneste lussen doen we dat zo:

```python
matrix = []
for i in range(0, 5):
  row = []
  matrix.append(row)
  for j in range(0, 5):
    row.append(j)

print(matrix)
```

```
[[0, 1, 2, 3, 4], [0, 1, 2, 3, 4], [0, 1, 2, 3, 4], [0, 1, 2, 3, 4], [0, 1, 2, 3, 4]]
```

Met een geneste list comprehension kan het zelfs in dit geval met één regel code:

```python
print([[j for j in range(0, 5)] for i in range(0, 5)])
```

```
[[0, 1, 2, 3, 4], [0, 1, 2, 3, 4], [0, 1, 2, 3, 4], [0, 1, 2, 3, 4], [0, 1, 2, 3, 4]]
```

Stel dat we een 2D matrix willen "flatten", wat wil zeggen dat we  alle elementen in één rij gaan plaatsen, dan doen we dat als volgt:

```python
# 2D matrix creëren
matrix = [[i*3 + j for j in range (0, 3)] for i in range (0, 3)]
print(matrix)

# 2D matrix flatten
flat = [element for row in matrix for element in row]
print(flat)
```

```
[[0, 1, 2], [3, 4, 5], [6, 7, 8]]
[0, 1, 2, 3, 4, 5, 6, 7, 8]
```

### Dictionary comprehensions

Op dezelfde manier kunnen we ook dictionaries creëren m.b.v. comprehensions. De algemene syntax is:

```python
new_dict = {key: expression for key, value in iterable if (key, value satisfies condition)}
```

Een voorbeeldje: Stel dat we een list hebben met gehele getallen, dat we uit die list de oneven getallen willen afzonderen, en als key in een dictionary stoppen, samen met hun derde macht als waarde. Met een lus  doen we dat op de volgende manier:

```python
input = [i for i in range(1, 8)]
print(input)

output = {}
for i in input:
  if i % 2 == 1:
    output[i] = i ** 3

print(output)
```

```
[1, 2, 3, 4, 5, 6, 7]
{1: 1, 3: 27, 5: 125, 7: 343}
```

Met een dictionary comprehension kan het weer in één lijn:

```python
print({i: i ** 3 for i in input if i % 2 == 1})
```

```
{1: 1, 3: 27, 5: 125, 7: 343}
```

Nog een voorbeeldje: Stel dat we een list hebben van landen en een  list met bijhorende hoofdsteden. We willen die nu samenbrengen in een  dictionary, met de landen als key en de hoofsteden als waarden. Met een  lus:

```python
landen = ["België", "Nederland", "Frankrijk"]
hoofdsteden = ["Brussel", "Amsterdam", "Parijs"]

d = {}
for land, hoofdstad in zip(landen, hoofdsteden):
  d[land] = hoofdstad

print(d)
```

```
{'België': 'Brussel', 'Nederland': 'Amsterdam', 'Frankrijk': 'Parijs'}
```

Met een comprehension:

```python
print({landen[i]: hoofdsteden[i] for i in range(len(landen))})
```

```
{'België': 'Brussel', 'Nederland': 'Amsterdam', 'Frankrijk': 'Parijs'}
```

Merk op dat het in feite nog korter kan door gebruik te maken van `zip()`:

```python
print(dict(zip(landen, hoofdsteden)))
```

```
{'België': 'Brussel', 'Nederland': 'Amsterdam', 'Frankrijk': 'Parijs'}
```

### Set comprehensions

Set comprehensions worden op dezelfde manier gecreëerd als list  comprehensions, alleen gebruiken we nu accolades i.p.v. vierkante  haakjes:

```python
new_set = {expression for element in iterable if (element satisfies condition)}
```

Het verschil met een dictionary comprehension is dat er bij die laatste een key wordt toegevoegd.

Een voorbeeldje: Stel dat we uit een list met gehele getallen de even getallen willen halen om in een set te stoppen. Met een lus gaat dit  als volgt:

```python
input = [1, 2, 3, 4, 4, 5, 6, 6, 6, 7, 7]

output = set()  # niet {}, want dat is een lege dict!
for i in input:
  if i % 2 == 0:
    output.add(i)

print(output)
```

```python
{2, 4, 6}
```

Bemerk dat 4 en 6 slechts één maal voorkomen omdat een set geen duplicaten bevat.

Met een comprehension kan het uiteraard in één lijn:

```python
print({i for i in input if i % 2 == 0})
```

```python
{2, 4, 6}
```

## Verzamelingen uitpakken

In Python, uitpakken of *unpacking* verwijst naar het proces waarbij we meerdere waarden in een collectie (zoals een list, tuple of gelijk welk iteraarbaar element) in één statement kunnen toekennen aan meerdere variabelen. Op die manier kunnen we sneller elementen uit een collectie halen.

Je kan elementen van een tuple of een lijst direct toekennen aan meerdere variabelen.


```python
# A tuple met drie elementen
person = ("John", 25, "Engineer")

# Het tuple uitpakken in meerdere variabelen
name, age, profession = person

print(name)       # Output: John
print(age)        # Output: 25
print(profession) # Output: Engineer
```


```python
# Een lijst met drie elementen
numbers = [1, 2, 3]

# de lijst uitpakken in meerdere variabelen
a, b, c = numbers

print(a)  # Output: 1
print(b)  # Output: 2
print(c)  # Output: 3
```

De operator * laat to om de resterende elementen op te vangen. Je kan dit gebruiken wanneer je niet precies weet hoeveel elementen er in een itereerbaar element zitten, of wanneer je slechts een deel van het itereerbaar element wil krijgen.


```python
numbers = [1, 2, 3, 4, 5]

# We kennen het eerste element toe aan first, en de rest stoppen we in de lijst rest
first, *rest = numbers

print(first)  # Output: 1
print(rest)   # Output: [2, 3, 4, 5]
```

```python
numbers = [1, 2, 3, 4, 5]

# We nemen het eerste element en kennen het toe aan first. Dan hebben we de lijst middle
# met de middelste elementen, en het laatste element kennen we toe aan last.
first, *middle, last = numbers

print(first)   # Output: 1
print(middle)  # Output: [2, 3, 4]
print(last)    # Output: 5
```

Je kan dit principe gebruiken om een lijst of a dictionary door te geven aan een functie. De lijst of dictionary heeft de argumenten, als positionele argumenten (in dat geval gebruiken we * en een lijst of tuple), or als zogenaamde keyword arguments (in dat geval gebruiken we ** en een dictionary).

In het volgende voorbeeld geven we de positionele argumenten x, y en z door. We noemen dit positionele argumenten omdat we ze geen naam geven, maar ze gewoon in dezelfde volgorde aanbieden. We gebruiken een asterisk (*) voor de lijst van argumenten.


```python
def add(x, y, z):
    return x + y + z

numbers = [1, 2, 3]

# Unpacking the list into the function arguments
result = add(*numbers)
print(result)  # Output: 6
```

In het volgende voorbeeld geven we een dictionary door die voor elke argument de naam van het argument geeft, en de waarde. We noemen dit keyword arguments (kwargs). We gebruiken een ** voor de dictionary van argumentens.


```python
def greet(name, age):
    return f"Hello, {name}. You are {age} years old."

person_info = {"name": "Alice", "age": 30}

# Unpacking the dictionary into keyword arguments
message = greet(**person_info)
print(message)  # Output: Hello, Alice. You are 30 years old.
```

## De module JSON

Wanneer we nu data opvragen aan een website via een API, dan krijgen  we die data vaak in JSON formaat aangeboden. JSON wordt gebruikt om  informatie op te slaan in een eenvoudig georganiseerde manier. De file  is leesbaar, en kan logisch opgeroepen worden. De grootste voordelen  zijn:

- Ondersteund in alle browsers
- Eenvoudig te lezen & schrijven
- Gebruikt weinig geheugen
- Simpele syntax
- Ondersteund in alle grote JavaScript frameworks
- Maakt het mogelijk om gestructureerde data over het netwerk te versturen (bijvoorbeeld van/naar een server)

JSON staat voor **JavaScript Object Notation**. Een  JavaScript object bestaat uit key/value paren, gescheiden door komma's  en omsloten door accolades. Het ziet er dus precies hetzelfde uit als  een Python dictionary. Werken met JSON-files in Python is dus heel  eenvoudig!

In Python is er de ingebouwde module "json" om met JSON data te  werken. Een JSON object definieer je als string en kan dan omgezet  worden met functie `loads()` naar een Python dictionary:

```python
import json

# Een voorbeeld van een JSON object:
x =  '{ "naam":"Jessie", "leeftijd":19, "stad":"New York"}'  # string!

# Parse x in y:
y = json.loads(x)
print("Volledige JSON:",y)

# Het resultaat is een Python dictionary:
print("Het argument leeftijd is:",y["leeftijd"])
```

Met `json.dumps)` zetten we dan een dictionary of een list van dictionaries om naar json.

```python
# Een Python object (dict):
x = {
  "naam": "Jessie",
  "leeftijd": 19,
  "stad": "New York"
}

# Omzetten in JSON:
y = json.dumps(x)

# the result is a JSON string:
print(y)
```

```python
import json

data = [
    {"name": "John", "age": 30, "city": "New York"},
    {"name": "Marie", "age": 22, "city": "Boston"},
    {"name": "Mike", "age": 32, "city": "Chicago"}
]

# Convert to JSON string
json_string = json.dumps(data, indent=4)  # `indent=4` will make the output nicely formatted

print(json_string)
```

```bash
[
    {
        "name": "John",
        "age": 30,
        "city": "New York"
    },
    {
        "name": "Marie",
        "age": 22,
        "city": "Boston"
    },
    {
        "name": "Mike",
        "age": 32,
        "city": "Chicago"
    }
]
```
