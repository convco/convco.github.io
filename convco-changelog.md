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
```

## Usage

```plain
Writes out a changelog

Usage: convco changelog [OPTIONS] [REV]

Arguments:
  [REV]  [default: HEAD]

Options:
  -C <PATH>                          Run as if convco was started in <path> instead of the current working directory
  -p, --prefix <PREFIX>              Prefix used in front of the semantic version [default: v]
  -c, --config <CONFIG>
  -s, --skip-empty
  -m, --max-versions <MAX_VERSIONS>  Limits the number of version tags to add in the changelog
      --max-minors <MAX_MINORS>      Only print this number of minor versions
      --max-majors <MAX_MAJORS>      Only show this number of major versions
      --max-patches <MAX_PATCHES>    Only show this number of patch versions
  -n, --no-links                     Do not generate links. Overrides linkReferences and linkCompare in the config
      --merges                       Include conventional merge commits (commits with more than 1 parent) in the changelog
      --include-hidden-sections      Print hidden sections
  -P, --paths <PATHS>                Only commits that update those <paths> will be taken into account. It is useful to support monorepos
      --first-parent                 Follow only the first parent of merge commits. Commits from the merged branche(s) will be discarded
      --line-length <LINE_LENGTH>    Max line length before wrapping. This only makes sense if the template makes use of `{{#word-wrap}}` blocks
      --no-wrap                      Do not wrap lines. This only makes sense if the template makes use of `{{#word-wrap}}` blocks
  -u, --unreleased <UNRELEASED>      Change the title for the unreleased commits. If a semantic version is given, the title will be prefixed [default: Unreleased]
  -o, --output <OUTPUT>              Path to write the changelog to [default: -]
  -h, --help                         Print help
```
