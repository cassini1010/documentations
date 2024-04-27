# Pytest

## Getting started

### `__tracebackhide__`

The assert_identical function sets **tracebackhide** = True. This is optional. The effect
will be that failing tests will not include this function in the traceback.

```python
from cards import Card
import pytest


def assert_identical(c1: Card, c2: Card):
    __tracebackhide__ = True
    assert c1 == c2
    if c1.id != c2.id:
        pytest.fail(f"id's don't match. {c1.id} != {c2.id}")


def test_identical():
    c1 = Card("foo", id=123)
    c2 = Card("foo", id=123)
    assert_identical(c1, c2)


def test_identical_fail():
    c1 = Card("foo", id=123)
    c2 = Card("foo", id=456)
    assert_identical(c1, c2)
```

### outcomes of test

Outcomes of test can be

```shell
PASSED (.)
FAILED (F)
XPASS (X) 
XFAIL (x)
SKIPPED (s)
ERROR (E)
```

### Testing expected exception

The normal try-catch block is not suitable for testing expected exceptions. Below code passes if exceptinois raised and fails if it is not raised. But a try-catch block passes the test if exception is raised and caught and it also passes the test of the exception is not raised.

```python
import cards
import pytest


# suggested way to test expected exception
def test_no_path_fail():
    with pytest.raises(TypeError):
        cards.CardsDB()
```

## pytest fixtures

Below example code represents fixtures in pytest, where first test passes, second results in Error and third fails.

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
    """Try to use failing fixture."""
    assert some_other_data == 42




@pytest.fixture()
def a_tuple():
    """Return something more interesting."""
    return (1, "foo", None, {"bar": 23})


def test_a_tuple(a_tuple):
    """Demo the a_tuple fixture."""
    assert a_tuple[3]["bar"] == 32


>>> test_fixtures.py::test_some_data PASSED                                                                                                      [ 33%]
>>> test_fixtures.py::test_other_data ERROR                                                                                                      [ 66%]
>>> test_fixtures.py::test_a_tuple FAILED  
```

**If a test results in “Fail,” the failure is somewhere in the test function (or something the function called). If a test results in “Error,” the failure is somewhere in a fixture.**

### tracing fixture execution

When two or more test functions use the same fixture, we can visually see how/when the fixture is called using `pytest --setup-show` flag.

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

We can have conftest.py files at really every level of our test directory. Tests can use
any fixture that is in the same test module as a test function, or in a conftest.py
file in the same directory, or in any level of parent directory up to the root of
the tests.

```python
pytest --fixtures # will bring all the locatin s of where fixtures are defined
```

```python
pytest --fixtures-per-test <folder name or testFile name>
# prints the fixturs used in test functions
```



## Parameterization

There are three types aof parameterization

- Parametrizing functions

- Parametrizing fixtures

-  Using a hook function called pytest_generate_tests



### Parameterizing test function

Test function takes `pytest.mark.parametrize` decorator to achive this. This takes variable names nd list of parameter values. Variable names can be comma separated strings or list of strings. Values must be in a list (list of tuples).

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



### Selecting one test when parameterized

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



### Parameterize using hook function `pytest_generate_test`

```python
def pytest_generate_tests(metafunc):
    if "start_state" in metafunc.fixturenames:
        metafunc.parametrize("start_state", ["done", "in prog", "todo"]) 

def test_finish(cards_db, start_state): 
    ...

```



### How to manage logging:

Simply pass the name of the test file to be tested to pytest to test it.

```python
pytest test_one.py # tests all the test functions in this python file
pytest test_card.py::test_defaults # tests only test_defaults funciton in this python file
pytest <folder name> # tests all the test funcitons present in all the files in thsi folder
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

Running the above code using `pytest` is not goig to show any logging messages or the print statement on the console nor a log file is given as an output.

Using `pytest --capture=no` to run the test is going to print only the `print` statements on the console. Here `this is a print statement` prints on the console and all the logging messages are negelted.

##### Print logging statements to console:

To print the logging messages too to the console it is advisable to write a pytest configuration file with logging configurations in it and use **`caplog`** fixture to the test.

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

Below configurations can be made in `pytest.ini` file to log logging messages in a file.

No `caplog` fixture to be used.

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

NOTE : **print statements are not printed**

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

Run `pytest --capture=no` 

# Handling test failures:

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

# Managing pytest output:

`pytest --tb` is helpful to log a detailed or rather short traceback when a test fails.

```python
pytest --tb=mode #Traceback print mode (auto/long/short/line/native/no)
```

`pytest --full-trace` is going to log a whole trace traverced by the test when it falis.

great way to understand the flow of the test script.

`pytest -v` increases verbosity of logging 

`pytest -vv` increases verbosity to two folds.

###### Creating JUnit format output files:

`pytest --junitxml=log.xml`  will create a log file `log.xml` with the standard log details in it.

`pytest --full-trace --junitxml.log.xml` is an efficient way to analyse code in depth when a test fails.

### The best feature of pytest is `pastebin`

`--pastebin=mode`       Send **failed|all** info to bpaste.net pastebin service.

sending all or failed mode to pastebin service creates an instant URL which contains the whole test session log details.

This URL can be used to share the log results with other collaborators.

# Temporary Directories and files in pytest:

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

By running `pytest --basetemp=TEMP` creates a base temp directory in the project directory itself and below folder structure is created.

```shell
C:.
├───jeevan0
│       waste.txt
│
└───test_kill0
        hello.txt
```

# Linting the pytest scripts:

```python
pip install flake8-pytest-style
```

 `flake8-pytest-style` is a  `flake8` plugin checking common style issues or inconsistencies with `pytest`-based tests. Could be a helpful tool.

# Changing standard test discovery:

`--ignore=path` ignores the test present in the folder path given. path can also be a specific python test file to igonre.

`--ignore-glob='*_01.p_'`  will ignore all the files which ends with glob pattern given.

pytest discovers tests by recursively searching the directory passed as an argument or current directory if no path is sent as an argument.

`pytest src/temp/`  or `pytest`

If, `norecursedirs` option is set in pytest.ini file then the it tells pytest not to recurse into these directories to find test files.

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

The other way to ignore the test files or folder in pytest is to provide the file of folder name in a standard list in pytest in <mark>conftest.py</mark> file

`collect_ignore` and `collect_ignore_glob`

# Fixtures:

`capsys` and `capsysbinary` are the built-in fixtures to capture the text in `sys.stdout` and `sys.stderr` 

```python
def test_output(capsys):
    print("hello")
    captured = capsys.readouterr()
    assert captured.out == "hello\n" 
    assert captured.out == b"hello\n" # for capsysbinary
```

`capfd` and `capfdbinary` are the built-in fixtures used to capture the text from file descriptors `1` and `2` 

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

Below files can be used as configuration files for a pytest project.

- pytest.ini

- tox.ini

- pyproject.toml

- setup.cfg
