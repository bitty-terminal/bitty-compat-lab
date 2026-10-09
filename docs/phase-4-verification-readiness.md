# Phase 4 readiness: integration security and migration parity

Priority: P1 | Area: architecture | Labels: chore,P1,area:architecture
| Milestone: v0.1.0 | RFC: W-75 | Task: CTX-0004

Phase 4 independently verifies integration security and migration
parity. Scope is this repository only. This note records the actual
state against the acceptance criteria, narrows the file scope, and
documents the blockers. It claims no Phase 4 completion and no
independent acceptance.

## Actual state found

- Suite migrated in `6887d08` (`#7`) out of the `bitty` workspace.
  The suite is headless and bounded: release-matrix suites, M1 golden
  suites, differential oracle, compare and report harnesses, plus
  collect, report, and runner binaries. Corpora live under
  `tests/compat`; the authoring tool lives under `scripts`.
- Tested production revision is pinned immutable: `bitty` at exact
  commit `9bc73207ab559d4d5de4ef283a4056dc8857de01` across all seven
  git dependencies in `crates/bitty-compat-lab/Cargo.toml` (W-75 pin
  discipline: exact commit, never a branch or tag, never a path
  dependency). Pin bumps are owned, reviewed changes here.
- `just check` passes on `main`: metadata gates plus `rust-fmt`,
  `rust-clippy` with `-D warnings`, and `rust-test` (suite evidence
  against the pinned revision, roster floors intact). All suite test
  targets report green (golden, oracle, report, vertical-slice gates,
  plus doctest ignored by design as harness documentation).
- Cross-repo prerequisite W-75 accepted (`bitty-docs` CTX-0265,
  Issue 404): validation-suite workspace ownership decided;
  independent validation repositories preserved with CI and evidence
  coverage.
- CarryCtx true state: CTX-0001 completed, CTX-0002 in progress,
  CTX-0003 planned, CTX-0004 planned, CTX-0005 completed. Local
  ordering is phases 1 through 2 through 3 through 4.

## Acceptance criteria versus state

Phase 4 requires all of: a different reviewer, real
platform and negative-path evidence, canonical documentation
synchronization, and no weakening of Core invariants.

- Different reviewer: pending. Prior closeout `#11` recorded
  NEEDS-FIX review (closeout diff verified but `Closes #1` while
  verification pending). No independent APPROVE for Phase 4 exists.
  This PR does not approve itself.
- Platform and negative-path evidence: suite green exists (oracle
  catches deliberate divergence, corpus green against the pinned
  build, bounded and deterministic, report rows mapped to live
  scenarios), but independent verification with a different reviewer
  has not landed. Acceptance belongs to the owning task.
- Canonical docs synchronization: pending with the owning task. This
  repository records the migrated pinned-revision role; the canonical
  corpus sync is not claimed here.
- No weakening of Core invariants: this repository is `publish = false`
  tooling with no shipped runtime authority. It pins the production
  revision and preserves required CI and evidence paths; scaffold
  success is not claimed as compatibility evidence. No Core weakening
  is introduced by this note.

## Phase ordering blocker

Local ordering phases 1 through 2 through 3 through 4 blocks Phase 4
until CTX-0002 (in progress) and CTX-0003 (planned) complete. Phase 4
cannot be accepted before its prerequisites. This note therefore
records readiness only.

## Narrow file scope

This change adds only this readiness note. No product code. No
pin bump. No fixture changes. No CI changes. Bootstrap authorizes
metadata only; implementation and independent acceptance remain
pending with the owning task.

## Verification on this head

- `just check` green (prettier, markdownlint, metadata, hygiene,
  portable-path gate, rust-fmt, rust-clippy, rust-test).
- English-only, no invented identifiers, no host paths.
- Independent review required. This PR does not merge itself, does
  not approve its own work, and does not close `#1`.

## Open points for the owning task

- Complete CTX-0002 and CTX-0003 in order before CTX-0004 acceptance.
- Independent verification by a different reviewer with platform and
  negative-path evidence.
- Canonical documentation synchronization.
- Confirmation that no Core invariant is weakened.
