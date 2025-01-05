# Python best practices

## Wrap a generator with a context manager

Wrapping a generator with a context manager helps cleanup the task when the context manager is exited. To convert a generator function into a context manager use `contextmanager` from `contextlib`.

```python
from contextlib import contextmanager

@contextmanager
def file_reader(filename):
    try:
        # Open the file
        f = open(filename, 'r')
        yield f  # Yield the file object to the caller
    finally:
        # Cleanup: Close the file
        f.close()

# Example usage
with file_reader('example.txt') as f:
    for line in f:
        print(line.strip())
```

Receive input arguments from the console, split them using space as the delimiter, and convert each element to an integer in a single line.

> The `input()` function treats all characters as `str` by default.

```python
arr = map(int, input().split())
```

## `from None` in `raise`

```python
def dequeue(self):
        try:
            return self._items.popleft()
        except IndexError:
            raise IndexError("dequeue from an empty queue") from None
```

`from None` in the `raise` statement is used in the situations where the originally raised exception and exception raised by `raise` statement are of same exception class (Ex IndexError).

when `IndexError` is already raised its is catches and another index error is raised. The first statement prints `dequeue from an empty q`  statement and another statement from the original Index error is also printed. To get rid of the original IndexError statement and print only the iser defined statement in the `raise` line, `from None` is used.

> Three basic built-in sequences in python are List, Tuples and Strings.





## list_iterator

In the below code snippet `number_iterator` is a `list_iterator` and it is used to save memory by saving one element at a time in the memory.

The `list_iterator` allows you to access the elements of a list (or any iterable) one at a time, rather than loading all elements into memory at once. This is useful when working with large datasets or when you only need to process elements sequentially, saving memory.

```python
numbers = [random.randint(1, 20) for _ in range(20)]
numbers_iterator = iter(numbers)
```
