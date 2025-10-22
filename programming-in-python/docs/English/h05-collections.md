# Collections: lists, tuples, sets, dictionaries

## Objectives

After this chapter, you will be able to work with lists, tuples, sets, and dictionaries:

* Access, add, remove, and modify elements (where possible),
* Correctly apply the in-operator,
* Combine collections,
* Apply set operations (union, intersect, difference, etc.),
* Copy collections,
* Sort lists and tuples,
* Filter and transform into a modified collection (map()),
* Use comprehensions,
* Use the json module to convert a dictionary or a list of dictionaries to json and vice versa.

## Lists

We have already discussed lists in a previous lesson. Therefore, this chapter is largely a review of what we have already seen.

### Characteristics

Lists have the following properties:

- They are **ordered**;
- They are **heterogeneous**, meaning that the elements do not have to be of the same data type;
- They are **mutable**, which means that their elements can be changed, and you can add or delete elements.

### Creating lists

Lists are created using square brackets, or `list()`.

```python
lst0 = []  # empty list
lst1 = [1, 2, 3, 4]  # list of integers
lst2 = ["Victor", "Axel", "Emma", "Aïsha"]  # list of strings
lst3 = [3.1415, "pi", True, lst1]  # list of heterogenuous elements
```

### Lenght of a list

You can get the lenght of a list using the function `Len()`.

```python
print(len(lst2)) # 4
```

### Select or replace elements in the list

We use square brackets and the index to access an element in the list. The index starts at 0. We can also use **slicing**.

```python
print(lst1[0])  # first element of the list
print(lst1[1:3]) # [2, 3]
lst3[1] = lst3[1].upper()  # [3.1415, 'PI', True, [1, 2, 3, 4]]
print(lst3)
```

When you assign a list to a variable, the variable contiains a **reference** to the list.

```python
lst1[-1] = 10  # laatste element vervangen [1, 2, 3, 10]
print(lst1) #[1, 2, 3, 10]
print(lst3[-1])  # [1, 2, 3, 10] laatste element in lst3 is lst1 en is dus ook gewijzigd!
```

### Searching a list and iterating through a list

We iterate through a list using a for loop:

```python
for num in lst1:
  print(num, end="\t")
```

Check whether a certain element is in the list:

```python
if "Alice" in lst2:
  print("Alice is in the house!")
else:
  print("Where the hell is Alice?")
```

Getting the index of a certain element:

```python
lst2.index("Victor") # 0
lst2.index("Alice") # ValueError. 'Alice' is not in list
```

### The `enumerate()` Function

When you loop over a list, you often need both the **index** (position)
and the **value** of each element.\
You *could* keep track of the index yourself with a counter, but Python
provides a much cleaner way: the built-in **`enumerate()`** function.

#### Example without `enumerate()`

``` python
fruits = ["apple", "banana", "cherry"]

index = 0
for fruit in fruits:
    print(index, fruit)
    index += 1
```

#### Example with `enumerate()`

``` python
fruits = ["apple", "banana", "cherry"]

for index, fruit in enumerate(fruits):
    print(index, fruit)
```

Output:

    0 apple
    1 banana
    2 cherry

By default, `enumerate()` starts counting from `0`, but you can choose a
different start index:

``` python
for index, fruit in enumerate(fruits, start=1):
    print(index, fruit)
```

Output:

    1 apple
    2 banana
    3 cherry

This makes your code cleaner, more Pythonic, and less error-prone when
you need both the index and the value of each item in a list.

### Add elements to a list

Relevant functions to add elements to a list are **extend()**, **append()**, **insert()** and the **plus-operator**.

* list.append(object): append object to the end of the list.
* list.extend(iterable): exend list by appending the elements of another list. It takes an iterable as argument.
* list.insert(index, object): insert an object before the index.
* Plus-operator: concatenate lists, combine multiple lists into one list

 ```python
 lst1.extend([5, 6, 7, 8, 9, 10])  # combines two lists
 print(lst1)
 lst2.append("Bernard")  # the element is added to the end of the list
 lst2.insert(1, "Norbert")  # "Norbert" is added at position 1
 print(lst2)
 ```

```python
abc = ["a", "b", "c"]
de = ["d", "e"]
fghi = ["f", "g", "h", "i"]
print(abc + de + fghi)
# ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i']
```

### Remove elements from a list

Removing elements from a list can be done with **pop()**, **remove()** or the **del**.

* list.pop(index): removes the element at a certain index and returns it, defaults to the last element;
* list.remove(value): removes the first occurrence of a value, returns an ValueError when the element does not exist.
* del: is used to remove slices of a list or clear a whole list.

```python
print(lst3.pop())  # remove last element from the list
print(lst3)
print(lst3.pop(0))  # remove element at index 0
print(lst3)
lst2.remove("Norbert")  # remove element "Norbert"
del lst2[-1]  # remove last element
print(lst2)
```

### Useful functions

Reversing a list:

```python
lst2.reverse()
print(lst2) # ['Korneel', 'Joris', 'Piet', 'Jan']
lst2 = lst2[::-1]
print(lst2) # ['Jan', 'Piet', 'Joris', 'Korneel']
```

Sort a list:

```python
lst1.sort() # changes the list, sorts it
lst1.sort(reverse=True) # changes a list, sorts it in reverse order
lst1.sort(key=str.lower) # sorts alphabatically by the lower case value of the strings
new_list = sorted(lst1) # returns a new list which is the sorted version of lst1
```

Je can apply function to a list of numerical values:

```python
print(sum(lst1))  # returns the sum of all elements in the list
print(max(lst1))  # returns the element with the highest value
print(min(lst1))  # returns the element with the lowest value
print(count(lst1)) # returns the number of times an element appears in the list.
	# Count also works with lists of strings
print(lst1)
```

