# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

`litelensapp/litelens-apt` is a self-hosted APT repository, not application code. It's the
`reprepro`-managed data tree served over GitHub Pages that lets users run `apt install litelens`
on Ubuntu/Debian, covering three codenames: `noble` (24.04), `jammy` (22.04), `focal` (20.04) —
each its own distribution in `conf/distributions` because a single `.deb` can't declare a
`Depends:` correct across all three (different `libwebkit2gtk` package names per Ubuntu version).

`dists/` (signed `Release`/`InRelease`/`Packages`) and `pool/` (the `.deb` files) are the actual
served content and are tracked in git, since GitHub Pages serves this repo's committed tree
directly. `keys/litelens-keyring.gpg` is the public half of the repository's signing key; the
private key lives only as a GitHub Actions secret on `litelensapp/litelens`.

Publishing is driven by CI in the separate `litelensapp/litelens` repo, which builds the `.deb`s
and pushes updates here via `reprepro`. This repo has no build/test/lint pipeline of its own.
