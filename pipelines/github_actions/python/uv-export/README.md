# Manual Python Export requirements.txt from uv

When executed in Github, pipeline will export a `requirements.txt` by compiling a list of dependencies added with [`uv`](https://docs.astral.sh/uv), and open a PR with the changes.

## Setup

- Enable Actions in your Github repository ([instructions](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository)).
- Copy [the pipeline's contents](./uv-export-requirements.yml) into a file at `.github/workflows/uv-export-requirements.yml`.
  - You can name the file whatever you want, as long as it ends with `.yml/.yaml` and exists under `.github/workflows/`
