# Manual Python Bump UV Package Versions

When executed in your code forge (Forgejo, Codeberg, Gitea, etc), the pipeline will update all Python dependencies in a [`uv`](https://docs.astral.sh/uv) managed project based on their definitions in the `pyproject.toml` file.

## Setup

> [!NOTE]
> This document assumes you're using Forgejo as your code forge. Forgejo is similar to Codeberg and Gitea still, so the documentation should apply to your instance.

- Add the [pipeline file](./uv-bump-package-versions.yml) to your repository's root at `./.woodpecker/uv-bump-package-versions`.
- In Forgejo, [Create a Forgejo API token]() for the pipeline
- In the Woodpecker UI, navigate to your repository's settings and open "secrets"
  - Click "Add secret", create one named `FORGEJO_TOKEN` (or `{GITEA,CODEBERG,etc}_TOKEN)`)
  - In the `Value` field, paste the token you created in your code forge.
