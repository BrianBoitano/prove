# Offline quickstart

The supported runtime target is Linux with Python 3.11 through 3.13. This is an unreleased candidate; see the readiness audit for observed gates. With a supported interpreter, create an isolated environment and install the reviewed wheel:

```sh
python3 -m venv .venv-prove
. .venv-prove/bin/activate
python -m pip install /absolute/path/to/triplepass_prove-0.1.0a1-py3-none-any.whl
prove --version
```

Alternatively install a reviewed source checkout with `python -m pip install /absolute/path/to/prove`. Installation may fetch dependencies. A fully offline installation needs a separately prepared wheelhouse containing Prove and all dependencies, then `python -m pip install --no-index --find-links /absolute/path/to/wheelhouse triplepass-prove==0.1.0a1`. No unpublished PyPI release is assumed.

Once installed, this workflow runs in a fresh directory unrelated to any repository. It uses no model, API key or private service. `python -m prove` can replace `prove` in every command.

```sh
mkdir my-receipt-demo
cd my-receipt-demo
prove --version
prove init --out manifest.json --name "Ordinary output demo"
```

`init` writes a fresh nonce and editable manifest. Review and edit its model, dataset, harness, attempts and budgets before freezing it. This demo keeps the explicit unspecified/self-declared values. `init` does not preregister anything or execute an evaluation.

```sh
prove pre-register manifest.json --receipt receipt
mkdir outputs
printf 'ordinary external output\n' > outputs/result.txt
prove seal receipt --artifacts outputs
prove inspect receipt
prove verify receipt --offline --policy integrity-only
```

`receipt` is created as a single final directory in its existing parent. Output parents must already exist. `seal` snapshots the external outputs without rewriting them. Reports contain `registration_id` and, after sealing, `receipt_id`. `inspect` is a bounded local presentation and explicitly performs no verification.

Verification checks the copied files under `receipt/artifacts`, not the original `outputs` directory. Editing the original outputs after sealing does not invalidate the receipt; editing its frozen copy does. The retained root `.prove/staging` files are producer recovery checkpoints. They are unnecessary in a read-only sharing copy. See [integration guidance](INTEGRATION.md) for disk usage, portable contents and retrospective sealing of existing results.

Integrity-only verification returns 0 here, checking frozen artifacts and records without timestamps. No score was selected, so scoring is `unavailable`. Explicit recorded-only scores remain `recorded_only`; their meaning or accuracy is not recomputed. Verification does not establish honest execution or model identity.

```sh
prove proof create receipt --index 0 --out inclusion.json --without-proofs
prove verify --inclusion inclusion.json --offline --policy integrity-only
```

The inclusion package is self-contained, including after the original receipt disappears. It proves only the selected record's membership in the ordered tree. It does not scan artifacts or verify the entire history or scoring. Keep outputs outside the receipt. Prove rejects destinations within the operated receipt, including aliases. Immutable output files never overwrite an existing file; choose a fresh filename for another package.

```sh
prove verify receipt --offline
```

This intentionally returns 3, insufficient evidence: default verification requires anchored evidence. No timestamp was requested. `--offline` makes the existing policy explicit; verification always stays offline. Under integrity-only, even an explicitly named chain cache is ignored without opening it.

Optional timestamping is a separate network action:

```sh
prove anchor receipt
prove upgrade receipt
prove verify receipt --chain-cache independently-selected-chain.json --offline
```

The last command requires an independently selected local `prove.chain.v1` cache with matching headers and at least six confirmations by default. `--min-confirmations N` selects a positive threshold. Prove never obtains that cache implicitly. Pending proofs, submission and an attestation's presence do not establish completed anchoring. Header time is not trusted execution time. Cache freshness and external provenance remain your responsibility.

`pre-register ... --anchor ots` and `seal ... --anchor ots` finish locally before timestamping. If that phase fails or is interrupted, reports retain completed local state and IDs with `anchor_action` failed/interrupted. Retry with `anchor`/`upgrade`; no reseal or original outputs are required. `recover-seal` is for an interrupted local checkpoint. `recover-lock --observed-sha256 SHA` requires the exact observed abandoned lock digest. Neither runs automatically.

Read static generic examples from the installed package without repository files:

```python
from importlib.resources import files

basic = files("prove").joinpath("data/examples/basic")
manifest_bytes = basic.joinpath("manifest.json").read_bytes()
metrics_bytes = basic.joinpath("outputs/metrics.json").read_bytes()
```

The static manifest has a fixed demonstration nonce. Use `prove init` for real registrations.
