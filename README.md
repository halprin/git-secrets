# git-secret
Git without secrets

## Prerequisites
[Python 3](https://www.python.org/downloads/) is required.  Python 2 is not supported.

Second, Python 3's `bin` directory needs to be in your `PATH` environment variable.  For example, if you are using the
python.org install on macOS, you will need to add the following to your `~/.profile`.
```bash
PATH="/Library/Frameworks/Python.framework/Versions/3.*/bin:${PATH}"
```

## Installation
`git-secrets` is located on [PyPI](https://pypi.org/project/qpp-git-secrets/).

To install, run the following.
```bash
$ pip3 install qpp-git-secrets
```

`sudo` may be needed if your Python 3 installation is in a protected directory.  This will put the command the `bin`
directory of your Python 3 installation.

To update `git-secrets` to the latest version, run the following.
```bash
$ pip3 install --upgrade qpp-git-secrets
```

Again, `sudo` may be required.

## Usage

Currently, `git-secrets` only checks the added lines of staged files.  AKA, only the added lines that are about to be
committed will be checked.

### Installing the Pre-commit Hook

Run the following when the PWD is in the repository you want to add a pre-commit hook...
```bash
$ git secrets install
```

If there exists a `pre-commit.d` directory, this will add a bash script into that directory.  If that directory doesn't
exist, the `pre-commit` bash script will be created directly.  If the `pre-commit` script already exists, `git-secrets`
will exit with an error since it chooses to not remove the previous pre-commit script.

### Manually scanning
If you want to manually scan a repository, you can run the following while your PWD is in the repository...
```bash
$ git secrets scan
```

Secrets are then scanned.

### Specifying Secrets
There are two locations that `git-secrets` checks for secret specifications.  The secrets from the two locations are
merged together.
1. A `.gitsecrets` file in the top level directory of the repository.
1. `~/.gitsecrets`.

Each line in these files should contain a regular expression.  The regular expression syntax is based off what the
[Python 3 `re` module](https://docs.python.org/3/library/re.html) supports.

#### Example Secrets
TINs that don't start with `000` or `999` or don't have `00` for the middle number group.
```regexp
(\D|^)(?!000)(?!999)\d{3}\s(?!00)\d{2}\s\d{4}(\D|$)
(\D|^)(?!000)(?!999)\d{3}-(?!00)\d{2}-\d{4}(\D|$)
(\D|^)(?!000)(?!999)\d{3}(?!00)\d{2}\d{4}(\D|$)
```

## Development
I accept PRs!  Check out the [issues](https://github.com/halprin/git-secrets/issues).
