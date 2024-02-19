---
layout: home
---

![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/convco/convco/docker.yml)
[![Crates.io](https://img.shields.io/crates/v/convco)](https://crates.io/crates/convco)

A Conventional commit cli built with [Rust](https://www.rust-lang.org/).

`convco` gives tools to work with [Conventional Commits][1].

The tool is still in early development, but already useful.
It provides already the following commands:

- [`convco changelog`](changelog): Create a changelog file.
- [`convco check`](check): Checks if a range of commits is following the convention.
- [`convco commit`](commit): Helps to make conventional commits.
- [`convco version`](version): Finds out the current or next version.

## Installation

Convco is build as a single binary. It does not need an additional runtime.
[Shell completions](https://github.com/convco/convco/releases/latest) are available for bash, zsh, elvish, fish and powershell.

### Ubuntu (x64)

Download the latest [convco-deb.zip](https://github.com/convco/convco/releases/latest/download/convco-deb.zip) file from the github releases.

```sh
curl -OL https://github.com/convco/convco/releases/latest/download/convco-deb.zip
unzip convco-deb.zip
sudo dpkg -i convco*.deb
```

### Homebrew

For macOS or Linux

```sh
brew install convco
```

### Windows

Download the latest [convco-windows.zip](https://github.com/convco/convco/releases/latest/download/convco-windows.zip) zip file.
Extract `convco.exe` into a folder in your `PATH`.

### Docker

[![docker build status](https://img.shields.io/docker/cloud/build/convco/convco)](https://hub.docker.com/r/convco/convco)
[![docker pulls](https://img.shields.io/docker/pulls/convco/convco)](https://hub.docker.com/r/convco/convco)

Mount the current work directory in a volume and run convco in it.

```sh
docker run --rm -v "$PWD:/tmp" -w /tmp convco/convco --help
```

### From source

[![Crates.io](https://img.shields.io/crates/d/convco)](https://crates.io/crates/convco)

```sh
cargo install convco
```

[1]: https://www.conventionalcommits.org/