### Copy lists

We mentioned earlier that a variable has a reference to the list. Assinging the list to a new variable, results in a situation in which two variables point to the same list. If, however, we want to copy the elements of a list to a new list, we use the function **copy()**.

```python
abc1 = ["a", "b", "c"]
abc2 = abc1  # abc1 and abc2 refer to the same list
abc2.append("d")
print("abc1:", abc1) # abc1: ['a', 'b', 'c', 'd']
print("abc2:", abc2) # abc2: ['a', 'b', 'c', 'd']
```

```python
abc3 = abc1.copy()  # abc3 is a new list with the same values as abc1
abc3.append("e")
print("abc1:", abc1) # abc1: ['a', 'b', 'c', 'd']
print("abc3:", abc3) # abc3: ['a', 'b', 'c', 'd', 'e']
```

In the context op copying it is worthwhile to point out the difference between the operators `==` and `is`. The operator `==` checks whether the contents of two variables is equal (value equality), while `is` checks whether the references are equal (reference equality).

```python
abc3.pop()  # remove "e"
print("abc1:", abc1)
print("abc3:", abc3)
print("abc1 == abc2:", abc1 == abc2)  # same content, so True
print("abc1 is abc2:", abc1 is abc2)  # same object, so True
print("abc1 == abc3:", abc1 == abc3)  # same contens, so True
print("abc1 is abc3:", abc1 is abc3)  # different objects, so False
```



## Tuples

### Characteristics

- They are **ordered**;
- They are **heterogeneous**, elements can be of different data types;
- They are **immutable**, meaning that once created, their elements cannot be changed.

Iterating tuples is faster than with lists because they are immutable. When you want to work with a list of constants, it is the safer choice.

### Create a tuple

Tuples consists of a list of values between brackets, separated by a comma.

```python
t1 = ("apple", "mango")
t2 = "banana", "cherry"
print(t1, "is an object of", type(t1))
# ('apple', 'mango') is an object of <class 'tuple'>

print(t2, "is an object of", type(t2))
# ('banana', 'cherry') is an object of <class 'tuple'>

# mixing data types
t1 = ("apple", 3, 1.4)
t2 = ("apple", 3, 1.4, ("banana", 5))

# create an empty tuple
empty_tuple = ()
print(empty_tuple) # ()
print(type(empty_tuple)) # <class 'tuple'>

# tuple with one element
t = (2, )
print(t) # (2,)
print(type(t)) # <class 'tuple'>

t = (2) # creates a variable with an integer
print(t) # 2
print(type(t)) # <class 'int'>
```

### Tuples are immutable

```python
fruit[-1] = "mango"
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-37-a16fa0115673> in <module>()
----> 1 fruit[-1] = "mango"

TypeError: 'tuple' object does not support item assignment

fruit.pop()
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-38-971343bd48cc> in <module>()
----> 1 fruit.pop()

AttributeError: 'tuple' object has no attribute 'pop'
```

You can of course create a new tuple and assign it to the same variable.

```python
tuple_fruit = ("apple", "banana", "cherry", "mango")
print(tuple_fruit) # ("apple", "banana", "cherry", "mango")
tuple_fruit = tuple_fruit[::-1]
print(tuple_fruit) # ('mango', 'cherry', 'banana', 'apple')
```

### Querying the number of elements

As with lists you can use the function **len()** to count the number of elements in the tuple.

```python
t1 = ("apple", "mango")
t2 = ("apple", 3, 1.4)
t3 = ("apple", 3, 1.4, ("banana", 5))
print(len(t1)) # 2
print(len(t2)) # 3
print(len(t3))  # 4
```

Mind: the lenght of t3 is four, not five. The last element in the tuple is a tuple itself `("banana", 5)`, and that is one element.

### The in-operator

You can use the **in**-operator in a **for**-loop to go through the elements in your tuple, as with lists:


```python
t1 = ("apple", 3, 1.4, ("banana", 5))
for element in t1:
  print(element)
```

You can also use the **in**-operator to test whether an element is part of a tuple:

```python
t1 = ("apple", "banana", "cherry")
print("banana" in t1) # True
print("mango" in t1) # False
```

### Tuples and variable assignment

As we mentioned earlier, Python gives you the possibility to put several variables at the left of the assignment symbol, and the same number of values at the right. Python will copy these values one by one to the variables at the left, in the same order. In the same way you can also put a tupple with the same number of elements at the left or the right of your assignment symbol. We call this unpacking.

A few examples will illustrate this:

```python
a, b = "apple", "banana"
print(a) # apple
print(b) # banana

(a, b) = "apple", "banana"
print(a) # apple
print(b) # banana

a = 1, 2, 3
print(a) # (1, 2, 3) 
# a is a tuple with three elements

t1, t2 = ("apple", "banana"), "cherry"
print(t1) # ('apple', 'banana')
print(t2) # cherry

# unpack a tuple
fruit = 'apple', 'banana', 'cherry'  # variabele fruit is a tuple with 3 elements
print(fruit) # ('apple', 'banana', 'cherry')
fruit1, fruit2, fruit3 = fruit  # assign the three elements of fruit to three different variables
print(fruit2) # banana
```

### Tuples and functie return values

Usually a function will return one value. If we wish to return several values, you can do that. In fact, your function will return a tuple.

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

### Select individual elements

As with lists, you can access individual elements using the **index**. You can also use **slicing**.

