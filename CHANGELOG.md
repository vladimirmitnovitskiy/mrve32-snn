# Changelog

All notable changes to this project are documented in this file. The format
is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and the
project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html)
(before 1.0, a minor version bump may contain breaking changes).

The Rust crate and the Python package `mrve32-snn` share version numbers.
Up to 0.1.1 the module lived in the
[MRVE32](https://github.com/vladimirmitnovitskiy/MRVE32) repository
(`modules/snn`) and was versioned together with the emulator; from 0.2.0 it
has its own repository and versions.

To release: rename `[Unreleased]` to `[X.Y.Z] - YYYY-MM-DD`, set the same
version in `Cargo.toml`, push a `vX.Y.Z` tag (PyPI, see
`.github/workflows/release.yml`) and run `cargo publish` (crates.io).

## [Unreleased]

## [0.2.0] - 2026-11-13

### Added

- `SYN_OPS` register (`0x024`): synaptic accumulations in the last step
  (`IN_SPIKES × N_OUT`), the basis of an energy-per-inference estimate;
  `SnnDriver.syn_ops` and `REG_SYN_OPS` in Python.

### Changed

- Moved out of the MRVE32 repository into its own. The crate depends on
  `mrve32` from crates.io.

## [0.1.1] - 2026-11-03

### Changed

- The README documents the Python API (it is the PyPI description).

## [0.1.0] - 2026-11-02

First public release.

### Added

- SNN layer accelerator device (behavioural model, spec v0 draft): LIF/IF
  neurons, `i16` saturating potentials, `i8` weights, reset by subtraction,
  one layer per `START`, local SRAM, an analytical cycle model and a
  completion interrupt; the computation behind a swappable `SnnBackend`.
- Python package `mrve32_snn` (abi3 wheels for CPython >= 3.10):
  `SnnAccelerator`, the host-side `SnnDriver`, and the NumPy reference model
  `reference_step`.
