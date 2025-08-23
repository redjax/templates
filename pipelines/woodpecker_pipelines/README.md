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

  ## Debug CODEFORGE_URL, exit early if not set
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
      - env | grep CODEFORGE_URL || echo "CODEFORGE_URL not set"
```

## Links

- [Woodpecker Docs: Built-in environment variables](https://woodpecker-ci.org/docs/usage/environment#built-in-environment-variables)
