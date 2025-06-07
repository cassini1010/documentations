# PyInstaller

- `pyinstaller` is the main command to build a bundled application.

- `pyi-makespec` is used to create a spec file.

- `pyi-archive_viewer` is used to inspect a bundled application.

- `pyi-bindepend` is used to display dependencies of an executable.

- `pyi-grab_version` is used to extract a version resource from a Windows executable.

- `pyi-set_version` can be used to apply previously-extracted version resource to an existing Windows executable.

> One folder bundle is faster than the single file bundle

## Hiding the Source Code

The bundled app does not include any source code. However, PyInstaller bundles compiled Python scripts (`.pyc` files), which could, in principle, be decompiled to reveal the logic of your code.

If you want to hide your source code more thoroughly, one option is to compile some of your modules with `Cython`. Using Cython, you can convert Python modules into C and then compile the C code to machine language. PyInstaller can follow import statements that refer to Cython C object modules and bundle them.

`pyinstaller.exe` takes either the `.py` python file or the `.spec` file as the scriptname argument.
