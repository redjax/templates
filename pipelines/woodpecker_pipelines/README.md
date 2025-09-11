# Woodpecker Pipelines

Pipeline files for [Woodpecker CI](https://woodpecker-ci.org).

## Notes

### ENV Vars

To use an environment variable in your pipeline, define it in the `environment:` section of your pipeline, like this:

```yaml
steps:
  - name: example-job
    image: alpine:latest
    environment:
      EXAMPLE_VAR: "Example value"

```

Then, reference it throughout your pipeline with `$${EXAMPLE_VAR}`. Note the double `$$` syntax. This ensures the environment variable is available at runtime. Also note you must "quote" the full full command/string, unless you start with a newline `|` character.

```yaml
---

when:
  event: [manual]

steps:

  ## Debug EXAMPLE_VAR, exit early if not set
  - name: debug
    image: alpine:latest
    environment:
      EXAMPLE_VAR: "Example value"
    commands:
      - "echo Example variable: $${EXAMPLE_VAR}"  # prints: Example variable: <value of EXAMPLE_VAR>
      
      ## Alternative syntax where you don't have to quote the whole string
      - |
        echo "Example variable: $${EXAMPLE_VAR}"  # prints: Example variable: <value of EXAMPLE_VAR>
      ## Print full env for manually reviewing value of $EXAMPLE_VAR
      - env | sort
      ## Test env var is set
      - env | grep EXAMPLE_VAR || echo "EXAMPLE_VAR not set"
```

### Woodpecker Secrets

You can also define Woodpecker secrets in the webUI (click a repository, then the settings cog, then click "Secrets") and [reference them in your pipeline](https://woodpecker-ci.org/docs/usage/secrets#usage). Just add `from_secret: SECRET_NAME` to the environment variable:

```yaml
steps:

  ## Debug EXAMPLE_VAR, exit early if not set
  - name: debug-url
    image: alpine:latest
    environment:
      EXAMPLE_VAR:
        ## The secret name must match what you put in Woodpecker exactly.
        #  If you use ALL_UPPERCASE, you must use that here, same for all_lowercase
        #  or camelCase.
        from_secret: EXAMPLE_VAR
    commands:
      ## Test env var is set
      - env | grep EXAMPLE_VAR || echo "EXAMPLE_VAR not set"
      ## Test env var is not empty string
      - "[ \"$${EXAMPLE_VAR}\" == \"\" ] && echo \"Woodpecker Forgejo URL is empty\" && exit 1 || echo \"Woodpecker Forgejo URL is not empty\""

```

## Links

- [Woodpecker Docs: Built-in environment variables](https://woodpecker-ci.org/docs/usage/environment#built-in-environment-variables)