```python
fruit = ("apple", "banana", "cherry", "strawberry")
print(fruit[2])  # third element (cherry) as indices start at 0
print(fruit[1:4]) # ('banana, 'cherry', 'strawberry')
print(type(fruit[1:4])) # <class 'tuple'>
print(fruit[1:]) #  ('banana, 'cherry', 'strawberry')
print(fruit[1:3]) # ('banana', 'cherry')
print(fruit[1:-1]) # ('banana', 'cherry')
```

### Iterating and searching in a tuple

You can iterate through your tuple using indices:


```python
for i in range(len(fruit)):
  print(fruit[i])

print()

i = 0
while i < len(fruit):
  print(fruit[i])
  i += 1
```

Of course, the version with the in-operator is faster and cleaner.

```python 
for piece_of_fruit in fruit:
    print(piece_of_fruit)
```

The **index()** method in tuples is used to find the first occurrence of a specified value and return its index (position). If the value is not found, it raises a ValueError.

```python
my_tuple = (10, 20, 30, 40, 20)
index_of_20 = my_tuple.index(20)
print(index_of_20) # 1
```

If you want to specify the range within which to search, you can provide optional start and end arguments:

```python
index_of_20 = my_tuple.index(20, 2)  # Start searching from index 2
print(index_of_20) # 4
```

Tuples also have a **count()**-method:

```python
t = (1, 2, 3, 4, 3, 2, 1)
print(t.count(3))  # geeft aan hoeveel keer het element 3 in de tuple voorkomt (2)
```

You can check whether an element is present in a tuple using the in operator. This operator returns True if the element exists in the tuple and False if it does not.

```python
my_tuple = (10, 20, 30, 40)

# Check if 20 is in the tuple
is_present = 20 in my_tuple
print(is_present) # True

# Check if 50 is in the tuple
is_present = 50 in my_tuple
print(is_present) # False
```

Iterating through a tuple is similar to lists:

```python
my_tuple = (10, 20, 30, 40)

# Iterating through the tuple, print elements separated by a tab
for item in my_tuple
    print(item, end="\t")
```


### Calculation in tuples

Like with lists you can use functions such as **max()** and **min()** to calculate the maximum and minimum value within a tuple. There is also a function **sum()** to return the sum of all numeric elements in a tuple.

```python
t1 = (327, 419, 101, 667, 925, 225)
print(max(t1)) # 925
print(min(t1)) # 101
print(sum(t1)) # 2664
```

### Concatenation and repetition

You can use the plus-operator to concatenate tuples.

```python
a = (1, 2, 3)
b = (4, 5)
print(a + b) # (1, 2, 3, 4, 5)
```

In Python, the * operator is used to **repeat** tuples a specified number of times. When you multiply a tuple by an integer, it creates a new tuple where the elements are repeated.

```python
my_tuple = (1, 2, 3)

repeated_tuple = my_tuple * 3
print(repeated_tuple) # (1, 2, 3, 1, 2, 3, 1, 2, 3)
```

Repitition works with lists too.

### Sort and reverse tuples 

A tuple is immutable, so you can not change the tuple to sort is, but you can create a new sorted tuple.

```python
print(sorted(fruit, reverse=True))
```

Reversing a tuple can be done in two ways: using slicing or using the function `reversed`.

```python
t = (1, 2, 3, 4)
reversed_t = t[::-1]
print(reversed_t)   # (4, 3, 2, 1)
```

This is the simples and the fastest method. The slice [::-1] means: start from the end, move backwards by steps of -1.

```python
t = (1, 2, 3, 4)
reversed_t = tuple(reversed(t))
print(reversed_t)   # (4, 3, 2, 1)
```

The `reversed()` function returns an iterator, so you need to wrap it in `tuple()` to get a new tuple.

### Copy tuples

Tuples have no copy() function, but the can concaternate with an empty tuple.

```python
a1 = (1, 2, 3)
a2 = a1  # a1 and a2 reference the same tuple
print("a1:", a1) # a1: (1, 2, 3)
print("a2:", a2) # a2: (1, 2, 3)
print("a1 == a2:", a1 == a2)  # a1 == a2: True (same content in the same order, so True)
print("a1 is a2:", a1 is a2)  # a1 is a2: True (same reference, so True)

a3 = a1 + ()  # creates new tuple
print("a3:", a3) # a3: (1, 2, 3)
print("a1 == a3:", a1 == a3)  # a1 == a3: True (same content in the same order, so True)
print("a1 is a3:", a1 is a3)  # a1 is a3: False (different reference, so False)
```

### Convert tuples to lists

Tuples can be converted to lists and vice versa.

```python
list_fruit = ("apple", "banana", "cherry", "strawberry")
list_fruit = list(tuple_fruit)
print(list_fruit) # ["apple", "banana", "cherry", "strawberry"]
tuple_fruit_2 = tuple(list_fruit) # ("apple", "banana", "cherry", "strawberry")
print(tuple_fruit_2)
```

## Sets

Sets are unordered data structures that can contain only unique elements. Few programming languages support the use of sets, but Python does. Sets are not often used, but can sometimes provide a useful solution to a problem.
You can think of sets as mathematical collections. In mathematics, a set is a collection of elements that are all unique, and each element is either in the set or not in the set. There are certain operators that allow sets to be combined.

### Characteristics

- They are **unordered**;
- They contain **unique elements**, meaning no duplicates are allowed;
- They are **mutable**, meaning you can add or remove elements, but you cannot change individual elements.
- They are **heterogenuous**, the elements can have different data types.

### Create a set

To create a set that already contains elements, place those elements between curly braces. Alternatively, you can call the set() function and pass a list with the elements as arguments.

```python
fruitset = { 'apple', 'banana', 'cherry', 'strawberry', 'mango'}
print(fruitset) # {'apple', 'banana', 'cherry', 'mango', 'strawberry'} (unordered)
s = set([1, 2, 3])
print(s) # {1, 2, 3}
```

