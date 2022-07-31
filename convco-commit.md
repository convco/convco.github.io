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
convco-commit 
Helps to make conventional commits

USAGE:
    convco commit [OPTIONS] [-- <EXTRA_ARGS>...]

ARGS:
    <EXTRA_ARGS>...    Extra arguments passed to the git commit command

OPTIONS:
        --breaking
            Introduces a breaking change

        --build
            Changes that affect the build system or external dependencies

    -c, --config <CONFIG>
            

    -C <PATH>
            Run as if convco was started in <path> instead of the current working directory

        --chore
            Other changes that don't modify src or test files

        --ci
            Changes to CI configuration files and scripts

        --docs
            Documentation only changes

    -f, --footers <token>(=|:)<value>
            Specify extra footers to the message [aliases: trailer]

        --feat
            A new feature

        --fix
            A bug fix

    -h, --help
            Print help information

    -i, --interactive
            Interactive mode

    -m, --message <MESSAGE>
            The first message will be the description. Other -m options will be used as the body

        --perf
            A code change that improves performance

        --refactor
            A code change that neither fixes a bug nor adds a feature

    -s, --scope <SCOPE>
            Specifies the scope of the message

        --style
            Changes that do not affect the meaning of the code (e.g. formatting)

    -t, --type <TYPE>
            Specify your own commit type

        --test
            Adding missing tests or correcting existing tests
```
