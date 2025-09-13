# Templates <!-- omit in toc -->

<!-- Repo image -->
<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="./.assets/img/github-header-image.png">
    <img src="./.assets/img/github-header-image.png" height="200">
  </picture>
</p>

<p align="center">
  <img alt="GitHub Created At" src="https://img.shields.io/github/created-at/redjax/templates">
  <img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/redjax/templates">
  <img alt="GitHub commit activity" src="https://img.shields.io/github/commit-activity/y/redjax/templates">
  <img alt="GitHub repo size" src="https://img.shields.io/github/repo-size/redjax/templates">
  <img alt="GitHub code size in bytes" src="https://img.shields.io/github/languages/code-size/redjax/templates">
</p>

A repository for templates I re-use. Most of the files are meant to be copied & pasted.

## Table of Contents <!-- omit in toc -->

- [Template Types](#template-types)

## Template Types

| Name      | Path                           | Description                                                                                                                      |
| --------- | ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------- |
| Configs   | [`configs/`](./configs/)       | Templates & examples of configurations for apps like Restic/Resticprofile.                                                       |
| Decontainers | [`devcontainers/`](./devcontainers/) | Templates for [Devcontainer](https://containers.dev) |
| Logrotate | [`logrotate`](./logrotate/) | Templates for Linux's [logrotate](https://linuxconfig.org/logrotate) utility. |
| Pipelines | [`./pipelines/`](./pipelines/) | Templates for pipelines like Github Actions, Drone CI, etc.                                                                      |
| Scripts   | [`./scripts/`](./scripts/)     | Scripts for repo management (i.e. auto Git branch pruning). Subdirectories are scripts for specific languages (Go, Python, etc). |
