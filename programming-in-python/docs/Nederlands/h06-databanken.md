# Werken met databanken

## Doelstellingen

Op het einde van dit hoofdstuk moet je in staat zijn om:

* Een SELECT-query te doen op een sqlite-database.
* Een UPDATE-, DELETE- of INSERT-query te doen op een sqlute-database.
* Bij deze query's moet je correct gebruik maken van placeholders.

## Documentatie

* [SQLite](https://www.sqlite.org)
* [DB Browser for SQLite](https://sqlitebrowser.org)
* [Officiële Pythondocumentatie for SQLite3](https://docs.python.org/3/library/sqlite3.html)

## Hoe benader je een database in Python?

Het spreekt vanzelf dat we met Python ook een relationele database willen benaderen. Dat kan voor nagenoeg alle types relationele databases: SQLite, Postgresql, Mysql, Microsoft SQL Sever, Oracle, ...

De stappen die hiervoor gezet moeten worden zijn meestel dezelfde:

* Importeer de module die nodig is om dat type database te benaderen.
* Maak een connectie met de database in kwestie. Daarvoor heb je allerlei connectiegegevens nodig, zoals de locatie van de database (bijv. een IP-adres of een servernaam), de poort waarop de database kan bereikt worden, een gebruikersnaam en een wachtwoord.
* Vanuit die connectie creëer je een cursorobject. Dat is een object waarmee je queries kan uitvoeren.
* Je creëert je query als string.
* Je voert de query uit met je cursorobject.
* Je haalt het resultaat op (één object, de hele lijst, enzovoort).
* Je verwerkt het resultaat.
* Je sluit je connectie.



Voor wijzigingen (insert, update, delete) moet je er ook over waken dat je je niet blootstelt aan SQL-injectie.

## Sqlite3

SQLite3 is een lightweight databasesysteem. Er is geen serverinstallatie nodig, je database bestaat uit één bestand en je benadert en beheert de database via software. Ondanks het feit dat SQLite weinig installatie nodig heeft, is dit toch een volwaardig relationeel databasesysteem dat een grote hoeveelheid gegevens kan bevatten.

SQLite is ingebouw in Python.

```python
import sqlite3
```

Je kunt SQLite benaderen via een command line interface. Hiervoor tik je in je terminal het commando `sqlite3` in gevolgd door de naam van de database die je wil openen.

```bash
$ sqlite3 chinook.db
```

Je kan dan de lijst van tabellen opvragen met het commando `.tables`, het schema van een tabel opvragen met `.schema` gevolgd door de naam van de tabel, sql-queries uitvoeren, importeren en exporten naar csv enzovoort. Die CLI-interface zal je nodig hebben wanneer je je database op een server wil beheren. Lees de [documentatie](https://www.sqlite.org/cli.html) van de CLI-interface hiervoor na.

Je kan ook je database op een eenvoudigere manier beheren met de grafische tool Db Browser for SQLite. Deze maakt ons het leven gemakkelijker.

## Een retrieve-query uitvoeren

Hoe je een eenvoudige query uitvoer in sqlite kunnen we snel aantonen met een voorbeeld. We nemen als voor een query in de chinook-database.

```python
import sqlite3 # stap 1: importeren

dbconnectie = sqlite3.connect("chinook.db")  # stap 2: connectie maken

mijncursor = dbconnectie.cursor() # Stap 3: cursor maken

# Stap 4: query definiëren
mijnquery = "SELECT name FROM tracks WHERE lower(composer) like 'johny%'"

# Stap 5: query uitvoeren
mijncursor.execute(mijnquery)

# Stap 6: het resultaat ophalen. Je krijgt nu een lijst van tupels terug.
rows = mijncursor.fetchall()

# Stap 7: verwerk het resulaat
for row in rows:
  pass # doe iets

# Stap 8: sluit de connectie
dbconnectie.close()
```

Je hebt naast het commando `fetchall()` ook het commando `fetchone()`. Deze geeft één tupel terug (of None als de query leeg was).

Je kun ook met het with-statement werken. Dan wordt de connectie automatisch gesloten. We zien in dit voorbeeld ook dat er een impliciet gebruik van de cursor is, door het execute-statement direct op de connectie uit te voeren.

```python
import sqlite3
with sqlite3.connect("chinook.db") as dbconnectie:
  resultaat = dbconnectie.execute("SELECT name FROM track")
  print(resultaat.fetchall())
```

## Een update-query uitvoeren met placeholders

Wanneer we een insert, update of delete-query uitvoeren, is het van essentieel belang dat we placeholders gebruiken om SQL-injectie te vermijden. Placeholders kunnen we ook gebruiken bij een SELECT-query. Je maakt je query hiermee parametriseerbaar.

Er bestaan verschillende manieren op placeholders te gebruiken. De eenvoudigste manier is dat je een vraagteken plaats op de plaats waar een waarde moet komen en dan een tuple toevoegt aan je query met de werkelijke waarden. Een voorbeeld kan dit illustreren:

```python
import sqlite3
with sqlite3.connect("chinook.db") as dbconnectie:
  mijncursor = dbconnectie.cursor()
  query = """
  UPDATE tracks set composer = "Mick Jagger, Keith Richards"
  WHERE composer LIKE ? or composer LIKE ?
  """
  
  # definieer nu een tupel met de waarden voor de vraagtekens
  parameters = ("Mick Jagger/Keith Richards", "Keith Richards/Mick Jagger")
  
  # Nu voer je de query uit met twee argumenten
  mijncursor.execute(query, parameters)
  
  # Vergeet geen commit te doen bij een wijziging, op het niveau van de connectie
  dbconnectie.commit() 
```

De meeste database operaties zullen we verpakken in een try-excerpt-blok om fouten op te vangen.

## Andere systemen dan SQLite

Om andere systemen te benaderen moet je normaal gezien een module installeren. Dat doe je met het commando `pip` of `pip3`, bijv.

```
pip install psycopg3 # voor Postgresql
```

Daarna kan je die module importeren en gebruiken. Twee voorbeelden kunnen dit illustreren, één met Postgresql, en één voor Mysql.

### Postgresql

```python
import psycopg2

def fetch_albums_by_artist(artist_name):
    # Connect to the PostgreSQL database
    connection = psycopg2.connect(
        dbname="chinook",    # Change these connection parameters as needed
        user="your_username",
        password="your_password",
        host="localhost",
        port="5432"
    )

    # Cursor to execute queries
    cursor = connection.cursor()

    # Use a placeholder to insert the artist's name into the query
    query = """
    SELECT Album.Title
    FROM Album
    INNER JOIN Artist ON Album.ArtistId = Artist.ArtistId
    WHERE Artist.Name = %s;
    """

    # Execute the query
    cursor.execute(query, (artist_name,))

    # Fetch results
    albums = cursor.fetchall()

    # Close the cursor and connection
    cursor.close()
    connection.close()

    return albums

if __name__ == "__main__":
    artist = "AC/DC"  # Just an example; replace with the desired artist name
    result = fetch_albums_by_artist(artist)
    for album in result:
        print(album[0])
```

Merk op dat we hier geen vraagteken als placeholder gebruiken, maar %s.

Raadpleeg zeker de [documentatie](https://www.psycopg.org/docs/usage.html).

### MySQL

Voor MySQL gebruiken we de module mysql-connector-python

```
pip install mysql-connector-python
```



```python
import mysql.connector

def update_track_price(track_id, new_price):
    # Connect to the MySQL database
    connection = mysql.connector.connect(
        host="localhost",
        user="your_username",
        password="your_password",
        database="chinook"
    )

    # Cursor to execute queries
    cursor = connection.cursor()

    # Use placeholders for both track ID and the new price
    query = """
    UPDATE Track
    SET UnitPrice = %s
    WHERE TrackId = %s;
    """

    # Execute the query
    cursor.execute(query, (new_price, track_id))

    # Commit changes
    connection.commit()

    # Close the cursor and connection
    cursor.close()
    connection.close()

if __name__ == "__main__":
    track_to_update = 1  # Just an example; replace with the desired track ID
    new_unit_price = 1.99  # Replace with the desired new price
    update_track_price(track_to_update, new_unit_price)
    print(f"Updated TrackId {track_to_update} to new price: ${new_unit_price}")
```

## Datetime

We hebben het in deze cursus nog niet over het omgaan met datums en tijd gehad. Aangezien een database vaak datumaanduidingen bevat, is het een goed moment om het hierover te hebben.

Om met datum en tijd om te gaan gebruike we de module datetime.

Wanneer we het hebben over datums en tijd, moeten we een onderscheid maken tussen objecten die zich bewust zijn van een tijdszone en de objecten die zich daar niet van bewust zijn. Voor de eenvoud hebben we over de tweede soort objecten.

### date

Een object van het type date stelt een datum voor, een jaar, een maand en een dag. We maken een datum door het jaar, de maand en de dag op te te geven.

```python
from datetime import date
my_date = date(2023, 09, 28)
print(mydate)
# 2023-09-28

# vandaag opvragen en het jaar, de maand en dag afdrukken
vandaag = date.today()
print("We zijn in het jaar: ", vandaag.year)
print("We zijn in de maand: ", vandaag.month)
print("We zijn op de dag: ", vandaag.day)
```

### time

We hebbeen ook de klasse time, die een tijdstip voorstel in uren, minuten, seconden en eventueel microseconden.

```python
from datetime import time

# time(hour = 0, minute = 0, second = 0)
a = time()
print(a)

# time(hour, minute and second)
b = time(11, 34, 56)
print(b)

# time(hour, minute and second)
c = time(hour = 11, minute = 34, second = 56)
print(c)

# time(hour, minute, second, microsecond)
d = time(11, 34, 56, 234566)
print(d)
```

Dit geeft als output

```
a = 00:00:00
b = 11:34:56
c = 11:34:56
d = 11:34:56.234566
```

```python
from datetime import time

a = time(20, 35, 53)

print("Uur =", a.hour) # 20
print("Minuten =", a.minute) # 34
print("Seconden =", a.second) # 56
print("Microseconden =", a.microsecond) # 0
```

### datetime

De klasse datetime combineert de gegevens van date en time.

```python
from datetime import datetime

a = datetime(2022, 12, 28, 23, 55, 59, 342380)

print("Year =", a.year)
print("Month =", a.month)
print("Hour =", a.hour)
print("Minute =", a.minute)
print("Timestamp =", a.timestamp())
```

Output:

```
year = 202
month = 12
day = 28
hour = 23
minute = 55
timestamp = 1511913359.34238
```

### timedelta

Timedelta geeft dan het verschil tussen twee datums of twee tijdstippen aan.

from datetime import datetime, date

```python
from datetime import datetime, date

# using date()
t1 = date(year = 2018, month = 7, day = 12)
t2 = date(year = 2017, month = 12, day = 23)

t3 = t1 - t2

print("t3 =", t3)

# using datetime()
t4 = datetime(year = 2018, month = 7, day = 12, hour = 7, minute = 9, second = 33)
t5 = datetime(year = 2019, month = 6, day = 10, hour = 5, minute = 55, second = 13)
t6 = t4 - t5
print("t6 =", t6)
```

Output:

```
t3 = 201 days, 0:00:00
t6 = -333 days, 1:14:20
```

### Datum en tijd formatteren

Om datums of tijdstippen op een aangepaste manier weer te geven, hebben we de functie `strftime()`. Deze functies is een onderdeel van de klassen `date`, `time` en `datetime` en heeft een formaat als argument.

Een voorbeeld kan dit duidelijk maken:

```python
from datetime import date
vandaag = date.today()
print(vandaag.strftime("%A %d %B %Y"))
```

Output:

```
Thursday, 28 September 2023
```

De formatcodes vind je in de [documentatie](https://docs.python.org/3/library/datetime.html#strftime-and-strptime-format-codes).

Omgekeerd kan je met de functie `strptime()` uit een string een datum of tijd afleiden.

```python
from datetime import datetime
tijdstip = datetime.strptime('31/01/22 23:59:59.999999', '%d/%m/%y %H:%M:%S.%f')
# 31 januari 2022 23:59
```

Als we datum in het Nederlands willen weergeven zullen we gebruik maken van de module locale:

```python
import locale
from datetime import date

locale.setlocale(locale.LC_ALL, 'nl_BE.UTF-8')
vandaag = date.today()
print(vandaag.strftime("%A %d %B %Y"))
# output: donderdag 28 september 2023
```

