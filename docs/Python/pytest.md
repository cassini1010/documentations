# Pytest

## Getting started

### `__tracebackhide__`

The `assert_identical` function sets `__tracebackhide__ = True`. This is optional. The effect is that failing tests will not include this function in the traceback.

```python
from cards import Card
import pytest


def assert_identical(c1: Card, c2: Card):
    __tracebackhide__ = True
    assert c1 == c2
    if c1.id != c2.id:
        pytest.fail(f"id's don't match: {c1.id} != {c2.id}")


def test_identical():
    c1 = Card("foo", id=123)
    c2 = Card("foo", id=123)
    assert_identical(c1, c2)


def test_identical_fail():
    c1 = Card("foo", id=123)
    c2 = Card("foo", id=456)
    assert_identical(c1, c2)
```

###### Test Outcomes

The possible test outcomes are:

```shell
PASSED (.)
FAILED (F)
XPASS (X) 
XFAIL (x)
SKIPPED (s)
ERROR (E)
```

### Testing expected exception

A normal try-except block is not suitable for testing expected exceptions. The code below passes if an exception is raised and fails if it is not. However, a try-except block passes the test if the exception is raised and caught, and also passes if the exception is not raised, which is not ideal for testing.

```python
import cards
import pytest


# suggested way to test expected exception
def test_no_path_fail():
    with pytest.raises(TypeError):
        cards.CardsDB()
```

## pytest fixtures

The example code below demonstrates fixtures in pytest. The first test passes, the second results in an error, and the third fails.

```python
"""Demonstrate simple fixtures."""

import pytest


@pytest.fixture()
def some_data():
    """Return answer to ultimate question."""
    return 42
def test_some_data(some_data):
    """Use fixture return value in a test."""
    assert some_data == 42




@pytest.fixture()
def some_other_data():
    """Raise an exception from fixture."""
    x = 43
    assert x == 42
    return x


def test_other_data(some_other_data):
    """Attempt to use a failing fixture."""
    assert some_other_data == 42




@pytest.fixture()
def a_tuple():
    """Return something more interesting."""
    return (1, "foo", None, {"bar": 23})


def test_a_tuple(a_tuple):
    """Demonstrate the a_tuple fixture."""
    assert a_tuple[3]["bar"] == 32


>>> test_fixtures.py::test_some_data PASSED                                                                                                      [ 33%]
>>> test_fixtures.py::test_other_data ERROR                                                                                                      [ 66%]
>>> test_fixtures.py::test_a_tuple FAILED  
```

**If a test results in "Fail," the failure is in the test function (or something it called). If a test results in "Error," the failure is in a fixture.**

### tracing fixture execution

When two or more test functions use the same fixture, you can see how and when the fixture is called by using the `pytest --setup-show` flag.

```python
from pathlib import Path
from tempfile import TemporaryDirectory
import cards

import pytest


@pytest.fixture()
def cards_db():
    with TemporaryDirectory() as db_dir:
        db_path = Path(db_dir)
        db = cards.CardsDB(db_path)
        yield db
        db.close()


def test_empty(cards_db):
    assert cards_db.count() == 0



def test_two(cards_db):
    cards_db.add_card(cards.Card("first"))
    cards_db.add_card(cards.Card("second"))
    assert cards_db.count() == 2


>>>     SETUP    F cards_db
        ch3/test_count.py::test_empty (fixtures used: cards_db).
        TEARDOWN F cards_db
        SETUP    F cards_db
        ch3/test_count.py::test_two (fixtures used: cards_db).
        TEARDOWN F cards_db
```

### Finding where fixtures are defined

You can have `conftest.py` files at any level of your test directory. Tests can use any fixture that is in the same test module, in a `conftest.py` file in the same directory, or in any parent directory up to the root of the tests.

```python
pytest --fixtures # shows all the locations where fixtures are defined
```

```python
pytest --fixtures-per-test <folder name or testFile name>
# prints the fixtures used in test functions
```

## Parameterization

There are three types of parameterization:

- Parameterising functions

- Parameterising fixtures

- Using a hook function called `pytest_generate_tests`

### Parameterizing test function

