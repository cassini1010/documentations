# Built-ins in Python

## abs()

Gives the magnitude of a number.

```python
a = complex(45,56)
b = -67
print(abs(a))
print(abs(b))


>>71.84010022264724
>>67
```

## any(iterable) and all(iterable)

`any()` and `all()` accepts an iterables.

`any()` returns `True` if any one of the elements of the iterator is non-zero.

```python
lst = [1,3,5,7,9,0]
print(all(lst)) # False
lst = [0,0,0,0,0]
print(any(lst)) # False
```

## breakpoint()

The `breakpoint()` function is used for debugging. It calls the built-in debugger (normally the Python debugger, `pdb`) to allow you to interactively debug your code.

The `breakpoint()` function can accept positional arguments (`*args`) and keyword arguments (`**kws`). These arguments are passed directly to the debugger, allowing you to customize the debugging session.

```python
# Example using breakpoint() with arguments
def my_function():
    x = 10
    y = 20
    breakpoint(x, y, z=30)

my_function()
```

## callable(object)

- Note that classes are callable (calling a class returns a new instance)
  instances are callable if their class has a `__call__` method in it.

```python
class trial:
    def __init__(self, name) -> None:
        self.name = name

    def __call__(self, *args , **kwds):
        print(f"the name is {self.name}")

boy = trial('kevin')
print(callable(boy))
boy()
'''This prints True if the __call__ definition is uncommentedAnd prints false if commented'''

>> True
>> the name is kevin
```

## @classmethod

Normally a method in classes are instance methods, as it receives instance as an implicit first argument.

`@classmethod` converts an instance method into a classmethod, which receives class as a first argument.

A class method can be called either on the class (such as `C.f()`) or on an instance (such as `C().f()`)

In the below example if `get_INI_value` is just an instance method, it must be called as `ParserINI().get_INI_value(section, option)`

Since it is a class method it can be called as `ParserINI.get_INI_value()`

```python
class ParseINI:
    config = ConfigParser()
    config.read("configuration.ini")

    @classmethod
    def get_INI_value(self, section: str, option: str) -> str:
        return self.config.get(section, option)
```

## compile()

Used to compile a source code string into an executable code.

```python
source = '''import osprint(os.__dir__())'''

executable = compile(source, '<string>', 'exec')
exec(executable)
```

Real world usage of this is in Scripting engines, making a custom Domain-specific language, Runtime code Evaluation, Code generator tools, code evaluation tools.

## enumerate(iterable)

```python
l = [1,5,9,5,2,0,12,56,78,34]

for index,value in enumerate(l):
    print(f"{index} : {value}\t")

output: 
0 : 1
1 : 5
2 : 9 
...

'''below is the output if enumerate(l, 7) is given second argument defines the start value of the indexing'''
output: 
7 : 1
8 : 5
9 : 9
...
```

## map() and filter()

### map(*function, iterable*)

map() function takes a function and a list. It computes the function for each element of the list.

```python
cube = lambda n : n*n*n
l = [7,3,6,1,2,9]
print(list(map(cube, l))) # [343, 27, 216, 1, 8, 729]
```

### filter( *function, iterable*)

Filters the elements of an iterable based on the function passed to it.

```python
l = [1,5,9,5,2,0,12,56,78,34]

def even(n):
    if n%2 == 0:
        return n

print(list(filter(even, l)))
```

## locals() and globals() function in python

`locals()` is a built-in function in python that is used to obtain the dictionary of current local symbol table.

```python
print(locals())


{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <_frozen_importlib_external.SourceFileLoader object at 0x0000022FC686C700>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, '__file__': 'c:\\Users\\JEEKUMA\\Desktop\\BLOB\\water.py', '__cached__': None}
```

Example code to demonstrate `locals()` function:

The `locals()` function call from the outside of the function `func()` prints all the general local variables in python.

`locals()` call from the inside of the `func()` function prints only the local variables defined inside that function.

```python
a = 10
b = 20

def func():
    x = 30
    y = 40
    print(locals())

print(locals())
func() 


>>{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <_frozen_importlib_external.SourceFileLoader object at 0x0000023AA031C700>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, '__file__': 'c:\\Users\\JEEKUMA\\Desktop\\BLOB\\water.py', '__cached__': None, 'a': 10, 'b': 20, 'func': <function func at 0x0000023AA0253E20>}
>>{'x': 30, 'y': 40}
```

