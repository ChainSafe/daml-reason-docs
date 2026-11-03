# CI: daml_reason Phase B (hosted MCP)

**~5 minutes to wire a DAML application repo**

## Who this is for (read first)

| Repo type | Use this guide? |
|-----------|-----------------|
| **Your DAML / Canton project** (`.daml` in PRs) | **Yes** — copy the workflow, set secrets, call hosted MCP |
| **`canton-mcp-go` (this repo)** | **No** — we ship the server and the **action template**; we do not lint our own Go tree with `daml_reason` |

Artifacts live in the private repo so ChainSafe teams can pin `ChainSafe/canton-mcp-go/.github/actions/...` and copy the [CI templates](https://github.com/ChainSafe/daml-reason-docs/tree/main/docs/ci). That is **packaging for downstream repos**, not an admission that the MCP server repo should run on `**.daml` paths.

Call the **hosted** `daml_reason` tool over **MCP streaming HTTP** (`POST /mcp`, `tools/call`) when pull requests change `**.daml`. Semantic gate only — not `daml build` in GitHub Actions.

Tracking issue: [#105](https://github.com/ChainSafe/canton-mcp-go/issues/105).

## What CI does / does not do

| Does | Does not |
|------|----------|
| Phase B with `businessIntent` + `damlCode` | Run Daml SDK / `daml build` |
| Fail on outcome **`fail`** (configurable) | Assert outcome **`pass`** (needs `compilationResult`) |
| Print `alignmentScore`, `reasoning`, outcome | Replace local compile workflow |

Developers compile **locally**; CI states loudly that **`pass`** is not verified in CI for v1.

## Secrets (repository)

| Secret | Example |
|--------|---------|
| `DAML_REASON_MCP_URL` | `https://your-host` or `https://your-host/mcp` |
| `DAML_REASON_API_KEY` | Service account API key (`Authorization: Bearer`) |

Issue keys per [DEVELOPING.md](https://github.com/ChainSafe/canton-mcp-go/blob/main/docs/internal/DEVELOPING.md) (Connecting to /mcp). Use an internal / unlimited account for CI where possible.

## Business intent convention

Pick one per repo (document in PR template):

1. **`.daml-reason/intent.md`** in the repo (default in the sample workflow), or  
2. **PR title** fallback, or  
3. A labeled section in the PR body (custom step).

## Add the workflow

Copy [`daml-reason-phase-b.workflow.yml`](https://github.com/ChainSafe/daml-reason-docs/blob/main/docs/ci/daml-reason-phase-b.workflow.yml) to your DAML repo as `.github/workflows/daml-reason.yml`.

Pin the action ref to a release tag once available; `@main` tracks this repo.

## Composite action (same repo)

Path: [`ChainSafe/canton-mcp-go/.github/actions/daml-reason-phase-b`](https://github.com/ChainSafe/canton-mcp-go/tree/main/.github/actions/daml-reason-phase-b)

Inputs: `mcp-url`, `api-key`, `business-intent`, `daml-code`, optional `fail-on-outcomes` (default `fail`).

## Outcomes (v1 policy)

| Outcome | Default CI |
|---------|------------|
| `fail` | **Fail** job |
| `ready_to_compile` | Pass (semantic OK — compile locally) |
| `abstain` | Pass (weak recall / sharpen intent) |
| `over_quota` | Fail (fix billing / key) |

## Manual test (curl)

See [DEVELOPING.md — Connecting to /mcp](https://github.com/ChainSafe/canton-mcp-go/blob/main/docs/internal/DEVELOPING.md). Phase B adds `"damlCode": "..."` to `arguments`.

## v2 (optional)

Repos that already run **`daml build`** in CI can call MCP again with `compilationResult` for a true **`pass`** — separate job, not required for the semantic linter.
