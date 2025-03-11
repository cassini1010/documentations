# Python Tricks:

## Unpacking in python:

Unpacking in python is a process of extracting items from iterable ( *list, tuple, set, string, dictionary* )object and assigning it to variables.

In the below example `a` ia an iterable and it is unpacked into variable and list.

`*` notation is used before a variable to unpack the iterable into a `list` 

```py title="tupleunpacking.py" linenums="1"
# Tuple unpacking
coordinates = (3, 4)
x, y = coordinates
print("x:", x)  # Output: 3
print("y:", y)  # Output: 4
```

```python
a = (1,2,3,4,5,6)
one, *rest, six = a
print(one, rest, six)
print(type(one), type(rest), type(six)) 

>> 1 [2, 3, 4, 5] 6
>> <class 'int'> <class 'list'> <class 'int'>
```

```python
# This can not be done
a = (1,2,3,4,5,6)
*f = a
print(f)

>>SyntaxError: Starred assignment target must be in a list or tuple
```

```python
# This can be used to convert tuple to list
a = (1,2,3,4,5,6)
[*f] = a
print(f)

>>[1,2,3,4,5,6]
```

Unpacking in a function allows us to provide variable number of arguments to the function.

```python
# Unpacking in function arguments
def print_values(*args):
    for value in args:
        print(value)

print_values(1, 2, 3, 4, 5)
# Output:
# 1
# 2
# 3
# 4
# 5 
```

## pop() method on lists:

`pop()` is used to pop all elements out of the list. Once the elements are popped out the list becomes empty. Printing the list now will print an empty list.

```python
a = [1,2,3,4,5,6,7]

while a:
    print(a.pop(-1), end='', flush=True)

print(a) 
>>7654321[]
```

## while() loop in one line:

A while loop can be specified in one line. Multiple line in the loop can be separated using `;` . Complex statements are not supported in one line though.

```python
a = [1,2,3,4,5,6,7]

while a: print(a.pop(-1), end='', flush=True); print(" hello")
```

## docstrings in python:

There are fewdocstring formats that can be used to help docstring parsers and users to have a familiar and known format. 

- Google docstrings : supported by Sphynx

- reStructuredText: This is the official python documentation standard. Supported by sphynx

- Numpy/SciPy docstrings: Combination of Google and reStructuredText docstrings.

# 

## if-else ternary operation:

```python
<expression 1> if <condition> else <expression 2>
```

Ex:

```python
print("Pass") if marks >= 45 else print("Fail")
```

## `importlib` standard library:

This module provides the `import_module` function, which allows you to programmatically import a module.

## for-if-else operation:

##### `list comprehension` and `generators` can be used interchangeably. While generators are more memory efficient list comprehensions are not.

```python
# using for and if list comprehension and generator
for_if = [i for i in range(1,10) if i<6]
>> [1, 2, 3, 4, 5]


# using for, if and else in list comprehension and generators
for_if_else = [5 if i<5 else 10 for i in range(1,20)]
>>[5, 5, 5, 5, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10]


# general if, else syntax for ternary operation
if_else = True if 3<5 else False
>>True
```

## type(self)._\_name_\_:

`print(type(self).__name__)`  is used to print the name of the class to which the instance `self` belongs to.

## Single and double underscore in variable and method/function names:

Leading or trailing single underscore and double underscore has a significance in python. 

| Convention                             | Example            | Meaning                                                                                                                                                                                                                                                                                                                       |
| -------------------------------------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Leading single underscore              | `_variable`        | The variable is meant for internal use only. Considered as a private variable.                                                                                                                                                                                                                                                |
| Trailing single underscore             | `class_`, `float_` | Built in keywords can be used as a variable/method names with this trick. Avoid conflict with the actual keyword.                                                                                                                                                                                                             |
| Leading double underscore              | `__attribute`      | In Python, name mangling is a technique used to make class attributes or methods private by prefixing their names with double underscore (__). When a name is mangled, Python internally modifies its name by appending _ClassName to make it harder to access directly from outside the class.   Ex: `_ClassName__attribute` |
| Leading and trailing Double underscore | `__init__`         | Special methods and attributes in python.                                                                                                                                                                                                                                                                                     |

## Diátaxis:

A systematic approach to technical documentation authoring. This has a widespread adoption in the python community.

## keyword listing:

To list all the keywords use below code;

```python
import keyword as _keyword 
print(_keyword.kwlist) 


>>['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```

## Ellipsis

Ellipses (`...`) in Python are primarily used as a placeholder or a marker for incomplete code or to represent an undefined value.

```python
# Represents incomplete tuple
my_tuple = (1, 2, ...) 

# Function will be written in the later stage an currently kept empty
def my_function():
    ...
```

## Integer string conversion length limitation

The limit for string to integer conversion is 4300(upper threshold) 640 (lower threshold)

```python
import sys

print(sys.int_info.default_max_str_digits)
print(sys.int_info.str_digits_check_threshold) 

>>> 4300 
>>> 640
```

To modify this getters and setters are made available. ;

```python
import sys

print(sys.get_int_max_str_digits()) #4300
sys.set_int_max_str_digits() # used to set it to a desired value
```

## 

## string formatters

| Expr   | Meaning                                      | Example                          |
| ------ | -------------------------------------------- | -------------------------------- |
| {:d}   | integer value                                | "{0:.0f}".format(10.5) → '10'    |
| {:.2f} | floating point with that many decimals       | '{:.2f}'.format(0.5) → '0.50'    |
| {:.2s} | string with that many characters             | '{:.2s}'.format('Python') → 'Py' |
| {:<6s} | string aligned to the left that many spaces  | '{:<6s}'.format('Py') → 'Py    ' |
| {:>6s} | string aligned to the right that many spaces | '{:>6s}'.format('Py') → '    Py' |
| {:^6s} | string centered in that many spaces          | '{:^6s}'.format('Py') → '  Py  ' |

## Queues

FIFO

Adding element to Queue is called `enqueue` 

Retrieving element from Queue is called `dequeue`

## Stack

LIFO

## Deque(Double ended queue)

It combines and extends the idea behind the stack and a queue. Deque can work as FIFO or LIFO

# Python Object Oriented Concepts

Methods in Python fall into several categories: 

- Instance methods

- Class methods

- Static methods

## Instance Method

**Instance methods** are the most common type of methods in Python. You define instance methods within a class by creating functions inside the class definition. When you instantiate instances of a class, those individual instances can have their methods called so the program can control and modify those instances directly. Instance methods can take a parameter called self, which represents the instance the method is being executed on, that allows you to access attributes of the instance using dot notation, like self.name, which will access the name attribute of that specific instance of the class object. When you have variables that contain different values for different instances, these are called instance variables.

## **Class methods**

**Class methods**, on the other hand, are called for the class itself instead of an instance. They are marked with a @classmethod decorator and take a cls parameter that points to the class—and not any specific instance—when the method is called. One common use-case for class methods is to create and modify data structures that contain records for all instances of a class. Usually, programmers make a list inside the class definition, and methods to add instances of the class to that list in order to keep track of that class. 

## **Static methods**

Lastly, static methods, marked with a @staticmethod decorator, do not take a self or a cls parameter. Static methods behave like plain functions, except that you can call them directly from the class. It is important to note that you do not have to actually instantiate the class, the methods just reside in there. This is because class definitions are themselves an object (i.e., an instance of abstract base class), which reduces overhead and allows functions to be encapsulated in an easy-to-use encapsulation. Programmers use static methods when the method does not need to access any instance or class-specific data.
