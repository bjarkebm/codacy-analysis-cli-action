# Codacy GitHub Action

[![Codacy Badge](https://app.codacy.com/project/badge/Grade/946b78614f154f81b1c9c0514fd9f35c)](https://www.codacy.com/gh/codacy/codacy-analysis-cli-action/dashboard?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=codacy/codacy-analysis-cli-action&amp;utm_campaign=Badge_Grade)

GitHub Action for running Codacy static analysis on over 30 [supported languages](https://docs.codacy.com/getting-started/supported-languages-and-tools/) and returning identified issues in the code.

<br/>

<a href="https://www.codacy.com" target="_blank"><img src="images/codacy-logo.svg" alt="Codacy" width="400"/></a>

<br/>

[Codacy](https://www.codacy.com/) is the easiest way to ensure your team is writing high quality code. It allows you to define your own quality rules, code patterns and quality settings you'd like to enforce to prevent issues from entering the master branch. Codacy supports and maintains all the tools you need to analyze [more than 30 programming languages](https://docs.codacy.com/getting-started/supported-languages-and-tools/) such as PHP, Javascript, Python, Java, and Ruby.

## GitHub Action

The following is an example GitHub Action workflow that uses the Codacy Analysis CLI
to analyze each commit and pull request.

```yaml
name: codacy-analysis-cli

on: ["push"]

jobs:
  codacy-analysis-cli:
    runs-on: ubuntu-latest
    name: Codacy Analysis CLI
    steps:
      - name: Checkout code
        uses: actions/checkout@master
      - name: Run codacy-analysis-cli
        uses: codacy/codacy-analysis-cli-action@master
```

Running the action with the default configurations will:

- Analyze the current commit or pull request by running all supported static code analysis tools, with their default configurations,
  for the languages you are using.
- Print analysis results on the console, visible on the GitHub Action's workflow panel.
- Fail the workflow if at least one issue is found in your code.

Read the next section to learn how you can further configure this action.

### Caveats

This action supports all [Codacy Analysis CLI configuration options](https://github.com/codacy/codacy-analysis-cli#commands-and-configuration), with the following exceptions:

- `--commit-uuid` -- **Not supported**. The action will always analyze the commit that triggered it.
- `--api-token`, `--username`, and `--project` -- **Not supported**. Use [`--project-token`](https://github.com/codacy/codacy-analysis-cli#project-token) instead.

The command `validate-configuration` is also **not supported**.

When using `--project-token` make sure that you use [GitHub security features](https://docs.github.com/en/actions/reference/encrypted-secrets)
to avoid committing the secret token to your repository. For example, if you store your Codacy project
token in GitHub, this is how you would use it in the action workflow:

```yaml
# ...
uses: codacy/codacy-analysis-cli-action@master
with:
    project-token: ${{ secrets.<PROJECT_TOKEN_NAME> }}
# ...
```

## Contributing

We love contributions, feedback, and bug reports.
If you run into issues while running this action,
[open an issue](https://github.com/codacy/codacy-analysis-cli-action/issues) in this repository.
