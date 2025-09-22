# Functions

## Objectives

After this chapter, you should be able to:

- import modules and functions and use those functions,
- assign functions to a variable or use them as arguments in another function,
- define functions yourself,
- define and use anonymous or lambda functions,
- define and use functions with default arguments,
- write a script with functions distinguishing between directly executable code and importable functions (`if __name__ == ‘__main__:`’)
- use the `dir()` function.

## From Pythons documentation

[functions](https://docs.python.org/3/reference/compound_stmts.html#function)

[modules](https://docs.python.org/3/tutorial/modules.html)

[top-level code environment](https://docs.python.org/3/library/__main__.html?highlight=__name__%20__main__)


## Functions and modules

### Built-in functions

We have already used built-in functions and functions from the *math* library in earlier chapters. We called functions using the functions' names, with the parameters in brackets. The function then returns a value.

```python
maximum = max(1, 3, 5, 6) # 6
```

### Functions from modules

If the function is not built-in, but belongs to a particular module, we need to import that module or the function itself.

In the example below, we import the module *math* and use the function that calculates the square root.

```python
import math
square_rool = math.sqrt(2)
```

We can also import the function itself:

```python
from math import sqrt
square_root = sqrt(4)
```

When importing, we can also give the function its own name:

```python
from math import sqrt as squareroot
square_root_hundred = squareroot(100)
```

### Functions as variables or parameters

A function can also be assigned to a variable:

```python
fnc = my_function
fnc()
```

   That way, you can also pass a function as an argument to another function:

```
def minmax(x, y, z, func):
  return func(x, y, z)
```

```
print(minmax(1, 2, 3, min))
print(minmax(1, 2, 3, max))
```

We will later make use of this feature when filtering, building or sorting lists.

## Defining functions

### Defining a function yourself

In Python, you can also define your own functions by using the keyword ‘def’. For example:

```python
def my_function():
  print("Hello from a function!")
```

```python
my_function() # output: Hello from a function!
```

 Python does not use curly braces or the keyword ‘end’ to indicate the end of the function. In Python, code indentation is part of the syntax, which in the case of a function means that all indented code after the colon is part of the function!  
In the following example, this explains why the third print statement is executed first:

```
def my_function_2():
  print("First print is inside function")
  print("Second print is inside function")
print("Third print is outside function")
my_function_2()
```

To indent your code, you use the tab key. Editors convert that to four spaces. Editors that support Python coding automatically indent the code after a colon.

### Default arguments

When defining a function, you can also include default arguments. These arguments do not have to be defined when called. If they are not defined, they are given the default value. If we have one default argument, we place it at the end since arguments are normally evaluated from left to right.

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

When there are multiple default arguments, we must explicitly specify the name of the argument when calling the function. We call this *keyword arguments*. We can do the same for regular arguments, by the way.

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

### Own developed modules

We can also use functions from our own developed modules. Every Python file is a module. For example, if we have a Python file myfunctions.py with the following code:

```python
# myfunctions.py
def welcome(name):
  print(f"Welcome {name}")
        
def good_morning(name):
	print(f"Good morning {name}")
```

Then, in the same folder, we can develop another `file greeting.py` that will look like this:

```python
# greeting.py
from myfunctions import welcome, good_morning
name = input("Give your name: ")
welcome(name)
good_morning(name)
```

We will see in a later chapter how to define more complex structures of modules with *packages*.

### if \_\_name\_\_ == " \_\_main\_\_" 

When we write a script that contains functions, we have to bear in mind that there may come a time when other pieces of code can import this script as a module to make use of that function. In that case, the idea is to use the functions, but not to execute the script immediately upon import. 

So we need to distinguish in our script between top-level code, which is code that is directly in the called script and executed there, and code that is wrapped in functions. When we have Python file with functions as well as top-level code, we will prefix the top-level code with `if __name__ == ‘__main__’:`. 

The variable `__name__` contains the name of the active module. If the script is called directly (and not from an import), that variable is given the value `‘__main__’`. So the above statement means: run this code only when this file is called directly and do not run it from an import. This way, you can define a script that can be executed on its own, but whose functions can also be used during an import.

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

If the script is executed on its own (stand-alone), then the function `main()` is called, but you can also do an import in another script. `main()` is then not called automatically when executing the import statement, but you can call the function `greet()` and `main()` in that other script at a time of your choosing.

### Anonymous functions (lambda)

When the code within a function is short, we like to define it as an anonymous function or a lambda function. We can then assign a lambda function to a variable or pass it along as an argument to another function.

A lambda function consists of the following components:

- the keyword *lambda* (after the Greek letter ‘l’),
- the list of arguments
- a colon, 
- the return statement (without the keyword *return*).

```python
sum = lambda x, y: x + y
print(sum(1, 2)) # output: 3
```

In the example below, we define a function `minmax()` that itself has a function as one of its arguments. We can define this argument as a lambda function.

```python
def minmax(x, y, z, func):
  return func(x, y, z)

my_function = lambda x, y, z: (x + y + z) # assign lambda function to variable
print(minmax(2, 3, 4, my_functions)) # output: 9
      
# define lamba function directly in function call
print(minmax(2, 3, 4, lambda x, y, z: (x * y * z))) # output: 24
      
# same, but with explicit naming of arguments
print(minmax(x=2, y=3, z=4, func=lambda x, y, z: ((x + y) ** z))) # output: 625
```

We will be happy to use lambda functions in the filter and sort function.

## The function dir()

When we use a module, we would like to know which attributes or functions that module contains. We can do that with the dir function. 

For example, if we want to know what functions the module random has, we can do so as follows:

```python
>>> import random
>>> dir(random)
['BPF', 'LOG4', 'NV_MAGICCONST', 'RECIP_BPF', 'Random', 'SG_MAGICCONST', 'SystemRandom', 'TWOPI', '_ONE', '_Sequence', '_Set', '__all__', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', '_accumulate', '_acos', '_bisect', '_ceil', '_cos', '_e', '_exp', '_floor', '_index', '_inst', '_isfinite', '_log', '_os', '_pi', '_random', '_repeat', '_sha512', '_sin', '_sqrt', '_test', '_test_generator', '_urandom', '_warn', 'betavariate', 'choice', 'choices', 'expovariate', 'gammavariate', 'gauss', 'getrandbits', 'getstate', 'lognormvariate', 'normalvariate', 'paretovariate', 'randbytes', 'randint', 'random', 'randrange', 'sample', 'seed', 'setstate', 'shuffle', 'triangular', 'uniform', 'vonmisesvariate', 'weibullvariate']
```

We can apply this to any object: a built-in module, an installed module, a self-written module, a variable, an object of a class, and so on.

