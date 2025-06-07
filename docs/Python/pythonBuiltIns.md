# Built-ins in Python

## abs()

Returns the magnitude of a number.

```python
a = complex(45, 56)
b = -67
print(abs(a))
print(abs(b))

# Output:
# 71.84010022264724
# 67
```

## any(iterable) and all(iterable)

`any()` and `all()` accept iterables.

`any()` returns `True` if any element of the iterable is non-zero.

```python
lst = [1, 3, 5, 7, 9, 0]
print(all(lst))  # False
lst = [0, 0, 0, 0, 0]
print(any(lst))  # False
```

## breakpoint()

The `breakpoint()` function is used for debugging. It calls the built-in debugger (normally the Python debugger, `pdb`) to allow you to interactively debug your code.

The `breakpoint()` function can accept positional arguments (`*args`) and keyword arguments (`**kwargs`). These arguments are passed directly to the debugger, allowing you to customize the debugging session.

```python
# Example using breakpoint() with arguments
def my_function():
    x = 10
    y = 20
    breakpoint(x, y, z=30)

my_function()
```

## callable(object)

- Note that classes are callable (calling a class returns a new instance).
- Instances are callable if their class has a `__call__` method.

```python
class Trial:
    def __init__(self, name) -> None:
        self.name = name

    def __call__(self, *args, **kwargs):
        print(f"The name is {self.name}")

boy = Trial('kevin')
print(callable(boy))
boy()
# This prints True if the __call__ definition is uncommented and prints False if commented.

# Output:
# True
# The name is kevin
```

## @classmethod

Normally, methods in classes are instance methods, as they receive the instance as the implicit first argument.

`@classmethod` converts an instance method into a class method, which receives the class as the first argument.

A class method can be called either on the class (such as `C.f()`) or on an instance (such as `C().f()`).

In the example below, if `get_INI_value` is just an instance method, it must be called as `ParserINI().get_INI_value(section, option)`. Since it is a class method, it can be called as `ParserINI.get_INI_value()`.

```python
class ParseINI:
    config = ConfigParser()
    config.read("configuration.ini")

    @classmethod
    def get_INI_value(cls, section: str, option: str) -> str:
        return cls.config.get(section, option)
```

## compile()

Used to compile a source code string into executable code.

```python
source = '''import os
print(os.__dir__())'''

executable = compile(source, '<string>', 'exec')
exec(executable)
```

Real-world usage includes scripting engines, creating custom domain-specific languages, runtime code evaluation, code generator tools, and code evaluation tools.

## enumerate(iterable)

```python
l = [1, 5, 9, 5, 2, 0, 12, 56, 78, 34]

for index, value in enumerate(l):
    print(f"{index} : {value}\t")

# Output:
# 0 : 1
# 1 : 5
# 2 : 9
# ...

# Below is the output if enumerate(l, 7) is given; the second argument defines the start value of the indexing.
# Output:
# 7 : 1
# 8 : 5
# 9 : 9
# ...
```

## map() and filter()

### map(function, iterable)

The `map()` function takes a function and an iterable. It applies the function to each element of the iterable.

```python
cube = lambda n: n * n * n
l = [7, 3, 6, 1, 2, 9]
print(list(map(cube, l)))  # [343, 27, 216, 1, 8, 729]
```

### filter(function, iterable)

Filters the elements of an iterable based on the function passed to it.

```python
l = [1, 5, 9, 5, 2, 0, 12, 56, 78, 34]

def even(n):
    return n % 2 == 0

print(list(filter(even, l)))
```

## locals() and globals() functions in Python

`locals()` is a built-in function in Python that returns the dictionary of the current local symbol table.

```python
print(locals())

# Output:
# {'__name__': '__main__', '__doc__': None, ...}
```

Example code to demonstrate the `locals()` function:

Calling `locals()` outside a function prints all the general local variables in Python.

Calling `locals()` inside a function prints only the local variables defined inside that function.

```python
a = 10
b = 20

def func():
    x = 30
    y = 40
    print(locals())

print(locals())
func()

# Output:
# {'__name__': '__main__', ... 'a': 10, 'b': 20, 'func': <function func at ...>}
# {'x': 30, 'y': 40}
```

