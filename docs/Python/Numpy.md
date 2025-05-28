# Numpy

`random` module in python uses Mersenne twister algo to generate random numbers.

`numpy` uses a more efficient PCG algo.

## Basic way of creating array

```python
import numpy as np
A = np.array([3, 7, 2, 4, 5])
```

```python
>>> np.arange(10)
array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])

>>> np.arange(2, 3, 0.1)
array([ 2., 2.1, 2.2, 2.3, 2.4, 2.5, 2.6, 2.7, 2.8, 2.9]).1)
```

## range() and numpy.arange()

Unlike Python’s standard range() function, numpy.arange() can handle non-integer increments, and it automatically generates an array with np.float elements in this case.

## built-in max() min() and numpy's max() and min()

Built in `max()` and `min()` functions allow us to find the max and min element of a list or array of single dimension. It fails when the array is of two or more dimension. numpy's max and min functions comes to help in this case.

## numpy.nanmax()

If the array contains missing element (happens in real time data) then the `numpy.max()` gives `nan` as a max value as max becomes unknown when there is an unknown value in the array. 

`nanmax()` must be used in this case to find the max value excluding the unknown values.

## Random number generators

### Generate random numbers

```python
import numpy as np

default_rng = np.random.default_rng()
default_rng
print(default_rng.random())
```

### Generate random numbers between low and high value

`.random` and `.uniform` are exactly same unless the `low` and `high` values are provided.

```python
import numpy as np

default_rng = np.random.default_rng()
print(default_rng.uniform(low = 3, high = 9))
```

### Generate random integers

```python
import numpy as np

default_rng = np.random.default_rng()
print(default_rng.integers(low = 0, high = 100))
```

### More powerful random number generator

```python
from numpy.random import Generator, PCG64DXSM
pcg64dxsm_rng = Generator(PCG64DXSM())
print(pcg64dxsm_rng.random())
```

### Generate an array of random numbers

If you assign a tuple to `size`, then you’ll generate an array.

```python
.random(size=(5,5)) 5X5 array
.uniform(low = 1, high = 10, size=(10,)) 1X10 array
.integer(size(50,32)) 50X32 array
```

### Selecting random element from array

The `Generator` object’s [`.choice()`](https://numpy.org/doc/stable/reference/random/generated/numpy.random.Generator.choice.html) method allows you to select random samples from a given array.

```python
>>> import numpy as np

>>> rng = np.random.default_rng()

>>> input_array_1d = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12])
>>> rng.choice(input_array_1d, size=3, replace=False)
array([ 6, 12, 10])

>>> rng.choice(input_array_1d, size=(2, 3), replace=False)
array([[ 8, 12, 11],
       [10,  7,  5]])
```

If you set `replace` to `False`, then you can’t select the same element more than once. By default, it’s set to `True`, meaning the same element *might* be selected multiple times.

### Generate normally distributed random numbers

```python
import numpy as np

default_rng = np.random.default_rng()
print(default_rng.normal())
```
