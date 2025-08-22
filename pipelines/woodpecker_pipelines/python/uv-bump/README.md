# Manual Python Bump UV Package Versions

When executed in your code forge (Forgejo, Codeberg, Gitea, etc), the pipeline will update all Python dependencies in a [`uv`](https://docs.astral.sh/uv) managed project based on their definitions in the `pyproject.toml` file.

> [!WARNING]
> This pipeline is untested until this notice is removed.

## Setup

> [!NOTE]
> This document assumes you're using Forgejo as your code forge. Forgejo is similar to Codeberg and Gitea still, so the documentation should apply to your instance.

- Add the [pipeline file](./uv-bump-package-versions.yml) to your repository's root at `./.woodpecker/uv-bump-package-versions`.
- In Forgejo, [Create a Forgejo API token]() for the pipeline
- In the Woodpecker UI, navigate to your repository's settings and open "secrets"
  - Click "Add secret", create one named `FORGEJO_TOKEN` (or `{GITEA,CODEBERG,etc}_TOKEN)`)
  - In the `Value` field, paste the token you created in your code forge.
- Add Woodpecker Forgejo & Git env vars (secrets) for the following:

| Env Var | Purpose | Example Value |
| ------- | ------- | ------------- |
| `WOODPECKER_FORGEJO_URL` | Base URL to your Forgejo server | `https://forgejo.example.com` |
| `GIT_AUTHOR_NAME` | Commit author name | `woodpecker-bot` |
| `GIT_AUTHOR_EMAIL` | Commit author email | `bot@woodpecker.localhost` | 
| `GIT_COMMITTER_NAME` | Committer name | *same as `GIT_AUTHOR_NAME`* |
| `GIT_COMMITTER_EMAIL` | Committer email | *same as `GIT_AUTHOR_EMAIL`* |
