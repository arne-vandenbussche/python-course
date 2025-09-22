# Klassen en objecten

## Doelstellingen

Op het einde van dit hoofdstuk kan je:

- een klasse definiëren met attributen en methoden,
- van een klasse objecten creëren,
- de objecten gebruiken in een Python-programma,
- omgaat met de zichtbaarheid (public, private),
- subklassen van een klasse definiëren,
- abstracte klassen definiëren,
- gebruik maken van polymorfisme.


## Documentatie

[Officiële documentatie over klassen](https://docs.python.org/3/tutorial/classes.html)


## Een klasse definiëren

Zoals we al eerder aanhaalden, bevat Python voorzieningen voor functioneel programmeren, maar ook voor objectgeoriënteerd programmeren. We kunnen dus in Python klassen definiëren en van die klassen objecten instantiëren. 

Nemen we het voorbeeld van een klasse `Car` met twee attributen: brand, color.

In onderstaand voorbeeld definiëren we de klasse `Car` en instantiëren we die klassen in een aantal objecten.

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

Wat zien we hier:

- De naam van de klasse wordt voorafgegaan door het keyword `class`.
- Bij conventie geven de klasse een naam met een hoofdlettter.
- De klassenaam wordt gevolgd door een dubbelpunt.
- De functie __init__ is de constructor voor de objecten van de klasse.
- Bij elke functie geven we eerst `self` mee als argument.
- Een attribuut definieer je in door het attribuut te laten voorafgaan door `self.` Dat gebeurt meestal in de constructor.
- Een klasse instantiëren, m.a.w. een object creëren van een klasse gebeurt door de naam van de klasse te geven, met de argumenten van de constructor (zonder `self`).
- Een methode of attribuut gebruik je met de dot-notaties: de naam vna het object, gevolgd door een punt, gevolgd door de methode of het attribuut.
- De methode `__str__` bepaalt wat er gebeurt als we aan object afdrukken.


## Encapsulation en data hiding

Zoals we weten, is een voordeel van objectgeoriënteerd programmeren dat we de implementatie van een methode verbergen voor de buitenwereld. We kunnen methodes en attributen verbergen wanneer we ze niet public, maar private maken. Standaard zijn methodes en attributen van een Pythonklasse publiek. Je kan ze private maken door het attribuut te laten voorafgaan door twee lages streepjes. Om de attributen toegankelijk te maken, moeten we getters en setters definiëren.

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

## Overerving

Om een subklasse van een klasse te maken, zetten we de naam van de moederklasse tussen haakjes na de naam van de klasse. De subklasse neemt de methodes en attributen van de moederklasse over, maar kan deze ook overschrijven (override) of de subklasse kan extra attributen of methodes definiëren.

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

# Klasseattributen en klassemethodes

Klasseattributten en klassemethodes horen niet bij objecten van de klasse, maar bij de klasse zelf. We weten dat we hiermee zuinig moeten omgaan, maar Python voorziet deze mogelijkheid wel. We noemen deze ook statische attributen of statische methodes.

Een statisch attribuut definiëren we gewoon in de klasse zonder deze te laten voorafgaan door het sleutelwoord `self`. 

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

Een klassemethode geven we niet het argument `self` en we laten de methode voorafgaan door de decorator `@classmethod`. We roepen de methoden niet aan bij het object (alhoewel dit wel kan), maar bij de klasse zelf.

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

## Abstracte klassen

Om een abtracte klasse te definiëren moet je gebruik maken van de library `abc`. De klasse moet ervan van de klasse `ABC`. Voor de abstracte methodes gebruiken we de decorator `@abstractmethod`.

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

We kunnen hier geen object van de klasse `Vehicle` definiëren, maar we kunnen wel overerven van die klasse.