The elements in a set are unique:

```python
s = {1, 1, 2, 2, 3, 3}
print(s) # {1, 2, 3}
```

If you want to create a set consisting of the different letters of a string, you can call set() with the string as argument. Again, duplicate letters are automatically ignored:

```python
helloset = set("hello world")
print(helloset) # {'w', 'l', 'e', ' ', 'r', 'o', 'd', 'h'}
```

Note that the space is also included as an element, as it is obviously also a character.
Python uses dictionaries to implement sets. Specifically, it implements the elements of a set as keys of a dictionary. We will discuss dictionaries in more detail below. Because Python uses dictionaries to implement sets, you might think that you can create an empty set by assigning {} to a variable. But as we are about to see, that creates an empty dictionary, not an empty set. Instead, you create an empty set by assigning the return value of the function set() (with no arguments) to a variable:

```python
empty_set = set() # not {}
print(empty_set) # set()
print(type(empty_set)) # <class 'set'>
```

The last example shows that in a set, the elements need not be of the same data type. However, the elements must be immutable. Therefore, you can include a tuple as an element, but not a list or set.

```python
print({1, 2, "abc", True, False, (1, 2, 3)}) # {False, 1, 2, 'abc', (1, 2, 3)}

print({1, 2, "abc", True, False, {1, 2, 3}})
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-65-4cad94302ef0> in <module>()
----> 1 print({1, 2, "abc", True, False, {1, 2, 3}})

TypeError: unhashable type: 'set'
```

### Iterate and search

```python
fruitset = { 'apple', 'banana', 'cherry', 'strawberry', 'mango'}
if "kiwi" not in fruitset: # True
	print("It's a pity there is no kiwi.")

for element in fruitset: # are passed through unordered
	print(element, end=" ")
# strawberry mango cherry apple banana

# length
print(f"\nFruitset has {len(fruitset)} elements.") # Fruitset has 5 elements.
```

### Add and remove elements from a set

With the **add()** method, you can add elements to a set:

```python
fruits = {"apple", "banana", "cherry", "strawberry", "mango"}
fruits.add("pear")
print(fruits) # {'strawberry', 'mango', 'pear', 'banana', 'apple', 'cherry'}
```

As you can see, the set is not ordered to you cannot predict where the element is added.

With the **remove()** method or the **pop()**, you can remove elements:

```python
fruits.remove("cherry")
print(fruits) # {'strawberry', 'mango', 'pear', 'banana', 'apple'}
fruits.pop()
print(fruits) #{'mango', 'pear', 'banana', 'apple'}
```

You cannot predict which element will be removed with the **pop()** method.

### Set operations

Python sets support several mathematical set operations such as:

- **Union:** Combines two sets.
- **Intersection:** Finds common elements between two sets.
- **Difference:** Finds elements in one set that are not in the other.
- **Disjunction**: no common elements.
- **Subset**.

```python
set1 = {"a", "b" , "c"}
set2 = {1, 2, 3}

# union
set3 = set1.union(set2)
print(set1) # {'b', 'a', 'c'}
print(set2) # {1, 2, 3}
print(set3) # {'a', 1, 'c', 2, 3, 'b'}

# update is an altnernative, but the first set is modified in that case
set1.update(set2)
print(set1) # {1, 'b', 'a', 2, 3, 'c'}
print(set2) # {1, 2, 3}

# duplicates are excluded
computers1 = {"HP", "Dell", "Asus", "Apple"}
computers2 = {"Lenovo", "HP", "Apple", "Acer"}
print(computers1.union(computers2)) # {'Apple', 'Acer', 'Asus', 'HP', 'Dell', 'Lenovo'}

# intersection
my_intersection = computers1.intersection(computers2)
print(computers1)
print(computers2)
print(my_intersection) # {'Asus', 'Dell'}

# isdisjoint (disjunction), have no common elements
print(computers1.isdisjoint(computers2))  # False because intersection is not empty
print({1, 2, 3}.isdisjoint({4, 5, 6}))  # True because intersection is empty

# issubset - issuperset
A = {1, 2, 3}
B = {1, 2, 3, 4, 5}

print(A.issubset(B))  # True because A is a subset of B
print(B.issuperset(A))  # True for the same reason
```

### Copy sets

Copying is similar to lists

```python
A1 = {1, 2, 3}
A2 = A1  # A1 and A2 refer to the same set
print("A1 == A2:", A1 == A2)  # True because they have the same values
print("A1 is A2:", A1 is A2)  # True because they refer to the same object

A3 = A1.copy()  # A3 is a new set with the same values as A1
print("A1 == A3:", A1 == A3)  # True because they have the same values
print("A1 is A3:", A1 is A3)  # False because they refer to different objects
```

Sets are not ordered, so the following is true:

```python
A4 = {3, 2, 1}
print("A1 == A4:", A1 == A4)  # A1 == A4: True
```

### Convert sets to lists

You cannot sort the elements in a set as long as they are in the set. However, you can use a list casting to convert the set into a list, and then sort that list. That way, you can be sure in which order the elements will be traversed when you apply a loop:

```python
fruitset = { ‘apple’, ‘banana’, ‘cherry’, ‘strawberry’, ‘mango’}
for element in fruitset: # are passed through unordered
	print(element, end=", ")
# cherry banana strawberry mango apple
print()

fruitlist = list(fruitset) # convert set to list
fruitlist.sort() # sort elements
for element in fruitlist: # list is sorted
	print(element)
# apple banana cherry mango strawberry
```

### Frozenset

