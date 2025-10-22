# Classes and objects

## Objectives

By the end of this chapter, you will be able to:

- define a class with attributes and methods,
- create objects from a class,
- use the objects in a Python program,
- handle visibility (public, private),
- define subclasses of a class,
- define abstract classes,
- use polymorphism.


## Documentation

[Official documentation about classes](https://docs.python.org/3/tutorial/classes.html)


## Define a class

As we touched on earlier, Python includes facilities for functional programming, as well as object-oriented programming. Thus, we can define classes in Python and instantiate objects from those classes. 

Let us take the example of a class `Car` with two attributes: brand, color.

In the example below, we define the class `Car` and instantiate those classes into a number of objects.

```python
class Car:
    def __init__(self, brand, color):
        self.brand = brand
        self.color = color
    
    def __str__(self):
        return f"{self.color} {self.brand}"
  
  
if __name__ == '__main__':

    car1 = Car("Mercedes", "green")
    car2 = Car("Bmw", "blue")
    car3 = Car("Audi", "orange")

    for car in [car1, car2, car3]:
        print(car)
```

What do we see here:

- The name of the class is preceded by the keyword `class`.
- By convention, we give the class a name with a capital letter.
- The class name is followed by a colon.
- The function `__init__` is the constructor for the objects of the class.
- For each function, we first pass `self` as an argument.
- You define an attribute in by prefixing the attribute with `self.` This is usually done in the constructor.
- Instantiating a class, i.e. creating an object of a class, is done by giving the name of the class, with the arguments of the constructor (without `self`).
- A method or attribute is used with dot notations: the name of the object, followed by a dot, followed by the method or attribute.
- With the method `__str__`, we define what the result when we print a car object.


## Encapsulation and data hiding

As we know, an advantage of object-oriented programming is that we hide the implementation of a method from the outside world. We can hide methods and attributes when we make them private rather than public. By default, methods and attributes of a Python class are public. You can make them private by preceding the attribute with two underscores. To make private attributes accessible, we need to define getters and setters.

```python
class Car:
  
    def __init__(self, brand, color):
        self.__brand = brand  # private
        self.__color = color
  
    def get_brand(self):  # getter voor brand
        return self.__brand
  
    def get_color(self):  # getter voor color
        return self.__color
  
    def set_color(self, color):  # setter voor color
        self.__color = color
  
    def __str__(self):
        return f"{self.__color} {self.__brand}"

if __name__ == '__main__':

    car = Car("Ferrari", "red")
    print(f"You have a {car}!")
    car.set_color("black")
    print(f"Now you have a {car}!")
```

## Inheritance

To create a subclass of a class, we put the name of the parent class in brackets after the name of the class. The subclass adopts the methods and attributes of the parent class, but can also override them or the subclass can define additional attributes or methods.

```python
class Robot:
    """
    Class representing a talking robot.
    """

    def __init__(self):
        """
        We set the default name of the Robot
        Because we define a subclass Robot, we set the attribute as protected
        by adding one underscore before it.
        This is not a enforced. It is just a convention.
        """
        self._name = "Nameless"  # start with one underscore, is merely a convention

    def say_hello(self):
        print("Hello, I am " + self._name + "!")

    def rename(self, name):
        self._name = name

    def get_name(self):
        return self._name


# TerminatorRobot inherits from Robot
class TerminatorRobot(Robot):
    """
    Class representing a robot in the future
    """

    def __init__(self):

        super().__init__()  #  call the constructor of the super class
        #Robot.__init__(self)  # alternative for super().__init__()

        self.eyes = "laser eyes"  # new attribute. _name is inherited 

    # Overrides the method say_hello from the super class
    def say_hello(self):

        super().say_hello()  # We first call the method of the super class
        #Robot.say_hello(self)  # alternative for super().say_hello()

        print("I have " + self.eyes + "...")  # we add an element to the method


if __name__ == '__main__':
    my_robot = Robot()
    my_robot.say_hello()
    my_robot.rename("Kirk")
    my_robot.say_hello()
    naam = my_robot.get_name()

    print("The robot is called " + naam)
    print("The robot is called " + my_robot._name)  # the attribute is not really protected

    terminator = TerminatorRobot()
    terminator.rename("Arnold")
    terminator.say_hello()
```

## Class attributes and class methods

Class attributes and class methods do not belong to objects of the class, but to the class itself. We know that we have to use these sparingly, but Python does provide them. We also call these static attributes or static methods.
We simply define a static attribute in the class without preceding it with the keyword `self`. 

````python
class Dog:

    kind = 'canine'         # a class variable shared by all instances of the class

    def __init__(self, name):
        self.name = name    # object attribute unique for each object of the class

        
if __name__ == '__main__':
    d = Dog('Fido')
    e = Dog('Buddy')
    print(d.kind)                  # 'canine', shared by all dogs
    print(e.kind)                  # 'canine, shared by all dogs
    print(d.name)                 # unique for d, thus 'Fido'
    print(e.name)                 # unique for e, thus 'Buddy'


````

We do not give a class method the argument `self` and we precede the method by the decorator `@classmethod`. We do not call the methods to the object (although this can be done), but to the class itself.

````python
class Person:
    _population = 0   #  class attribute

    def __init__(self, name):
        self.name = name
        Person._population += 1  # the population gets larger when creating a new person

    @classmethod
    def total_population(cls):   
        return cls._population

if __name__ == '__main__':
    john = Person("John")
    pete = Person("Pete")

    print(Person.total_population())  # should be two
````

## Abstract classes

To define an abtract class, you must use the library `abc`. The class must inherit from the class `ABC`. For the abstract methods, we use the decorator `@abstractmethod`.

```python
from abc import ABC, abstractmethod

class Vehicle(ABC):  # abstract inherits from class AB

    def __init__(self, speed):
        self.speed = speed

    @abstractmethod  # decorator showing that the method is abstract
    def drive(self):
        pass  # pass because an abstract method had no implementation


class Bike(Vehicle):
    def drive(self):
        print(f"I am driving my bike. My speed is {self.speed} km/h.")

        
class SportsCar(Vehicle):
    def drive(self):
        print(f"I am racing and I am going really fast! {self.speed} km/h!")


if __name__ == '__main__':
    my_bike = Bike(25)
    my_bike.drive()

    my_porsche = SportsCar(185)
    my_porsche.drive()
```

We cannot create an object from the class `Vehicle` but we kan inherit from this class.

## Data classes

In many programs, we create classes that mainly store data — for example, to represent a Student, a Book, or a Point in 2D space. Such classes often contain only attributes and very little logic.
In Python, there is a convenient shortcut for writing these data containers: the **data class**.

A data class automatically generates several useful methods for you, such as `__init__()`, `__repr__()` and `__eq__()`. This makes your code shorter and clearer.

To use data classes, import the dataclass decorator from the dataclasses module:

```python
from dataclasses import dataclass

@dataclass
class Student:
    name: str
    number: int
    email: str
```

This automatically creates an initializer like:

```python
def __init__(self, name: str, number: int, email: str):
    self.name = name
    self.number = number
    self.email = email
```

You can now create and print students easily:

```python
s1 = Student("Alice", 123, "alice@example.com")
s2 = Student("Bob", 456, "bob@example.com")

print(s1)
# Output: Student(name='Alice', number=123, email='alice@example.com')
```

Data classes are especially useful for:

- keeping your code concise,
- comparing objects (they implement `__eq__` automatically),
- or converting to and from dictionaries (using `dataclasses.asdict()`).

Example:

```python
from dataclasses import asdict

print(asdict(s1))
# {'name': 'Alice', 'number': 123, 'email': 'alice@example.com'}
```

