---
layout: page
title: convco-commit
permalink: /commit/
---

Interactive cli to create a conventional commit.
A wizard will guide you to create a conventional commit.
The interactive scope prompt can complete scopes found in previous conventional commits while still accepting new valid scopes.
Use `--scope-history-limit` to control how many commits are scanned for those suggestions.

## Example

```sh
convco commit --feat -- -p --edit
convco commit --fix --scope parser --message "handle empty input"
convco commit --feat --breaking --trailer "Reviewed-by: Z"
convco commit --interactive --patch
```

The first `--message` value is used as the commit description.
Additional `--message` values become the commit body.

Use `--patch` to run `git add -p` before committing, and `--intent-to-add` to run `git add -N <PATH>`.
Both options can also be set with `CONVCO_PATCH` and `CONVCO_INTENT_TO_ADD`.

Extra arguments after `--` are passed to `git commit`.
`convco commit` can also be used as `GIT_EDITOR`; in that mode git invokes convco to edit the commit message instead of convco invoking `git commit`.

```sh
GIT_EDITOR='convco commit' git commit -p
git config --global alias.convco '!GIT_EDITOR="convco commit" git commit'
```

## Usage

```plain
Helps to make conventional commits

Usage: convco commit [OPTIONS] [-- <EXTRA_ARGS>...]

Arguments:
  [EXTRA_ARGS]...  Extra arguments passed to the git commit command

Options:
  -C <PATH>                            Run as if convco was started in <path> instead of the current working directory
      --fix                            A bug fix
  -c, --config <CONFIG>                [env: CONVCO_CONFIG=]
      --feat                           A new feature
      --build                          Changes that affect the build system or external dependencies
      --chore                          Other changes that don't modify src or test files
      --ci                             Changes to CI configuration files and scripts
      --docs                           Documentation only changes
      --style                          Changes that do not affect the meaning of the code (e.g. formatting)
      --refactor                       A code change that neither fixes a bug nor adds a feature
      --perf                           A code change that improves performance
      --test                           Adding missing tests or correcting existing tests
  -t, --type <TYPE>                    Specify your own commit type
  -s, --scope <SCOPE>                  Specifies the scope of the message
      --scope-history-limit <SCOPE_HISTORY_LIMIT>
                                        Limit the number of commits scanned for scope history [env: CONVCO_SCOPE_HISTORY_LIMIT=] [default: 500]
  -m, --message <MESSAGE>              The first message will be the description. Other -m options will be used as the body
  -f, --footers <token>(=|:)<value>    Specify extra footers to the message [aliases: --trailer]
      --breaking                       Introduces a breaking change
  -i, --interactive                    Interactive mode. Start the wizard if no type and description is given [env: CONVCO_INTERACTIVE=]
  -N, --intent-to-add <INTENT_TO_ADD>  Runs `git add -N <PATH>`. An entry for the path is placed in the index with no content. This is useful in combination with --patch [env: CONVCO_INTENT_TO_ADD=]
  -p, --patch                          Runs `git add -p`. Interactively choose hunks of patch between the index and the work tree [env: CONVCO_PATCH=]
  -h, --help                           Print help
```
