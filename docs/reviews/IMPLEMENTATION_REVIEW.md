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

## Descriptor-safe filesystem and writer locks

Source: src/prove/filesystem.py. Evidence: tests/test_filesystem.py and independently owned tests/test_filesystem_adversarial.py. Main-session cumulative rerun:343 passed in1.81s in the capped Python3.12 worker, including106 filesystem cases. Scoped independent re-review returned APPROVED after direct fault-injection probes.

The first green implementation was rejected. Root-ancestor replacements could evade reads and destination publication; lock acquisition repeated that mistake at .prove. The corrected implementation retains directory identities and checks reachability from the opened receipt root. Enumeration now applies path and prefix-collision rules. File and ancestor-publication fsync failures cannot report success. Lock acquisition is nonblocking, recovery binds the complete bounded file through EOF, and live-writer/empty-lock races have process-level regressions.

Repeated review exposed a systemic descriptor-ownership defect: close-after-release EIO could trigger a second close, mask the original failure and leak a sibling descriptor. A fresh implementer replaced scattered cleanup with one ownership mechanism that relinquishes descriptors before closing, drains all remaining cleanup and preserves primary exceptions. Meaningful RED cases preceded the fix. Direct reviewer probes for rewalk, enumeration, failed opening, stream and acquisition failures returned operational code5 with zero descriptor leaks and zero repeated closes. Minimal context reentry guards preserve existing ownership.

This covers the declared opened-root boundary and detectable replacements before its checks. It is not a sandbox against an actor with unrestricted same-user filesystem control after the last check, nor a hardware power-loss proof. Application-level receipt staging, interrupted-finalization recovery and durability repair for hash-identical reuse are later persistence requirements.

## Receipt persistence and later consumers

Not implemented or accepted yet. Later review entries must record actual source/commit boundaries, reproduced findings, regression tests, main-session verification and remaining limits. Reviewer approval alone never establishes whole-candidate readiness.

## Pure normalized-record engine

Source: src/prove/records.py and the prepared event/inventory additions in schema.py. Evidence: tests/test_records.py, schema regressions and independently owned tests/test_records_adversarial.py. Main-session final cumulative run:391 passed in2.46s in the capped worker. Scoped independent review returned APPROVE after direct semantic probes.

Main rejected the initial minimal test set. Expanded tests cover honestly rehashed contradictory records, lifecycle/retry/reference errors, terminal and coverage rules, exact resources, overflow, usage unknowns and canonical JSONL limits. Main source review also exposed repeated manifest hashing during artifact generation; it is now computed once. Invalid attempt argument types produce structured errors, the one-shot validator keeps its prior error precedence, and stored-record verification reuses computed metadata rather than repeating the tree calculation.

Independent acceptance cases bind real canonical hashes and trees while contradicting a budget outcome: known token use above a ceiling must still reject completed when another call reports null usage. Explicit budget_exceeded retains a null full total and its known lower bound; below/equal-ceiling subtotals with unknown constrained usage remain unknown. Known call-count violations remain detectable with unknown token totals. Exact1MiB event and64MiB JSONL positive boundaries pass, with over-limit input rejected. Distinguishable code2/code4 cases exercise one-shot validation precedence.

This is pure supplied-record consistency. It does not authenticate execution/model identity, establish real-world call completeness, read artifacts, recompute scores, persist receipts, contact calendars or make an installed CLI available.
