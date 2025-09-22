# Writing a simple script

## Learning objectives

At the end of this chapter you will be able to:

- write a simple script,
- handle basic data types such as int, float, string and list,
- execute basic operations with these data types,
- use the control statement `if` ,
- Iterate using `for` or `while`,
- test whether a variable is of a certain datatype,
- convert data to another data type,
- ask input from the user,
- return output in a formatted way,
- use arguments in a script,
- use string operations (slicing, ...)

## Extra documentation

### From the official documentation

- [Using Python as a Calculator](https://docs.python.org/3/tutorial/introduction.html): in these examples the basic data types and their operators are demonstrated.
- [Numeric Types](https://docs.python.org/3/library/stdtypes.html#typesnumeric): description of all numeric data types (int, float, complex) and their operators.
- [Boolean operations](https://docs.python.org/3/library/stdtypes.html#boolean-operations-and-or-not)
- [Text](https://docs.python.org/3/library/stdtypes.html#text-sequence-type-str)
- [Arithmatic functions from the module math](https://docs.python.org/3/library/math.html#math.trunc)
- [Built-in Functions](https://docs.python.org/3/library/functions.html?highlight=input#input)
- [More Control Flow Tools](https://docs.python.org/3/library/functions.html?highlight=input#input): statements and functions such as if, for, range(), break, continue, pass, match (vanaf Python 3.10).
- [Custom String Formatting](https://docs.python.org/3/library/string.html#custom-string-formatting)

## Variabels en data types

As we described earlier Python is dynamically types. We do not have to declare the data type of a variable beforehand. The data type is inferred at the first assignment.

### Numbers

We know two numeric data types:

- `int`: integers or whole numbers
- `float`: numbers with a fractional part, with decimals.

Decimal numbers use a decimal point.

```python
age = 23
weight = 78.5
```

The variable `age`  will be of type `int` and the variable weight will be of type `float`.

Python has the following **numeric operators**:

*   Add: +
*   Subtract: -
*   Multiply: *
*   Power: **
*   Division: /
*   Integer division: //
*   Modula (remainder of integer division): %

The following numeric functions are also interesting:

- `abs(x)`: absolute value of x.
- `max(x,y)`: the largest of x and y.
- `min(x,y)`: the smallers number of x and y.

If we import the built-in module math - and we do this by putting the statement `import math` at the beginning of our script -, we add a few usefull functions to our repertoire:

- `math.ceil(x)`: returns the smallest integer larger than or equal to x.
- `math.floor(x)`: returns the largest integer smaller than or equal to x.

Examples:

```python
import math
print(math.ceil(2.3)) # 3
print(math.floor(2.3)) # 2
print(abs(-5)) # 5
print(max(5,7)) # 7
```

### Boolean values

As you know, a boolean value is either true (`True`) of not true (`False`).

We know the traditional operations on booelan values. In Python they look like this: `or`, `and` and `not`.

The comparison operators in Python look like this:

| Operator | Meaning                  |
| -------- | ------------------------ |
| `<`      | smaller than             |
| `<=`     | smaller than or equal to |
| `>`      | larger than              |
| `>=`     | groter than or equal to  |
| `==`     | equal to                 |
| `!=`     | not equal to             |
| `is`     | object equality          |
| `is not` | object inequality        |

### Text 

Text of `str` should be put between single or double quotes. The following statements are equivalent:

```python
print("Hello world")
print('Hello world')
```

If you want to use literal quotes in a piece of text, you can do that by switching between single and double quotes:

```python
print('And father said: "Son, you must start studying in time."')
```

To **concatenate** strings, we use the plus operator (+).  You can use the star operator (\*) to create a string that is a repitition of the original string.

The command:

```python
print("VIVES" + " University of Applied Sciences")
```

will give the following output: VIVES University of Applied Sciences.

The command:

```python
print(3 * "ai")
```

will give the output: aiaiai.

A few usefull **string functions** :

- `str.lower()`: str in lower case.
- `str.upper()`: str in capitals.
- `str.title()`: every word will start with a capital letter.
- `len(str)`: returns the number of characters in a string.
- `str.count(sub [,start [,end]])`: count the number of times a non-overlapping piece of text occurs in the string.
- `str.find(sub, [, start [,end]])`: return -1 if `sub` does not occur in `str` and if it does, it return the index of the first character of sub (indexes start at 0).
- `sub in str`: return `True` if `sub` if found in `str` , else `False`.
- `str.replace(str1, str2)`: replaces `str1` by `str2`.

Keep in mind that string are **immutable**. A changed string is printed or assigned to a new variable.

Examples:

```python 
print("VIVES University").lower() # vives university
print("VIVES University").upper() # VIVES UNIVERSITY
print("vives university").title() # Vives University
print(len("This is text")) # 12
message = "This is text"
print(message.count('i')) # 2
print(message.count('t')) # 3
print(message.count('t', 4)) # 2 (I start counting from position 4)
print(message.find('t', 4)) # 8
print("text" in "This is text.") # True
print("word" in "This is text.") # False
new_message = message.replace("text", "a message") # This is a message.
```

In a string `\t`  is a tab and  `\n` a new line. Beware, in Windows a new line is a combination of a new line and a carriage return:  `\n\r`'.

When you want to escape a character, to indicate that it must be taken literally, you put a backslash in front of it, the so called **escape sign**.

```python
print("We use the character \", or double quotes in a citation.")
print("The directory is C:\\Windows\\System32.")
```

When you want to **select** a character from a string, you can use the index. The index starts at 0.

```python
message = "Hello, World!"
print(message[1]) # resultaat: e
```

With the **slice operator**, you can select a substring. Keep in mind that the start index is included, the end index is not.

```python
message = "Hello, World!"
print(message[2:5]) # result: llo
```

 The start `i1` of the slice `i1:i2` can be omitted if  `i1` is the first index, and `i2` can be omitted if  `i2`  is the last index:      

```python
print(message[:5]) # result: Hello
print(message[7:]) # result: World!
```

### Conversion van data types

We do not always get a value in the correct data type. In that case we must do type casting, or conversion to another data type.

- `int(x)`: conversion to integer.

- `float(x)`: conversion to float.
- `str(x)`: conversion to string.

### Test whether a value is of a certain data type

The most general function to test whether a value is of a certain data type is:  `isinstance(object, type)`.

You can use one type or a list of types:

```python
x = isinstance("Hello", str) # x is True
x = isinstance(2, str) # x is False
x = isinstance(2.5, int) # is is False
x = isinstance(2.5, (int, float)) # x is True
```

Another way is using the function `type()`.

```python
x = 5
y = type(x) == int # y is True
```

The function `str.isnumeric()` will check whether all characters are numeric.

```python
x = "122343".isnumeric() # x is True
x = "2.5".isnumeric() # x is False
```

You can use the module `number` to really test whether a value is numeric:

```python
import numbers

x = 5
print(isintance(x, numbers.Number)) #resultaat True
```

### Mutliple assignment

You can assign multiple values in one command (although this makes your code less readable):

```python
x, y, z = 10.0, 20.0, 30.0
print(x + y + z) # 60.0
```


##  Read input

A script can do a meaningful action is it can ask input to the user. To do that we use the function  `input()`. This function can contain a promt, a piece of text that is presented to the user as a message. Keep in mind that the input is always of type `str`. You may have to convert your input to another data types;

```python
first_name = input("Give your first name: ")
print("Welcome " + first_name)
```

```python
my_number = input("Give a whole number: ")
print("The square is this number is " + int(my_number)**2)
```



## Make desisions (if)

Python uses the traditional `if`. 

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

This notation is also possible for short statements:

```python
cost = 24.54
revenue = 93.01
profit = revenue - cost
print("Nice, keep going!") if profit > 0 else print("Watch out for bankruptcy.")
```

If you need an empty statement that you will define later, you can use `pass` . This way you avoid an error.

```python
height = 150
if height < 300:
    pass
else:
    print("Too high.")
```

You can also use three dots instead of pass, the so called Ellipsis object:

```python
naam = 'KULeuven'
if naam.lower() == 'vives':
  print('Hogeschool')
else:
  ...
```

## Comments and indentation

As you noticed in the previous examples, Python does not use curly braces or semicolons to structure the code. It uses indentation instead. You indent four spaces to indicate a code block. In most text editors you can use the tab key. This is automatically converted to four spaces.

To give comments, pieces of text that are not compiles, you use `#`. All code after this sign (on the same line) is ignored.

A comment that spans multiple lines begins and ends with `'''` or `"""`.

## Multiple lines

Sometimes you want to spread a long statement over multiple lines. You can use a backslash at the end of the line as a continuation symbol.

```python
if school1[1] == school2[1] 
        and school1[2] == school2[2] \
        and school1[3] == school2[3] \
        and school1[4] == school[4]: 
        return True
else:
        return False
```

An alternative method is to include your code in rounded brackets, square brackets or curly braces.

```python
 if (school1[1] == school2[1]
        and school1[2] == school2[2]
        and school1[3] == school2[3]
        and school1[4] == school2[4]): 
        return True
    else:
        return False
```

If you want a string to run over multiple lines, you can use the same method, of work with triple quotes. In the latter case the line break is included in the string.

```python
my_text = """Python is 
a very readable
programming language
"""
print(my_text)
```

This code will produce the following output:

```
Python is 
a very readable
programming language
```

## Lists

In a later chapter we will discuss lists in detail, but we will already show how basic lists or arrays work. You can declare a list in two ways.

```python
myList = ["car", "bike", "airplane", "step"]
myUnimportantList = list(("a", "b", "c"))
```

To indicate a specific member of the list, you use indexes, as you do with strings. The index is zero based. Use square brackets with indexes.

```python
my_list = ["car", "bike", "airplane", "step"]
print(my_ist[1]) # bike
```

In contrast to strings, list are mutable. You can change an individual member of a list:

```python
my_list[1] = "e-bike"
print(my_list[1]) # e-bike
```

As with strings you can use slicing to select part of a list. You create a new shorter list. Don't forget that the element at the end index is not included (exclusive boundary).

```python
my_list = ["car", "bike", "airplane", "step"]
print(my_list[1:3]) # ['bike', 'airplane']
```

To add items at the end of an ordered list, use `append()`.

```python
my_list = ['bike', 'car']
my_list.append("boat") # ['bike', 'car', 'boat']
```

We will learn more about lists later.

## Iteration 

When an element is "iterable" , that means that you can go through is as a list, use the `for`-loop. Strings as well as lists are iterable.

```python
my_list = ["car", "bike", "airplane", "step"]
for item in my_list:     
    print(item)
```

You have no counter in the `for`-loop. If you need a fixed number of iteration, use the `range()` function.

```python
for i in range(10):
    print(i*2)
```

Python also knows the `while`-loop to iterate until a condition is met.

```python
i = 0;
while i < 5:
    i += 1
    print("i has the value of: " + str(i))
```

You can interrupt an iteration with the statement `break`. You can go on with an iteration using the statement `continue`.

## Formatted String output

You have noticed that the function `print()` prints output to the terminal. This function can have multiple arguments. These are concatenated.

```python
my_number = int(input("Give a number: "))
print("The square of this number is: ", my_number**2)
```

In most cases we want to present our output in a nice, structure way. We usually want to mix literal text with the value of a variable.

The easiest way to do this if to put the letter 'f' before the quotes. When you want to use the value of a variable, you put the variable name between curly braces.

```python
name = "Saïd"
age = 23
print(f"Hello {name}, I heard that you are {age} years old.")
```

In fact this a brief notation of the function`format()`. You could rewrite this as:

```python
name = "Saïd"
age = 23
salutation = "Hello {}, I heard that your {} years old."
print(salutation.format(name, age))
```

The empty curly braces are placeholders. You fill in the placeholders using the format function.

You can add extra formatting using the function `format()'. A few examples may illustrate this.

**Center:** you can center a piece of text using the `^` sign in a placeholder, following by the width of the field.

**Centreren:** Je kunt tekst centreren in een bepaald aantal tekens met behulp van het `^`-teken in de plaatsaanduiding, gevolgd door een getal dat de breedte van de velden aangeeft. Hier is een voorbeeld:

```python
text = "Python"
centered_text = "{:^10}".format(text)
print(centered_text)
```

This Python code with center the text 'Python' in a field of 10 characters.

**Left align:** you can left align the text with the character `<` in the placeholder, followed by the field width.

```python
text = "Python"
left_aligned_text = "{:<10}".format(text)
print(left_aligned_text)
```

**Right align:** you can right align the text with the `>` symbol in the placeholder, followed by the width of the field.

```python
text = "Python"
right_aligned_text = "{:>10}".format(text)
print(right_aligned_text)
```

With a floating comma number, you can define the number of decimals in the output with `.2f` (or another number of decimals).

```python
my_number = 3.14159265
rounded_output = "{:.2f}".format(getal)
print(rounded_output)
```

The output will show the number with two decimals: `3.14`.

You can use the `f`-notation to get the same effect. 

```python
my_number = 3.14159265
print(f"Het number pi is {my_number:.2f}.")"
```

## Arguments

Script do no only ask input from a user, but you can also pass values when calling the script. Suppose you want to calculate the circumference of a rectangle. You will call the script as follows:

```bash
python3 perimeter.py 5 10
```

5 is the width of the rectangle and 10 the height.

How do you process these arguments width and height. In the module `sys` there is a list `sys.argv`. This list contains all the arguments that were passed to the script, including the name of the script itself as the first element (index 0). An example will illustrate this.

```python
import sys

# The first element is the name of the script
script_name = sys.argv[0]

# De rest of the list are the arguments
arguments = sys.argv[1:]

# Je count the arguments as follows
number_of_arguments = len(sys.argv) - 1

# Now you can use the arguments
print("Name of the script:", script_name)
print("Arguments:", arguments)
```

In the example of the rectangle the script would look like thios:

```python
import sys

script_name, width, height = sys.argv

perimeter = int(width) * int(height)
print(f"The perimeter of the rectangle is {perimeter}.")
```

We will make this script more robust by checking the number of arguments.

```python
import sys

if len(sys.argv) -1 != 2:
	print("You have to pass two arguments, width and height")
	sys.exit(1)

script_name, width, height = sys.argv

perimeter = int(width) * int(height)
print(f"The perimeter of the rectangle is {perimeter}.")
```

If the number of arguments is not equal to two, a error message is given and the script is stopped with error code 1, which is equal to a non-successful termination (0 is successful)
