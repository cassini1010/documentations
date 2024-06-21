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
