# tox

## Installing tox

```bash
pip install tox
```



> After installing tox, create an empty `tox.ini` file and run the `tox` command. This will generate a `.tox` folder in the project directory.



## .tox

The `.tox` folder contains subdirectories named `.pkg`, `.tmp`, and `py`. The `.pkg` and `py` folders contain Python virtual environments. Among these environments, you should use the virtual environment in the `py` folder for project debugging and testing. The virtual environment in the `.pkg` folder is only used during the build process.

| Folder | Purpose                                                        | Should you use its interpreter? |
| ------ | -------------------------------------------------------------- | ------------------------------- |
| .pkg   | Builds the package before testing                              | ❌                              |
| .tmp   | Used by tox for storing cache and temporary files              | ❌                              |
| py     | Contains the virtual environment that users should make use of | ✅                              |
