# Work with databases

## Objectives 

At the end of this chapter you should be able to:

* Do a SELECT query on a SQLite database.
* Do a UPDATE; DELETE or INSERT query on a SQLite database.
* Use placeholders correctly when doing a SQL query.
* Use the modules `date`, `time` and `datetime` correctly.

## Documentation

* [SQLite](https://www.sqlite.org)
* [DB Browser for SQLite](https://sqlitebrowser.org)
* [Offical Python documentation for SQLite3](https://docs.python.org/3/library/sqlite3.html)

## How do you access a database in Python?

Of course we want to access relational databases using Python. We can do this for all types of relational databases: SQLite, Postgresql, Mysql, Microcoft SQL Server, Oracle, ...

The steps to be taken are ususally the same:

* Import the modules you need to access this type of database.
* Make a connection to the database with the function `connect()`. You need connection data, such as the location of the database (e.g. an IP address or a server name), a port number, a user name and a password. For sqlite3 you will need a local file path to the database.
* Create a cursor object. A cursor object act as intermediaries for executing SQL command and managing results.
* Write and execute the SQL Query. The SQL query is a string, which you can execute using the function `execute()`. If you use dynamic input you will parameterize your query using placeholders.
* Fetch th results. Retrieve the results using methods like `fetchone()` for a single row, `fetchall()` for all results, or iterate over the cursor for large datasets.
* Close the cursor and connection.

## Sqlite3

Ssqlite3 is a lightweight, serverless, self-contained SQL database engine that is built into Python's standard library. It provides a simple way to create, query, and manage databases directly from Python without needing an external server or setup. Instead of connecting to a remote database server, sqlite3 stores all data in a single file on disk, making it ideal for small applications, local data storage, or quick prototyping.

Because sqlite3 is embedded, it’s widely used in applications where a full-scale database setup isn’t necessary, such as mobile apps, local data logging, and testing environments. It supports standard SQL commands (like SELECT, INSERT, UPDATE, and DELETE), transactions, and basic indexing, making it compatible with many SQL-based applications.

Because of its speed and lightweight setup, we also see SQLite more and more in full-fledged web applications.

When we test your SQLite3-database locally, we can use the command line interface of SQLite. To to that you enter the command `sqlite3` followed by the path to the file containing the database you want to open.

You can ask for the list of tables using the command `.tables`, for the schema of a table using the commend `.schema` followed by the name of the table. You can execute SQL queries, import from csv or export to csv, and so on. You will need the CLI interface when you want to manage a database on a server. Check the [official documentation](https://www.sqlite.org/cli.html)  for more information.

In the development phase, a handy tool to use is DB Browser for SQLlite, which offers a GUI-interface to our database. DB Browser for SQLite is available for Windows, Mac and Linux. 

### Import the SQLite library

Python includes SQLite3 in the standard library, so no installation is necessary. Just import sqlite3.

```python
import sqlite3
```

### Establish a connection

Use `sqlite3.connect()` to create or open a connection to an SQLite database file. If the specified file doesn’t exist, SQLite will create it.

```python
connection = sqlite3.connect("chinook.db")
```

### Create a cursor object

A cursor object allows you to execute SQL commands and retrieve data.

```python
cursor = connection.cursor()
```

### Write and execute the SQL query

Define you SQL query as a string. To prevent SQL injection we use placeholders (`?`) for any dynamic parameter. The list of values to replace the placeholders is a tuple.

```python
query = "SELECT * FROM students WHERE age > ?"
cursor.execute(query, (18,))
```

### Fetch the results

You can retrieve the results using `fetchone()`, `fetchall()`, or by iterating over the cursor.

```python
results = cursor.fetchall()
for row in results:
    print(row)
```

Each row in the result is represented as a tuple.

### Close the cursor and the connection

When done with the cursor and the connection, close them to free up resources.

```python
cursor.close()
connection.close()
```

### Example: a retrieve in SQLite

We will take the chinook database as an example. 

```python
import sqlite3 # step 1: import sqlite3 library

db_connection = sqlite3.connect("chinook.db")  # step 2: make connection

my_cursor = db_connection.cursor() # Step 3: make cursor

# Step 4: define query
my_query = "SELECT name FROM tracks WHERE lower(composer) like 'johny%'"

# Step 5: execute query
my_cursor.execute(my_query)

# Step 6: retrieve the result, a list of tuples
rows = my_cursor.fetchall()

# Step 7: process the result
for row in rows:
  pass # doe something

# Step 8: close the connection
db_connection.close()
```

### Example with a context manager

SQLite connections support context maangers (using the `with` statement), which will automatically handle closing the connection and cursor when done.

```python
import sqlite3
with sqlite3.connect("chinook.db") as dbconnection:
  result = dbconnection.execute("SELECT name FROM track")
  print(result.fetchall())
```

### An example of an update query with placeholders

```python
import sqlite3
with sqlite3.connect("chinook.db") as db_connection:
  my_cursor = db_connection.cursor()
  query = """
  UPDATE tracks set composer = "Mick Jagger, Keith Richards"
  WHERE composer LIKE ? or composer LIKE ?
  """
  
  # define a tuple with the values to replace the placeholders.
  parameters = ("Mick Jagger/Keith Richards", "Keith Richards/Mick Jagger")
  
  # Eecute the query with two arguments.
  my_cursor.execute(query, parameters)
  
  # Do not forget to commit your update, at the connection level.
  db_connection.commit() 
```

In real code we will put our database operations in a try-except block to cath potential errors.

## Other DBMS'es

To access a Postgresql, Mysql, Oracle, ... database you will have to install a module using `pip` or `pip3`. 

```
pip install psycopg3 # for Postgresql
```

We will illustrate this with two examples, one for Postgresql and on for Mysql.

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

Not that we do not use a question mark for the placeholder, but `%s`.

Check the [documentation](https://www.psycopg.org/docs/usage.html).

### MySQL

For MySQL we use the module mysql-connector-python.

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

A topic that we have not yet covered in this course is dates an time. A database often contains date fields, so this is a good time to do so.

To use dates and time we use the module `datetime`.

When we cover date and time, we must make a difference between objects that are aware of time zones and objects that are not. For simplicity we mainly cover the second kind.

### date

An object of type `date` represents a date: a year, a month and a day. We create a `date` object by specifycing these three values:


```python
from datetime import date
my_date = date(2023, 09, 28)
print(my_date)
# 2023-09-28

# Retrieve today's date and print the year, month and day
date_of_today = date.today()
print("We are in the year: ", date_of_today.year)
print("We are in the month: ", date_of_today.month)
print("Today's day is: ", date_of_today.day)
```

### time

There is also a class `time`. Each `time` object represents a moment in time, expressed in hours, minutes, seconds and possibly microseconds. 

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

The output will be

```
a = 00:00:00
b = 11:34:56
c = 11:34:56
d = 11:34:56.234566
```

```python
from datetime import time

a = time(20, 35, 53)

print("Hour =", a.hour) # 20
print("Minutes =", a.minute) # 34
print("Seconds =", a.second) # 56
print("Microseconds =", a.microsecond) # 0
```

### datetime

The class datetime combines date and time.

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

The timestamp is the number of seconds since the Unix epoch, i.e. since January 1, 1970, 00:00:00 (UTC).

Here's how you can get the current time: 

```python
from datetime import datetime

# Get the current time: date and time
current_time = datetime.now()
print(current_time)
```

### timedelta

Timedelta gives the difference between two dates and time.

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

### Format date and time

To represent date and times in a formetted way, we use the method `strftime()` from the `datetime` module. This method allows you to format a `datetime` object into a string using format codes. The following example will show this:

```python
from datetime import date
current_date = date.today()
print(current_date.strftime("%A %d %B %Y"))
```

Output:

```
Thursday, 28 September 2023
```

You can find the format codes in the [documentation](https://docs.python.org/3/library/datetime.html#strftime-and-strptime-format-codes).

The method `strptime()` will parse a date-time string into a `datetime` object.

```python
from datetime import datetime
tijdstip = datetime.strptime('31/01/22 23:59:59.999999', '%d/%m/%y %H:%M:%S.%f')
# 31 january 2022 23:59
```

ATo format dates in Dutch (Belgium) in Python, you can use the locale module to set the locale for date formatting. This allows strftime() and strptime() to produce date and time strings in Dutch. Here’s how to do it:

```python
import locale
from datetime import date

locale.setlocale(locale.LC_ALL, 'nl_BE.UTF-8')
current_date = date.today()
print(current_date.strftime("%A %d %B %Y"))
# output: donderdag 28 september 2023
```

