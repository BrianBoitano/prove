# Prove

Prove is a planned open source protocol and Python CLI for verifiable AI evaluation receipts, developed by [TriplePass Labs](https://github.com/TriplePassLabs). Created and maintained by [Christopher Ayers](https://github.com/BrianBoitano).

[Lab website](https://triplepasslabs.com) · [GitHub organization](https://github.com/TriplePassLabs) · [Founder profile](https://github.com/BrianBoitano)

It will bind an evaluation plan, recorded artifacts and reported results to commitments anchored with OpenTimestamps. Verification will distinguish artifact integrity from claims about execution, model identity, timing and scientific validity.

**Status: standalone CLI implementation in progress; no released Python package yet.** Commands in the plan are proposed interfaces until their implementation and installation checks pass.

Prove is independent of any particular benchmark, model, provider or research project. Its primary workflow uses generic manifests and output directories. Harness importers are optional conveniences; basic installation and verification must not require them.

- [Project plan](PLAN.md): scope, protocol decisions, milestones and release gates.
- [Threat model](docs/THREAT_MODEL.md): attacks, defenses and remaining trust.
- [Acceptance tests](docs/ACCEPTANCE.md): tests required before implementation claims.
- [Sources and alternatives](docs/SOURCES.md): primary references and reuse decisions.
- [Review log](docs/reviews/REVIEW_LOG.md): critiques and their disposition.

## License

Licensed under [Apache-2.0](LICENSE). Copyright 2026 Christopher Ayers.

## What a receipt means

A valid completed timestamp establishes that a commitment existed by a Bitcoin block. Artifact hashes reveal changes to committed bytes. Neither establishes that an evaluator ran honestly, used the claimed model, disclosed all attempts, or produced a scientifically sound result.

Prove will work alongside evaluation harnesses. It will not become a new model runner, leaderboard authority or custom blockchain verifier.

The Public Agent Drift Observatory and Colony Zero are planned users of the protocol. Their experiments and results remain separate from the protocol's cryptographic checks.
