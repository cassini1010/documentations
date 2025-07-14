# Python Interview Questions

## What are mutable and immutable data types?

The value of mutable objects can be changed without changing their `id`. Lists, dicts, and sets are examples.

The value of immutable objects cannot be changed after creation. Any modification results in a new object with a new `id`. Examples include int, float, str, and tuple.

Mutable datatypes are not hashable, while the immutable datatypes are.

## == and is

`==` compares the value of two objects, while `is` compares the `id` of two objects.

## Decorator

A **decorator** is a function that takes another function (or method) as input, wraps or extends its behavior, and returns a new function.

## Memory management

It consists of four concepts: `stack`, `heap`, `reference counting`, and `garbage collection`.

The stack stores local variable names, the return address of a function, etc.

The heap stores the actual data or objects. The reference to an object in the heap is stored as the value of a variable in the stack.

If a = 5 and id(a) = 4567342321

b = 5, id is same as a

| Stack          | Heap               |
| -------------- | ------------------ |
| a = 4567342321 | 5 (refcounter = 2) |
| b = 4567342321 |                    |

Objects in the heap also hold a value called the `reference counter`. This keeps track of how many references point to the object. If this value becomes zero, the object is collected by the garbage collector.

## Python as an Interpreted Language

Python is indeed an **interpreted language**, **but** it still has both a **compile-time** and a **runtime** phase — just not the same way as C or Java.

### What happens when you run a `.py` file?

#### 1. **Compilation Phase (to Bytecode)**

- Python first **compiles your code into bytecode** (low-level, platform-independent instructions). This bytecode is run by the Python Virtual Machine (PVM), not by the system's operating system.

- This happens **automatically**, and the result is usually stored in `.pyc` files (under `__pycache__/`).

- This phase is **where scope is analyzed**, including:
  
  - Is a variable local or global?
  
  - Are there syntax errors?
  
  - Where are function boundaries?

#### 2. **Execution Phase (Runtime)**

- The **Python Virtual Machine (PVM)** then **executes** this bytecode line by line.

- This is the actual “interpreting” part — where variable values are assigned, functions are called, etc.

## Docstrings

- The **docstring itself is just a string** — it is **not executed** by default.

- However, if the docstring contains **Python code**, it can be **run using a testing tool** called `doctest`.

## Tuple is efficent than list

- Tuple is a immutable datatype in python. One the tuple object is created it cannot be modified. Hence python doesn'e need to allocate extra space for expansion or reduction of tuple. 

- On the other hand List is a mutable datatype. Onece created, it can be modified. In order to achive the mutability of list, python has to allocate extra space for potential expansion or redcution of list elements.

## Namespace in Python

Namespace in python is a mapping of name and object. 

For example:

```python
x=5
```

`x` is the name, and it is refering to the object `5`.

When a name is used in a script, python first checks in the local namespace, then in the enclosing namespace, then globla namespace nad finally in the built-in namespace.

## What are frozenset in python

frozenset is a set which is immutable. `set` datatype in python is mutable and is not hashable and also cannot be used as a key in a dictionary. `forzenset` is hashable and can be used as a key in a dictionary.

## None in python

`x = None` means the name or variable is refering to no value or object.

## What is shallow copy and deep copy

### Shallow copy

```python
import copy
a = [[1, 2], [3, 4]]
b = copy.copy(a)

# appending element to list b doesn't affect a
b.append([5,6])

# modifying a nested element affects a too
b[0][0] = 100
print(a)
print(b) 
# Output:
# [[100, 2], [3, 4]]
# [[100, 2], [3, 4], [5, 6]]
```

### deep copy

```python
import copy
a = [[1, 2], [3, 4]]
b = copy.deepcopy(a)

# appending element to list b doesn't affect a
b.append([5,6])

# modifying a nested element affects a too
b[0][0] = 100
print(a)
print(b)

# Output:
# [[1, 2], [3, 4]]
# [[100, 2], [3, 4], [5, 6]]
```

## What is the GIL in Python, and how does it affect multi-threading?

GIL (Global interpreter lock) is a mechanism in CPython implementation where multiple threads are prevented from executing Bytecode at once. This is a safty mechanism as the `python memory management` is not thread-safe.

GIL ensures that onlt one thread is executes the bytecode at any given time. Therefore, no more than one core gets used even though the system has multiple cores.

Threading in python works similar to `async await` . Both prove useful in I/O bound task where waiting is involved and other task can be executed in that time.

## hashability in python

Hashability in python is where an object can be used as a key in a dictionary or as an element of a set.

> Set is not hashable but its elements must be hashable. So set can not contain a list. 😅(strange)

hash of an object can be generated if the object doesn't get modified in its lifetime after created. List can be modified after creation, hence its not hashable.

## What is context manager and write a program using `__enter__` and `__exit__`

Context manager is a resource management technique that allows setup and teardown of resource ensuring exception safty and thread safety.

> Context manager ensures that the resource is released safely even if the exception occurres.

```python
class OPEN:
    def __init__(self, file:str):
        self.file = file

    def __enter__(self):
        self.fp = open(self.file)
        return self.fp

    def __exit__(self, exc_type, exc_value, traceback):
        self.fp.close()

with OPEN(r"C:\Users\jeeva\OneDrive\Desktop\req.txt") as fp:
    for i in fp:
        print(i)
```

# 

## Pytest vs unittest

| Pytest                                     | Unit test                                                 |
| ------------------------------------------ | --------------------------------------------------------- |
| Flexible and powerful featurs in fixtuers  | setup and teardown fixture are the only available fixture |
| supports pythons assert statement          | It has its own assertion statements and keyworkds         |
| test parameterisation for code reusability | no parameterisation                                       |
| Powerful Plugins and hooks                 | ---                                                       |



## Pytest fixture

In pytest, fixtures are a powerful feature used to set up and tear down the environment for tests. They help in providing a consistent and reusable way to prepare test data, resources, or configurations before running tests, and clean up afterward. Fixtures make your tests more modular, readable, and maintainable.
