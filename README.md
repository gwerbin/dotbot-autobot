Inspired by https://github.com/anishathalye/dotbot/issues/91


### Requirements
- A Git repository
- A Dotbot configuration file in that repository
- Python 3

There are non-Python dependencies for this tool. On Debian Jessie, you can install them with:
```
apt-get install libgit2-dev python3-cffi python3-yaml
```

and on OSX/macOS:
```
brew install libgit2 libyaml
```

Then install the Python requirements:
```
pip install -r requirements.txt
```

You can also use this technique to configure a [virtualenv](https://pypi.python.org/pypi/virtualenv) or [pyenv-virtualenv](https://github.com/yyuu/pyenv-virtualenv) for this, once you have found the full path to the executable.

### Usage instructions
Save `pre-commit` and `prepare-commit-msg` to `.git/hooks` in your dotfiles directory. Alternatively, use a Git [hook manager](http://githooks.com).

Then when a file is added to the index and committed, your Dotbot configuration file will be updated with a new "link" entry:
```
link:
    ~/.filename: filename
```

If your Python executable has a name other than Python (e.g. `python3` or `python3.5`, or if you are using a virtualenv) you could use a wrapper script with the correct executable:
```
#! /usr/bin/env sh
python3.5 pre-commit.py "$@"
```


### Options
Options are configurable through environment variables:

- `AUTOBOT_DISABLED`: If this is non-empty, these hooks do nothing (default is empty).
- `AUTOBOT_REPO_ROOT`: Set the root directory for the repository (default is `.`).
- `AUTOBOT_DOTBOT_CONF`: Set an alternative name for your Dotbot config file (default is `install.conf.yaml`).
- `AUTOBOT_INCLUDE`: Colon-separated list of files or directories files to exclude (default is the value of `$AUTOBOT_REPO_ROOT`). Basic wildcards (`*`, `**`, `?`, `[abc]`, and `[!abc]`) are allowed. Paths are first expanded using `glob.glob()`, and then matched using `Path.match()`, both in the Python standard library.
- `AUTOBOT_EXCLUDE`: Same notes as above. The exclusion check is applied _after_ the inclusion check.
- `AUTOBOT_DELETE_BACKUP`: If this is non-empty, delete the backup file when finished (not recommended).
- `AUTOBOT_DEBUG`: If this is non-empty, activate extremely verbose debug-level logging.


### Missing features

- Wildcard include/exclude
- Gitignore parsing
