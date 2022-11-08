# GitHub Action For Retrieving Experiments Stats With ClearML

Search ClearML for a task corresponding to the current PR and automatically add a comment with its scalars.

The action will identify a ClearML task as "corresponding" to the current PR if:
- The commit hash captured in the task is equal to the commit hash of the current PR
- There are NO uncommitted changes logged on the ClearML task
- The ClearML task was successful

## Example usage

```yaml
name: Get task stats
on:
  pull_request:
    branches: [ main ]
    types: [ assigned, opened, edited, reopened, synchronize ]

jobs:
  task-stats-to-comment:
      runs-on: ubuntu-20.04
      steps:
        - name: Get task stats
          uses: allegroai/clearml-get-stats@master
          with:
            CLEARML_API_ACCESS_KEY: ${{ secrets.ACCESS_KEY }}
            CLEARML_API_SECRET_KEY: ${{ secrets.SECRET_KEY }}
            CLEARML_API_HOST: ${{ secrets.CLEARML_API_HOST }}
            GH_TOKEN: ${{ secrets.GH_TOKEN }}
            COMMIT_ID: ${{ github.event.pull_request.head.sha }}
```

## Inputs