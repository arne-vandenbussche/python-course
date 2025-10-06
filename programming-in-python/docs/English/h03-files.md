# Working with files

## Objectives

After this chapter, you will be able to:

- open a text file and read the information (in its entirety or line by line) and process it;

- write text into a text file (in its entirety or line by line);

- add information to an existing text file (at the end);

- perform reading and writing of text files using the `with` structure;

- catch errors with exeption handling;

- throw exceptions;

- define exceptions;

- read and process csv files;

- write information to a csv file;

- manipulate files and folders (add, delete, rename, move, ...);

- navigate folders;

- test whether something is a file or a folder;

- create compressed files in zip or tar format;

- extract compressed files.

##  Read and process files

To read a file, we use the built-in function `open()`. This creates an object. This object must be closed afterwards with the `close()` command.

The function `open()` always expects an argument containing the reference to the file name. The second optional parameter is the ‘mode’ in which you want to open the file. The different modes are:

- ‘r’: open to read only (default).
- ‘w’: open to write, but delete all content first.
- ‘x’: tries to create the file and returns an error if the file already exists.
- ‘a’: open to write, adding content at the end.
- '+': read and write (update)

You can also specify that you want to open the file as text (‘t’) or binary data (‘b’). By default, a file is opened as text.

See also the [official documentation on open()](https://docs.python.org/3/library/functions.html#open).

We can best illustrate this with some examples:

```python
# Open the file for writing
# The should not already exist, but it can.
# If the file already exists, the original content is deleted.
myFile = open("myTestFile.txt", 'w')
print(f"The type of 'myFile' is: {type(myFile)}.")

# I store a line of text in the file.
myFile.write("Vives University of Applied Sciences")

# I close the file.
myFile.close()

# Read the contents of the file.
myFile = open("myTestFile.txt", 'r')
print(myFile.read())
myFile.close()  # do not forget to close the file at the end.
```

Python wil search for a file in the current directory. If you wish to access a file in another directory, you should give the path.

The function `read()`reads to the end of the file (until the symbol EOF). You can also give a specific length. In a text file that is the number of characters you will read. If you call read without arguments again, the rest of the file is read.

```
myFile = open("myTestFile.txt", 'r')
print(myFile.read(20))  # Read the first 20 characters
print(myFile.read())  # Reads the rest of the file
myFile.close()
```

If you have more than one line to write, you can write one long string, or you can call `write()`several times. For each `write()` statement, a new line symbol is added to the end of the line. The `write()` function return the number of characters written.

```python
letter = open("letter.txt", 'w')
print(letter.write("Dear,\n"))  # Do not forget the new line symbol to add a blank line.
print(letter.write("Please contact me.\n"))
print(letter.write("Yours sincerely,\nVictor"))
letter.close()
```

Note that when a file is opened in ‘write’ mode, all content of that file is deleted. If you merely want to  add something to the file, this can be handled via two modes.

1. First, the file is read and the content is then stored in a variable. Additional text is then added to that variable. Next, that variable is written to the file.
2. The text file is opened in ‘append’ mode. In the same way as ‘write’ mode, data can be written away. This data is automatically added at the end of the file.

If it is not desired to read the content of a file in large chunks, the method `readlines()` can be used. This method creates a list. Each element in the list corresponds to a read line. An example:

```python
# create a text file with multiple lines
monty_python = open("monty_python.txt", 'w')

tekst = ("Monty Python is a British comedy group.\n" + 
         "The group is known for breaking the comedy conventions of that time.\n" + 
         "The group consists of the following members:\n" +  
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
# read the text file and print the contents.
monty_python = open("monty_python.txt", 'r')
my_text = monty_python.readlines()  # list of strings
monty_python.close()

print(my_text) # print as a list

print("".join(my_test)) # concatenate each element in the list and print as text
```

There is also a method `readline()` to read the lines one by one, or you can iterate over the `TextIOWrapper` object:

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
  print(line, end="")  
  # I set an empty sting as line and because the lines already contain \n
monty_python.close()
```

## Working with exceptions

[Python documentation: errors and exceptions](https://docs.python.org/3/tutorial/errors.html)

[Overview of alle built-in exceptions in Python](https://docs.python.org/3/library/exceptions.html)

Up to now we wrote code that impled that the given input was correct. We know this is not reality. Users make mistakes. There Python, as well as other programming languages, have a way to catch exceptions.

We of course know that we can make syntax errors. A syntax error activates the SyntaxError exception.

```python
if False:
  print("cannot be reached")
else
  print("only executable statement")
```

When running this code, we will get the following error:

```bash
File "<ipython-input-1-c85e64124321>", line 3
    else
        ^
SyntaxError: invalid syntax
```

Apart from syntax errors, there can be many reasons why an error occurs: we want to open a file that does not exist, we try to combine variables of different types, we try to divide by zero, and so on. All these give an execution error. An _exeption_ is thrown.

Python has a large number of [built-in exceptions](https://docs.python.org/3/library/exceptions.html). Examples of  **built-in excpetions** are:

- `NameError`: a variable has not been defined;
- `TypeError`: an operator or function is done on a value of the wrong type;
- `ValueError`: a function argument has an invalid value;
- `ImportError`: an import statement fails;
- `KeyboardInterrupt`: a user insterrupts the execution of a script, for example by pressing CTRL+C;
- `FloatingPointError`: an operation of a variable of type `float` fails;
- `IndexError`: a given index, for example in a list, does not exist;
- `KeyError`: a given key in a dictionary does not exist;
- `IOError`: a input/output operation fails;
- `OSError`: a general error on the operating system level, such as a full disk, wrong access rights, file not found, ...
- `FileNotFoundError`: a file is not found;
- `ZeroDivisionError`: division by 0.

The goal is to anticipate errors like that and deal with them. We do that using the try-except block

```python
try:
  result = 7/0
  print(result)
except:
  print("Oops, wrong operation,... but your script does not crash!")
```

In the **try** block we anticipate an action can go wrong. In the **except** block we define what should happens if the action goes wrong. You can use **except** withou any specification, but you can also catch a very specific error and print or log the original message.

```python
try:
  result = 7/0
  print(result)
except ZeroDivisionError as err:
  print(f"Error: {err}!")
```

A good practice can be to catch specific errors that you can think of with a custom message, and add a general **except** block to catch all remaining errors.

```python
def division():
  try:
    numerator = int(input("Give the numerator of a fraction: "))
    denominator = int(input("Geef de denominator of a fraction: "))
    result = numerator / denominator
    print(f"The result is: {result:.2f}.")
  except ZeroDivisionError as err:  # denominator is zero
    print(f"Error 1: {err}!")
  except ValueError as err:  # wrong input by the user
    print(f"Error 2: {err}!")
  except:  # unexpected error
    print("Error 3: unknown error at this moment...")
```

If the same action is required for different error:

```python
except (RuntimeError, TypeError, NameError):
    pass
```

You can use the **else** block to specify what should happen if there is no error:

```python
try:
  result = x / y
except ZeroDivisionError as err:
  print(f"Error: {err}.")
else:
  print(f"The result of this division is: {result:.2f}.")
```

The **finally** block is used to close external resources such as database or network connections, whatever happens.

```python
try:
    result = x / y
except ZeroDivisionError as err:
  print(f"Error: {err}.")
else:  # is executed when there is no exception
  print(f"Het resultaat van de deling is: {result:.2f}.")  
finally:  # is always executed
  print("I am the finally block and I always execute.")
```

To raise an exception yourself, is done the statement **raise**:

```python
if speed > 120:
  raise SpeedError("Speed too high!")
else:
  print("All cool.")
```

A common pattern is to catch an exception and then raise a general exception that should be caught by another part of the application:

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

You can define **exception** yourself. This is done by creating a new exception class that inherits from `Exception`. This can be done directly of indirectly via a subclass of `Exception`.

It is enough to pass the name of the superclass as a ‘parameter’ when defining the subclass to make the latter inherit from the former. It's a good idea to give all your own exceptions a name ending with `Error`.

```python
class SpeedError(Exception):  # inherits from the class Exception
  def __init__(self, message):
    self.message = message


speed = 125
if speed > 120:
  raise SpeedError("Speed too high!")
else:
  print("All cool.")
```

## With

Opening, reading and closing a file can actually be done more elegantly and securely with the statement `with`. 

Example without `with`: 

```python
file = open('file_path', 'w')
file.write('hello world !')
file.close()
```

 We are running a risk here. If an exeption occurs, then the file will not be closed and that could cause nasty side effects. To avoid that, we should use a block try-finally.

```python
file = open('file_path', 'w')
try:
  file.write('hello world')
finally:
  file.close()
```

Using `with` is a shorter and more elegant way to do this

```python
# using with statement
with open('file_path', 'w') as file:
  file.write('hello world !')
```

There is no `close()` here. The file is automatically closed, whatever happens

## Processing files

### Process text in a file

We have already covered basis text file processing, but it might be a good idea to point out a few functions for text manipulation.

`str.strip()`: remove the empty characters (spaties, tabs, ...) at the beginning and the end of a string. We also have `str.rstrip()` and `str.lstrip()` the remove empty space at the beginning or the end of a string.

`str.find(key_str, [start], [end])`: returns -1 is `key_str` was not found. If it was found, the lowest index where `key_str` was found within the boundaries of start and end in `str` is returned. Start and end are interpreted as with slicing. Start is included, end is not.

Example

```python
s = '/test/in.txt'
where_found = s.find('in') # where_found is 6
```

`str.replace(old, new, [count])`: returns a copy in which _old_ is replaced by *new*. The argument *count* restricts the number of time the replacedment is done.

```python
s = 'hello hello hello, world'
new_string = s.replace('ll', '**') #'he**o he**o he**o, world'
new_string = s.replace('ll', '**', 2) # 'he**o he**o hello, world'
```



`s.split([sep], [maxsplit=-1])`: returns a list of words with *sep* as separating symbol. If you do not specify *sep*, a space is used as the default separating symbol. The argument *maxsplit* restricts the number of splits. The default value is -1, which means unlimited.

```python
my_list = 'apple, orange, pear'.split()       # ['apple,', 'orange,', 'pear']
my_list = 'apple, orange, pear'.split(', ')   ['apple', 'orange', 'pear']
my_list = 'apple, orange, pear'.split(', ', maxsplit=1)  # ['apple', 'orange, pear']
```



`sep.join([str])`: is the opposite of split. This will concatenate a list of strings with *sep* as separating symbol.

```python
', '.join(['apple', 'orange, pear']) # 'apple, orange, pear'
```

### Processing csv files

A commonly used type of text file is the csv file. CSV stands for ‘comma separated value’. These files are often the result of an export from an Excel file or a table in a database. We use the [csv module](https://docs.python.org/3/library/csv.html) in Python for this purpose .
The function `csv.reader(csv-file, dialect=‘excel’, **fmtparams)` returns an object that we can use to iterate over the lines of a csv file. The default dialect is *excel*, which is OK for most cases. So-called *fmtparams* are, for example:

- `delimiter`: the separator. By default this is a comma, but in many csv files it can also be something else, such as a semicolon.
- `doublequote`: specifies how the escape of double quotes is done. If this is *True*, it is done by repeating the double quotes, otherwise the escape symbol is used.
- `escape`: defines the escapes symbol.
- `quoting`: defines whether the fields are enclosed in quotes. This is done with a quoting constant. The default value is csv.QUOTE_MINIMAL.
  - csv.QUOTE_ALL: everything in quotes.
  - csv.QUOTE_MINIMAL: only fields with special characters are enclosed in quotes.
  - csv.QUOTE_NONNUMERIC: the non-numeric fields are enclosed in quotes. The reader will read the fields not enclosed in quotes as *float*.
  - csv.QUOTE_NONE: never enclose fields in quotes.

The example below processes a csv file containing covid data. The separator is a semicolon.

```python
import csv

with open('covid.csv', newline='') as myCovidFile:
  
  myReader = csv.reader(myCovidFile, delimiter=';')
  print("The current delimiter is: " + myReader.dialect.delimiter) # ;

  # next() return the next line as a list 
  # We use it to process the first line, the header
  # Then we iterate over the rest of the lines.
  print("First row: " + str(next(myReader)))  # header
  largestNumberOfCases = 0
  for row in myReader:
    print(row)
    if int(row[4]) > largestNumberOfCases:
      largestNumberOfCases = int(row[4])

  print("The day with most COVID-cases in the list is: " + str(largestNumberOfCases))
```

We first create a reader object. The file name is ‘myCovidFile’ and the separator is a semicolon. Using next(), we read the first row and place the pointer on the second row. Then we iterate with a for loop. The output would look like this:

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

Similarly, you can also write data to a csv file using the csv module. That data is best structured as a list of rows, where each row is also a list.

Below, randomly generated rainfall values per day of a week are stored as a table:

```python
import random

days = ["monday", "tuesday", "wednesday", "thursday", "friday", "saturday", "sunday"]

table = []  # table is a list of rows
for day in days:
  row = [day, random.randint(0, 100)]  # each row is a list of attributes
  table.append(row)
```

We then write the data away to a CSV file. Can you open that file in Excel to create a graph from it?

```python
import csv

# Open a csv file in a safe way for writing
with open('rain.csv', 'w', newline='') as myRainyFile:
  myWriter = csv.writer(myRainyFile, delimiter=';')

  # We use a for loop to go through all the elements of the list and write them
  # one by one into the csv file
  for row in table:
    myWriter.writerow(row)  
```

We will see later that we can process csv files in an even more powerful way with the *pandas* module.

## Manipulate folders and files

For file manipulation, we use the modules `os`, `os.path` and `shutil`.

The `os` module contains functions specific to the operating system, including functions to manipulate files.

### About paths and file names

To manipulate file names and paths, we have the module `os.path` (see [documentation](https://docs.python.org/3/library/os.path.html)). Let us look at some useful functions of `os.path`.

- `os.path.abspath(path)`: returns the full path of the given directory .
- `os.path.basename(path)`: will give the last part of the absolute path. 
- `os.path.dirname(path)`: will give everything of the path except the last part.
- `os.path.exists(path)`: returns `True` if the path of that folder or file exists.
- `os.path.join(path, *paths)`: pastes paths or parts of paths together, intelligently.
- `os.path.isdir(path)`: is `True` if the path is a folder.
- `os.path.isfile(path)`: is `True` if the path is a file.



```python
# Our current folder is /Users/pythonuser/
print(os.path.abspath(os.getcwd())) # getcwd() reutrn the path of the current folder. 
# The result of the command above: /Users/pythonuser

print(os.path.basename(os.getcwd())) # pythonuser
print(os.path.dirname(os.getcwd())) # /Users
```

The function `os.path.join()` does deserve special mention. The function is intelligent in several ways:

- It filters directory separators (backslash (Windows) or slash (unix systems)) so that no two come after each other in the result.
- It puts a directory separator at the end if needed.
- If one element is an absolute path, the elements before it are discarded and the path starts from that absolute path.

```python
pad = os.path.join(os.getcwd(), 'file.txt'))
```

The above compiles a correct pathname, e.g. `/Users/pythonuser/file.txt` regardless of the operating system. The slash will be replaced by a backslash in a Windows system.

### Copy, remove and move files

The shutil module (shell utilities) offers a number of higher-level operations than the os module for files and collections of files. In particular, it offers functions that support copying and deleting files.

For example, `shutil.copy()` allows you to copy a file, as in the piece of code below. `os.rename()` renames the file and `path.exists()` checks whether the file to be copied actually exists.

```python
import os
from os import path
import shutil

