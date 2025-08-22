# Manual Python Bump UV Package Versions

When executed in your code forge (Forgejo, Codeberg, Gitea, etc), the pipeline will update all Python dependencies in a [`uv`](https://docs.astral.sh/uv) managed project based on their definitions in the `pyproject.toml` file.

## Setup

Add the [pipeline file](./uv-bump-package-versions.yml) to your repository's root at `./.woodpecker/uv-bump-package-versions`.
