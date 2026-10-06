# bitty-compat-lab

Independent compatibility validation suite for Bitty (W-105 relocation, bitty CTX-0931). Read [AGENTS](AGENTS.md) and [TODO](TODO.md).

- Suite: `crates/bitty-compat-lab` — headless, bounded compatibility lab
  (release-matrix suites, M1 golden suites, differential oracle, compare and
  report harnesses, collect/report/runner binaries). Corpora and oracle
  scenarios live under `tests/compat/`; the scenario authoring tool lives
  under `scripts/`. Vendored product-snapshot fixtures live under
  `fixtures/` (freshness enforced by the bitty-side thin gate).
- Tested production revision: the pinned immutable `bitty` commit recorded
  in `crates/bitty-compat-lab/Cargo.toml` (W-75 pin discipline: exact
  commit, never a branch or tag, never a path dependency). Pin bumps are
  owned, reviewed changes.
- Gates: `just check` runs the metadata gates plus `just rust-fmt`,
  `just rust-clippy`, and `just rust-test` (suite evidence against the pinned
  revision, roster floors intact). The bitty product change path keeps thin
  required invocations of this suite (Tier-1 M1/compat matrices) against the
  pinned suite revision.
- This repository is `publish = false` tooling with no shipped runtime
  authority; an independent repository is not an independent gate.

Prerequisite: W-75 / bitty-docs CTX-0265, Issue #404, and W-105 Core CTX-0931. Preserve required CI and pin the production revision under test.

CTX-0001 -> CTX-0002 -> CTX-0003 -> CTX-0004 maps to Issues #4 -> #3 -> #2 -> #1. CTX-0001 (bootstrap) is complete: metadata gates, independent review, first publication, redacted CarryCtx snapshot and branch protection are recorded. Suite migration landed in 6887d08 (#7) under CTX-0003; acceptance (including CTX-0004 independent verification) belongs to the owning tasks.
