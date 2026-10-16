# Research Consumer Contract Locks

Research App does not own the Knowledge Retrieval/Citation schemas. The only
editable source of truth is `knowbase-app/contracts/retrieval/`.

`knowbase-retrieval-provider-lock.json` pins the compatible major and SHA-256
of every provider schema consumed by Research. Contract CI must download or
check out the Knowledge provider artifact, set
`KNOWBASE_RETRIEVAL_CONTRACT_DIR`, and run the Research consumer tests.
Updating this lock without provider and consumer tests is not a valid contract
upgrade. Generated or copied schemas must not become a second source of truth.

## Knowbot manifest (knowmart)

`knowmart-knowbot-manifest-lock.json` pins the outer knowbot manifest that the
workbench summons from knowmart (SDD 0027 P4, service identity
`knowmart:summon`). The source of truth is
`knowmart-app/contracts/knowbot/v1/`. The backend test
`tests/test_knowbot_contract_lock.py` checks the lock against a sibling
`knowmart-app` checkout (or `KNOWMART_KNOWBOT_MANIFEST_SCHEMA_PATH`) and
validates the workbench's sample manifest against the provider schema. The
inner `pack` is the workbench's own expert-pack shape and is validated by the
backend (`app/domain/workbench/knowbots.py`).

## Knowbot test runs (knowlab)

`knowlab-test-run-lock.json` pins the `knowbot-test-run/v1` contract that the
workbench implements as a runtime (SDD 0027 §3.4, service identity
`investment:testrun`, routes under `/api/internal/v1/knowbot-runtime`). The
source of truth is `knowlab-app/contracts/knowbot-test-run/v1/`. The backend
test `tests/test_knowbot_test_run_lock.py` checks every pinned digest against a
sibling `knowlab-app` checkout and validates a sample request and the results
the workbench produces against the provider schemas.
