# Install Pantheon Terminus

Reusable action for installing Pantheon's CLI tool [Terminus](https://pantheon.io/docs/terminus) 
to be used in Github actions.

This requires [creating a machine token in pantheon](https://pantheon.io/docs/machine-tokens), and adding it to the repository
or organization that you are running this action on.

## Input options
`pantheon-machine-token`
`setup-ssh`
`pantheon-ssh-key`
`terminus-version`

## Examples

### Install terminus without ssh set up.

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

### Install terminus with SSH set up.

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

