# Standalone CLI candidate readiness audit

Status: implementation in progress. No testing candidate or production-readiness claim is established yet. Passing counts are scoped evidence, not a substitute for the requirements below.

The user objective is a rigorously critiqued standalone Prove CLI ready for external research-session testing, followed by a testing handoff and documented feedback before public stable release. Research projects are ordinary external consumers. The goal remains active until the testing boundary is actually satisfied; it is not reduced to primitives or a fixture demo.

| Requirement | Evidence needed | Current state |
|---|---|---|
| General-purpose product | Generic primary commands/examples, no lab-specific core/import dependency, optional adapters only | Contract and generic example written; executable workflow incomplete |
| Easy independent installation | Versioned wheel/sdist, clean pip and isolated CLI installs outside source checkout, packaged schemas/examples/version/help | Metadata written; distribution not built or accepted |
| Canonical identities and trees | Independent vectors, invalid-encoding/depth/type tests, correct empty/odd trees and exact inclusion consumption | Task1 and independent Task5b accepted: four canonical vectors, eight roots/all35 paths,103 fixed cases,94 production comparisons |
| Versioned contracts | Closed interoperable static schemas, typed/direct binding checks and malformed/unsupported behavior | Task2 accepted at0771498:204 contract tests plus33 primitives; independent re-review approved |
| Safe storage | No-follow ancestors/files, FIFO rejection, read-race tests, streamed hashing/copies and directory fsync | Task3 accepted:106 filesystem checks/343 cumulative, independent namespace/lock/close-failure probes approved; receipt persistence remains separate |
| Atomic freeze/seal/recovery | Durable immutable cores, no-clobber finalization, one writer, live/stale-lock handling and interruption tests | Task4b accepted:475 passed plus actual bind-alias case separately; process-crash/source-independent recovery tested; no anchoring claim |
| Generic artifact records | Case-preserving ordinary names, deterministic snapshots/tree, multiple attempts as distinct receipt dirs | Record engine and generic immutable snapshot APIs accepted, including exact1024-byte wire paths; CLI workflow pending |
| Optional trace consistency | Open-sample lifecycle, indices/retry binding, exact terminal outcome, coverage and known-subtotal budget bounds | Task4a accepted:391 cumulative tests and scoped independent probes; no claim of honest/complete actual execution |
| Honest scoring | Independent deterministic fixture recomputation, valid-hash/wrong-score rejection, other scorers labeled recorded-only | Task4c and independent Task5b accepted, including correct-hash false math, opaque metric17/3, null scores and duplicate pinned-dataset copies |
| Full and inclusion verification | Distinct scope/policy/report fields, direct partial-proof consistency, no complete-history claim from a leaf | Task5a and materialized-wire Task5b accepted; final main142 affected conformance checks passed, scoped re-review approved |
| Offline behavior | Read-only verifier with no producer code, network lookup or implicit cache; process-level blocked-network test | Read-only consumer accepted, no producer/online imports and local-state/write traps pass; installed process-level acceptance remains pending |
| Real OpenTimestamps path | Standard compatible proofs, bounded allowlisted requests/retries/caching, pending status, atomic upgrades and fresh submitted/completed anchors | Parser/transport/durable upgrades accepted. Actual generic manifest and result each received four pending calendar proofs; fresh completed anchors remain pending |
| Independent Bitcoin evidence | Safe configurable RPC export from a validated source, active-chain snapshot, header/hash/root/confirmation checks, cached-view limits | Task6c exporter accepted: main794 cumulative passes/1 prerequisite skip, independent scoped review. Actual validated-node acquisition/export unresolved; synthetic/explorer data will not substitute |
| Generic external integration | Another program's outputs sealed using the installed CLI alone, with a data-only interface and preserved original files | Not tested |
| Packaging and compatibility | Linux/Python3.11-3.13 checks, clean build/install, dependencies/licenses and no private infrastructure artifacts | Worker3.12 bootstrapped; matrix pending |
| Adversarial evaluation | Meaningful negative corpus, failure injection, independent whole-candidate review and documented fixes | Scoped critiques/fixes through Task5b/6d accepted. Main full1006 passes before final reference-order repair; final142 affected checks pass. Whole-candidate review remains pending |
| Reproducible test handoff | Exact version/commit/asset hashes, install commands, independent test prompt, expected behaviors and structured feedback schema/template | Not produced |
| Testing pause | All necessary candidate gates justified; goal paused at user's requested external-test boundary with remaining limits visible | Not reached |

## Release boundary

The external session should install and use Prove like any independent evaluator. It must not rely on the lab's private services, edit Prove to make tests pass, or turn sealed research material into public artifacts without the research owner's existing authorization. Its feedback should separate installation/API friction, reproducible defects, mismatched claims and missing general capabilities.

No stable public release should be inferred from a development branch or an internal green suite. At candidate freeze, replace this live audit with concrete artifact/test/review references and retain any unsatisfied requirement explicitly. Do not describe an unresolved prerequisite as passed.

Scoped review evidence and concrete regression fixes are recorded in [the implementation review log](reviews/IMPLEMENTATION_REVIEW.md).
