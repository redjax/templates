# CodeQL Analysis

Analyze code for insecure/poor practice, errors, weak encryption, & more.

## Setup

- Enable Actions in your Github repository ([instructions](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository)).
- Copy [the pipeline's contents](./manual-ruff-lint.yml) into a file at `.github/workflows/codeql-analysis.yml`.
  - You can name the file whatever you want, as long as it ends with `.yml/.yaml` and exists under `.github/workflows/`