if path.exists("myShUtilsTestFile.txt"):  # does the file exist?
  
  source = "myShUtilsTestFile.txt"  # file to copy
  destination = "./temp/myShUtilsTestFile.txt"  # copied file
  
  if not path.exists("./temp"): os.mkdir("temp")  
  # create directory "temp" if it does not yet exist
  
  file = shutil.copy(source, destination)  # copy file
  
  newname = "./temp/test.txt"
  os.rename(file, newname)  # rename file
```

### Manipulate folders
A specific type of file is a folder or directory. You can **list** the files in a directory using the `scandir()` function.
```python
import os

with os.scandir('my_directory/') as entries:
    for entry in entries:
        print(entry.name)
```

The functions `os.scandir()` returns a list of objects, one object per file or folder in ‘my_directory’. We have called that list ‘entries’ here. With the `with` statement, we create a context in which we will iterate over the elements of `entries`. By `with`, we guarantee that system resources will be automatically released after iteration. We iterate over the list of elements in the directory and we print the name of each element. The result is similar to what a command `ls` or `dir` would do.

Each object `entry` in this example contains more than just the name of the files or folders. We also have all sorts of other properties of the object. For example, we can test whether it is a file with `entry.is_file()`. Similar is the function `entry.isdir()`.

Creating a **folder** is done with the function `os.mkdir(‘name_folder’)`. Beware, if the folder already exists, the exception `FileExistsError` is thrown up. You can create a folder with subfolders with `os.mkdirs(‘folder/subfolder/subsubfolder’)`.

Deleting a **folder** is done with the command `os.rmdir(‘name_folder’)`. If a folder is not empty, a `OSError` will occur. With `os.removedirs()` you will delete a folder and all underlying folders, but this only works with empty folders. In the module `shutil` you do have a function `shutil.rmtree` that allows you to delete a folder and all underlying files and folders at once.

You can query the **current folder** with `os.getcwd()`.

**Change folder**: `os.chdir()`.

## Compressed files

The `shutil` module also contains functions to work with compressed files. These can be zip files or tar files.

```python
from shutil import make_archive
make_archive("sample_data_archive", "zip", "./sample_data")  # De hele map 'sample_data' zippen.
```

In fact, the `make_archive()` function uses the ‘zipfile’ and ‘tarfile’ modules behind the scenes:

```python
from zipfile import ZipFile
with ZipFile("file.zip", "w") as newzip:
  newzip.write("myShUtilsTestFile.txt")  # add file to Zip.
```

```python
with ZipFile('file.zip', 'r') as zipObj:
   # unzip the zip-file and place the contents in folder ‘temp’
   # If you do not specify a folder, the contents will be placed in the current directory
   zipObj.extractall(‘temp’) # ‘temp’ does not need to exist yet
```
