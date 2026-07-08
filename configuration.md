---
layout: page
title: configuration
permalink: /configuration/
---

Configuration is based on the [conventional changelog config spec][1].

YAML or JSON can be used to declare the configuration.
Configuration is loaded in this order:

1. Start with convco's internal defaults.
2. If `-c` or `--config` is provided, load that file.
3. Otherwise, load `.convco` from the working directory when it exists.
4. Otherwise, load `.versionrc` for compatibility with conventional-changelog.

If `host`, `owner` and `repository` are not supplied, convco derives them from the `origin` git remote.
They are not read from `package.json` because convco is build tool agnostic.

Additionally `scopeRegex`, `template`, `commitTemplate`, description length limits, message ignore patterns, and version bump policy can be specified.
Most configuration is used with `convco changelog`, but `scopeRegex`, `stripRegex`, `types`, `description`, `initialBumpVersion`, `treatMajorZeroAsStable`, and `ignoreMessagePattern` are also used by other commands.

## Configuration

{% raw %}
| config key                   | description                              | default value                              |
| ---------------------------- | ---------------------------------------- | -------------------------------------------|
| `header`                     | the header of the changelog              | `"# Changelog\n"`                          |
| `types`                      | show/hide/group commit types             | see [default configuration](#default-configuration)                              |
| `preMajor`                   | automatically set by `convco`            | `true` if version `<1.0.0` else `false`    |
| `commitUrlFormat`            | a URL to a specific commit hash          | `"{{host}}/{{owner}}/{{repository}}/commit/{{hash}}"`                            |
| `compareUrlFormat`           | a URL to compare two git shas            | `"{{host}}/{{owner}}/{{repository}}/compare/{{previousTag}}...{{currentTag}}"`   |
| `issueUrlFormat`             | a URL to the issue                       | `"{{host}}/{{owner}}/{{repository}}/issues/{{id}}"`                              |
| `userUrlFormat`              | a URL to the user's profile              | `"{{host}}/{{user}}"`                      |
| `releaseCommitMessageFormat` | not used                                 | `"chore(release): {{currentTag}}`          |
| `issuePrefixes`              | used to detect issues in the commit body | `[ "#" ]`                                  |
| `host`                       | the host to be used in `commitUrlFormat`, `compareUrlFormat`, `issueUrlFormat` | extracted from `git remote get-url origin` |
| `owner`                      | the repository owner                     | extracted from `git remote get-url origin` |
| `repository`                 | the repository url                       | extracted from `git remote get-url origin` |
| `template`                   | template directory path                  | empty, the build in [template][2] is used  |
| `commitTemplate`             | template file path for `convco commit`   | empty, the built-in commit template is used |
| `scopeRegex`                 | limit valid scopes                       | `"^[[:alnum:]]+(?:[-_/][[:alnum:]]+)*$"`   |
| `lineLength`                 | default changelog line length for templates that use word wrapping | `80` |
| `wrapDisabled`               | disable changelog word wrapping          | `false`                                    |
| `linkCompare`                | add compare links between versions       | `true`                                     |
| `linkReferences`             | link commit and issue references         | `true`                                     |
| `merges`                     | include merge commits                    | `false`                                    |
| `firstParent`                | follow only the first parent             | `false`                                    |
| `stripRegex`                 | strip matching content from commit messages before parsing | `""`       |
| `description.length.min`     | minimum description length for `convco commit` | `10`                                |
| `description.length.max`     | maximum description length for `convco commit` | empty                              |
| `initialBumpVersion`         | version to use for the first bump when no previous version is found | `0.1.0` |
| `treatMajorZeroAsStable`     | use stable SemVer bump mapping while the current version is `0.y.z` | `false` |
| `ignoreMessagePattern`       | regex patterns for commits that should be ignored by check/changelog/version parsing | `[]` |
{% endraw %}

### URL formats

The commit, compare, issue and user URL formats are handlebars templates.
They can use the derived or configured repository values and the values available for each commit, tag, issue, or user.

### Default configuration

{% raw %}

```yaml
# .versionrc
---
header: |
  # Changelog
types:
- type: feat
  increment: Minor
  section: Features
  hidden: false
- type: fix
  increment: Patch
  section: Fixes
  hidden: false
- type: build
  increment: None
  section: Other
  hidden: true
- type: chore
  increment: None
  section: Other
  hidden: true
- type: ci
  increment: None
  section: Other
  hidden: true
- type: docs
  increment: None
  section: Documentation
  hidden: true
- type: style
  increment: None
  section: Other
  hidden: true
- type: refactor
  increment: None
  section: Other
  hidden: true
- type: perf
  increment: None
  section: Other
  hidden: true
- type: test
  increment: None
  section: Other
  hidden: true
preMajor: false
commitUrlFormat: '{{@root.host}}/{{@root.owner}}/{{@root.repository}}/commit/{{hash}}'
compareUrlFormat: '{{@root.host}}/{{@root.owner}}/{{@root.repository}}/compare/{{previousTag}}...{{currentTag}}'
issueUrlFormat: '{{@root.host}}/{{@root.owner}}/{{@root.repository}}/issues/{{issue}}'
userUrlFormat: '{{host}}/{{user}}'
releaseCommitMessageFormat: 'chore(release): {{currentTag}}'
issuePrefixes:
- '#'
host: null
owner: null
repository: null
template: null
commitTemplate: null
scopeRegex: ^[[:alnum:]]+(?:[-_/][[:alnum:]]+)*$
lineLength: 80
wrapDisabled: false
linkCompare: true
linkReferences: true
merges: false
firstParent: false
stripRegex: ''
description:
  length:
    min: 10
    max: null
initialBumpVersion: 0.1.0
treatMajorZeroAsStable: false
ignoreMessagePattern: []
```

{% endraw %}

[1]: https://github.com/conventional-changelog/conventional-changelog-config-spec/blob/master/versions/2.1.0/README.md
[2]: https://github.com/convco/convco/tree/master/src/conventional/changelog
