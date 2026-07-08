---
layout: page
title: convco-changelog
permalink: /changelog/
---

Creates changelog based on the conventional commits.
It is possible to change some substitutions in the template, or even to define your own template.
See [configuration](../configuration) for all options.

## Custom template

The template language is [handlebars](https://handlebarsjs.com/).
There should be at least 1 file `template.hbs`.
All `*.hbs` files in the template directory will be loaded and are usable as [partials](https://handlebarsjs.com/guide/partials.html).

The default template can be found [here](https://github.com/convco/convco/tree/master/src/conventional/changelog).

## Examples

```sh
convco changelog > CHANGELOG.md
convco changelog --output CHANGELOG.md
convco changelog --max-versions 3
```

Limit changelog commits with git pathspecs:

```sh
convco changelog --paths 'packages/app,packages/lib'
convco changelog --paths src --paths ':(exclude)src/generated'
```

Use `--ignore-prereleases` to find the last stable version when generating release notes.
Use `--include-hidden-sections` to print sections that are hidden by configuration, and `--no-links` to disable generated compare, commit, and issue links.

Line wrapping can be controlled with `--line-length` or disabled with `--no-wrap` when the template uses `{{#word-wrap}}` blocks.
Most options can also be supplied with environment variables, such as `CONVCO_OUTPUT`, `CONVCO_MAX_VERSIONS`, `CONVCO_PATHS`, and `CONVCO_NO_LINKS`.

## Usage

```plain
Writes out a changelog

Usage: convco changelog [OPTIONS] [REV]

Arguments:
  [REV]  [env: CONVCO_REV=] [default: HEAD]

Options:
  -C <PATH>                          Run as if convco was started in <path> instead of the current working directory
  -p, --prefix <PREFIX>              Prefix used in front of the semantic version [env: CONVCO_PREFIX=] [default: v]
  -c, --config <CONFIG>              [env: CONVCO_CONFIG=]
  -s, --skip-empty                   [env: CONVCO_SKIP_EMPTY=]
  -m, --max-versions <MAX_VERSIONS>  Limits the number of version tags to add in the changelog [env: CONVCO_MAX_VERSIONS=]
      --max-minors <MAX_MINORS>      Only print this number of minor versions [env: CONVCO_MAX_MINORS=]
      --max-majors <MAX_MAJORS>      Only show this number of major versions [env: CONVCO_MAX_MAJORS=]
      --max-patches <MAX_PATCHES>    Only show this number of patch versions [env: CONVCO_MAX_PATCHES=]
      --ignore-prereleases           Ignore pre-release versions when finding the last version [env: CONVCO_IGNORE_PRERELEASES=]
  -n, --no-links                     Do not generate links. Overrides linkReferences and linkCompare in the config [env: CONVCO_NO_LINKS=]
      --merges                       Include conventional merge commits (commits with more than 1 parent) in the changelog [env: CONVCO_MERGES=]
      --include-hidden-sections      Print hidden sections [env: CONVCO_INCLUDE_HIDDEN_SECTIONS=]
  -P, --paths <PATHS>                Only commits that update those <pathspecs> will be taken into account. It is useful to support monorepos. Pathspecs are evaluated relative to the root of the repository [env: CONVCO_PATHS=]
      --first-parent                 Follow only the first parent of merge commits. Commits from the merged branche(s) will be discarded [env: CONVCO_FIRST_PARENT=]
      --line-length <LINE_LENGTH>    Max line length before wrapping. This only makes sense if the template makes use of `{{#word-wrap}}` blocks [env: CONVCO_LINE_LENGTH=]
      --no-wrap                      Do not wrap lines. This only makes sense if the template makes use of `{{#word-wrap}}` blocks [env: CONVCO_NO_WRAP=]
  -u, --unreleased <UNRELEASED>      Change the title for the unreleased commits. If a semantic version is given, the title will be prefixed [env: CONVCO_UNRELEASED=] [default: Unreleased]
  -o, --output <OUTPUT>              Path to write the changelog to [env: CONVCO_OUTPUT=] [default: -]
  -h, --help                         Print help
```