`globals()` is a built-in function in Python that returns the dictionary of the global symbol table. Similar to `locals()`, `globals()` is used to obtain variables in the respective scope.

```python
print(globals())
```

## zip(*iterable)

Iterate over several iterables in parallel, producing tuples with an item from each one.

```python
for item in zip([1, 2, 3], ['sugar', 'spice', 'everything nice']):
    print(item)

# Output:
# (1, 'sugar')
# (2, 'spice')
# (3, 'everything nice')
```

`zip()` stops when the shortest iterable is exhausted.

## zip and unzip

```python
x = [1, 2, 3, 4, 5]
y = [6, 7, 8, 9, 10]
zip_object = zip(x, y)
print(list(zip_object))  # After zipping two iterables

p, q = zip(*zip(x, y))  # This is a way to unzip zipped iterables
print(list(p))
print(list(q))
```

## super()

```python
class Student:
    def __init__(self, name) -> None:
        self.student_name = name

class Marks(Student):
    def __init__(self, name, marks) -> None:
        Student.__init__(self, name)
        self.marks = marks

s1 = Marks('farzi', 10)
print(s1.__dict__)

# The above code can be written using the super() function as below:

class Student:
    def __init__(self, name) -> None:
        self.student_name = name

class Marks(Student):
    def __init__(self, name, marks) -> None:
        super().__init__(name)
        self.marks = marks

s1 = Marks('farzi', 10)
print(s1.__dict__)
```

## slice(start, stop [, step]) method in Python

The `slice` method is an alternative way of using `list[start:stop:step]` in Python.

```python
l = [1, 6, 3, 2, 8, 6, 89, 23, 5, 25, 76, 87, 42, 61, 90, 22, 13, 45, 78, 65]
print(l)
# [1, 6, 3, 2, 8, 6, 89, 23, 5, 25, 76, 87, 42, 61, 90, 22, 13, 45, 78, 65]

print(l[0::2])  # One way of list slicing method.
# [1, 3, 8, 89, 5, 76, 42, 90, 13, 78]

print(l[slice(0, len(l), 2)])  # Alternate way of slicing
# [1, 3, 8, 89, 5, 76, 42, 90, 13, 78]
```

## `__call__()`

The `__call__()` method is used to make a class instance callable like a function, and is often used to make a class act as a decorator.

```python
class Trial:
    def __init__(self, name) -> None:
        self.name = name

    def __call__(self, *args: Any, **kwargs: Any) -> Any:
        print(f"The name is {self.name}")

boy = Trial('kevin')
boy()  # Object of the class Trial called as a function.
```

## String Methods

```python
# Strings are immutable and cannot be changed once assigned to a variable.
# However, string methods can be used to create a new string from the existing one.

a = "!!starwar!!"
a.upper()        # Outputs an uppercase version of the string
a.lower()        # Outputs a lowercase version of the string
a.rstrip("!")    # Strips the occurrence of the given character at the end of the string -> !!starwar
a.strip("!")     # Strips the given character from both sides -> starwar
a.replace('war', 'jar')  # Replaces all occurrences of 'war' with 'jar' -> !!starjar!!
```

```python
b = "avenger.com"
b.split('.')        # ['avenger', 'com']
b.capitalize()      # 'Avenger.com' - Converts first character to uppercase
b.count('com')      # Counts the occurrence of 'com' in this string -> 1
b.endswith('m')     # Returns True if the string ends with 'm'
```

```python
# Both the methods below work similarly, but when a given string is not found,
# find() returns -1, while index() raises an exception.

c = "Spiderman is an avenger"
c.find('is')        # Returns the index of the first occurrence of 'is'
c.find('was')       # Returns -1 if not found

c.index('is')       # Returns the index of the first occurrence of 'is'
c.index('lwhoeu')   # Raises ValueError if not found
```

```python
isalnum(), isalpha(), islower()
swapcase()  # Swaps the case of the given string
title()     # Converts the string to title case
```

## List Methods

To initialize a list with an initial size:

```python
l = [None] * 5
# Here the length of the list is 5 and all 5 elements are assigned None
```

A list is a mutable type. Any list methods used on a list will affect the original list.