A test function uses the `pytest.mark.parametrize` decorator for parameterization. This decorator takes variable names and a list of parameter values. Variable names can be a comma-separated string or a list of strings. Values must be provided as a list (or list of tuples).

```python
# test_func_param.py


@pytest.mark.parametrize(
"start_summary, start_state",
[
("write a book", "done"),
("second edition", "in prog"),
("create a course", "todo"),
],
)
def test_finish(cards_db, start_summary, start_state): 
    ...
```

### Selecting a Single Parameterized Test

```shell
 pytest -v "test_func_param.py::test_finish[write a book-done]"
```

### Parameterizing fixture

```python
@pytest.fixture(params=["done", "in prog", "todo"])
def start_state(request):
    return request.param

def test_finish(cards_db, start_state): 
    ...
```

### Parameterize using the hook function `pytest_generate_test`

```python
def pytest_generate_tests(metafunc):
    if "start_state" in metafunc.fixturenames:
        metafunc.parametrize("start_state", ["done", "in prog", "todo"]) 

def test_finish(cards_db, start_state): 
    ...
```

### How to manage logging:

Simply pass the name of the test file to pytest to run the tests.

```python
pytest test_one.py # tests all the test functions in this python file
pytest test_card.py::test_defaults # tests only test_defaults function in this python file
pytest <folder name> # tests all the test functions present in all the files in this folder
```

### A basic example:

```python
import logging

def  test_apple():
    logging.debug("LEET Debug message")
    logging.info("LEET info message")
    logging.warning("LEET warning message")
    logging.error("LEET error message")
    print("this is a print statement")
```

Running the above code using `pytest` will not show any logging messages or print statements on the console, nor will it produce a log file.

Using `pytest --capture=no` will print only the `print` statements to the console. In this case, `this is a print statement` will be printed, but all logging messages will be ignored.

##### Print logging statements to console:

To print logging messages to the console, it is advisable to write a pytest configuration file with logging settings and use the **`caplog`** fixture in your test.

```ini
pytest.ini file


[pytest]
log_format = %(asctime)s %(levelname)s %(message)s
log_date_format = %Y-%m-%d %H:%M:%S
log_level=DEBUG
```

```python
import logging

def  test_apple(caplog):
    logging.debug("LEET Debug message")
    logging.info("LEET info message")
    logging.warning("LEET warning message")
    logging.error("LEET error message")
    print("this is a print statement")
    print(caplog.text)
```

OUTPUT:

```shell
test_leet.py this is a print statement
2023-08-07 07:33:20 DEBUG LEET Debug message
2023-08-07 07:33:20 INFO LEET info message
2023-08-07 07:33:20 WARNING LEET warning message
2023-08-07 07:33:20 ERROR LEET error message
```

##### Print logging messages in a log file:

The following configurations can be added to the `pytest.ini` file to log messages to a file.

Do not use the `caplog` fixture in this case.

```python
import logging

def  test_apple():
    logging.debug("LEET Debug message")
    logging.info("LEET info message")
    logging.warning("LEET warning message")
    logging.error("LEET error message")
    print("this is a print statement")
```

```ini
pytest.ini file

[pytest]
log_file=log\logging.log
log_file_level=DEBUG
log_file_format=%(asctime)s %(levelname)s %(message)s
logfile_date_format=%Y-%m-%d %H:%M:%S
log_auto_indent=true
```

in /log/logging.log

```shell
07:39:08 DEBUG LEET Debug message
07:39:08 INFO LEET info message
07:39:08 WARNING LEET warning message
07:39:08 ERROR LEET error message
```

**Note: Print statements are not included in the log file.**

##### Print `logging` and `print` statements to console and log file:

```ini
[pytest]
log_format = %(asctime)s %(levelname)s %(message)s
log_date_format = %Y-%m-%d %H:%M:%S
log_level=DEBUG
log_file=log\logging.log
log_file_level=DEBUG
log_file_format=%(asctime)s %(levelname)s %(message)s
logfile_date_format=%Y-%m-%d %H:%M:%S
log_auto_indent=true
```

Run `pytest --capture=no` to print both logging and print statements to the console.

# Handling Test failures:

```python
pytest -x # stop after first failure
pytest -x --pdb #jump to pdb after first failure

pytest --max-fail=3 # stop after 3 failures
pytest --max-fail=3 --pdb #jump to pdb all the 3 failures.


pytest --pdb #jumps to pdb on every failure
pytest --trace # jumps to pdb from the beginning of the test
```

###### Two ways to add breakpoint:

```python
#pythons built in breakpoint() method
breakpoint()


#importing pdb module
import pdb
pdb.set_trace() ''' add this line where-ever 
executions needs to jump to pdb'''
```

# Managing Pytest Output:

`pytest --tb` is helpful for logging a detailed or shortened traceback when a test fails.

```python
pytest --tb=mode #Traceback print mode (auto/long/short/line/native/no)
```

`pytest --full-trace` is going to log a whole trace traversed by the test when it fails.

This is a great way to understand the flow of the test script.

`pytest -v` increases verbosity of logging 

`pytest -vv` increases verbosity to two folds.

###### Creating JUnit format output files:

`pytest --junitxml=log.xml`  will create a log file named `log.xml` with the standard log details.

`pytest --full-trace --junitxml=log.xml` is an efficient way to analyze code in depth when a test fails.

### The Pastebin Feature in Pytest

`--pastebin=mode`       Send **failed|all** info to bpaste.net pastebin service.

Sending all or failed test results to the pastebin service creates an instant URL containing the entire test session log details.

This URL can be used to share the log results with other collaborators.

# Temporary Directories and Files in Pytest:

```python
# from pytest import TempPathFactory
import os

def test_kill(tmp_path):
    print(tmp_path)
    with open(tmp_path/"hello.txt", 'x') as fp:
        fp.write("hello this is Dustin")

    assert os.path.exists(tmp_path)

def test_groot(tmp_path_factory):
    fp = tmp_path_factory.mktemp("Dustin") / "waste.txt"
    with fp.open('x') as fl:
        fl.write("Dustin")
```

Running `pytest --basetemp=TEMP` creates a base temporary directory in the project directory, resulting in the following folder structure:

```shell
C:.
├───jeevan0
│       waste.txt
│
└───test_kill0
        hello.txt
```

# Linting Pytest Scripts:

```python
pip install flake8-pytest-style
```

`flake8-pytest-style` is a `flake8` plugin that checks for common style issues or inconsistencies in `pytest`-based tests. It can be a helpful tool.

# Changing Standard Test Discovery:

`--ignore=path` ignores tests in the specified folder path. The path can also be a specific Python test file to ignore.

`--ignore-glob='*_01.p_'` will ignore all files that match the given glob pattern.

Pytest discovers tests by recursively searching the directory passed as an argument, or the current directory if no path is provided.

`pytest src/temp/`  or `pytest`

If the `norecursedirs` option is set in the pytest.ini file, pytest will not recurse into these directories to find test files.

```ini
[pytest]
norecursedirs = .env tmp*
```

This will not find test files in tmp prefixed dirs and .env dir.

###### To change the test file discovery pattern from test_*.py and *_test.py to some other pattern.

```ini
[pytest]
python_files= groot_*.py
python_classes=Groot
python_functions=groot_*
```

Another way to ignore test files or folders in pytest is to provide the file or folder name in a standard list in the `conftest.py` file.

`collect_ignore` and `collect_ignore_glob`

# Fixtures

`capsys` and `capsysbinary` are built-in fixtures used to capture text from `sys.stdout` and `sys.stderr`.

```python
def test_output(capsys):
    print("hello")
    captured = capsys.readouterr()
    assert captured.out == "hello\n" 
    assert captured.out == b"hello\n" # for capsysbinary
```

`capfd` and `capfdbinary` are built-in fixtures used to capture text from file descriptors 1 and 2.

```batch
where python 1>NUL //1 captures the output from terminal and directs it to NUL
where tycon 2>NUL //2 captures the error from the terminal and directs it to NUL
```

```python
def test_system_echo(capfd):
    os.system('echo "hello"')
    captured = capfd.readouterr()
    assert captured.out == "hello\n"
```

###### The `readouterr()` method in `capsys, capsysbinary, capfd, capfdbinary` returns `(out,err)` which is a tuple.

## Configuration files in pytest

The following files can be used as configuration files for a pytest project.

- pytest.ini

- tox.ini

- pyproject.toml

- setup.cfg
