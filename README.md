# Building and deploying mkdocs

- Add new content in `docs/` folder.

- Run `git add` to add relevant changes.

- Run `git commit` to commit the changes made.

- Run `git push` to push the changes.

- Run `mkdocs gh-deploy` to deploy the page.



## What `mkdocs gh-deploy` does

- `mkdocs gh-deploy` first builds the project and creates a directory named `site/`.

- Contents of the`site/` directory is then copied to a branch named `gh-pages`. (this directory can be gitignored).

- This branch is then pushed to github.

- In github project `settings` -> `Pages` option, you can see that the branch `gh-pages` is used to deploy your static site.



## Best Practice

- gitignore `site/` directory

- No matter from which branch the `mkdocs gh-deploy` command is run, the `site/` directory will get copied to the `gh-page` branch and gets deployed as a site.
