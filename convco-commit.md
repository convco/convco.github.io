---
layout: page
title: convco-commit
permalink: /commit/
---

Interactive cli to create a conventional commit.
A wizard will guide you to create a conventional commit.

## Example

```sh
convco commit --feat -- -p --edit
```

## Usage

```plain
Helps to make conventional commits

Usage: convco commit [OPTIONS] [-- <EXTRA_ARGS>...]

Arguments:
  [EXTRA_ARGS]...  Extra arguments passed to the git commit command

Options:
  -C <PATH>                          Run as if convco was started in <path> instead of the current working directory
      --fix                          A bug fix
  -c, --config <CONFIG>
      --feat                         A new feature
      --build                        Changes that affect the build system or external dependencies
      --chore                        Other changes that don't modify src or test files
      --ci                           Changes to CI configuration files and scripts
      --docs                         Documentation only changes
      --style                        Changes that do not affect the meaning of the code (e.g. formatting)
      --refactor                     A code change that neither fixes a bug nor adds a feature
      --perf                         A code change that improves performance
      --test                         Adding missing tests or correcting existing tests
  -t, --type <TYPE>                  Specify your own commit type
  -s, --scope <SCOPE>                Specifies the scope of the message
  -m, --message <MESSAGE>            The first message will be the description. Other -m options will be used as the body
  -f, --footers <token>(=|:)<value>  Specify extra footers to the message [aliases: trailer]
      --breaking                     Introduces a breaking change
  -i, --interactive                  Interactive mode
  -h, --help                         Print help
```
