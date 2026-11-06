# Prove development checks

Prove is being built as a standalone CLI. The reviewed product architecture is in PLAN.md, the implementation tasks are in docs/IMPLEMENTATION_PLAN.md and the wire contract is in docs/PROTOCOL.md. No stable CLI release is available yet.

For contributors using an isolated development environment:

```bash
python -m venv .venv
. .venv/bin/activate
python -m pip install -e '.[dev]'
python -m pytest
python -m build
```

Do not run batch builds or tests in a resource-constrained shared editor environment. Use a separate bounded worker there. Test evidence must distinguish local integrity checks, synthetic timestamp fixtures, live calendar submissions and independently trusted chain evidence.

The generic example is examples/basic/. Protocol and verifier changes need adversarial vectors and independent review. Research projects are external consumers: product code and installation must not depend on them.
