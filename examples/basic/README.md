# Generic artifact receipt example

This example represents outputs from any evaluation program. It needs no model, API account, hosted service or research-project checkout. The fixed manifest nonce is a conformance fixture, not a recommendation for real registrations.

The first CLI candidate will freeze this manifest, snapshot outputs/, commit an ordered artifact tree and verify byte integrity offline. Reported metrics remain recorded-only; passing a receipt check does not establish that the metric is correct or that the evaluation ran honestly.

Real users will generate a fresh manifest with `prove init`, edit the relevant evidence and budgets, then use the same generic workflow for their own output directory. Bitcoin anchoring is an additional explicit step, and independently trusted chain evidence is required for offline anchored verification.
