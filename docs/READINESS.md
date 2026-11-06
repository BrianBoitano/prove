# Standalone CLI candidate readiness audit

Status: implementation in progress. No testing candidate or production-readiness claim is established yet. Passing counts are scoped evidence, not a substitute for the requirements below.

The user objective is a rigorously critiqued standalone Prove CLI ready for external research-session testing, followed by a testing handoff and documented feedback before public stable release. Research projects are ordinary external consumers. The goal remains active until the testing boundary is actually satisfied; it is not reduced to primitives or a fixture demo.

| Requirement | Evidence needed | Current state |
|---|---|---|
| General-purpose product | Generic primary commands/examples, no lab-specific core/import dependency, optional adapters only | Contract and generic example written; executable workflow incomplete |
| Easy independent installation | Versioned wheel/sdist, clean pip and isolated CLI installs outside source checkout, packaged schemas/examples/version/help | Metadata written; distribution not built or accepted |
| Canonical identities and trees | Independent vectors, invalid-encoding/depth/type tests, correct empty/odd trees and exact inclusion consumption | Task1 accepted:33 scoped tests plus independent review; later conformance corpus pending |
| Versioned contracts | Closed interoperable static schemas, typed/direct binding checks and malformed/unsupported behavior | Task2 accepted at0771498:204 contract tests plus33 primitives; independent re-review approved |
| Safe storage | No-follow ancestors/files, FIFO rejection, read-race tests, streamed hashing/copies and directory fsync | Task3 accepted:106 filesystem checks/343 cumulative, independent namespace/lock/close-failure probes approved; receipt persistence remains separate |
| Atomic freeze/seal/recovery | Durable immutable cores, no-clobber finalization, one writer, live/stale-lock handling and interruption tests | Not implemented |
| Generic artifact records | Case-preserving ordinary names, deterministic snapshots/tree, multiple attempts as distinct receipt dirs | Pure deterministic record engine accepted; snapshot persistence still pending |
| Optional trace consistency | Open-sample lifecycle, indices/retry binding, exact terminal outcome, coverage and known-subtotal budget bounds | Task4a accepted:391 cumulative tests and scoped independent probes; no claim of honest/complete actual execution |
| Honest scoring | Independent deterministic fixture recomputation, valid-hash/wrong-score rejection, other scorers labeled recorded-only | Contract written; not implemented |
| Full and inclusion verification | Distinct scope/policy/report fields, direct partial-proof consistency, no complete-history claim from a leaf | Contract written; not implemented |
| Offline behavior | Read-only verifier with no producer code, network lookup or implicit cache; process-level blocked-network test | Not implemented |
| Real OpenTimestamps path | Standard compatible proofs, bounded allowlisted requests/retries/caching, pending status, atomic upgrades and fresh submitted/completed anchors | Upstream library inspected; not implemented or submitted |
| Independent Bitcoin evidence | Safe configurable RPC export from a validated source, active-chain snapshot, header/hash/root/confirmation checks, cached-view limits | No existing node located; acquisition unresolved; synthetic/explorer data will not substitute for this evidence |
| Generic external integration | Another program's outputs sealed using the installed CLI alone, with a data-only interface and preserved original files | Not tested |
| Packaging and compatibility | Linux/Python3.11-3.13 checks, clean build/install, dependencies/licenses and no private infrastructure artifacts | Worker3.12 bootstrapped; matrix pending |
| Adversarial evaluation | Meaningful negative corpus, failure injection, independent whole-candidate review and documented fixes | Primitive and protocol critiques completed; whole candidate absent |
| Reproducible test handoff | Exact version/commit/asset hashes, install commands, independent test prompt, expected behaviors and structured feedback schema/template | Not produced |
| Testing pause | All necessary candidate gates justified; goal paused at user's requested external-test boundary with remaining limits visible | Not reached |

## Release boundary

The external session should install and use Prove like any independent evaluator. It must not rely on the lab's private services, edit Prove to make tests pass, or turn sealed research material into public artifacts without the research owner's existing authorization. Its feedback should separate installation/API friction, reproducible defects, mismatched claims and missing general capabilities.

No stable public release should be inferred from a development branch or an internal green suite. At candidate freeze, replace this live audit with concrete artifact/test/review references and retain any unsatisfied requirement explicitly. Do not describe an unresolved prerequisite as passed.

Scoped review evidence and concrete regression fixes are recorded in [the implementation review log](reviews/IMPLEMENTATION_REVIEW.md).
