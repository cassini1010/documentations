# Python String Module

### Some constants defined in this module:

The constants defined in this module are:

##### string.ascii_letters:

The concatenation of the [`ascii_lowercase`](https://docs.python.org/3/library/string.html#string.ascii_lowercase "string.ascii_lowercase") and [`ascii_uppercase`](https://docs.python.org/3/library/string.html#string.ascii_uppercase "string.ascii_uppercase") constants described below. This value is not locale-dependent.

`abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ`

##### string.ascii_lowercases:

The lowercase letters `'abcdefghijklmnopqrstuvwxyz'`. This value is not locale-dependent and will not change.

### Unpacking from string:

```python
print("{0} is your first alphabet".format(*"galaxy"))
>> g is your first alphabet


print('{2}, {1}, {0}'.format(*'abc'))      # unpacking argument sequence
```

### Unpacking from variable assigned with string:

```python
a = '{0}'.format(*"jeevan")
print(a) 
>> j


groot = "hello this is jeevan"
a = '{0}'.format(*groot)
print(a)
>> h
```

### Alignment of the text:

`:` is used in the format string to align the string to left, right or center.

```python
'{:<30}'.format('left aligned')
>> 'left aligned                  '
'{:>30}'.format('right aligned')
>> '                 right aligned'
'{:^30}'.format('centered')
>> '           centered           '
'{:*^30}'.format('centered')  # use '*' as a fill char
>>'***********centered***********'
```

### Percentages:

```python
points = 19
total = 22
print('Correct answers: {:.2%}'.format(points/total)) 
>>86.36%
```
