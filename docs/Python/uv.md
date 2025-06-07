# uv

`uv` is a popular Python library used for project management. It is written in Rust and is 10x to 100x faster than conventional Python libraries for similar tasks.

## Creating a Project

Use the following command to create a new project directory named `project_app` in the current location:

```bash
uv init project_app
```

This command generates various files and folders as shown below. The `pyproject.toml` file is prefilled with basic metadata. The `.python-version` file specifies the version of Python used in the project.

```bash
project_app
│   .git
│   .gitignore
│   .python-version
│   main.py
│   pyproject.toml
│   README.md
```

## Using uv in an Existing Project

To use `uv` in an existing project, ensure that a `pyproject.toml` file is not already present in the project directory.

```bash
uv init
```

Run the above command to create the standard file structure that `uv` provides in your existing project. This will create a new `pyproject.toml` file and other files as described above.

## Running main.py Using uv

Running `main.py` with `uv` creates a `.venv` folder and a `uv.lock` file. The script is executed using the Python interpreter from the virtual environment.

```bash
uv run main.py
```

The folder structure after running the above command will look like this:

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

## Adding Dependencies

Use the following command to add dependencies to your project. For example, to add the `requests` module:

```bash
uv add requests
```

This command also adds the module entry to the `pyproject.toml` file:

```bash
dependencies = [
    "requests>=2.32.3",
]
```

## Upgrading Dependencies

To upgrade an installed package in the project, use:

```bash
uv add --upgrade requests
```

## Removing Dependencies

To remove the `requests` module from the project, use:

```bash
uv remove requests
```

## Adding Development Dependencies

To add a development dependency (e.g., `black`) and update the `pyproject.toml` file accordingly:

```bash
uv add --dev black
```

## Listing Dependencies

To list dependencies, you can use any of the following commands:

```bash
uv pip freeze
uv pip list
uv tree
```
