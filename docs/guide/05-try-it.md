# 5. Try it locally

**About two minutes** once the stack is already up.

Full contributor setup lives in the private repo: `docs/internal/DEVELOPING.md`. Short path:

```bash
cd canton-mcp-go
make sidecar          # terminal A - cross-encoder for trust gates
make db-up && make token-key && make migrate
make server           # terminal B → http://127.0.0.1:7286/mcp
```

Issue an API key (email / log flow in DEVELOPING), then:

```bash
make cursor-env KEY=$KEY
```

Tip: the first Phase A call after sidecar start can be slow while the rerank model loads. Warm once before a demo.

### Minimal Phase A

```json
{
  "businessIntent": "IOU template with issuer owner and a Transfer choice"
}
```

Expect `suggest_patterns`, `propose_search_query` (ACK the proposed search), or `abstain`. On failure paths you should not see a pile of weak hits. Never `reformulated: true` without an ACK'd `searchQuery`.

### Minimal Phase B (you already have a draft)

```json
{
  "businessIntent": "IOU template with issuer owner and a Transfer choice",
  "damlCode": "module Main where\n…"
}
```

Expect `ready_to_compile`, `fail`, or `abstain`. Not `pass` until you pass a successful `compilationResult`.

### After `daml build` succeeds

```json
{
  "businessIntent": "…",
  "damlCode": "…",
  "compilationResult": { "succeeded": true, "exitCode": 0 }
}
```

Inspector / curl scripts: `docs/internal/DEMO.md`. In-chat script: `docs/internal/DEMO_CHAT.md`.

---

[← Agent loop](04-agent-loop.md) · [Where next →](06-further.md)