`globals()` is a built-in function in python that is used to obtain the dictionary of global symbol table. Similar to `locals()` , `globals()` is used to obtain respective scope variable.

```python
print(globals())


{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <_frozen_importlib_external.SourceFileLoader object at 0x0000022FC686C700>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, '__file__': 'c:\\Users\\JEEKUMA\\Desktop\\BLOB\\water.py', '__cached__': None}
```

## zip(*iterable)

Iterate over several iterables in parallel, producing tuples with an item from each one.

```python
for item in zip([1, 2, 3], ['sugar', 'spice', 'everything nice']):
    print(item)

>>(1, 'sugar')
>>(2, 'spice')
>>(3, 'everything nice')
```

`zip()` stops when the shortest iterable is exhausted.

## zip and unzip

```python
x = [1,2,3,4,5]
y = [6,7,8,9,10]
zip_object = zip(x,y)
print(list(zip_object)) # after zipping two iterables


p, q = zip(*zip(x,y)) # this is a way to unzip zipped iterables
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
        Student.__init__(self,name)
        self.marks = marks

s1 = Marks('farzi', 10)
print(s1.__dict__)



'''the above code can be written using super class as below''

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

## slice(start, stop [,step]) method in python

slice method is an alternate way of using ***list[start:stop:step]*** in python.

```python
l = [1,6,3,2,8,6,89,23,5,25,76,87,42,61,90,22,13,45,78,65]
print(l)
#[1,6,3,2,8,6,89,23,5,25,76,87,42,61,90,22,13,45,78,65]

print(l[0::2]) # one way of list slicing method.
#1, 3, 8, 89, 5, 76, 42, 90, 13, 78]

print(l[slice(0,len(l),2)]) # alternate way of slicing
#1, 3, 8, 89, 5, 76, 42, 90, 13, 78]
```

## `__call__()`

`__call__()` function is practically used to make a class as a decorator and a class instance to be used as a function.

```python
class trial:
    def __init__(self, name) -> None:
        self.name = name

    def __call__(self, *args: Any, **kwds: Any) -> Any:
        print(f"the name is {self.name}")

boy = trial('kevin')
boy() # object of the class trial called as a function.
```

## String Methods

```python
'''strings are immutable and can not be changed once it is assigned to a variable. But string methods on the other hand can be used to create a new string with the existing one.'''


a="!!starwar!!"
a.upper() # outputs a upper case version of the string
a.lower() # outputs a lower case version of the string
a.rstrip() # this method strips the occurrence of the given 
#character at the end of the string. -> !!starwar
a.strip() # strips the given char from both the sides -> starwar
a.replace('war', 'jar') # replaces all occurrence of `war` with `jar`
# -> !!starjar!!
```

```python
b= "avenger.com"
b.split('.') # gives ['avenger', 'com']
b.capitalize() # gives Avenger.com  It converts first char to capital
b.count('com') # counts the occurrence of `com` in this string. -> 1
b.endswith('m') # returns a boolean if the string ends with m -> True
```

```python
'''Both the below methods work the same way but when a given string is not found find() return -1, index() returns an exception.'''


c = "Spiderman is an avenger"
c.find('is') # returns the index of the first occurrence of `is`
c.find('was') # returns -1 otherwise

c.index('is') # returns the index of the first occurrence of `is`
c.index('lwhoeu') # gives and exception saying ValueError
```

```python
isalnum(), isalpha(), islower()
swapcase() # swaps teh case of the given string
title() # converts the given strings case in to title case.
```

## List Methods

To initialize a list with an initial size we can do :

```python
l = [None] * 5
'''Here the length of the list is 5 and all the 5 elements if the list is assigned with None'''
```

List is a mutable type. Any list methods used on a list will affect the original list.

```python
a = [3,8,2,9,7,5,1,23,54]
a.append(4) #[3, 8, 2, 9, 7, 5, 1, 23, 54, 4]
a.sort() #[1, 2, 3, 4, 5, 7, 8, 9, 23, 54]
a.sort(reverse=True) #[54, 23, 9, 8, 7, 5, 4, 3, 2, 1]

a = [3,8,2,9,7,5,1,23,54]
a.reverse() #[54, 23, 1, 5, 7, 9, 2, 8, 3]
print(a.index(7)) # prints 4 as index of 7 in reversed list is 4
print(a.count(3)) # prints number of occurrence of 3 in the list

