# Release it Composite GitHub Action

`Release it` is a Composite GitHub Action designed to automate the release process for your project. It supports publishing to npm, GitHub releases, and allows customization through various inputs.

## Inputs

| Name             | Description                                    | Required | Default |
| ---------------- | ---------------------------------------------- | -------- | ------- |
| `release-branch` | Which branch you would like to release         | No       | `main`  |
| `dry-run`        | Enable dry run mode (no changes made)          | No       | `false` |
| `no-npm`         | Skip releasing to npm                          | No       | `false` |
| `no-git`         | Skip releasing to GitHub                       | No       | `false` |
| `manual-version` | Explicit version for the release (e.g., 1.0.0) | No       |         |
| `git-user`       | GitHub username                                | Yes      |         |
| `git-email`      | GitHub email                                   | Yes      |         |
| `git-token`      | GitHub token to push the release               | Yes      |         |

## Outputs

| Name      | Description                       |
| --------- | --------------------------------- |
| `version` | Version of the successful release |

## Usage Example

Below is an example workflow that demonstrates how to use the `Release it` composite action:

```yaml
name: Release Workflow

on:
  push:
    branches:
      - main

permissions:
  contents: write

jobs:
  release:
    runs-on: ubuntu-latest
    timeout-minutes: 5

    steps:
      - name: Checkout
        uses: actions/checkout@v4.1.6
        with:
          fetch-depth: 0

      - name: Run Release it Action
        uses: codemask-labs/release-it-action@v1
        with:
          git-user: "your-username"
          git-email: "your-email@example.com"
          git-token: "${{ secrets.GITHUB_TOKEN }}"
```

## Features

- **Dry Run**: Test the release process without making any changes.
- **Selective Releases**: Skip npm or GitHub releases as needed.
- **Custom Versioning**: Set a manual version for the release.
- **Branch-Specific Releases**: Release from branches other than `main`.

## Notes

1. Ensure that `actions/checkout` and `actions/setup-node` are properly configured in your workflow if required.
2. Use a valid GitHub token with `repo` permissions to enable release functionality.
3. This action uses `release-it` under the hood; refer to the [release-it documentation](https://github.com/release-it/release-it) for additional configuration options.

## License

This project is licensed under the [MIT License](LICENSE).