```python
a = [3, 8, 2, 9, 7, 5, 1, 23, 54]
a.append(4)           # [3, 8, 2, 9, 7, 5, 1, 23, 54, 4]
a.sort()              # [1, 2, 3, 4, 5, 7, 8, 9, 23, 54]
a.sort(reverse=True)  # [54, 23, 9, 8, 7, 5, 4, 3, 2, 1]

a = [3, 8, 2, 9, 7, 5, 1, 23, 54]
a.reverse()           # [54, 23, 1, 5, 7, 9, 2, 8, 3]
print(a.index(7))     # Prints 4 as index of 7 in reversed list is 4
print(a.count(3))     # Prints number of occurrences of 3 in the list

# Changing an element of b changes the element of a. b is a reference to a.
a = [3, 8, 2, 9, 7, 5, 1, 23, 54]
b = a  # Assigning like this is not best practice.
b[0] = 0
print(a)  # [0, 8, 2, 9, 7, 5, 1, 23, 54]

a = [3, 8, 2, 9, 7, 5, 1, 23, 54]
b = a.copy()  # This is best practice; changes made in b remain in b.
b[0] = 0
print(a)  # [3, 8, 2, 9, 7, 5, 1, 23, 54]

a = [3, 8, 2, 9, 7, 5, 1, 23, 54]
a.insert(4, 100)
print(a)  # [3, 8, 2, 9, 100, 7, 5, 1, 23, 54]
```

## f-strings in Python

```python
spacecraft = 'voyager'
year = '1977'
print(f"{spacecraft} is a fly-by satellite launched in {year}")
# voyager is a fly-by satellite launched in 1977

# If a curly bracket is also needed in the string
print(f"{spacecraft} is a fly-by satellite launched in {year} weighs {{Nothing}}")
# voyager is a fly-by satellite launched in 1977 weighs {Nothing}
```

## try-except-finally

In try-except-finally, a piece of code is tried. If an exception occurs, it can be caught in the except block. The finally block always gets executed no matter what.

```python
# Demo of finally
def pool():
    try:
        something
        return return_value
    except:
        error_handling
        return return_value
    finally:
        final_wrap_up_lines

# Here, even after the try or except block hits the return statement, finally gets executed.
# This is the specialty of the finally block.
```

## if-else in a single line statement

```python
print("4 greater than 2") if 4 > 2 else print("5 greater than 3") if 5 > 3 else print("nothing")
```

## File handling

```python
with open("file.txt", "r") as f:
    print(f.read(), "\n", type(f))  # Reads entire file till EOF
    print(f.tell())                 # Gives current position of the pointer -> 766
    f.seek(0)                       # Seek to a required position in a file. Here file pointer seeks the 0th char and points to it -> points to G here
    print(f.tell())                 # Current position of pointer -> 0
    print(f.read(5))                # Read 5 bytes from the current pointer position -> Galax

with open("file.txt", '+a') as f:
    f.truncate(300)  # Truncates the file content to 300 bytes

# Now reading the file would contain only 300 characters
```

## Decorators

Decorators take a function as an argument, modify it, and return a new function. Here, `raptor` is a decorator that takes a function as an argument, adds print statements at the beginning and end, and returns a new function `endo()`.

```python
def raptor(func):
    def endo(*args):
        print("hello from the decorator")
        func(*args)
        print("Bye!! from Decorator")
    return endo

@raptor
def average(a, b, c):
    print("average is :")
    print((a + b + c) / 3)

if __name__ == "__main__":
    average(8, 1, 6)

# Output:
# hello from the decorator
# average is :
# 5.0
# Bye!! from Decorator
```

Below is a good boilerplate template for decorators in Python that can be used to build more complex decorators.

```python
def decorator(func):
    def wrapper_decorator(*args, **kwargs):
        # Do something before
        value = func(*args, **kwargs)
        # Do something after
        return value
    return wrapper_decorator
```

## Asterisk * and / as arguments to functions

When you see an asterisk (*) in the function parameter list, it typically indicates that all the parameters following it are keyword-only arguments.

