---
layout: page
title: convco-check
permalink: /check/
---

Check all commits or range for errors against the convention.
It returns a non-zero exit code when any checked commit is not conventional.

## Examples

```sh
convco check
convco check origin/main..HEAD
git log -1 --format=%B | convco check --from-stdin
git log -1 --format=%B | convco check --from-stdin --strip
```

Output:

```plain
FAIL   123ab45   first line doesn't match `<type>[optional scope]: <description>`   lorem ipsum

1/13 failed
```

This could be used in a git pre-push or pre-receive hook to enforce conventional commits.

```sh
#!/usr/bin/env sh
# put this file in: .git/hooks/pre-push
z40=0000000000000000000000000000000000000000
while read _ local_sha _ remote_sha; do
  if [ "$local_sha" != $z40 ]; then
    if [ "$remote_sha" = $z40 ]; then
      # New branch, examine all commits
      range="$local_sha"
    else
      # Update to existing branch, examine new commits
      range="$remote_sha..$local_sha"
    fi

    # Check for WIP commit
    if ! convco check "$range"; then
      exit 1
    fi
  fi
done
```

```sh
#!/usr/bin/env sh
# put this file in: .git/hooks/pre-receive
z40=0000000000000000000000000000000000000000
while read old_sha new_sha _; do
  if [ "$new_sha" != $z40 ]; then
    if [ "$old_sha" = $z40 ]; then
      # New branch, examine all commits
      range="$new_sha"
    else
      # Update to existing branch, examine new commits
      range="$old_sha..$new_sha"
    fi

    # Check for WIP commit
    if ! convco check "$range"; then
      exit 1
    fi
  fi
done
```

Use `--ignore-message-pattern` to skip commits whose messages match a regex pattern.
This can also be configured with `CONVCO_IGNORE_MESSAGE_PATTERN`.

## Usage

```plain
Verifies if all commits are conventional

Usage: convco check [OPTIONS] [REV]

Arguments:
  [REV]  Start of the revwalk, can also be a commit range. Can be in the form `<commit>..<commit>` [env: CONVCO_REV=]

Options:
  -C <PATH>
          Run as if convco was started in <path> instead of the current working directory
  -n, --max-count <NUMBER>
          Limit the number of commits to check [env: CONVCO_MAX_COUNT=]
  -c, --config <CONFIG>
          [env: CONVCO_CONFIG=]
      --merges
          Include conventional merge commits (commits with more than 1 parent) in the changelog [env: CONVCO_MERGES=]
      --first-parent
          Follow only the first parent [env: CONVCO_FIRST_PARENT=]
      --ignore-reverts
          Ignore commits created by `git revert` commands [env: CONVCO_IGNORE_REVERTS=]
      --ignore-message-pattern <IGNORE_MESSAGE_PATTERN>
          Ignore commits whose message matches the given regex pattern [env: CONVCO_IGNORE_MESSAGE_PATTERN=]
      --from-stdin
          Read a single commit message from stdin
      --strip
          String comments and whitespace from commit message This is similar to `git commit --cleanup=strip`
  -h, --help
          Print help
```
