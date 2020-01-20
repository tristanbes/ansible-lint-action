# Ansible Lint for GitHub Action
This action allows you to run `ansible-lint` with no additional options.


## Usage
To use the action simply create an `ansible-lint.yml` (or choose custom `*.yml` name) in the `.github/workflows/` directory.

For example:

```yaml
name: Ansible Lint  # feel free to pick your own name

on: [push, pull_request]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    # Important: This sets up your GITHUB_WORKSPACE environment variable
    - uses: actions/checkout@v2

    - name: Lint Ansible Playbook
      # replace "master" with any valid ref
      uses: ansible/ansible-lint-action@master
      with:
        # [required]
        # Paths to ansible files (i.e., playbooks, tasks, handlers etc..)
        # or valid Ansible directories according to the Ansible role
        # directory structure.
        # If you want to lint multiple ansible files, use the following syntax
        # targets: |
        #   playbook_1.yml
        #   playbook_2.yml
        targets: ""
        # [optional]
        # Arguments to be passed to the ansible-lint

        # Options:
        #   -q                    quieter, although not silent output
        #   -p                    parseable output in the format of pep8
        #   --parseable-severity  parseable output including severity of rule
        #   -r RULESDIR           specify one or more rules directories using one or
        #                         more -r arguments. Any -r flags override the default
        #                         rules in ansiblelint/rules, unless -R is also used.
        #   -R                    Use default rules in ansiblelint/rules in addition to
        #                         any extra
        #                         rules directories specified with -r. There is no need
        #                         to specify this if no -r flags are used
        #   -t TAGS               only check rules whose id/tags match these values
        #   -x SKIP_LIST          only check rules whose id/tags do not match these
        #                         values
        #   --nocolor             disable colored output
        #   --exclude=EXCLUDE_PATHS
        #                         path to directories or files to skip. This option is
        #                         repeatable.
        #   -c C                  Specify configuration file to use. Defaults to ".ansible-lint"
        args: ""

```

> TIP: N.B. Use `ansible/ansible-lint-action@v4.1.0` or any other valid tag, or branch, or commit SHA instead of `v4.1.0` to pin the action to use a specific version.

Alternatively, you can run the ansible lint only on certain branches:

```yaml

on:
  push:
    branches:
    - stable
    - release/v*
```

or on various [events](https://help.github.com/en/articles/events-that-trigger-workflows).

<br>

## License
The Dockerfile and associated scripts and documentation in this project are released under the [MIT](license).


## Credits
The initial GitHub action has been created by [Stefan Stölzle](/stoe) at
[stoe/actions](https://github.com/stoe/actions).
