# Python Interview Questions

### What are mutable and immutable data types?

The value of mutable objects can be changed without changing their `id`. Lists, dicts, and sets are examples.

The value of immutable objects cannot be changed after creation. Any modification results in a new object with a new `id`. Examples include int, float, str, and tuple.

### == and is

`==` compares the value of two objects, while `is` compares the `id` of two objects.

### Decorator

A **decorator** is a function that takes another function (or method) as input, wraps or extends its behavior, and returns a new function.

### Memory management

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

### Python as an Interpreted Language

Python is indeed an **interpreted language**, **but** it still has both a **compile-time** and a **runtime** phase — just not the same way as C or Java.

#### What happens when you run a `.py` file?

##### 1. **Compilation Phase (to Bytecode)**

- Python first **compiles your code into bytecode** (low-level, platform-independent instructions). This bytecode is run by the Python Virtual Machine (PVM), not by the system's operating system.

- This happens **automatically**, and the result is usually stored in `.pyc` files (under `__pycache__/`).

- This phase is **where scope is analyzed**, including:
  
  - Is a variable local or global?
  
  - Are there syntax errors?
  
  - Where are function boundaries?

##### 2. **Execution Phase (Runtime)**

- The **Python Virtual Machine (PVM)** then **executes** this bytecode line by line.

- This is the actual “interpreting” part — where variable values are assigned, functions are called, etc.

### Docstrings

- The **docstring itself is just a string** — it is **not executed** by default.

- However, if the docstring contains **Python code**, it can be **run using a testing tool** called `doctest`.
