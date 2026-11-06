# Prove implementation review evidence

This log records scoped implementation acceptance. It does not establish whole-candidate or production readiness; see [the live readiness audit](../READINESS.md).

## Canonical JSON and Merkle primitives

Accepted commit:10344f3. Source: src/prove/canonical.py, errors.py, merkle.py. Evidence: tests/test_canonical.py and tests/test_merkle.py.

The first implementation was not accepted on its initial green suite. Main review and expanded fixed vectors exposed empty-tree rejection, incorrect largest-power-of-two splitting for odd tree sizes and an unnormalized deep-parser RecursionError. Regression-first fixes corrected these. The independent reviewer then demonstrated otherwise-valid uppercase/whitespace hash encodings being accepted by bytes.fromhex. New tests modified valid proof/root strings, and strict lowercase encodings were enforced.

The main session read the actual final source and reran the scoped tests in an isolated capped worker:33 passed. The independent reviewer rechecked the corrections and returned APPROVED. This acceptance covers primitives and their declared bounds, not receipt persistence, real anchoring or installation.

## Versioned contracts and direct bindings

Accepted commit:0771498. Source: src/prove/schema.py and data/schemas/protocol-v1.json. Evidence: tests/test_schema.py and tests/fixtures/contracts/.

The worker first wrote meaningful failing contract tests. Additional RED cycles exposed regex end-anchor behavior accepting final newlines, a missing closed root in the packaged schema and an incorrectly nullable trace call count. The corrections use portable ECMA-compatible patterns and a closed local-reference schema.

Independent review demonstrated a valid Merkle path for an attempt_end event positioned before the end of its declared tree. The schema had accepted that visible contradiction; it now requires the final position. Review also caught malformed embedded format types being classified as unsupported instead of malformed; nested validation now applies the intended precedence.

Main review added direct checks implied by the generic contract: generated artifact count and UTF8 inventory rank, fixture aggregate count bounds and a non-null digest for declared weight-digest evidence. Regression inputs include actual valid Merkle proofs so rejection is attributable to the contract contradiction rather than a broken hash.

Final main-session cumulative rerun:237 tests passed in0.31s on Python3.12 in the capped worker (204 contracts,33 primitives). Independent scoped re-review returned APPROVED. These validators deliberately do not authenticate cache/model/issuer claims, read artifacts, verify whole-trace history, recompute arbitrary scores or validate Bitcoin header hashes; later consumers must supply those checks.

## Filesystem, persistence and later consumers

Task3 is active. No acceptance or readiness claim yet. Later review entries must record actual source/commit boundaries, reproduced findings, regression tests, main-session verification and remaining limits. Reviewer approval alone is never empirical evidence that a candidate works.
