# Prove plan review log

Started 2026-11-05. Maximum five adversarial rounds. Main session owns decisions and final acceptance. Reviewers provide evidence and findings, not implementation authority. No product code is written during this review.

## Round 0, main-session critique

The initial brief corrected timestamp overclaims but left the receipt format, verification policy, scientific analysis and recovery behavior underspecified. It also included a new runner that would compete with mature evaluation harnesses and increase adoption cost.

Revision 2 makes the product an evidence layer; defines independent chain trust, report scopes, canonical core boundaries, Merkle construction, explicit execution assertions, failure outcomes, atomic finalization and parser limits; separates offline core acceptance from the fresh real-anchor experiment; and adds scientific, usability and stop gates.

## Round 1, independent reviews

Both independent reviewers returned REVISE on the original brief. Findings and dispositions:

| Finding | Disposition in revision 3 |
|---|---|
| OTS cannot establish preregistration/execution chronology | Accepted: remove cryptographic launch verdict; keep plan anchoring and operator assertions separate |
| Offline trust store and chain view ambiguous | Accepted: explicit node-export cache schema, stable snapshot and verifier-controlled trust input |
| Add cumulative-work/checkpoint validator | Rejected for v0.1: a validated-node export is the explicit trust model; custom consensus validation is a different implementation |
| Artifact namespace and set binding ambiguous | Accepted: closed ASCII path profile, canonical inventory, byte sizes, roles and rejection of unlisted artifacts |
| Merkle completeness overclaim | Accepted: distinguish submitted-record consistency from real-world completeness; inclusion is a separate scope |
| Model identity evidence taxonomy missing | Accepted: mandatory evidence classes, none claiming executed-model attestation |
| JSON profile and immutable identities unspecified | Accepted: closed schemas, deterministic canonical cores, bounded integers, proof-independent receipt IDs and immutable corrections |
| Issuer signatures are mandatory | Rejected for v0.1: issuer identity explicitly unverified; signatures are useful optional later assurance but do not fix execution truth |
| Private tasks leak and repeated public tasks contaminate | Accepted: salted private holdouts, delayed reveal and public sentinel labeling |
| Scoring integrity confused with correctness | Accepted: built-in deterministic fixture recomputation only; arbitrary scorers remain recorded-only |
| Observatory statistics and evaluator controls vague | Accepted: frozen control target, explicit primary endpoints and simulated sequential/multiple-testing contract before live studies |
| Volume target mistaken for statistical evidence | Accepted: 100 runs remains operational only; power comes from the study design |
| Resource accounting needs separate observable fields | Accepted at research-design boundary; detailed study ledger freezes before G5 |
| Build another evaluation runner | Rejected: keep generic fixture only; Inspect is first actual harness adapter |
| Three adopters as release prerequisite | Accepted: external adoption is a project metric after release, not a package release blocker |
| Ten-user usability study before v0.1 | Deferred: two-user formative pilot first; larger study follows evidence of usefulness and recruitment |

## Round 2, revised-plan review

Both reviewers returned REVISE on revision 3. Neither required signatures, independent execution attestation, a new consensus verifier or live scientific studies for the first milestone.

| Remaining finding | Resolution in revision 4 |
|---|---|
| Attempt IDs not bound to declared attempts | Manifest lists permitted constrained IDs and coverage; result must match |
| Event schema too loose | G1 explicitly freezes closed event/score/resource schemas and byte-level vectors before writing the core |
| Score artifact linkage ambiguous | Explicit path/digest/length/profile/aggregate binding resolving to a fixed-role inventory entry |
| Verification read-time file races | Descriptor-relative no-follow reads, regular-file checks and metadata/hash validation; unsupported platforms fail closed |
| Inspect mapping completeness unclear | Preserve original log and classify every source record as mapped, preserved-unmapped or unsupported |
| Secret-inventory commitment/reveal not actually specified | Defer the feature explicitly; v0.1 uses explicit sample IDs and cannot claim secret-inventory verification |
| Integer limits ambiguous | Exact inclusive safe-integer bounds and boundary vectors |
| Reference verifier may share bugs | Separately authored reference code with no shared canonicalization, tree or scoring implementation |
| Imported logs might execute or fetch content | Only pinned exported Inspect JSON, parsed as data; no task/plugin/attachment resolution |
| Artifact completeness confused with root files | Unlisted-file rejection explicitly scoped to artifact directory; core/proof files have fixed roles |

## Round 3, final checks

The protocol reviewer returned APPROVED: its five remaining blockers were closed and the narrow v0.1 claims were consistent. The research/adoption reviewer returned APPROVED: numeric, independent-corpus, import-boundary and deferred-private-inventory fixes were sufficient at project-plan level.

A separate final read-only review used the configured Codex default, GPT-6.1 Sol at high effort, with a ten-minute ceiling and returned APPROVED. Its [full critique](FINAL_REVIEW.md) is retained. Four nonblocking suggestions were incorporated: qualify trust-cache rejection claims, allow explicit incomplete coverage for every non-completed outcome, freeze policy/exit tables inside G1, and prohibit parallel unsalted disclosures from defeating later private commitments.

## Main-session acceptance

The reviewed plan is accepted as a basis for G1 specification, subject to Chris's first-build scope approval. No remaining plan-level blocker requires another review round. Exact schemas/vectors are G1 work and must precede its implementation. Independent acquisition of a validated Bitcoin chain view remains a G2 prerequisite, not a solved infrastructure task. Chris selected public repository visibility and Apache-2.0 on 2026-11-05; the initially private repository will be published with that license after checks.

Verification in this phase checks document consistency, repository contents, local links, whitespace and remote commit equality. No implementation tests have been run because the repository contains design documents only. Reviewer approval is a design assessment, not proof of protocol correctness or scientific results.