```python
def fixture(
    fixture_function: Optional[FixtureFunction] = None,
    *,
    scope: "Union[_ScopeName, Callable[[str, Config], _ScopeName]]" = "function",
    params: Optional[Iterable[object]] = None,
    autouse: bool = False,
    ids: Optional[
        Union[Sequence[Optional[object]], Callable[[Any], Optional[object]]]
    ] = None,
    name: Optional[str] = None,
) -> Union[FixtureFunctionMarker, FixtureFunction]:
    ...
```

The `/` symbol specifies **positional-only arguments**, meaning they **must be provided in order** and **cannot be used as keyword arguments**.

```python
def divide(a, b, /):
    return a / b

print(divide(10, 2))         # ✅ Works: Positional arguments
print(divide(a=10, b=2))     # ❌ Error: Cannot use keyword arguments
```

## %s in Python

A string can be formed using the line below, where `filename` and `line` are the strings that are printed in place of `%s`:

```python
print("Bad line in config-file %s:\n%s" % (filename, line))
```

A plain string can be formed as below:

```python
default_cfg = "turtle_%s.cfg" % cfgdict1["importconfig"]
```

## reversed() and reverse()

`reverse()` is used on a list and modifies the original list in place.

On the other hand, `reversed()` is a built-in function in Python that returns an iterator that accesses the given sequence in the reverse order. The original list remains unchanged.

```python
lst_ = [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]

lst_.reverse()
print(lst_)
# [0, 9, 8, 7, 6, 5, 4, 3, 2, 1]
print(list(reversed(lst_)))
# [0, 9, 8, 7, 6, 5, 4, 3, 2, 1]
```

## sorted() and sort()

Both of these functions use `key` as an argument, where a callable can be passed.

Syntax for both functions:

```python
sorted(iterable, /, *, key=None, reverse=False) -> iterable
sort(iterable, /, *, key=None, reverse=False) -> None
```

```python
lst = [6, 1, 4, 0, 9, 3, 8, 7, 2, 5]

print(sorted(lst))  # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9] - doesn't change the original list
print(lst)          # [6, 1, 4, 0, 9, 3, 8, 7, 2, 5]

lst.sort()
print(lst)          # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9] - changes the list
```

## @staticmethod

Transforms a method into a static method. A static method can be called either on the class (such as `C.f()`) or on an instance (such as `C().f()`).

A static method does not receive an implicit first argument. To declare a static method, use this idiom:

```python
class C:
    @staticmethod
    def f(arg1, arg2, argN):
        ...
```

## round(number, ndigits=None)

For example, both `round(0.5)` and `round(-0.5)` are `0`, and `round(1.5)` is `2`. The return value is an integer if `ndigits` is omitted or `None`. Otherwise, the return value has the same type as `number`.

`round(2.675, 2)` gives `2.67` instead of the expected `2.68`. This is not a bug.

## str(object), repr(object), and ascii(object)

### str(object=b'', encoding='utf-8', errors='strict')

Returns the string version of the object.

### repr(object)

Returns a string containing a printable representation of an object. A class can control what this function returns for its instances by defining a `__repr__()` method.

### ascii(object)

The `ascii()` function in Python is used to generate a string representation of an object, similar to what the `repr()` function does. However, `ascii()` differs in that it escapes non-ASCII characters in the string returned by `repr()` using `\x`, `\u`, or `\U` escapes. This means that any characters outside the ASCII range (0-127) will be represented using escape sequences.

```python
# Define a string with non-ASCII characters
s = "Café"

# Use repr() to get the string representation
print("Using repr():", repr(s))  # Output: 'Café'

# Use ascii() to get the ASCII representation with escape sequences
print("Using ascii():", ascii(s))  # Output: 'Caf\xe9'
```

```python
fring = "₮₰₩Ꞧﯔ"
print(ascii(fring))

# Output:
# '\u20ae\u20b0\u20a6\u20a9\ua7a6\ufbd4'
```

## chr(), ord(), bin(), hex(), and oct()

### ord() and chr()

`ord()` and `chr()` are inverses of each other.

- `ord()`: gives the Unicode value of a character.
- `chr()`: gives the character corresponding to a Unicode value.

```python
char = 'a'
unicode_value = ord(char)
char_equivalent_of_unicode = chr(unicode_value)

print(f"unicode = {unicode_value}")
print(f"Character equivalent to unicode value = {char_equivalent_of_unicode}")
```

