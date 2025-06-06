# Material for MkDocs

## Getting started

Install `mkdocs-material`

```bash
pip install mkdocs-material
```

Initialaize new project, `.` is used to initialize the project in the current working directory.

```bash
mkdocs new .
```

Project Directory looks something like;

```bash
├───docs
│       index.md 
├───mkdocs.yml
```

Quick look on the page can be made using

```bash
mkdocs serve
```

This stats the server at http://127.0.0.1:8000



Site can be publised to GitPages using the below actions workflow

```yml
name: ci 
on:
  push:
    branches:
      - master 
      - main
permissions:
  contents: write
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Configure Git Credentials
        run: |
          git config user.name github-actions[bot]
          git config user.email 41898282+github-actions[bot]@users.noreply.github.com
      - uses: actions/setup-python@v5
        with:
          python-version: 3.x
      - run: echo "cache_id=$(date --utc '+%V')" >> $GITHUB_ENV 
      - uses: actions/cache@v4
        with:
          key: mkdocs-material-${{ env.cache_id }}
          path: .cache 
          restore-keys: |
            mkdocs-material-
      - run: pip install mkdocs-material 
      - run: mkdocs gh-deploy --force
```

This actions basically runs `mkdocs gh-deploy` command to deploy the site into github



## customization

custom javascript and css can be added as given below

```bash
.
├─ docs/
│  └─ stylesheets/
│  │  └─ extra.css 
│  └─ javascripts/
│     └─ extra.js
└─ mkdocs.yml
```

## Theam extension

If you want to alter the HTML source (e.g. add or remove some parts), you can extend the theme. MkDocs supports [theme extension](https://www.mkdocs.org/user-guide/customizing-your-theme/#using-the-theme-custom_dir), an easy way to override parts of Material for MkDocs

```bash
theme:
  name: material
  custom_dir: overrides
```

create a folder called `overrides` and add the custom html files.

> The folder structure, foldernames and file names under `overrides` folder must match the standard theams folder/file names and structure. Materials for MkDocs replaces the intended file with a custom file it it find the file with same name.



### writing own theam

In order to write own theam, below configuration must be used in the `mkdocs.yml`

```yml
theme:
  name: null
  custom_dir: overrides
```

`theam.name` = null, makes mkdocs to use them written in overrides folder which is located in the same path as `mkdocs.yml`



> Learn about writing own theam at [Themes - MkDocs](https://www.mkdocs.org/dev-guide/themes/) documentation.




