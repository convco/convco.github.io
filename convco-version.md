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

Use `--treat-major-zero-as-stable` with `--bump` to use the stable mapping while the current version is still `0.y.z`.
With this option, a commit of type `feat` increases the `MINOR` version and a commit with a breaking change increases the `MAJOR` version.

## Examples

```sh
# print out the current version
convco version
# print out the next version
convco version --bump
# print a prerelease version
convco version --bump --prerelease rc
# print the bump label instead of the version
convco version --bump --label
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

Use `--print-prefix` or its alias `--pp` when the output should include the configured tag prefix.
Use `--commit-sha` to print the commit that provided the current version instead of printing the semantic version.

Limit version calculation to commits that touched specific git pathspecs.
Pathspecs can be comma-delimited or passed repeatedly:

```sh
convco version --bump --paths 'packages/app,packages/lib'
convco version --bump --paths src --paths ':(exclude)src/generated'
```

Most options can also be supplied with environment variables.
For example, `CONVCO_PREFIX`, `CONVCO_PRINT_PREFIX`, `CONVCO_PATHS`, `CONVCO_IGNORE_PRERELEASES`, `CONVCO_INITIAL_BUMP_VERSION`, `CONVCO_TREAT_MAJOR_ZERO_AS_STABLE`, and the force bump variables map to their matching CLI options.

## Usage

```plain
Show the current version

Usage: convco version [OPTIONS] [REV]

Arguments:
  [REV]  Revision to show the version for [default: HEAD]

Options:
  -C <PATH>
          Run as if convco was started in <path> instead of the current working directory
  -p, --prefix <PREFIX>
          Prefix used in front of the semantic version [env: CONVCO_PREFIX=] [default: v]
  -c, --config <CONFIG>
          [env: CONVCO_CONFIG=]
      --print-prefix
          Print prefix in front of the semantic version [env: CONVCO_PRINT_PREFIX=] [aliases: --pp]
  -b, --bump
          Get the next version
  -l, --label
          Instead of printing out the bumped version, prints out one of: major, minor or patch
      --major
          Bump to a major release version, regardless of the conventional commits [env: CONVCO_FORCE_MAJOR_BUMP=]
      --minor
          Bump to a minor release version, regardless of the conventional commits [env: CONVCO_FORCE_MINOR_BUMP=]
      --patch
          Bump to a patch release version, regardless of the conventional commits [env: CONVCO_FORCE_PATCH_BUMP=]
      --prerelease <PRERELEASE>
          Suffix with a prerelease version. Requires --bump [default: ""]
  -P, --paths <PATHS>
          Only commits that update those <pathspecs> will be taken into account. It is useful to support monorepos. Pathspecs are evaluated relative to the root of the repository [env: CONVCO_PATHS=]
      --commit-sha
          Print the commit-sha of the version instead of the semantic version
      --ignore-prereleases
          Ignore pre-release versions when finding the last version [env: CONVCO_IGNORE_PRERELEASES=]
      --initial-bump-version <INITIAL_BUMP_VERSION>
          If no version is found use this version for the first bump [env: CONVCO_INITIAL_BUMP_VERSION=]
      --treat-major-zero-as-stable
          Treat major version zero as stable when calculating the next version. Requires --bump [env: CONVCO_TREAT_MAJOR_ZERO_AS_STABLE=]
  -h, --help
          Print help
```
