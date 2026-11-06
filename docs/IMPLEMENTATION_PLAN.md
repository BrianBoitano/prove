# Standalone Prove CLI implementation plan

> For agentic workers: use subagent-driven-development with bounded owned files, test-first changes and independent review. This plan implements the reviewed PLAN.md and Chris's explicit standalone-product clarification.

Goal: an independently installable generic CLI candidate that ordinary external evaluators can use, with auditable receipt guarantees, a real OpenTimestamps path, safe offline verification and documented external-testing feedback.

Architecture: separate canonical data/Merkle primitives, versioned contract validation, safe local persistence, read-only verification, timestamp/network transport, optional imports and CLI presentation. No Colony/Ouroboros runtime dependency. Primary path uses generic artifact directories; optional normalized traces provide more detail. Harness adapters are data converters only.

Tech stack: Python 3.11-3.13/Linux first, setuptools packaging, RFC8785 library, upstream OpenTimestamps library, standard-library CLI and unittest/pytest. Wheel/source installs must work outside the repo. Keep verifiers free of model SDKs and live service calls.

## Global constraints

- Product name Prove; provisional distribution triplepass-prove; console prove plus python -m prove to avoid an unrelated executable on PATH.
- Unsigned identity and execution claims always unverified. Integrity, membership, timestamps and scoring are separate report fields.
- Full anchored verification needs externally supplied verifier-trusted validated-node cache. Explorer headers and test-generated evidence are never mislabeled independently validated.
- Frozen canonical cores and receipt IDs never change during proof upgrades. Atomic persistence, one writer, safe recovery and hostile filesystem handling are required.
- Builds and batch tests use the capped external worker, not this editor container. No GPU, model inference, lab experiment or family-service changes.
- Workers own only assigned modules/tests, do not revert others, and do not mutate services or secrets. Main session owns architecture, integration, external submissions and final acceptance.

### Task 1: Canonical data and ordered Merkle primitives

Files: src/prove/errors.py, src/prove/canonical.py, src/prove/merkle.py, tests/test_canonical.py, tests/test_merkle.py. Main owns packaging and other modules.

Ownership: create and edit only the named files under `/workspace/projects/prove-build/src/prove/` and `/workspace/projects/prove-build/tests/`. You are not alone in this worktree; preserve others' changes. Write a report to the assigned plan workspace. Use `bash .planning/worker.sh test tests/test_canonical.py tests/test_merkle.py` from the worktree to run scoped checks outside the editor. Do not start model/GPU services, access secrets, install dependencies locally or commit main-session files.

Interfaces: ProveError(message: str, code: int=2) exposes message/code. canonical.loads(data: bytes|str)->JSON value; dumps(value)->bytes; digest(value)->str SHA256 hex. Strict JSON, duplicate-key rejection, no floats, UTF8/surrogate checks, safe integer range, 64-depth bound, 8MiB JSON limit. Use rfc8785 for canonical output; metadata parsing is non-executable. merkle.root(leaves: Sequence[bytes])->str, proof(leaves,index)->list[str], verify(leaf,index,size,siblings,expected_root)->bool. RFC9162 construction and exact proof consumption; malformed proof returns false, invalid producer arguments raise ProveError.

- [ ] Write meaningful failing tests for unsupported/malformed canonical inputs and known independent Merkle vectors; record initial failure.
- [ ] Implement only these primitives and test boundary/odd-size/inclusion/extra-node behavior.
- [ ] Run scoped tests in the worker. Record actual commands/results and commit as Chris after review.

### Task 2: Versioned standalone contracts

Files owned: create/edit only `/workspace/projects/prove-build/src/prove/schema.py`, `/workspace/projects/prove-build/src/prove/data/schemas/protocol-v1.json`, `/workspace/projects/prove-build/tests/test_schema.py`, and `/workspace/projects/prove-build/tests/fixtures/contracts/`. You are not alone; preserve other workers' changes. Main owns the normative docs and packaging. Read docs/PROTOCOL.md in full; it resolves the prior review findings and is the source of exact wire fields. No lab-specific fields or dependencies.

Use packaged JSON Schema Draft202012 plus explicit deterministic cross-field checks; runtime jsonschema==4.26.0 is available in the capped worker. Schema is static, self-contained and closed, with only local #/$defs references, never producer-supplied or remotely resolved schemas. Export `validate_manifest(value)->dict`, `validate_result(value, manifest)->dict`, `validate_event(value, manifest, attempt_id)->dict`, `validate_inclusion(value)->dict`, `validate_chain(value)->dict`, `validate_artifact_path(path: str)->str`, `validate_inventory_paths(paths)->None`, and `default_manifest(name: str='Evaluation receipt')->dict`. Return the supplied validated dict, not silently coerced/mutated data. `default_manifest` generates a fresh random nonce and mirrors the generic example's explicit unknowns.

