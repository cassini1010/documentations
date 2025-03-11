# tox

## Installing tox

```bash
pip install tox
```



> After installing tox, create a empty `tox.ini` file and run `tox` command. This will generate a `.tox` folder in the project directory.



## .tox

`.tox` folder contains subdirectories named `.pkg` , `.tmp` and `py` . The .pkg and py are the folders that contain python virtual environments. Among these envirinments one must use the virtual environment in the py folder for project debugging and testing. Vitual environment in .pkg folder is only used during building process. 



| Folder | purpose                                                         | Should you uses its interpreter |
| ------ | --------------------------------------------------------------- | ------------------------------- |
| .pkg   | Builds the package before testing                               | ❌                               |
| .tmp   | Used by tox for storing cache and temporary files               | ❌                               |
| py     | contains the virtual environment that users shuold make use of. | ✅                               |
