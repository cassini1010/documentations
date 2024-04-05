# Logging in python

## Introduction

```python
import logging
```

To use logging import logging in python file.

```python
import logging


logging.basicConfig(filename='example.log', encoding='utf-8',
                     level=logging.DEBUG, format='%(asctime)s : %(levelname)s : %(message)s',
                       filemode='w', datefmt='%Y-%m-%d %I:%M:%S %p')

logging.debug('This message should go to the log file')
logging.info('So should this')
logging.warning('And this, too')
logging.error('And non-ASCII stuff, too, like Øresund and Malmö')
```

`logging.basicConfig` is used to log the messages in a file given in `filename` keyword argument.

`level=logging.DEBUG` logs all the messgaes given.

```shell
example.log

2023-07-27 08:43:27 AM : DEBUG : This message should go to the log file
2023-07-27 08:43:27 AM : INFO : So should this
2023-07-27 08:43:27 AM : WARNING : And this, too
2023-07-27 08:43:27 AM : ERROR : And non-ASCII stuff, too, like Øresund and Malmö
```

if `level=logging.WARNING` only below messages are printed in the file.

```shell
example.log

2023-07-27 08:43:27 AM : WARNING : And this, too
2023-07-27 08:43:27 AM : ERROR : And non-ASCII stuff, too, like Øresund and Malmö
```

`format` is used to format the apperance of the message in the file.



```python
DEBUG:root:This message should go to the log file

INFO:root:So should this
```

with `format='%(asctime)s : %(levelname)s : %(message)`





```python
  2023-07-27 08:43:27 AM : DEBUG : This message should go to the log file
  2023-07-27 08:43:27 AM : INFO : So should this
```

- Default `filemode` is `r` . This keepes appending the messages to the file on each run of the project. `w` overwrites the file on each run of the projcet.

## Advanced Logging

Four catogoris of logging:

- Loggers

- Handlers

- Filters

- Formatters

Its a god convention to use a module level logger in each module which uses logging

```shell
logger = logging.getLogger(__name__)
```

There can be two types of destination to which the logger can log the message:

- Console

- File

#### Loggers

Most common method of configuring loggers is to use 

```python
Loggers.setLevel()
Loggers.addHandler() or Logger.removeHandler()
Loggers.addFilter() or Logger.removeFilter()
```

#### Handlers

Commonly used handlers are StreamHandlers and FileHandlers.

#### 

#### <u>Example for console handler</u>

Here it is important to set the logger level as a whole before setting the handler log level. 

```python
import logging

# Create Logger
logger = logging.getLogger(__name__)

# Set log level to the logger 
logger.setLevel(logging.DEBUG)

# create formatter
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')

# Create console handler
cons_hand = logging.StreamHandler()
cons_hand.setLevel(logging.WARNING)
cons_hand.setFormatter(formatter)

# 'application' code
logger.debug('debug message')
logger.info('info message')
logger.warning('warn message')
logger.error('error message')
logger.critical('critical message')

OUTPUT :
2023-08-03 22:24:59,105 - __main__ - WARNING - warn message
2023-08-03 22:24:59,106 - __main__ - ERROR - error message
2023-08-03 22:24:59,106 - __main__ - CRITICAL - critical message
```

#### Same logging can be achived using a configuration file:

```python
import logging

# Create Logger
logger = logging.getLogger(__name__)

# 'application' code
logger.debug('debug message')
logger.info('info message')
logger.warning('warn message')
logger.error('error message')
logger.critical('critical message')

OUTPUT :
2023-08-03 22:24:59,105 - __main__ - WARNING - warn message
2023-08-03 22:24:59,106 - __main__ - ERROR - error message
2023-08-03 22:24:59,106 - __main__ - CRITICAL - critical message
```

```ini
[loggers]
keys=root,simpleExample

[handlers]
keys=consoleHandler

[formatters]
keys=simpleFormatter

[logger_root]
level=DEBUG
handlers=consoleHandler

[logger_simpleExample]
level=DEBUG
handlers=consoleHandler
qualname=simpleExample
propagate=0

[handler_consoleHandler]
class=StreamHandler
level=DEBUG
formatter=simpleFormatter
args=(sys.stdout,)

[formatter_simpleFormatter]
format=%(asctime)s - %(name)s - %(levelname)s - %(message)sl
```
