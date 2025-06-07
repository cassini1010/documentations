# Numpy

`random` module in Python uses the Mersenne Twister algorithm to generate random numbers.

The `numpy` library uses a more efficient PCG (Permuted Congruential Generator) algorithm.

## Creating a basic array

```python
import numpy as np
A = np.array([3, 7, 2, 4, 5])
```

```python
>>> np.arange(10)
array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])

>>> np.arange(2, 3, 0.1)
array([ 2., 2.1, 2.2, 2.3, 2.4, 2.5, 2.6, 2.7, 2.8, 2.9])
```

## range() vs numpy.arange()

Unlike Python’s built-in `range()` function, `numpy.arange()` supports non-integer step sizes and returns an array of floats when needed.

## Built-in vs numpy's max() and min() functions

The built-in `max()` and `min()` functions work for one-dimensional lists or arrays, but do not handle multi-dimensional arrays. In such cases, numpy's `max()` and `min()` functions are useful.

## numpy.nanmax()

If the array contains missing elements (common in real-world data), `numpy.max()` will return `nan` because the maximum cannot be determined. 

`nanmax()` should be used in this case to find the maximum value while ignoring `nan` values.

## Random Number Generators

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

### Selecting a random element from an array

The `Generator` object’s [`.choice()`](https://numpy.org/doc/stable/reference/random/generated/numpy.random.Generator.choice.html) method allows you to select random samples from an array.

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

If you set `replace=False`, the same element cannot be selected more than once. By default, `replace` is `True`, so elements may be selected multiple times.

### Generate normally distributed random numbers

```python
import numpy as np

default_rng = np.random.default_rng()
print(default_rng.normal())
```
