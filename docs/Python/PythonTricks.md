# Python Tricks

## Unpacking in Python

Unpacking in Python is the process of extracting items from an iterable (*list, tuple, set, string, dictionary*) and assigning them to variables.

In the example below, `a` is an iterable and it is unpacked into a variable and a list.

The `*` notation is used before a variable to unpack the iterable into a `list`.

```python
# Tuple unpacking
coordinates = (3, 4)
x, y = coordinates
print("x:", x)  # Output: 3
print("y:", y)  # Output: 4
```

```python
a = (1, 2, 3, 4, 5, 6)
one, *rest, six = a
print(one, rest, six)
print(type(one), type(rest), type(six))

# Output:
# 1 [2, 3, 4, 5] 6
# <class 'int'> <class 'list'> <class 'int'>
```

```python
# This cannot be done
a = (1, 2, 3, 4, 5, 6)
*f = a
print(f)

# Output:
# SyntaxError: Starred assignment target must be in a list or tuple
```

```python
# This can be used to convert a tuple to a list
a = (1, 2, 3, 4, 5, 6)
[*f] = a
print(f)

# Output:
# [1, 2, 3, 4, 5, 6]
```

Unpacking in a function allows you to provide a variable number of arguments to the function.

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

## pop() Method on Lists

`pop()` is used to remove and return elements from a list. Once all elements are popped out, the list becomes empty. Printing the list now will print an empty list.

```python
a = [1, 2, 3, 4, 5, 6, 7]

while a:
    print(a.pop(-1), end='', flush=True)

print(a)
# Output:
# 7654321[]
```

## while Loop in One Line

A while loop can be written in one line. Multiple statements in the loop can be separated using `;`. However, complex statements are not supported in a single line.

```python
a = [1, 2, 3, 4, 5, 6, 7]

while a: print(a.pop(-1), end='', flush=True); print(" hello")
```

## Docstrings in Python

There are several docstring formats that can be used to help docstring parsers and users have a familiar and consistent format:

- **Google docstrings**: Supported by Sphinx.
- **reStructuredText**: This is the official Python documentation standard. Supported by Sphinx.
- **Numpy/SciPy docstrings**: A combination of Google and reStructuredText docstrings.

## If-Else Ternary Operation

```python
<expression 1> if <condition> else <expression 2>
```

Example:

```python
print("Pass") if marks >= 45 else print("Fail")
```

## `importlib` Standard Library

This module provides the `import_module` function, which allows you to programmatically import a module.

## For-If-Else Operation

##### `list comprehensions` and `generators` can be used interchangeably. While generators are more memory efficient, list comprehensions are not.

```python
# Using for and if in list comprehensions and generators
for_if = [i for i in range(1, 10) if i < 6]
# Output:
# [1, 2, 3, 4, 5]

# Using for, if, and else in list comprehensions and generators
for_if_else = [5 if i < 5 else 10 for i in range(1, 20)]
# Output:
# [5, 5, 5, 5, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10]

# General if-else syntax for ternary operation
if_else = True if 3 < 5 else False
# Output:
# True
```

## `type(self).__name__`

`print(type(self).__name__)` is used to print the name of the class to which the instance `self` belongs.

## Single and Double Underscore in Variable and Method/Function Names

Leading or trailing single and double underscores have significance in Python.

| Convention                             | Example            | Meaning                                                                                                                                                                                                                                                                                                                       |
| -------------------------------------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Leading single underscore              | `_variable`        | The variable is intended for internal use only. Considered as a private variable.                                                                                                                                                                                                                                             |
| Trailing single underscore             | `class_`, `float_` | Built-in keywords can be used as variable or method names with this trick to avoid conflicts with actual keywords.                                                                                                                                                                                                            |
| Leading double underscore              | `__attribute`      | Name mangling is used to make class attributes or methods private by prefixing their names with double underscores (`__`). Python internally modifies the name by appending `_ClassName` to make it harder to access directly from outside the class. Example: `_ClassName__attribute`                                         |
| Leading and trailing double underscore | `__init__`         | Special methods and attributes in Python.                                                                                                                                                                                                                                                                                     |

## Diátaxis

A systematic approach to technical documentation authoring. This has widespread adoption in the Python community.

## Keyword Listing

To list all the keywords, use the code below:

```python
import keyword as _keyword
print(_keyword.kwlist)

# Output:
# ['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```

## Ellipsis

Ellipses (`...`) in Python are primarily used as a placeholder or a marker for incomplete code or to represent an undefined value.

```python
# Represents an incomplete tuple
my_tuple = (1, 2, ...)

# Function to be written at a later stage and currently kept empty
def my_function():
    ...
```

## Integer String Conversion Length Limitation

The limit for string to integer conversion is 4300 (upper threshold) and 640 (lower threshold).

```python
import sys

print(sys.int_info.default_max_str_digits)
print(sys.int_info.str_digits_check_threshold)

# Output:
# 4300
# 640
```

To modify this, getters and setters are available:

```python
import sys

print(sys.get_int_max_str_digits())  # 4300
sys.set_int_max_str_digits()         # Used to set it to a desired value
```

## String Formatters

| Expr   | Meaning                                      | Example                          |
| ------ | -------------------------------------------- | -------------------------------- |
| {:d}   | integer value                                | "{0:.0f}".format(10.5) → '10'    |
| {:.2f} | floating point with that many decimals       | '{:.2f}'.format(0.5) → '0.50'    |
| {:.2s} | string with that many characters             | '{:.2s}'.format('Python') → 'Py' |
| {:<6s} | string aligned to the left that many spaces  | '{:<6s}'.format('Py') → 'Py    ' |
| {:>6s} | string aligned to the right that many spaces | '{:>6s}'.format('Py') → '    Py' |
| {:^6s} | string centered in that many spaces          | '{:^6s}'.format('Py') → '  Py  ' |

## Queues

FIFO (First-In, First-Out)

Adding an element to a queue is called `enqueue`.

Retrieving an element from a queue is called `dequeue`.

## Stack

LIFO (Last-In, First-Out)

## Deque (Double-Ended Queue)

A deque combines and extends the concepts behind stacks and queues. A deque can operate as either FIFO or LIFO.

# Python Object-Oriented Concepts

Methods in Python fall into several categories:

- Instance methods
- Class methods
- Static methods

## Instance Methods

**Instance methods** are the most common type of methods in Python. You define instance methods within a class by creating functions inside the class definition. When you create instances of a class, those individual instances can have their methods called so the program can control and modify those instances directly. Instance methods take a parameter called `self`, which represents the instance the method is being executed on. This allows you to access attributes of the instance using dot notation, like `self.name`, which will access the `name` attribute of that specific instance. When you have variables that contain different values for different instances, these are called instance variables.

## Class Methods

**Class methods**, on the other hand, are called on the class itself instead of an instance. They are marked with a `@classmethod` decorator and take a `cls` parameter that points to the class—not any specific instance—when the method is called. One common use case for class methods is to create and modify data structures that contain records for all instances of a class. Usually, programmers make a list inside the class definition, and methods to add instances of the class to that list in order to keep track of that class.

## Static Methods

Lastly, static methods, marked with a `@staticmethod` decorator, do not take a `self` or a `cls` parameter. Static methods behave like plain functions, except that you can call them directly from the class. It is important to note that you do not have to actually instantiate the class; the methods just reside in there. This is because class definitions are themselves objects (i.e., instances of abstract base classes), which reduces overhead and allows functions to be encapsulated in an easy-to-use way. Programmers use static methods when the method does not need to access any instance- or class-specific data.
