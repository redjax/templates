# Manual Python Bump UV Package Versions

When executed in Github, pipeline will update all Python dependencies in a [`uv`](https://docs.astral.sh/uv) managed project based on their definitions in the `pyproject.toml` file.

## Setup

- Enable Actions in your Github repository ([instructions](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository)).
- Copy [the pipeline's contents](./uv-bump-package-versions.yml) into a file at `.github/uv-bump-package-versions.yml`.
  - You can name the file whatever you want, as long as it ends with `.yml/.yaml` and exists under `.github/workflows/`