All validation first enforces canonical JSON value limits. ProveError uses code2 for malformed/contradictory data, code4 for genuinely unsupported format/profile/tree algorithms. Missing/incorrectly typed format is malformed, not unsupported. Implement object/event shape and direct core bindings here; whole-trace lifecycle, streaming filesystem checks, budget subtotal aggregation, OTS parsing and scoring recomputation belong to later modules. `validate_result` binds the manifest digest, declared attempt, profile, inventory, score path/digest/size/profile, and explicit outcome/reason rules, but cannot claim it has read artifacts or full records. `validate_event` checks allowed kind/profile, exact fields, bindings, IDs/refs and scalar types, not history it has not seen. `validate_inclusion` validates embedded cores/event/index/size/sibling encodings and IDs; cryptographic membership verification is a later consumer.

Data constraints: preserve NFC Unicode/uppercase/interior-space artifact names; reject collisions after casefold/NFC and forbidden components from the protocol. Artifact-profile resources are all null. Fixture scoring requires trace profile, a pinned dataset and nonempty sample IDs. Completed fixture result requires score; failed/aborted/budget-exceeded may omit it. Score/profile cannot disagree with the manifest. Counter types exclude bool. Known shape checks never pretend source/issuer/model identity is authenticated. Chain data uses decimal-string verificationprogress and canonical decimal height keys; verify header syntax and internal height/confirmation shape here, while exporter/proof logic independently checks actual header hashes and source trust.

- [ ] Write meaningful failing contract tests before implementation and record RED in the report.
- [ ] Freeze the static schema and minimal positive fixtures; use examples/basic/manifest.json as an independent positive input. Cover profile combinations, case-preserving paths/collisions, null vs missing, unknown fields, boundary types, substituted core/score/attempt bindings, malformed inclusion and cache shapes.
- [ ] Implement strict data validation with no filesystem/network/producer code execution beyond reading the package's fixed schema resource.
- [ ] Run `bash .planning/worker.sh test tests/test_schema.py` and cumulative primitives tests. Do not commit or edit sibling modules. Write full evidence to the assigned task report and return concise status.

### Task 3: Safe persistence and artifact receipts

Files: src/prove/filesystem.py, src/prove/store.py, src/prove/records.py, src/prove/fixture.py and owned tests. Uses the validated contract from Task2. Core uses generic artifacts by default; optional trace profile is explicit.

- [ ] Write failing tests for freeze/seal/repeat/conflict, immutable IDs, path attacks, read races, interrupted writes, trace lifecycle/budget lower bounds and outcome coverage.
- [ ] Implement descriptor-safe reads and snapshots, locking/recovery, atomic canonical cores and deterministic generated artifact records, preserving exact raw input bytes.
- [ ] Run scoped/cumulative tests and obtain independent correctness/security review.

### Task 4: Read-only verification and independent conformance

Files: src/prove/verify.py, src/prove/scoring.py, tools/reference_verify.py, conformance/ and owned tests.

- [ ] Write failing adversarial tests, including honestly hashed wrong scores, unsupported versions, mismatched bindings and partial/inclusion scope.
- [ ] Implement report/policy/exit-code matrix and built-in deterministic fixture scoring only; never execute receipt code or resolve receipt URLs.
- [ ] Independently author a verifier sharing no production canonicalization/tree/scoring functions and check a fixed corpus.
- [ ] Verify process-level network isolation and realistic size limits in the worker; map evidence to docs/ACCEPTANCE.md.

### Task 5: Upstream OpenTimestamps and trusted chain evidence

Files: src/prove/anchors.py, src/prove/evidence.py, local integration evidence and owned tests.

- [ ] Write offline known-proof, malformed-proof, bounded-parser, retry and interrupted-upgrade tests before implementation.
- [ ] Implement bounded allowlisted timestamp submission/upgrades and canonical proof-independent state.
- [ ] Implement local Bitcoin Core RPC export with credentials from config/cookie, stable active-chain snapshot and explicit provenance. No deployment of a new node in this task.
- [ ] Submit a fresh generic manifest and result to free calendars, preserve pending work, and later check completed anchors with independent evidence if available. Document any unavailable prerequisite without substituting mocks.

### Task 6: Standalone CLI, distribution and generic integrations

Files: src/prove/cli.py, src/prove/__main__.py, optional adapter module, pyproject.toml, README.md, docs/QUICKSTART.md, docs/INTEGRATION.md, docs/TESTING_HANDOFF.md and feedback schema/template.

- [ ] Exercise failing subprocess tests for generic init/pre-register/seal/inspect/verify/proof/upgrade/evidence commands and policy exit codes.
- [ ] Ship generic artifact ingestion first. Add data-only optional Inspect JSON import only after core is useful without it. Research-project usage belongs in external handoff docs, not core behavior.
- [ ] Build wheel/sdist in worker, install each into clean isolated environments, complete the domain-neutral quickstart with networking disabled, and verify packaged examples/vectors and dependency/license notices.
- [ ] Run full acceptance audit and a frontier independent adversarial review. Fix material issues and rerun affected checks. Do not let reviewer approval replace direct testing.
- [ ] Produce exact candidate version/commit/artifact hashes, testing prompt and machine-readable feedback template. The external session must document commands, environment, reproduced bugs and scientific-claim limits. Pause at the user-requested testing boundary only after the actual candidate and audit justify it.

## Progress ledger

The plan-scoped SDD ledger is the durable recovery source. Each task entry records actual files, test evidence, review findings/dispositions and commits. A failed or missing external prerequisite remains explicit in the release-readiness audit.