### bin(integer)

```python
print(bin(10))
# Output: 0b1010
```

### hex()

```python
hex(255)
# Output: '0xff'
```

### oct()

```python
oct(8)
# Output: '0o10'
```

## iter() and next()

`iter()` creates an iterator object.

With this iterator object, use `next()` to iterate through it.

```python
iterator = iter(lst_)
print(next(iterator))
```

`next()` or `__next__()` can be used with the iterator object to iterate through the values.

```python
a = [1, 2, 23, 3, 5, 6, 7, 8]
Itr = iter(a)

for _ in range(len(a)):
    print(Itr.__next__())
# Output: 1 2 23 3 5 6 7 8
```

## min() and max()

Take an iterable and return the minimum or maximum value accordingly.

- `min(iterable, *, key=None)`
- `min(iterable, *, default, key=None)`
- `min(arg1, arg2, *args, key=None)`
- `max(iterable, *, key=None)`
- `max(iterable, *, default, key=None)`
- `max(arg1, arg2, *args, key=None)`

## isinstance() and issubclass()

`isinstance(object, class)` checks if the object is an instance of the given class.

The `class` argument can also be a tuple of classes, where the function returns True if the object is an instance of at least one of the classes.

```python
class Planet:
    pass

class Animal:
    pass

class Dog():
    pass

dog_instance = Dog()

print(isinstance(dog_instance, Dog))
print(isinstance(dog_instance, (Dog, Animal)))
print(isinstance(dog_instance, (Planet, Animal)))

# Output:
# True
# True
# False
```

`issubclass(class, classinfo)` accepts two classes and checks if one class is a subclass of the other. The `classinfo` argument can also be a tuple of classes. Here, the class has to be a subclass of at least one of the classes in the tuple.

```python
class Shape:
    pass

class Circle(Shape):
    pass

# Check if Circle is a subclass of Shape
result = issubclass(Circle, Shape)
print(result)  # Output: True
```

## open()

It is recommended to use `open` in a `with` statement as it takes care of closing the file once it exits the `with` block, even when an exception occurs.

`fp` is a file object, similar to a file pointer in other languages.

```python
with open('abcd.txt', 'r') as fp:
    ...
```

### mode parameter can be:

| mode         | description                 |
| ------------ | --------------------------- |
| 'r'          | open the file in read mode  |
| 'w'          | open the file in write mode |
| 'rb' or 'wb' | open in binary mode         |

### Reading a file after opening:

| definition                                    | description                                                                                                              |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| .read(size=-1)                                | Reads the file based on the byte size passed.<br>Default byte size is -1, which reads all the bytes in the document.<br> |
| .readline(size=-1)                            | Reads one line.<br>                                                                                                      |
| .readlines()                                  | Reads all the lines of a document and returns a list.                                                                    |
| *list(fp) is also equivalent to .readlines()* | Where `fp`, the file object, is typecast to a list.                                                                      |

### readline()

```python
# readline() to read a whole document

with open(r"example.log", 'r') as fp:
    line_ = fp.readline()
    while line_ != '':
        print(line_)
        line_ = fp.readline()
```

### readlines()

```python
# readlines() to read the whole document

with open(r"example.log", 'r') as fp:
    for line in fp.readlines():
        print(line)
```

### read()

```python
with open(r"example.log", 'r') as fp:
    print(fp.read())
```

### Working with two files at a time

```python
with open(r"example.log", 'r') as reader, open('writer.txt', 'w') as writer:
    writer.write(reader.read())
```

## venv

```python
python -m venv .env

# To clear the existing .env/ and create it again
python -m venv .env --clear

# To upgrade the Python binary in the virtual environment with the system Python
python -m venv .env --upgrade

# Install updated pip as soon as you create .env/
python -m venv .env --upgrade-deps

# Create multiple environments
# Here, three Python environments are created in the existing directory.
python -m venv .env/ .venv/ .environment/

# Change the displayed command prompt name
python -m venv .env --prompt="client_1"
```

## Miscellaneous

### Three ways of setting attribute values of a class

This can be done in three ways:

