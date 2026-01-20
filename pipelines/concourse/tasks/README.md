# Concourse Tasks

[Concourse tasks](https://concourse-ci.org/docs/tasks/) are the smallest configurable unit of a pipeline. This is where you define business logic/what the pipeline "does." Tasks can be separated from the pipelines to make them modular and re-usable.

## Using a task file in a pipeline

*[Concourse docs](https://concourse-ci.org/docs/how-to/pipeline-guides/common-pipeline/#putting-task-configs-in-files)*

While you can embed task steps directly in a Concourse pipeline, breaking them out into separate task files makes them useable in other pipelines. For example, this task runs [Vale](https://vale.sh) against a configurable path:

```yaml
platform: linux

image_resource:
  type: registry-image
  source:
    repository: jdkato/vale
    tag: latest

inputs:
  - name: repo

params:
  VALE_CONFIG: ".vale.ini"
  VALE_ARGS: ""
  VALE_PATH: content/

run:
  path: sh
  args:
    - -c
    - |
      cd repo

      vale sync
      eval vale --config "${VALE_CONFIG}" "${VALE_PATH}" ${VALE_ARGS}

```

To call this task in a pipeline, use the `file:` argument in a `task`:

```yaml
resources:
  - name: repo
    type: git
    source:
      uri: https://github.com/redjax/templates.git
      branch: main

jobs:
  - name: Check writing
    plan:
      ## Clone the git repository defined in resources:
      - get: repo
      
      ## With `try`, the pipeline will not fail if this step fails.
      #  Useful for checking writing without stopping deployments.
      - try:
          task: vale-lint
          file: repo/pipelines/concourse/tasks/vale/lint.yml
          ## Params to pass into task file. If you do not define these params,
          #  the default defined in the task file will be used.
          params:
            VALE_CONFIG: .vale.ini
            VALE_PATH: path/to/content/to/lint
            ## Optionally pass additional vale CLI args
            VALE_ARGS: "--max-warnings 5 --output line"
```