Python has the **frozenset** as a variant of the **set** type . You create a frozenset via the `frozenset()`constructor. As the name suggests, the elements of a frozenset cannot be changed. So you create a frozenset immediately when you call the frozenset() constructor, because once the frozenset exists you cannot add or remove elements. In other words, unlike regular sets, frozensets are **immutable**. All regular set methods also work on frozensets, except those that try to change the set (e.g. add() to add elements or remove() to remove elements). If you try to call such a method for a frozenset, you get a syntax error.

The use of frozensets is that they are faster than sets.

```python
ruit1 = frozenset(["apple", "banana", "cherry"])
fruit2 = frozenset(["banana", "cherry", "strawberry"])
print(fruit1.union(fruit2))    # frozenset({'banana', 'strawberry', 'cherry', 'apple'})
```

```python
fruit1.add("pear")
```

```bash
Traceback (most recent call last):
  File "/h5-collections/sets.py", line 19, in <module>
    fruit1.add("pear")
    ^^^^^^^^^^
AttributeError: 'frozenset' object has no attribute 'add'
```

## Dictionaries

Tuples and lists (and also strings) are ordered data structures, which means they can be accessed via indices. But not all data collections have a natural way of being numerically ordered, and so these cannot be (easily) indexed. Python provides ‘dictionaries’ as a way to structure unordered data.

### Characteristics

A ‘dictionary’ (as the English word: ‘dictionary’, but that comparison backfires in Python) is an unordered data structure that contains a collection of elements. To find an element or value, you need to know the ‘key’ (‘key’) of the element.
Basically, a dictionary is a collection of ‘keys’ with associated values. In other programming languages, you sometimes encounter dictionaries as ‘associative memories’ or ‘associative arrays’. Any immutable datatype may be used as a key. A common data type used as a key is the string, which is immutable in Python.
In summary, dictionaries have the following properties:

- they are **unordered**;
- they are **heterogeneous**, which means that the elements need not be of the same data type;
- they are **mutable**, meaning their elements can be changed, and you can add or remove elements.
- they consist of **key/value** pairs; the keys must be immutable datatypes.

### Create a dictionary

Dictionaries are created with curly braces {}, similar to how you create lists with square brackets. You can create a dictionary with content by putting each element you want in it between the curly braces, using <key>:<value> syntax, and commas between the elements.
Below, we build a dictionary fruit basket, with three elements, namely the key ‘apple’ with value 3, the key ‘banana’ with value 5, and the key ‘cherry’ with value 50. You can interpret the numbers, for example, as the number of pieces of a particular fruit in the basket:

```python
fruit_basket = {"apple": 3, "banana": 5, "cherry": 50}
print(fruit_basket) # {'apple': 3, 'banana': 5, 'cherry': 50}
```

You can also use **dict()**. Here you use a `=` instead of a `:`.

```python
car = dict(brand="Ford", model="Mustang", year=1964)
print(car) # {'brand': 'Ford', 'model': 'Mustang', 'year': 1964}
```

You create an empty dictionary by making an assignment to a variable with {}:

```python
empty_dict = {}
```

Dictionaries are heterogeneous. The elements can be of different data types.

```python
person = {'name': "Jos", 'age': 58, 'car': car}
print(person)
# {'name': 'Jos', 'age': 58, 'car': {'brand': 'Ford', 'model': 'Mustang', 'year': 1964}}
```

### Accessing values

You can access the value associated with a key by using square brackets. If the key exists in the dictionary, it will return the corresponding value. If the key does not exist, it raises a KeyError.

```python
person = {"name": "John", "age": 30, "city": "New York"}

# Accessing values using keys
print(person["name"])  # Output: John
print(person["age"])   # Output: 30
```

If you try to access a key that doesn’t exist, it will raise a KeyError.

```python
print(person["country"])  # Raises KeyError: 'country'
```

The get() method is a safer way to access elements. It returns the value associated with the key if the key exists. If the key does not exist, it returns None (or a default value you can specify).

```python
person = {"name": "John", "age": 30, "city": "New York"}

# Accessing values using get() method
print(person.get("name"))    # Output: John
print(person.get("country")) # Output: None (since "country" key doesn't exist)

# Using a default value if the key doesn't exist
print(person.get("country", "USA"))  # Output: USA
```

Python provides methods to access all the keys, values, or both (key-value pairs) in a dictionary.

* keys(): Returns a view object that displays a list of all the keys.

* values(): Returns a view object that displays a list of all the values.

* items(): Returns a view object that displays a list of key-value pairs (tuples).

```python
person = {"name": "Alice", "age": 28, "city": "London"}

# Accessing all keys
print(person.keys())   # Output: dict_keys(['name', 'age', 'city'])

# Accessing all values
print(person.values()) # Output: dict_values(['Alice', 28, 'London'])

# Accessing all key-value pairs
print(person.items())  # Output: dict_items([('name', 'Alice'), ('age', 28), ('city', 'London')])
```

### Iterating and searching

You can loop over the view mentioned above to extract or use the data:

```python
# Looping through keys
for key in person.keys():
    print(key)

# Looping through values
for value in person.values():
    print(value)

# Looping through key-value pairs
for key, value in person.items():
    print(f"{key}: {value}")
```

You can use the in operator to check if a specific key exists in the dictionary.

```python
person = {"name": "Alice", "age": 28, "city": "London"}

# Check if a key exists in the dictionary
if "age" in person:
    print("Age is present in the dictionary")

if "country" not in person:
    print("Country is not present in the dictionary")
```

### Modifying dictionaries or their values

You can add a new key-value pair to a dictionary by simply assigning a value to a new key. If the key already exists, this operation will update the value associated with that key.

```python
# Create a dictionary
person = {"name": "Alice", "age": 28}

# Add a new key-value pair
person["city"] = "London"

print(person) # {'name': 'Alice', 'age': 28, 'city': 'London'}
```

