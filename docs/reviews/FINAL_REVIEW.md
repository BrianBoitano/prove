No remaining blocker prevents beginning G1 specification after Chris approves the scope. The plan is sufficiently bounded for that step. This is a design opinion, not empirical test evidence or implementation authorization.

The missing exact schemas and vectors belong at the start of G1. Their absence does not justify another plan-review cycle.

Remaining blockers: none.

Nonblocking suggestions, ranked:

1. **Narrow T02’s promise about rejecting bad chain evidence.** The acceptance matrix says wrong block hashes, roots or heights cannot yield anchored success. That is defensible for mismatches against trusted evidence, but not for a coherently fabricated cache that the auditor explicitly trusts. The plan correctly acknowledges this limitation elsewhere.

   Minimal fix: qualify T02 as detecting inconsistent or mismatched evidence under the selected trust store. Add a G2 case demonstrating that self-consistent fabricated trust material may pass internal checks. The report must identify the supplied cache and leave independent acquisition as an auditor responsibility. Software cannot establish who supplied that cache.

2. **Align incomplete-coverage acceptance with every supported outcome.** `PLAN.md` permits missing sample terminals when incomplete coverage is declared. C06 describes missing terminals as failures, with an exception specifically for aborted coverage. Failed and budget-exceeded attempts need equally explicit treatment.

   Minimal fix inside G1: freeze a small outcome/coverage table. Specify which outcomes permit incomplete coverage, which terminal records remain mandatory, and how zero-event attempts work. Exercise failed and budget-exceeded cases alongside aborted ones.

3. **Freeze the policy-to-exit-code matrix before implementing verification.** The evidence dimensions are well separated, but their combinations still need operational meaning. For example, a fixture can have valid commitments and an incorrect score. Pending anchors can coexist with successful integrity-only verification. An aborted evaluation can have a valid receipt.

   Minimal fix inside G1: publish expected report fields and exit codes for those combinations, plus inclusion verification with unavailable artifacts and unsupported algorithms. Scope and selected policy must remain visible in successful output. A valid receipt must not become shorthand for a successful evaluation or correct score.

4. **Make salted-commitment protection apply to every public representation.** Salting a private task commitment provides little protection if the inventory also publishes an ordinary digest of the same guessable plaintext.

   Minimal fix when specifying disclosure profiles: trace every public digest of withheld material, including artifact inventory entries. Define which bytes are salted and revealed later. Include a synthetic low-entropy example showing that no parallel unsalted commitment defeats the intended protection. This need not expand G1 into a private-data platform.

What materially improved:

- The central guarantee is now credible: binding declared plans, preserved bytes and results to timestamp evidence. Honest execution, model identity, authorship and absence of hidden attempts remain assertions.
- The Bitcoin trust boundary is explicit. A verifier-trusted Bitcoin Core export supports this scope without requiring a new consensus implementation. Rejecting mandatory cumulative-work validation is reasonable.
- Unsigned receipts consistently report issuer identity as unverified. Mandatory signatures would expand scope without establishing execution truth.
- Full and inclusion verification are separated. Ordered records establish consistency of submitted history without claiming that omitted calls never happened.
- Scoring has a practical first-build boundary: deterministic fixture recomputation, with arbitrary receipt-provided code excluded from ordinary verification.
- Persistence, proof upgrades and immutable receipt identities now have concrete failure and recovery requirements.
- G1 is independent of Bitcoin availability. G2 requires a fresh real anchoring experiment and independently acquired chain evidence; mocks cannot satisfy it.
- Observatory and swarm work are gated research proposals. Statistical calibration, accounting, permissions and budget precede live claims.
- Adoption measures actual integration and comprehension. Three external adopters no longer block the release they would need to adopt, and the plan includes a credible simplify-or-reposition stop rule.

The remaining work is specification discipline within G1, followed by evidence from implementation. None of the deferred identity, execution-attestation or consensus subsystems is required by the guarantees currently stated.

VERDICT: APPROVED