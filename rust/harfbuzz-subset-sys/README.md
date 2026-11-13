# harfbuzz-subset-sys

Rust bindings to the HarfBuzz subsetter, built from this repository's own
source. `build.rs` compiles the `src/harfbuzz-subset.cc` amalgamation at the
repository root with the C++ compiler `cc` finds; it downloads nothing and
the package holds no copy of HarfBuzz. `src/lib.rs` declares the few C
functions and constants a font subsetter needs, by hand, and `src/safe.rs`
wraps them in a safe API, so callers need no `unsafe`. Native only.

## HarfBuzz release

This branch, `rust-subset-15.0.0`, starts at HarfBuzz tag `15.0.0` and changes
nothing outside `rust/`.

## Use

Depend on it by git URL and a full commit sha:

```toml
harfbuzz-subset-sys = { git = "https://github.com/storytold/harfbuzz.git", rev = "<sha>" }
```

The package reads `../../src`, so it builds only from a checkout of the whole
repository (a git dependency); it cannot be published to crates.io as is.

## Updating to a new HarfBuzz release

1. Create a branch `rust-subset-<version>` from the new tag and bring `rust/`
   over from the previous branch.
2. Read the release notes (`NEWS`) for subsetter changes, and check that the
   declarations in `src/lib.rs` still match `hb-subset.h`, `hb-blob.h`,
   `hb-face.h` and `hb-set.h`.
3. Update the HarfBuzz version in `Cargo.toml` and in this README.

## Licence

The Rust code in this directory is MIT. HarfBuzz is under its "Old MIT"
licence (`COPYING` at the repository root, SPDX `MIT-Modern-Variant`), which
covers the C++ source the build compiles.
