# github-coverage-badge-action

Simple coverage badge that doesn't require external services or hosting, using just GitHub Actions.

## Prerequisites

The way this action works is by leveraging GitHub Pages deployments and pushing the generated badge in a `./badges` folder. So in order to use this action, you need to have GitHub Pages enabled for your repository.

First create a `gh-pages` branch in your repository, and then enable GitHub Pages in the repository settings.

> [!IMPORTANT]
> Make sure that a coverage summary report is generated by your test runner.<br />The action will look for a `coverage/coverage-summary.json` file in the root of your repository.

## Usage

Adding the badge to your README is as simple as:

```markdown
![coverage](https://<username>.github.io/<repo>/badges/<branch>/coverage.svg)]
```

### Installing the action in your workflow

1. Enable write permissions by adding the following on top of your tests workflow:

```yaml
permissions:
  contents: write
```

2. Add the following step to your workflow after tests have run:

```yaml
- name: Coverage badge
  uses: wouterds/github-coverage-badge-action@v1
```

### Options

| Option | Description | Default |
| --- | --- | --- |
| `label` | The label of the badge | `coverage` |
| `coverage-summary-path` | The path to the coverage summary file | `coverage/coverage-summary.json` |

### Example workflow

```yaml
name: tests

permissions:
  contents: write

on:
  push:

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
      - run: npm ci
      - run: npm run test
      - uses: wouterds/github-coverage-badge-action@v1
```

### Credits

Forked from https://github.com/we-cli/coverage-badge-action <3