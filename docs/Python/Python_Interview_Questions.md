# Python Interview Questions

### What are mutable and immutable data types?

Mutable objects value can be changed without changing their `id`. List, dict, set are the examples.

Immutable objects value cannot be changed after its creation. Any modification resullts in a new object with new `id` . int, float, str, tuple

### == and is

`==` compares the value of two objcets, while `is` compares the `id`` of two objects.

### Decorator

A **decorator** is a function that takes another function (or method) as input, wraps or extends its behavior, and returns a new function.

### Memory management

It consist of 4 concepts `stack` , `heap`, `reference counting`, `garbage collection` .

Stack, stores the local variable names, return address of a funciton, etc ...

Heap, stores the actual data/object, the referrence to this object in heap is strored as a value in the variable stored in stack.

If a = 5 and id(a) = 4567342321

b = 5, id is same as a

| Stack          | Heap               |
| -------------- | ------------------ |
| a = 4567342321 | 5 (refcounter = 2) |
| b = 4567342321 |                    |

Object in the heap also hold another value called `reference counter`. This keeps track of how may references points to it. If this value becomes zero, it is collected by garbage collector.

### Python an Interpreted language

Python is indeed an **interpreted language**, **but** it still has both a **compile-time** and a **runtime** phase — just not the same way as C or Java.

#### What happens when you run a `.py` file?

##### 1. **Compilation Phase (to Bytecode)**

- Python first **compiles your code into bytecode** (low-level, platform-independent instructions). Since bytecode is run by PVM (python virtual Machine) and not by the systems OS.

- This happens **automatically**, and the result is usually stored in `.pyc` files (under `__pycache__/`).

- This phase is **where scope is analyzed**, including:
  
  - Is a variable local or global?
  
  - Are there syntax errors?
  
  - Where are function boundaries?

##### 2. **Execution Phase (Runtime)**

- The **Python Virtual Machine (PVM)** then **executes** this bytecode line by line.

- This is the actual “interpreting” part — where variable values are assigned, functions are called, etc.
