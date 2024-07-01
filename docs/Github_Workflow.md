# Github Workflow

## Adding actions from public repo

Github actions can be added to your workflow from below possible places:

- The same repository as your workflow file

- Any public repository

- A published Docker container image on Docker Hub

Public repositories can be found in github marketplace. https://github.com/marketplace/actions/

## Adding actions from same repo

If an action is defined in the same repository where your workflow file uses the action, you can reference the action with either the ‌`{owner}/{repo}@{ref}` or `./path/to/dir` syntax in your workflow file.

Example repository file structure:

```shell
|-- hello-world (repository)
|   |__ .github
|       └── workflows
|           └── my-first-workflow.yml
|       └── actions
|           |__ hello-world-action
|               └── action.yml
```

## Save reports in artifact

Reports and log files generated in the project could be saved in an artifact using the below workflow:

```yaml
- name: Upload output file
  uses: actions/upload-artifact@v4
  with:
    name: output-log-file
    path: output.log
```

Download of this report or log file can be done from the artifact using below worflow. The download is often done using a separate workflow. If the download is supposed to be done in the same workflow file, use the `needs: <upload job name>` in the below wrokflow to specify that upload job has to run before hte download job.

```yaml
steps:
- name: Download a single artifact
  uses: actions/download-artifact@v4
  with:
    name: output-log-file
```
