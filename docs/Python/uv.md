# uv

`uv` is the most popular python library used to manage project. It is written in Rust and is 10x to 100x faster than its conventional counterpart libraries in python.

## create a project

Using the below command a new project directory `project_app` gets created in the location where the command is run.

```bash
uv init project_app
```

This generates different files and folders as shown below. `pyproject.toml` is prefilled with a basic metadata. `.python-version` file contains the version of python used in the project.

```bash
project_app
│   .git
│   .gitignore
│   .python-version
│   main.py
│   pyproject.toml
│   README.md
```

## use uv in an existing project

To use `uv` in an existing project,  `pyproject.toml`  should not be already present in the project. 

```bash
uv init
```

Use the above command to create the standard file structure that uv provides in the existing project. This newly created a `pyproject.toml` file and other files as described above.

## Run main.py using uv

Running `main.py` using `uv` creates a `.venv` folder and an `uv.lock` file. Running main.py using uv uses the python in the virtual environment to run the script.

```bash
uv run main.py
```

Folder structure after running the above command;

```bash
│   .venv
│   .git
│   .gitignore
│   .python-version
│   main.py
│   pyproject.toml
│   README.md
│   uv.lock
```

## adding dependencies

Below command can be used to add dependencies to the project. Here requests python module is added to the project. Running below command also adds the module entry in the pyproject.toml file too.

```bash
uv add requests
```

```bash
dependencies = [
    "requests>=2.32.3",
]
```

## Upgrade dependencies

This upgrades the installed package in the project.

```bash
uv add --upgrade requests
```

## Remove dependencies

This removes requests module from the project

```bash
uv remove requests
```

## Add dev dependencies

Here black module is added as a development dependency in the project and `pyproject.toml` file is also modified accordingly.

```bash
uv add --dev black
```

## list dependencies

To list dependencies one of the below commands can be used;

```bash
uv pip freeze
uv pip list
uv tree
```
