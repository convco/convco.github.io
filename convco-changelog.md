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
convco-changelog 
Writes out a changelog

USAGE:
    convco changelog [OPTIONS] [REV]

ARGS:
    <REV>    [default: HEAD]

OPTIONS:
    -c, --config <CONFIG>
            

    -C <PATH>
            Run as if convco was started in <path> instead of the current working directory

        --first-parent
            Follow only the first parent of merge commits. Commits from the merged branche(s) will
            be discarded

    -h, --help
            Print help information

        --include-hidden-sections
            Print hidden sections

    -m, --max-versions <MAX_VERSIONS>
            Limits the number of version tags to add in the changelog

        --merges
            Include conventional merge commits (commits with more than 1 parent) in the changelog

    -n, --no-links
            Do not generate links. Overrides linkReferences and linkCompare in the config

    -p, --prefix <PREFIX>
            Prefix used in front of the semantic version [default: v]

    -P, --paths <PATHS>
            Only commits that update those <paths> will be taken into account. It is useful to
            support monorepos

    -s, --skip-empty
```
