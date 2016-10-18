### Requirements
- A Git repository
- A Dotbot configuration file in that repository
- Python 3

#### Dependencies installation

##### Debian Jessie

On Debian Jessie, run the following commands:

    # apt-get install libgit2-dev python3-cffi python3-yaml
    # pip3 install -r requirements.txt


### Instructions
Save `pre-commit` and `prepare-commit-msg` to `.git/hooks` in your dotfiles directory. Alternatively, use a Git hook manager like [git-hooks](https://github.com/git-hooks/git-hooks).

Then when a file is added to the index and committed, your Dotbot configuration file will be updated with a new "link" entry:
```
link:
    ~/.filename: filename
```

If your Python executable has a name other than Python (e.g. `python3` or `python3.5`) you could use a wrapper script with the correct executable:
```
#! /usr/bin/env sh
python3.5 pre-commit "$@"
```

### Options
Options are configurable through environment variables:

- `AUTOBOT_DISABLED`: If this is non-empty, these hooks do nothing (default is empty).
- `AUTOBOT_REPO_ROOT`: Set the root directory for the repository (default is `.`).
- `AUTOBOT_DOTBOT_CONF`: Set an alternative name for your Dotbot config file (default is `dotbot.conf.yaml`).
- `AUTOBOT_INCLUDE`: Colon-separated list of files or directories files to exclude (default is the value of `$AUTOBOT_REPO_ROOT`). Basic wildcards (`*`, `**`, `?`, `[abc]`, and `[!abc]`) are allowed. Paths are first expanded using `glob.glob()`, and then matched using `Path.match()`, both in the Python standard library.
- `AUTOBOT_EXCLUDE`: Same notes as above. The exclusion check is applied _after_ the inclusion check.
- `AUTOBOT_DELETE_BACKUP`: If this is non-empty, delete the backup file when finished (not recommended).
- `AUTOBOT_DEBUG`: If this is non-empty, activate extremely verbose debug-level logging.


### Missing features

- Wildcard include/exclude
- Gitignore parsing