```python
@dataclass
class Student:
    name: str
    grade: str
    age: int

s1 = Student('jeeva', 'C', 20)
print(f"Student {s1.name} of age {s1.age} has {s1.grade} grade")
setattr(s1, 'grade', 'A')
print(f"Student {s1.name} of age {s1.age} has {s1.grade} grade")
s1.grade = 'F'
print(f"Student {s1.name} of age {s1.age} has {s1.grade} grade")

# Output:
# Student jeeva of age 20 has C grade
# Student jeeva of age 20 has A grade
# Student jeeva of age 20 has F grade
```

One is the conventional way where the attributes are given when declaring an instance of the class `s1`.

Using `setattr`.

And using `s1.grade = 'F'`.

```python
if sys.version_info >= (3, 8):
    ...
```

The above line is used to verify the version of Python and, based on that, execute certain code.

### Floor division operator

```python
print(15 // 4)
```

### Match case statements in Python

These are valid from Python 3.10. Match-case is similar to switch-case in C.

## len()

A `range` object doesn’t store all the values but generates them when they’re needed. However, you can still find the length of a `range` object using `len()`:

```python
len(range(1, 20, 2))
# Output: 10
```

## weakref in Python

```python
import weakref

class MyClass:
    def __init__(self, name):
        self.name = name

    def print_name(self):
        print(self.name)

my_obj = MyClass("Nitrogen")
my_obj.print_name()
# Output: Nitrogen

# Create a weak reference to my_obj
weak_reference = weakref.ref(my_obj)

# weak_reference object is callable; it must be called
if weak_reference() is not None:
    print("Object alive")
else:
    print("Object not alive")
# Output: Object alive

# weakref object must also be called, upon which its instance methods can be called
print(weak_reference().print_name())

# Delete main object
del my_obj

# Check if the object is still alive
if weak_reference() is not None:
    print("Object alive")
else:
    print("Object not alive")
# Output: Object not alive
```

## Dictionary in Python

```python
a = dict(one=1, two=2, three=3)
b = {'one': 1, 'two': 2, 'three': 3}
c = dict(zip(['one', 'two', 'three'], [1, 2, 3]))
d = dict([('two', 2), ('one', 1), ('three', 3)])
e = dict({'three': 3, 'one': 1, 'two': 2})
f = dict({'one': 1, 'three': 3}, two=2)
assert a == b == c == d == e == f
```

```python
# List of keys
g = list(a)

# List of values
h = list(a.values())

# Delete an entry in dict
del a['one']

# Clear all entries in a dict
a.clear()

# Shallow copy a dict into another
i = b.copy()
```

```python
# Create a dict from 'fromkeys' method
j = dict.fromkeys(['four', 'five', 'six', 'seven', 'eight'], None)

# Pop an entry by key
j.pop('six')

# Pop the last entry
print(j.popitem())
```

```python
j.update({'seven': 7})
# OR
j.update(seven=9)
j
```

### ChainMap

```python
from collections import ChainMap

baseline = {'music': 'bach', 'art': 'rembrandt'}
adjustments = {'art': 'van gogh', 'opera': 'carmen'}
bboss = {'opera': [1, 2, 3, 4, 5], 'maven': 'kalmi'}

# `|` can be used to chain multiple dicts; the last dict is considered the latest
print(baseline | adjustments | bboss)

# collections.ChainMap can be used to chain multiple dicts; the first dict is considered the latest
chain_obj = ChainMap(baseline, adjustments, bboss)
chain_obj = dict(chain_obj)
print(chain_obj)

# Output:
# {'music': 'bach', 'art': 'van gogh', 'opera': [1, 2, 3, 4, 5], 'maven': 'kalmi'}
# {'opera': 'carmen', 'maven': 'kalmi', 'art': 'rembrandt', 'music': 'bach'}
```

## `collections` module

### Counter

```python
from collections import Counter

# Tally occurrences of words in a list
cnt = Counter()
for word in ['red', 'blue', 'red', 'green', 'blue', 'blue']:
    cnt[word] += 1
print(cnt)
```

### deque

Below are the methods of the deque class:

> 'append', 'appendleft', 'clear', 'copy', 'count', 'extend', 'extendleft', 'index', 'insert', 'maxlen', 'pop', 'popleft', 'remove', 'reverse', 'rotate'