'''Here Changing an element of b changed the element of a. b is a reference of a '''
a = [3,8,2,9,7,5,1,23,54]
b=a # assigning like this is not a best practice.
b[0]=0
print(a) #[0, 8, 2, 9, 7, 5, 1, 23, 54]

a = [3,8,2,9,7,5,1,23,54]
b=a.copy() # this is best practice as, any changes made in b remains in b.
b[0]=0
print(a)#[3, 8, 2, 9, 7, 5, 1, 23, 54]

a = [3,8,2,9,7,5,1,23,54]
a.insert(4,100)
print(a) #[3, 8, 2, 9, 100, 7, 5, 1, 23, 54]
```

## f-strings in python

```python
spacecraft = 'voyager'
year = '1977'
print(f"{spacecraft} is a fly by satellite launched in {year}") 
#voyager is a fly by satellite launched in 1977

# if a curly bracket is also needed in the string
print(f"{spacecraft} is a fly by satellite launched in {year} 
weighs {{Nothing}}")
# voyager is a fly by satellite launched in 1977 weighs {Nothing}
```

## try-except-finally

In try-except-finally, a piece of code is tried. If exception occurs it can be caught in the except block. Finally block always get executed no matter what.

```python
'''demo of finally'''
def pool():
    try:
        something
        return return_value
    except:
        error handling
        return return_value
    finally:
        final wrap up lines

'''Here even after the try or except block hits the return statement finally gets executed. This is teh specialty of finally block'''
```

## if-else in single line statement:

```python
print("4 greater than 2") if 4>2 else print("5 greater than 3 ") if 5>3 else print("nothing")
```

## File handling

```python
with open("file.txt", "r") as f:
    print(f.read(), "\n", type(f)) # reads entire file till EOF
    print(f.tell()) # gives current position of the pointer. -> 766
    f.seek(0) # seek to a required position in a file. Here file pointer
    # seeks the 0th char and points to it -> points to G here
    print(f.tell()) # current position of pointer -> 0
    print(f.read(5)) # read 5 bytes from the current pointer position -> Galax

with open("file.txt", '+a') as f:    
    f.truncate(300) # truncates the file content into 300 bytes

'''now reading the file would contain only 300 char'''
```

## Decorators

Decorators take function as an argument and modify it and return a new function. Here raptor is a decorator that takes a function as an argument adds print statements at the beginning and end and returns a new function *endo()*

```python
def raptor(func):
    def endo(*args):
        print("hello form the decorator")
        func(*args)
        print("Bye!! from Decorator")
    return endo

@raptor
def average(a,b,c):
    print("average is :")
    print((a+b+c)/3)

if __name__ == "__main__":
    average(8,1,6)


output : hello form the decorator
average is :
5.0
Bye!! from Decorator
```

Below is a good boilerplate template for decorators in python that can be used to build more complex decorators.

```python
def decorator(func):
    def wrapper_decorator(*args, **kwargs):
        # Do something before
        value = func(*args, **kwargs)
        # Do something after
        return value
    return wrapper_decorator
```

## Asterisk * and / as arguments to function

When you see an asterisk (*) in the function parameter list, it typically indicates that all the parameters following it are keyword-only arguments.

```python
def fixture(  # noqa: F811
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
```

The `/` symbol specifies **positional-only arguments**, meaning they **must be provided in order** and **cannot be used as keyword arguments**.

```python
def divide(a, b, /):
    return a / b

print(divide(10, 2))  # ✅ Works: Positional arguments
print(divide(a=10, b=2))  # ❌ Error: Cannot use keyword arguments
```

## %s in python

A string can be formed using below line where `filename` and `line` are the strings that are printed in the place of `%s`

```python
print("Bad line in config-file %s:\n%s" % (filename,line))
```

A plain string can be formed as below:

```python
default_cfg = "turtle_%s.cfg" % cfgdict1["importconfig"]
```

## reversed() and reverse()

`reverse()` is used on the list and it modifies the original list into reversed list.

On the other hand `reversed()` is a builtin function in python that reverses the original list and provide a new list. The original list remains unchanged.

```python
lst_ = [1,2,3,4,5,6,7,8,9,0]

lst_.reverse()
print(lst_) 
>> [0, 9, 8, 7, 6, 5, 4, 3, 2, 1]
print(list(reversed(lst_))) 
>> [0, 9, 8, 7, 6, 5, 4, 3, 2, 1]
```

## Sorted() and sort()

Both of these functions use key as an argument where a callable can be passed.

Syntax of argument for both the functions are as:

```python
sorted(iterable, /, *, key=None, reverse=False) -> iterable
sort(iterable, /, *, key=None, reverse=False) -> None
```

```python
lst = [6,1,4,0,9,3,8,7,2,5]

print(sorted(lst)) #[0, 1, 2, 3, 4, 5, 6, 7, 8, 9] doesn't change the original list
print(lst) #[6, 1, 4, 0, 9, 3, 8, 7, 2, 5]

lst.sort()
print(lst) #[0, 1, 2, 3, 4, 5, 6, 7, 8, 9] Changes the list
```

## @staticmethod

Transform a method into a static method. A static method can be called either on the class (such as `C.f()`) or on an instance (such as `C().f()`).

A static method does not receive an implicit first argument. To declare a static method, use this idiom:

```python
class C:
    @staticmethod
    def f(arg1, arg2, argN): ...
```

## round(number, ndigits=None)

example, both `round(0.5)` and `round(-0.5)` are `0`, and `round(1.5)` is `2`. The return value is an integer if *ndigits* is omitted or `None`. Otherwise, the return value has the same type as *number*.

 `round(2.675, 2)` gives `2.67` instead of the expected `2.68`. This is not a bug.

## class str(object), repr(object) and ascii(object)

### str(*object=b''*, *encoding='utf-8'*, *errors='strict'*)

Return string version of the object. 

### repr(*object*)

Return a string containing a printable representation of an object. A class can control what this function returns for its instances by defining a `__repr__()` method.

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

>> '\u20ae\u20b0\u20a6\u20a9\ua7a6\ufbd4'
```

## chr() ord() and bin() hex() oct()

### ord() and chr()

`ord()` and `chr()` are inverse to each other.

`ord()` : gives unicode value of a character.

`chr()` : gives character of a unicode value.

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
>> 0b1010
```

### hex()

```python
hex(255)
'0xff'
```

### oct()

```python
oct(8)
'0o10'
```

## iter() and next()

`iter()` creates an iterator object.

with this iterator object use `next()` to iterate throughout.

```python
iterator = iter(lst_) 
print(next(iterator))
```

`next()` or `__next__()` could be used in association with the `iter` object to iterate through the values.

```python
a = [1,2,23,3,5,6,7,8]
Itr = iter(a)

for _ in range(len(a)):
    print(Itr.__next__()) 
>> 122335678
```

## min() and max()

Takes iterable and gives max or min accordingly.

`min(*iterable*, ***, *key=None*)`

`min(*iterable*, ***, *default*, *key=None*)`

`min(*arg1*, *arg2*, **args*, *key=None*)`

`max(*iterable*, ***, *key=None*)`

`max(*iterable*, ***, *default*, *key=None*)`

`max(*arg1*, *arg2*, **args*, *key=None*)`

## isinstance() and issubclass()

`isinstance(object, class)` shows if the object is an instance of the given class.

`class` attribute also accepts a tuple of classes, where the function returns true if `object` attribute is an instance of at lest one of the classes.

```python
class planet:
    pass

class Animal:
    pass

class Dog():
    pass

dog_instance = Dog()

print(isinstance(dog_instance, Dog))
print(isinstance(dog_instance, (Dog, Animal)))
print(isinstance(dog_instance, (planet, Animal))) 

>>True
>>True 
>>False
```

`issubclass(class, classinfo)` accepts two classes and checks if one class is the subclass of other. `clsasinfo` attribute can also accept a tuple of classes. Here the class has to be a subclass of either one of the classes in the tuple.

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

It is recommended to use `open` in the `with` statement as it takes care of closing the file once it exits `with` block. Even when an exception occur.

`fp` is a file object. Like file pointer in other languages.

```python
with open('abcd.txt', 'r') as fp:
    ....
```

### mode parameter can be:

| mode         | description                 |
| ------------ | --------------------------- |
| 'r'          | open the file in read mode  |
| 'w'          | open the file in write mode |
| 'rb' or 'wb' | open in binary mode         |

### reading a file after opening:

| definition                                    | description                                                                                                         |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| .read(size=-1)                                | reads the file based on byte size passed.<br>default byte size is -1 which reads all the bytes in the document.<br> |
| .readline(size=-1)                            | reads one line.<br>                                                                                                 |
| .readlines()                                  | reads all the lines of a document and returns a list.                                                               |
| *list(fp) is also equivalent to .readlines()* | where `fp`, the file object is type casted to list                                                                  |

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
    print(fp.read()
```

### working with two files at a time

```python
with open(r"example.log", 'r') as reader, open('writer.txt', 'w') as writer:
    writer.write(reader.read())
```

## venv

```python
python -m venv .env


# To clear the exisitng .env/ and create it again
python -m venv .env --clear


# To upgrade the python binary in virtual env with the system python
python -m venv .env --upgrade


# Install updated pip as soon as you create .env/
python -m venv .env --upgrade-deps


# Create multiple environments
# Here three python environments are created in the existing directory.
python -m venv .env/ .venv/ .environment/


# Change the displayed command prompt name
python -m venv .env --prompt="clinet_1"
```

## Miscellaneous

### Three ways of setting attribute value of a class

This can be done in three ways

```python
@dataclass
class Student:
    name: str
    grade: str
    age:int 


s1 = Student('jeeva', 'C', 20)
print(f"Student {s1.name} of age {s1.age} has {s1.grade} grade")
setattr(s1, 'grade' , 'A')
print(f"Student {s1.name} of age {s1.age} has {s1.grade} grade")
s1.grade = 'F'
print(f"Student {s1.name} of age {s1.age} has {s1.grade} grade")



>>> Student jeeva of age 20 has C grade
>>> Student jeeva of age 20 has A grade
>>> Student jeeva of age 20 has F grade
```

One is a conventional way where the attributes are given when declaring an instance of class `s1`

Using `setattr`

And using `s1.grade = 'F'`

```python
if sys.version_info >= (3, 8)
```

Above line is used to verify the version of python and based on that execute a certain code.

### Floor division operator

```python
print(15//4)
```

### Match case statements in python

These are valid form python 3.10. Match case is like switch case in C.

## len()

A `range` object doesn’t store all the values but generates them when they’re needed. However, you can still find the length of a `range` object using `len()`:

```python
len(range(1, 20, 2))
>> 10
```

## weakref in python

```python
import weakref

class MyClass:
    def __init__(self, name):
        self.name = name

    def print_name(self):
        print(self.name)

my_obj = MyClass("Nitrogen")
my_obj.print_name()
# >>>  Nitrogen

# Create weakref of my_obj
weak_reference = weakref.ref(my_obj)

# weak_ref object is callable | It must be called
if weak_reference() is not None:
    print("Object alive")
else:
    print("object Not alive")
# >>>  Object alive

# weakref object must be called and upon which its instance methods can be called
print(weak_reference().print_name())

# delete main object
del my_obj

# weakref must also be deleted
if weak_reference() is not None:
    print("Object alive")
else:
    print("object Not alive")
# >>> object Not alive
```

## dictionary in python

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
# list of Keys
g = list(a)

# List of Values
h = list(a.values())

# Delete an entry in dict
del a['one']

# clear all entries in a dict
a.clear()

# shallow copy a dict into other 
i = b.copy()
```

```python
# create a dict from 'fromkeys' method
j = dict.fromkeys(['four', 'five', 'six', 'seven', 'eight'], None)

# pop an entry by key
j.pop('six')

# pop the last entry
print(j.popitem())
```

```python
j.update({'seven':7})
# OR
j.update(seven=9)
j
```

### Chain map

```python
from collections import ChainMap

baseline = {'music': 'bach', 'art': 'rembrandt'}
adjustments = {'art': 'van gogh', 'opera': 'carmen'}
bboss = {'opera': [1,2,3,4,5], 'maven': 'kalmi'}

# `|` can be used to chain multiple dicts, last dict considered as latest
print(baseline|adjustments|bboss)

# collections.ChainMap can be used to chain multiple dicts, first dict considered as latest
chain_obj = ChainMap(baseline, adjustments, bboss)
chain_obj = dict(chain_obj)
print(chain_obj) 

output: 
>>> {'music': 'bach', 'art': 'van gogh', 'opera': [1, 2, 3, 4, 5], 'maven': 'kalmi'}
>>> {'opera': 'carmen', 'maven': 'kalmi', 'art': 'rembrandt', 'music': 'bach'}
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

Below are the methods of deque class

> 'append', 'appendleft', 'clear', 'copy', 'count', 'extend', 'extendleft', 'index', 'insert', 'maxlen', 'pop', 'popleft', 'remove', 'reverse', 'rotate'
