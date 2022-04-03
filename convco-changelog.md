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
convco-changelog 0.3.1
Writes out a changelog

USAGE:
    convco changelog [OPTIONS] [rev]

FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information

OPTIONS:
    -c, --config <config>
    -C <path>                           Run as if convco was started in <path> instead of the current working directory
    -m, --max-versions <MAX_VERSIONS>   Limits the number of version tags to add in the changelog
    -p, --prefix <prefix>               Prefix used in front of the semantic version [default: v]
    -s, --skip-empty                    Skip empty releases

ARGS:
    <rev>     [default: HEAD]
```
