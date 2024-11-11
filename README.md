# action-restrict-base-branch

[![license](https://img.shields.io/badge/License-MIT-green.svg)](https://github.com/praha-inc/action-restrict-base-branch/blob/main/LICENSE)
[![Github](https://img.shields.io/github/followers/praha-inc?label=Follow&logo=github&style=social)](https://github.com/orgs/praha-inc/followers)

Restrict pull requests to merge only into specific branches.

## 👏 Getting Started

Create a workflow file under ```.github/workflows``` directory.

```yaml
name: Restrict base branch
on:
  pull_request_target:
    types: [opened, edited, synchronize]

jobs:
  restrict-base-branch:
    runs-on: ubuntu-latest
    permissions:
      pull-requests: write
    steps:
      - uses: praha-inc/action-restrict-base-branch@v1
        with:
          rules: |
            main <- development
            development <- feature/* bugfix/* refactor/* chore/* deps/*
            feature/* <- feature/**/*
```

## 🔧 Configurations

### `rules`

A list of rules that restrict pull requests to be merged into only certain branches.

Each rule is a list of branch patterns separated by `<-`.

The left-hand side specifies the name of the base branch, and the right-hand side specifies the name of the head branch.

If you want to merge only development branches into the main branch, configure as follows.

```yaml
rules: |
  main <- development
```

Multiple branch names can be specified on the right side, separated by spaces.

```yaml
rules: |
  main <- development staging
```

You can also use Glob to specify the branch name.

[Minimatch](https://github.com/isaacs/minimatch) is used for the matching process.

If you want to merge only feature and bugfix branches into the development branch, configure as follows.

```yaml
rules: |
  development <- feature/* bugfix/*
```

Also, multiple rules can be specified by adding a new line as shown below.

```yaml
rules: |
  main <- development
  development <- feature/* bugfix/*
```

## 🤝 Contributing

Contributions, issues and feature requests are welcome.

Feel free to check [issues page](https://github.com/praha-inc/action-restrict-base-branch/issues) if you want to contribute.

## 📝 License

Copyright © 2020 [PrAha](https://www.praha-inc.com/).

This project is [```MIT```](https://github.com/praha-inc/action-restrict-base-branch/blob/main/LICENSE) licensed.