You can modify the value associated with a key by reassigning a new value to that key. If the key exists, the value will be updated; if it doesn’t exist, a new key-value pair will be created.

```python
person = {"name": "Alice", "age": 28, "city": "London"}

# Modify the value associated with the key "age"
person["age"] = 29

print(person) # {'name': 'Alice', 'age': 29, 'city': 'London'}
```

There are several methods to remove elements from a dictionary: **del()**, **pop()** and **popitem()**.

You can remove a specific key-value pair from a dictionary using the del statement. This permanently deletes the key and its associated value.

```python
person = {"name": "Alice", "age": 29, "city": "London"}

# Remove the key-value pair with the key "city"
del person["city"]

print(person) # {'name': 'Alice', 'age': 29}
```

The pop() method removes the key-value pair for a given key and returns the value that was removed. If the key doesn’t exist, it raises a KeyError unless you provide a default value.

```python
person = {"name": "Alice", "age": 29, "city": "London"}

# Remove and return the value associated with the key "age"
age = person.pop("age")
print(age)      # Output: 29
print(person)   # Output: {'name': 'Alice', 'city': 'London'}
```

If the key does not exist, you can provide a default return value:

```python
non_existent = person.pop("country", "Key not found")
print(non_existent)  # Output: Key not found
```

The popitem() method removes and returns the **last** key-value pair added to the dictionary as a tuple. Since Python 3.7, dictionaries are insertion-ordered, so popitem() will remove the most recently added item. It raises a KeyError if the dictionary is empty.

```python
person = {"name": "Alice", "age": 29, "city": "London"}

# Remove the last added key-value pair
last_item = person.popitem()
print(last_item)  # Output: ('city', 'London')
print(person)     # Output: {'name': 'Alice', 'age': 29}
```

The clear() method removes all key-value pairs from the dictionary, leaving it empty.

```python
person = {"name": "Alice", "age": 29, "city": "London"}

# Clear the dictionary
person.clear()

print(person)  # Output: {}
```

With the **update()** method you can add a dictionary to an existing one

```python
fruit_basket = {"banana": 2, "apple": 5}
fruit_basket.update({"pear: 3", "kiwi": 2})
print(fruit_basket) # {'banana': 2, 'apple': 5, 'pear: 3', 'kiwi': 2}}
```

### Copy dictionaries

Dictionaries also have a **copy()** method. Note that two dictionaries are equal (==) if they have the same key/value pairs. Dictionaries are not ordered, so the order in which those pairs are defined does not matter.

```python
d1 = {'a': 1, 'b': 2, 'c': 3}
d2 = d1 # d1 and d2 refer to the same dictionary
print('d1 == d2:', d1 == d2) # d1 and d2 have the same content, so True
print('d1 is d2:', d1 is d2) # d1 and d2 refer to the same object, so True

d3 = d1.copy() # copy the contents of d1 into a new dictionary d3
print('d1 == d3:', d1 == d3) # d1 and d3 have the same content, so True
print('d1 is d3:', d1 is d3) # d1 and d3 refer to different objects, so False

d4 = {'c': 3, 'a': 1, 'b': 2}
print('d1 == d4:'', d1 == d4) # d1 and d4 have the same content, so True
```

## Sorting in Python

This is a good time to dive into sorting. What we explain here about sorting applies to lists, tuples, and strings. Sets and dictionaries cannot be sorted because they are unordered.

The sort() function modifies the list. By default, sorting is done in ascending order, but it can also be done in descending order.

```python
fruitlist = ["apple", "strawberry", "banana", "raspberry",
             "cherry", "banana", "durian", "mango"]
fruitlist.sort()
print(fruitlist)
# ['apple', 'banana', 'banana', 'cherry', 'durian', 'mango', 'raspberry', 'strawberry']

numlist = [314, 315, 642, 246, 129, 999]
numlist.sort(reverse=True)
print(numlist)
# [999, 642, 315, 314, 246, 129]
```

Tuples are *immutable*, meaning unchangeable. Therefore, this function cannot be used with that data type. Even with lists, it is not always a good idea to modify the list. We will look at an alternative later, but first, a bit more about the sort() function.

In the interactive version of Python, we can get more information about the sort() function using the help() function:

```python
>>> help(list.sort)
```

We get the following information:

```bash
Help on method_descriptor:

sort(self, /, *, key=None, reverse=False)
    Sort the list in ascending order and return None.

    The sort is in-place (i.e. the list itself is modified) and stable (i.e. the
    order of two equal elements is maintained).

    If a key function is given, apply it once to each list item and sort them,
    ascending or descending, according to their function values.

    The reverse flag can be set to sort in descending order.
```

So, as shown in the example above, we can sort in ascending or descending order.

In a previous chapter, we talked about lambda functions. The key argument expects a function, and lambda functions are particularly useful for this. Suppose we have a list of tuples with people and their height in centimeters. We want to sort them by name or height. To do this, we need to define a function that determines which key we want to sort by.

```python
people = [ ("John", 172), ("Fatima", 165), ("Igor", 168), ("Rune", 176), ("Anja", 174)]
name = lambda person: person[0]
height = lambda person: person[1]
people.sort(key=name)   # sorts the list of tuples by name
people.sort(key=height) # sorts the list of tuples by height
```

However, we don’t always want to modify our original list, but rather create a sorted copy. For that, we can use the `sorted()` function. This function can take tuples, strings, and lists as arguments. These are so-called iterable, ordered objects. The function signature is: `sorted(iterable, key=None, reverse=False)`.

```python
people = ["John", "Fatima", "Igor", "Rune", "Anja"]
sorted_people_list = sorted(people)
# ["Anja", "Fatima", "Igor", "John", "Rune"]
```

