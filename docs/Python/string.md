# Python String Module

### Some constants defined in this module:

The following constants are defined in the `string` module:

#### `string.ascii_letters`:

The concatenation of the [`ascii_lowercase`](https://docs.python.org/3/library/string.html#string.ascii_lowercase "string.ascii_lowercase") and [`ascii_uppercase`](https://docs.python.org/3/library/string.html#string.ascii_uppercase "string.ascii_uppercase") constants described below. This value is not locale-dependent.

`abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ`

#### `string.ascii_lowercase`:

The lowercase letters `'abcdefghijklmnopqrstuvwxyz'`. This value is not locale-dependent and will not change.

### Unpacking from a string:

```python
print("{0} is your first alphabet".format(*"galaxy"))
# Output:
# g is your first alphabet

print('{2}, {1}, {0}'.format(*'abc'))  # Unpacking argument sequence
# Output:
# c, b, a
```

### Unpacking from a variable assigned with a string:

```python
a = '{0}'.format(*"jeevan")
print(a)
# Output:
# j

groot = "hello this is jeevan"
a = '{0}'.format(*groot)
print(a)
# Output:
# h
```

### Alignment of text:

The `:` character is used in the format string to align text to the left, right, or center.

```python
'{:<30}'.format('left aligned')
# Output:
# 'left aligned                  '

'{:>30}'.format('right aligned')
# Output:
# '                 right aligned'

'{:^30}'.format('centered')
# Output:
# '           centered           '

'{:*^30}'.format('centered')  # Use '*' as a fill character
# Output:
# '***********centered***********'
```

### Percentages:

```python
points = 19
total = 22
print('Correct answers: {:.2%}'.format(points / total))
# Output:
# 86.36%
```
