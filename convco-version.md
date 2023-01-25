---
layout: page
title: convco-version
permalink: /version/
---

Version is a tool to print out the current or next version of the git repository.
The current version is calculated based on the version tags.
The next version is calculated based on conventional commits added since the current version:

* A commit of type `fix` will increase the `PATCH` version.
* A commit of type `feat` will increase the `MINOR` version.
* A commit with a breaking change increases the `MAJOR` version.

Major version zero (`0.y.z`) has the following rules:

* A commit of type `fix` will increase the `PATCH` version.
* A commit of type `feat` will increase the `PATCH` version.
* A commit with a breaking change increases the `MINOR` version.

## Examples

```sh
# print out the current version
convco version
# print out the next version
convco version --bump
```

Convco can be used to update the version of your project:

```sh
# rust
cargo release $(convco version --bump)
# java
mvn versions:set -DnewVersion=$(convco version --bump)
# javascript
npm version $(convco version --bump)
# git
git tag v$(convco version --bump)
```

## Usage

```plain
Show the current version

Usage: convco version [OPTIONS] [REV]

Arguments:
  [REV]  Revision to show the version for [default: HEAD]

Options:
  -C <PATH>              Run as if convco was started in <path> instead of the current working directory
  -p, --prefix <PREFIX>  Prefix used in front of the semantic version [default: v]
  -b, --bump             Get the next version
  -c, --config <CONFIG>
  -l, --label            Instead of printing out the bumped version, prints out one of: major, minor or patch
      --major            Bump to a major release version, regardless of the conventional commits
      --minor            Bump to a minor release version, regardless of the conventional commits
      --patch            Bump to a patch release version, regardless of the conventional commits
  -P, --paths <PATHS>    Only commits that update those <paths> will be taken into account. It is useful to support monorepos
  -h, --help             Print help
```