Here too, we can define the value for key using a function.

```python
people = [ ("John", 172), ("Fatima", 165), ("Igor", 168), ("Rune", 176), ("Anja", 174)]
name = lambda person: person[0]
height = lambda person: person[1]
people_sorted_reverse_by_name = sorted(people, key=name, reverse=True)
people_sorted_by_height = sorted(people, key=height)
```

Note: the sorted() function returns a *list*. If we need a sorted copy of a tuple, we must convert the list back to a tuple.

```python
weights = (62, 81, 59, 78, 72, 63, 65)
sorted_weights = tuple(sorted(weights))
# (59, 62, 63, 65, 72, 78, 81)
```

The same applies to a string. sorted() returns a list of characters, so we must convert the list back into a string.

```python
letters = "azertyuiopqsdfghjklm"
sorted_letters = sorted(letters)
# ['a', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'o', 'p', 'q', 'r', 's', 't', 'u', 'y', 'z']
sorted_string = "".join(sorted_letters)
print(sorted_string)
# adefghijklmopqrstuyz
```

## Filter() and map() with lambda functions

In Python, lambda functions are anonymous functions (i.e., functions without a name) that are defined using the lambda keyword. They are often used with functions like filter() and sort() because they allow you to write simple, concise functions without having to define a separate function using def.

The filter() function is used to filter elements from an iterable (like a list) based on a condition. It takes two arguments: a function (which returns either True or False for each element) and an iterable. The elements for which the function returns True are included in the result.

A lambda function is often used with filter() to define a condition without needing a separate function.

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Using filter() with a lambda function to filter even numbers
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))

print(even_numbers) # Output: [2, 4, 6, 8, 10]
```

Explanation: The lambda function lambda x: x % 2 == 0 returns True if the number is even, and False otherwise. The filter() function keeps only the elements where the lambda function returns True.

The sort() function (or sorted()) is used to sort a list. By default, it sorts in ascending order, but you can customize the sorting using the key argument, which expects a function. This is where lambda functions come in handy for specifying custom sorting logic.

```python
people = [("Alice", 25), ("Bob", 20), ("Charlie", 30)]

# Using sort() with a lambda function to sort by age (second element in the tuple)
people.sort(key=lambda person: person[1])

print(people) # Output: [('Bob', 20), ('Alice', 25), ('Charlie', 30)]
```

Explanation: The lambda function lambda person: person[1] extracts the second element (age) from each tuple, and sort() uses this value to sort the list of tuples.

```python
people = [("Alice", 25), ("Bob", 20), ("Charlie", 30)]

# Using sorted() with lambda to sort by name (first element) in reverse order
sorted_people = sorted(people, key=lambda person: person[0], reverse=True)

print(sorted_people) # Output: [('Charlie', 30), ('Bob', 20), ('Alice', 25)]
```

The map() function in Python is used to apply a given function to every item of an iterable (like a list) and return an iterator of the results. It allows you to transform elements in an iterable by applying the function to each one. A lambda function is often used with map() to create simple and inline transformations without defining a separate function. The syntax is:

```python
map(function, iterable)
```

* function: A function (like a lambda function) that is applied to each item.

* iterable: The sequence (like a list) whose elements will be passed to the function.

In the following example we will double each element in the list:

```python
numbers = [1, 3, 4, 5]
# Using map() with a lambda function to double each number
doubled_numbers = list(map(lambda x: x * 2, numbers))

print(doubled_numbers) # Output: [2, 4, 6, 8, 10]
```

Explanation: The lambda function lambda x: x * 2 multiplies each number in the numbers list by 2. The map() function applies this lambda to every element in the list, and the result is a new list of doubled numbers.

The following example will transform each element to upper case.

```python
words = ["apple", "banana", "cherry"]

# Using map() with a lambda function to convert each word to uppercase
uppercase_words = list(map(lambda word: word.upper(), words))

print(uppercase_words) # Output: ['APPLE', 'BANANA', 'CHERRY']
```

## Comprehensions

Python also provides us with the ability to create sequences such as lists, sets and dictionaries in a short and elegant way using comprehensions. These are often seen as more ‘pythonic’ than loops, and they are also said to be more efficient. That's why we include them in this lesson, although we won't go very deep into them. We will only briefly discuss how list, dictionary and set comprehensions work.

### List comprehensions

The general syntax for a list comprehension is:

```python
new_list = [expression for element in iterable if (element satisfies condition)]
```

The condition (if statement) is not obligatory.

An example will clarify list comprehension. Suppose we want a list from 1 to 10. With a for loop, this will be our code:

```python
lst = []
for i in range(1, 11):
  lst.append(i)
print(lst) # [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

With a list comprehension we can do this in one line of code:

```python
lst = [x for x in range(1,11)]
print(lst) # [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

Suppose we want the power of two of each element from 1 to 10:

```python
print([x*x for x in range(1,11)]) # [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

Another example: suppose we have a list of integers and we want to create a new list that contains only the even numbers from that list.

```python
input = [1, 2, 3, 4, 4, 5, 6, 7, 7]
new_list = [x for x in input if x%2 == 0] # [2, 4, 4, 6]
```

A nested list, or a matrix can be created with a list comprehension.

```python
print([[j for j in range(0, 5)] for i in range(0, 5)])
# [[0, 1, 2, 3, 4], [0, 1, 2, 3, 4], [0, 1, 2, 3, 4], [0, 1, 2, 3, 4], [0, 1, 2, 3, 4]]
```

Suppose we want to "flatten" a matrix, i.e. we want to put all the elements in one list.

