---
layout: home
---

![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/convco/convco/docker.yml)
[![Crates.io](https://img.shields.io/crates/v/convco)](https://crates.io/crates/convco)

A Conventional commit cli built with [Rust](https://www.rust-lang.org/).

`convco` gives tools to work with [Conventional Commits][1].

It provides the following commands:

- [`convco changelog`](changelog): Create a changelog file.
- [`convco check`](check): Checks if a range of commits is following the convention.
- [`convco commit`](commit): Helps to make conventional commits.
- [`convco version`](version): Finds out the current or next version.
- `convco config`: Prints the effective configuration or the default configuration.
- `convco completions`: Generates tab completions for shells when convco is built with the `completions` feature.

## Installation

Convco is built as a single binary. It does not need an additional runtime.
Release archives are available from the latest [GitHub release](https://github.com/convco/convco/releases/latest).

### Linux

Download the archive for your target and put `convco` somewhere in your `PATH`.

```sh
target=x86_64-unknown-linux-musl
curl -OL "https://github.com/convco/convco/releases/latest/download/convco-${target}.tar.gz"
tar -xzf "convco-${target}.tar.gz" --strip-components=1 "convco-${target}/convco"
sudo install -m 755 convco /usr/local/bin/convco
```

### Homebrew

For macOS or Linux:

```sh
brew install convco
```

### Windows

Download the latest Windows archive from the [GitHub releases](https://github.com/convco/convco/releases/latest).
Extract `convco.exe` into a folder in your `PATH`.

### Docker

[![docker pulls](https://img.shields.io/docker/pulls/convco/convco)](https://hub.docker.com/r/convco/convco)

Mount the current work directory in a volume and run convco in it.

```sh
docker run --rm -v "$PWD:/tmp" -w /tmp convco/convco --help
```

The image is also available from the GitHub Container Registry:

```sh
docker run --rm -v "$PWD:/tmp" -w /tmp ghcr.io/convco/convco --help
```

### From source

[![Crates.io](https://img.shields.io/crates/d/convco)](https://crates.io/crates/convco)

```sh
cargo install convco
```

## GitHub Actions

Use `convco check` in pull requests to validate the commits in the PR range.

{% raw %}

```yaml
name: Pull request
on: [pull_request]

jobs:
  convco:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v6
        with:
          fetch-depth: 10
      - name: Validate commit messages
        shell: bash
        run: |
          set -euo pipefail
          target="x86_64-unknown-linux-musl"
          curl -sSfL "https://github.com/convco/convco/releases/latest/download/convco-${target}.tar.gz" \
            | tar -xz --strip-components=1 "convco-${target}/convco"
          chmod +x convco
          ./convco check ${{ github.event.pull_request.base.sha }}..${{ github.event.pull_request.head.sha }}
```

{% endraw %}

[1]: https://www.conventionalcommits.org/
