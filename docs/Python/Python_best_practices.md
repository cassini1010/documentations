# Python Best Practices

## Wrap a Generator with a Context Manager

Wrapping a generator with the `contextmanager` decorator helps clean up resources when the context manager is exited. To convert a generator function into a context manager, use `contextmanager` from `contextlib`.

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

`from None` in the `raise` statement is used in situations where the originally raised exception and the exception raised by the `raise` statement are of the same exception class (e.g., `IndexError`).

When an `IndexError` is raised and caught, and another `IndexError` is raised, both the user-defined message and the original exception message are shown. Using `from None` suppresses the original exception message, so only the user-defined message is displayed.

> The three basic built-in sequence types in Python are lists, tuples, and strings.

## list_iterator

In the code snippet below, `number_iterator` is a `list_iterator` and is used to save memory by storing only one element at a time in memory.

The `list_iterator` allows you to access the elements of a list (or any iterable) one at a time, rather than loading all elements into memory at once. This is useful when working with large datasets or when you only need to process elements sequentially, saving memory.

```python
numbers = [random.randint(1, 20) for _ in range(20)]
numbers_iterator = iter(numbers)
```
