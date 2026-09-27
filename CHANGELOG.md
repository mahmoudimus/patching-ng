# Changelog

All notable changes to patching-ng. Releases of the original plugin are on [gaasedelen/patching](https://github.com/gaasedelen/patching/releases).

## [0.5.0](https://github.com/mahmoudimus/patching-ng/releases/tag/v0.5.0) - 2026-09-25

### Changed

- The vendored Keystone libraries are now built by CI from [mahmoudimus/keystone](https://github.com/mahmoudimus/keystone) at `c8cf85e`: gaasedelen's fixes merged with current upstream Keystone (`c0b646f`). See the [`patching-v0.5.0`](https://github.com/mahmoudimus/keystone/releases/tag/patching-v0.5.0) release.
- The `third_party/keystone` submodule now pins `c8cf85e`, the exact commit the shipped libraries were built from.
- Lower runtime requirements:
  - macOS 11 or later, as a universal arm64 / x86_64 binary.
  - glibc 2.17 or later on Linux (built on manylinux2014).
  - No MSVC runtime dependency on Windows (static CRT).

### Added

- `tests/keystone/regression.py` compares two Keystone builds byte for byte on 18,048 x86_64, ARM64 and other-architecture inputs, and checks inputs that hang upstream Keystone.
- The *Keystone regression test* workflow runs it on Windows, Linux and macOS against any Keystone release.

## [0.4.0](https://github.com/mahmoudimus/patching-ng/releases/tag/v0.4.0) - 2026-09-25

### Changed

- The plugin is named `patching-ng`, and the repository has moved to [mahmoudimus/patching-ng](https://github.com/mahmoudimus/patching-ng).
- The Keystone source fork now includes upstream Keystone's build fixes.

### Removed

- `install.py`. Install with `hcli plugin install patching-ng`, or manually from the release zip.

## [0.3.0](https://github.com/mahmoudimus/patching-ng/releases/tag/v0.3.0) - 2026-09-24

The first patching-ng release.

### Added

- Support for IDA 9.2 and later (Qt6 / PySide6), keeping the PyQt5 fallback.
- Assemblers for PPC, MIPS, SPARC, SystemZ, Hexagon and EVM.
- Syntax fixups ported from KeyPatchX: MASM hex and `ptr` / `offset` stripping on x86, pre-UAL ARM syntax, and PPC register names.
- A comment after the assembly (`;` or `//`) in the patching dialog is set as the instruction's comment.
- Patched Mach-O binaries are re-signed ad hoc on macOS, and their quarantine attribute is removed.
- The patching dialog uses IDA's disassembly font.
- `ida-plugin.json` for HCLI and the IDA plugin manager.
- A single cross-platform `patching.zip` that includes Keystone for Windows, Linux and macOS.

### Fixed

- Crashes when opening, reusing and closing the patching dialog on IDA 9.1 and later.
- The patch target file browser on PySide6.
- The plugin core no longer loads twice per database, for example under `ida -A`.
- Applying patches to bytes that have no file offset.
- Clean and backup copies of the executable keep its file mode.
