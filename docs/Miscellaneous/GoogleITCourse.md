# GoogleIT Course

## Interpreted languages

- Python 

- Ruby

- Javascript

- Bash

- Powershell





In `Windows` system python file can be run without adding `python` in front of it.

Ex : File `chocolate.py` can be run as `chocolate.py` and `python chocolate.py`

### \_\_init\_\_.py file in a module:

If you want python to consider a directory consisting of python files as a module, then you are required to create a `__init__.py` file inside the directory. This file can be empty, but the file need to be present in the directory.

# 

# Git

To avoid entering username and password every time when you clone a repo or push the changes;

- Generate SSH key pair and store the public in your profile

- use Credential helper

## credential helper

```git
git config --global credential.helper cache
```

After enabling `credential helper` , type the password one last time.
