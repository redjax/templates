# Automated Go Release <!-- omit in toc -->

Automate the process of building a Go project for multiple platform, creating a git tag, and creating a Github release. The release will have .zip files for each platform that was built.

## Table of Contents <!-- omit in toc -->

- [Setup](#setup)
- [Usage](#usage)

## Setup

- Copy [the pipeline's contents](./release.yml) into a file at `.github/workflows/release.yml`.
  - You can name the file whatever you want, as long as it ends with `.yml/.yaml` and exists under `.github/workflows/`
- Edit the pipeline file.
  - In the `env:` section:
    - Set `BIN_NAME` to the name you want to compile a binary to.
      - Should most likely match/approximate the name of the repository.
    - Set `MAIN_PACKAGE_PATH` to the path to your `main.go` file.
      - If `main.go` is at the repository root, you can use `.`
- Uncomment `push:` to enable triggering via git tag push.

## Usage

- Enable Actions in your Github repository ([instructions](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository)).
- Run the pipeline from Actions.
  - Choose release type (version bump):
    - `major` --> `vX.o.o`
    - `minor` --> `v0.X.0`
    - `patch` --> `0.0.X`
