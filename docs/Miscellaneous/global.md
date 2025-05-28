# Using and creating global variables:

 In Python, you’ll typically define global variables at the module level. Once you’ve defined a global variable, you can use it from within the module itself or from within other modules in your code.

Accessing a global variable works, but directly modifying a variable doesn’t work. You can’t directly modify a variable from a high-level scope like global in a lower-level scope like local.

### UnboundLocalError:

In the below example, python first tries to find variables `a`, `b`, `c` inside the `print_globas` function. It doesn't find any of the variables inside the function, but it finds it outside the function in the global scope.

```python
a = 10
b = 20
c = 30

def print_globals():
    print(a, b, c) 

>> 10 20 30
```

In the below example, python first tries to find variables `a`, `b`, `c` inside the `print_globas` function and it finds `c` but the value `100` doesn't get assigned to it in the first line. So `UnboundLocalError: cannot access local variable 'c' where it is not associated with a value` error is seen on the terminal.

`c` is both global and local variable in this function. Python gives priority to the local variable and shows error.

```python
a = 10
b = 20
c = 30

def print_globals():
    print(a, b, c) 
    c = 100
```

Below code resolves the UnboundLocalError exception by using `global` keyword.

```python
a = 10
b = 20
c = 30

def print_globals():
    global c
    print(a, b, c)
    c = 100
    print(c)

print_globals()
print(a,b,c)

>>> 10 20 30
>>> 10 20 100
>>> 10 20 100
```

If you want to modify a global variable inside a function, then you need to explicitly tell Python to use the global variable rather than creating a new local one. To do this, you can use one of the following:

1. The `global` keyword
2. The built-in `globals()` function
3. The `nonlocal` keyword

### Using `nonlocal` keyword:

`nonlocal` keyword is similar to `global` keyword. Only, it is used to in case of nested functions where a outer scoped variable is made use inside a inner function. 

```python
    def trial():
        a = 10
        print(a)
        def inner_func():
            print(a)
            a=100
        inner_func()
        print(a)

trial()
>>> UnboundLocalError
```

#### Fixing UnboundLocalError above:

```python
    def trial():
        a = 10
        print(a)
        def inner_func(): 
            nonlocal a 
            print(a)
            a=100
        inner_func()
        print(a)


trial() 
>>> 10
>>> 10
>>> 100
```

## globals() functions:

This function comes in handy when you have local variables with the same name as your target global variables, and you still need to use the global variable inside the function:

```python
>>> a = 10
>>> b = 20
>>> c = 30

>>> def print_globals():
...     print(a, b, globals()["c"])
...     c = 100
...     print(c)
...

>>> print_globals()
10 20 30
100

>>> c
30
```

## Best practices:

- Use only constant as globals, which are not going to change within the script.

- ```python
  USER = 'oia'
  ID = '1234235356'
  ```

- Use a function that takes argument and modified it and returns it if you need a global kind of variable which needs to be modified.

- Create a class and use the class attribute as a global variable throughout the class.
