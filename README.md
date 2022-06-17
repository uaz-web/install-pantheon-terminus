# Install Pantheon Terminus

**install-pantheon-terminus** is a Github Action that downloads, installs, and authenticates Pantheon's CLI tool, [Terminus](https://pantheon.io/docs/terminus). As per [Pantheon's documentation](https://pantheon.io/docs/terminus/install#ssh-authentication), some commands may require SSH authentication, so this can be configured to setup SSH authentication with Pantheon. 

## Inputs

| Input Name | Description | Default |
|------------|-------------|---------|
| patheon-machine-token | A [machine token](https://pantheon.io/docs/machine-tokens) that must be created in the Pantheon dashboard and added as secret in Github. | **Must be provided (required)** |
| terminus-version | A specific version of Terminus. | **3.0.7** |
| setup-ssh | Boolean value that determines if an SSH key is setup or not.| **false** |
| pantheon-ssh-key | A SSH key that must be [added in the Pantheon dashboard](https://pantheon.io/docs/ssh-keys) and added as a secret in Github. | **Must be provided** |

## Examples

### Install Terminus without SSH key.

```
jobs:
  install-terminus:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Install Pantheon Terminus
        uses: az-digital/install-pantheon-terminus/@1.0.0
        with:
          pantheon-machine-token: ${{ secrets.PANTHEON_MACHINE_TOKEN }}
```

### Install Terminus and setup SSH key.

This requires [adding an SSH key](https://pantheon.io/docs/ssh-keys) to both pantheon, and the repository or organization
that you are running this action on.
```
jobs:
  install-terminus:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Install Pantheon Terminus
        uses: az-digital/install-pantheon-terminus/@1.0.0
        with:
          pantheon-machine-token: ${{ secrets.PANTHEON_MACHINE_TOKEN }}
          setup-ssh: true
          pantheon-ssh-key: ${{ secrets.PANTHEON_SSH_KEY }}
```

### Install a specific version of terminus.
You can specify which version of terminus to use, by default the latest version is downloaded.

```
jobs:
  install-terminus:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Install Pantheon Terminus
        uses: az-digital/install-pantheon-terminus/@1.0.0
        with:
          pantheon-machine-token: ${{ secrets.PANTHEON_MACHINE_TOKEN }}
          terminus-version: '3.0.5'
```