```python
matrix = [[i*3 + j for j in range(0, 3)] for i in range(0, 3)]
print(matrix) # [[0, 1, 2], [3, 4, 5], [6, 7, 8]]
flattened = [element for row in matrix for element in row]
print(flattened) # [0, 1, 2, 3, 4, 5, 6, 7, 8]
```

### Dictionary comprehensions

In the same way we can create dictionaries using comprehensions. The general syntax is:

```
new_dict = {key: expression for key, value in iterable if (key, value satisfies condition)}
```

Suppose we have a list of integers. We want to get the odd numbers and create a dictionary with the odd number as key and the power of three of that number as values:

```python
my_numbers = [1, 2, 5, 2, 7, 5, 11, 12, 9]
my_dict = {key: key**3 for key in my_numbers if key %2 == 1}
# {1: 1, 5: 125, 7: 343, 11: 1331, 9: 729}
```

Suppose we have a list of countries and a list of capital cities. We want to fuse both lists in one dictionary.

```python
countries = ('Belgium', 'France', 'Germany', 'Italy', 'Spain')
cities = ('Brussels', 'Paris', 'Berlin', 'Rome', 'Madrid')
my_dict = {countries[i]: cities[i] for i in range(0, len(countries))}
# {'Belgium': 'Brussels', 'France': 'Paris', 'Germany': 'Berlin', 'Italy': 'Rome', 'Spain': 'Madrid'}
```

There is in fact a shorter way to do this, using the zip function.

```python
countries = ('Belgium', 'France', 'Germany', 'Italy', 'Spain')
cities = ('Brussels', 'Paris', 'Berlin', 'Rome', 'Madrid')
my_dict = zip(countries, cities)
# {'Belgium': 'Brussels', 'France': 'Paris', 'Germany': 'Berlin', 'Italy': 'Rome', 'Spain': 'Madrid'}
```

### Set comprehensions

Set comprehensions are created in a very similar way as lists, except for the fact that we use curly braces instead of square brackets.

```
new_set = {expression for element in iterable if (element satisfies condition)}
```

Suppose we have a list of integers and we want to put the even numbers in a set.

```python
input = [1, 2, 3, 4, 4, 5, 6, 6, 6, 7, 7]
 set_even = {even_number for even_number in input if even_number%2 == 0}
  # {2, 4, 6} every even number occurs only once as we have a set
```

## Unpacking collections

In Python, unpacking refers to the process of assigning the values from a collection (like a list, tuple, or any iterable) into multiple variables in a single statement. Unpacking is a powerful feature that simplifies the extraction of elements from collections.

You can unpak elements of a tuple or list directly into variables

```python
# A tuple with three elements
person = ("John", 25, "Engineer")

# Unpacking the tuple into individual variables
name, age, profession = person

print(name)       # Output: John
print(age)        # Output: 25
print(profession) # Output: Engineer
```

```python
# A list with three elements
numbers = [1, 2, 3]

# Unpacking the list into individual variables
a, b, c = numbers

print(a)  # Output: 1
print(b)  # Output: 2
print(c)  # Output: 3
```

The * operator allows you to capture the remaining elements in an iterable when unpacking. It can be used when you don’t know how many elements are in the iterable or when you want to capture part of the iterable.

```python
numbers = [1, 2, 3, 4, 5]

# Unpacking the first element, and capturing the rest in 'rest'
first, *rest = numbers

print(first)  # Output: 1
print(rest)   # Output: [2, 3, 4, 5]
```

```python
numbers = [1, 2, 3, 4, 5]

# Unpacking the first element, the middle elements, and the last element
first, *middle, last = numbers

print(first)   # Output: 1
print(middle)  # Output: [2, 3, 4]
print(last)    # Output: 5
```

You can use this principle to pass a list or dictionary to a function. The list or dictionary has the arguments, as positional arguments (in which case we use * and a list or tuple) or as keyword arguments (in which case we use ** and a dictionary).

In the following example we pass a list with the positional arguments x, y, z. We call this positional arguments because we offer them in the same order as in the function definition without referring to their name. We use a asterisk (*) before the list of arguments.

```python
def add(x, y, z):
    return x + y + z

numbers = [1, 2, 3]

# Unpacking the list into the function arguments
result = add(*numbers)
print(result)  # Output: 6
```

In the following example we pass a dictionary that contains, for each argument, the name of the argument and the value. We call this keyword arguments (kwargs). We use ** before the dictionary of arguments.

```python
def greet(name, age):
    return f"Hello, {name}. You are {age} years old."

person_info = {"name": "Alice", "age": 30}

# Unpacking the dictionary into keyword arguments
message = greet(**person_info)
print(message)  # Output: Hello, Alice. You are 30 years old.
```

## JSON module

When we request data from a website via an API, we are often presented with that data in JSON format. JSON is used to store information in an easily organised way. The file is readable, and can be called logically. The main advantages are:

- Supported in all browsers
- Easy to read & write
- Uses little memory
- Simple syntax
- Supported in all major JavaScript frameworks
- Allows structured data to be sent over the network (e.g. to/from a server)

JSON stands for **JavaScript Object Notation**. A JavaScript object consists of key/value pairs separated by commas and enclosed by curly braces. So it looks exactly the same as a Python dictionary. So working with JSON files in Python is very easy!
In Python, there is the built-in module ‘json’ to work with JSON data. You define a JSON object as a string and it can then be converted with function `loads()` to a Python dictionary:

### Example:

```python
import json

# Convert a dictionary to JSON
person = {"name": "John", "age": 30, "city":"New York"} # dictionary
person_json = json.dumps(person) # '{"name": "John", "age": 30, "city": "New York"}'

# Convert JSON back to a dictionary
person_dict = json.loads(person_json)
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
