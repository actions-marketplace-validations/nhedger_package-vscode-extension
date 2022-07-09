# Package VS Code Extension Action

This repository contains the source code for the `Package VS Code Extension` GitHub Action.

## Inputs

This action accepts the following inputs.

| Name             | Required | Default                          | Description                                                                                                                      |
| ---------------- | -------- | -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `extensionPath`  | NO       | `./`                             | Path to the root directory of the unpackaged extension. This is the directoy that holds the extension's `package.json` manifest. |
| `packagePath`    | NO       | `{extensionPath}/extension.vsix` | Path to which the VSIX package should be written                                                                                 |
| `baseContentUrl` | NO       |                                  | Base URL for links detected in Markdown files.                                                                                   |
| `baseImagetUrl`  | NO       |                                  | Base URL for images detected in Markdown files.                                                                                  |
| `githubBranch`   | NO       |                                  | GitHub branch used to publish the package. Used to automatically infer the base content and images URI.                          |
| `gitlabBranch`   | NO       |                                  | GitLab branch used to publish the package. Used to automatically infer the base content and images URI.                          |
| `useYarn`        | NO       | `false`                          | Whether to use Yarn instead of NPM.                                                                                              |
| `targetPlatform` | NO       |                                  | Target platform the extension should run on.                                                                                     |
| `preRelease`     | NO       | `false`                          | Whether to mark the package as a pre-release.                                                                                    |

## Outputs

This actions sets the following output values.

| Name          | Description                         |
| ------------- | ----------------------------------- |
| `packagePath` | Path to the generated VSIX package. |

## Example usage

### Simple

In this example, we rely on the defaults to package the extension.

```yaml
- name: Checkout
  uses: actions/checkout@v3

- name: Package VS Code extension
  uses: nhedger/package-vscode-extension@v1
```

### Alternative extension path

This example demonstrates using an alternative `extensionPath`.

```yaml
- name: Checkout
  uses: actions/checkout@v3

- name: Package VS Code extension
  uses: nhedger/package-vscode-extension
  with:
      extensionPath: ./packages/my-extension
```

### Publishing as an artifact

This example demonstrates publishing the generated VSIX package as an artifact.

```yaml
- name: Checkout
  uses: actions/checkout@v3

- name: Package VS Code extension
  id: package
  uses: nhedger/package-vscode-extension@v1

- name: Publish VS Code extension artifact
  uses: actions/upload-artifact@v3
  with:
      name: my-extension
      path: ${{ steps.package.outputs.packagePath }}
```
