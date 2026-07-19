# Vibra standard library

This repository is the canonical source distribution for Vibra's standard
library. Vibra projects consume an exact Git revision as an ordinary source
dependency and vendor it under `dep/std`.

```yaml
dependencies:
  std:
    git: https://github.com/nahharris/vibra-stdlib.git
    rev: <full-commit-id>
```

The Vibra compiler repository pins this repository as its `stdlib/` submodule.
Compiler and runtime releases bundle the same pinned source snapshot; executable
`.vapp` packages statically link the used implementation and retain the source
snapshot for verification and tooling.

## Validate

Using a compatible `vibra` executable:

```sh
vibra check .
vibra fmt --output yaml
vibra lint --deny-warnings
```

The end-to-end stdlib behavior suite currently runs from the compiler
repository with `cargo run -- test`. Changes to this repository must update the
matching `tests/stdlib-*.vibra` coverage there until the suite is migrated into
this repository.

## Collections

`src/collections.vibra` provides the canonical v1 array and string-key map
operations. Updates return copied values, lookup misses are optional, invalid
bounds and allocation limits are typed errors, and map order is deterministic.

## License

Licensed under either Apache-2.0 or MIT, at your option.

