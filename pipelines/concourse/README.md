# Concourse CI Pipelines <!-- omit in toc -->

Pipeline/task files for [Concourse CI](https://concourse-ci.org).

## Table of Contents <!-- omit in toc -->

- [Notes](#notes)
- [Login to Concourse](#login-to-concourse)
  - [Fly CLI targets](#fly-cli-targets)
- [Deploy a pipeline](#deploy-a-pipeline)
- [Do a test run](#do-a-test-run)
- [Archive a pipeline](#archive-a-pipeline)
- [Destroy a pipeline](#destroy-a-pipeline)
- [Links](#links)

## Notes

- [Fly CLI docs](https://concourse-ci.org/docs/fly/)

## Login to Concourse

Login to Concourse with the `fly login` command. You must provide "target name," which is the name you will refer to this session as when running other Fly commands.

```shell
fly login -t <target-name> --concourse-url https://ci.example.org
```

### Fly CLI targets

Show all targets:

```shell
fly targets
```

Edit a target's name, team, or URL:

```shell
fly -t <target-name> edit-target \
  --target-name <new-name> \
  --concourse-url https://ci.example.com \
  --team-name <team-name>
```

To delete a target:

```shell
fly -t <target-name> delete-target
```

## Deploy a pipeline

> [!NOTE]
> This command assumes the pipeline you want to deploy exists on your current machine. You can also [run `set-pipeline` from a Concourse pipeline](https://concourse-ci.org/examples/set-pipeline/), which automatically deploys the latest version on git changes.

After creating or changing a pipeline, you have to "deploy" it to Concourse with `set-pipeline`:

```shell
fly -t <target-name> set-pipeline --pipeline <name-in-webui> --config path/to/pipeline.yml
```

## Do a test run

You can use [`fly exec`](https://concourse-ci.org/docs/tasks/#running-tasks-with-fly-execute) to execute a [Concourse task](./tasks/) or [pipeline](./pipelines/) without deploying it to Concourse:

```shell
fly -t <target-name> execute -c path/to/pipeline-or-task.yml -i repo=.
```

## Archive a pipeline
[Archiving a pipeline](https://concourse-ci.org/docs/pipelines/managing-pipelines/#fly-archive-pipeline) hides it from the webUI, but retains its build history:

```shell
fly -t <target-name> archive-pipeline -p <name-in-webui>
```

## Destroy a pipeline

[Destroying a pipeline](https://concourse-ci.org/docs/pipelines/managing-pipelines/#fly-destroy-pipeline) removes it from the webUI and deletes its configuration & build history:

```shell
fly -t <target-name> destroy-pipeline -p <name-in-webui>
```

## Links

- [Concourse home](https://concourse-ci.org)
- [Concourse Docs](https://concourse-ci.org/docs)
  - [Getting started guide](https://concourse-ci.org/docs/getting-started/)
  - [Installation instructions](https://concourse-ci.org/docs/install/)
  - [Fly CLI reference](https://concourse-ci.org/docs/fly/)
  - [Example pipelines](https://concourse-ci.org/examples/)
- [Concourse Github](https://github.com/concourse/concourse)
  - [Example workflows](https://github.com/concourse/examples)
