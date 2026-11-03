# CI templates for **DAML application repos**

This directory is **distribution packaging** for teams that build Canton/DAML projects — **not** CI for `canton-mcp-go` itself.

| In this repo (`canton-mcp-go`) | In your DAML repo |
|--------------------------------|-------------------|
| Go MCP server, no `.daml` sources | `.daml` modules, PRs to `main` |
| Hosts `daml_reason` | **Calls** hosted MCP from GitHub Actions |
| Ships the **composite action** + copy-paste workflow | Copies [`daml-reason-phase-b.workflow.yml`](daml-reason-phase-b.workflow.yml) |

Do **not** expect a `pull_request` + `**.daml` workflow to run meaningfully here. Maintainers may use [`.github/workflows/action-smoke-daml-reason-phase-b.yml`](../../.github/workflows/action-smoke-daml-reason-phase-b.yml) (`workflow_dispatch` only) to smoke-test the action against a hosted MCP.

**Developer guide:** [the developer guide](https://chainsafe.github.io/daml-reason-docs/ci-daml-reason/) · Issue [#105](https://github.com/ChainSafe/canton-mcp-go/issues/105).
