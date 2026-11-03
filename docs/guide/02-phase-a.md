# 2. Phase A - intent only

**About two minutes**

Call with **`businessIntent`** and **no** `damlCode`. This is the “orient before you write” step.

### Outcomes

| Outcome | Meaning |
|---------|---------|
| `suggest_patterns` | At least one **strong** hit from honest corpus retrieval. Draft from these. |
| `propose_search_query` | Verbatim recall is weak; server proposes a better search string. **Patterns stay empty.** You must **ACK or refuse**. |
| `abstain` | Intent is vague or recall is weak (and no proposal / you refused). Sharpen the ask. **Patterns stay empty.** |
| `over_quota` | Metered free tier spent (returned as a result, not a mysterious disconnect). |

### Why empty patterns on `abstain` / `propose_search_query` matter

If the tool returned “something kind of related” on a bad ask, an agent would dress uncertainty up as guidance. Abstention is the safety feature. Shared practice only works if weak sessions do not invent their own private corpus.

### Reformulation is opt-in

The server never rewrites search under the hood. If it has a better query, it returns `propose_search_query` with `proposedSearchQuery`. Re-call with:

```json
{
  "businessIntent": "<your original intent>",
  "searchQuery": "<proposedSearchQuery>",
  "acknowledgeSearchQuery": true
}
```

Refuse by calling again with only `businessIntent` (no ack). Then the tool stays on your original intent.

### What a good hit looks like

On `suggest_patterns`, each pattern should carry identity, `path`, and a snippet **or** a real description. Prefer `sourceUrl` (pinned upstream blob) when present. Incomplete hits are dropped. No half-delivery. Order matches corpus CE+authority ranking.

### Mental model (corpus_v2 + honest CE)

Today’s promoted bundle does **not** treat every “sharp” finance keyword the same. Calibrated expectations:

```text
  settlement batch + instructions/allocation  →  suggest_patterns (strong domain recall)
  IOU / DvP-style intents                     →  often abstain or propose_search_query
                                                 (finance chunks can outscore domain templates)
  weak but expandable ask                     →  propose_search_query (ACK or refuse)
  "make it work"                              →  abstain, [] patterns
```

Abstaining on a popular template name is not a bug when CE confidence is low — it is the product doing its job.

### Example `suggest_patterns` response

```json
{
  "outcome": "suggest_patterns",
  "businessIntent": "settlement batch with instructions and allocation",
  "reasoning": "…",
  "recommendedPatterns": [
    {
      "identity": "BatchSettlement…",
      "path": "…/Batch.daml",
      "score": 0.82,
      "sourceUrl": "https://github.com/…/blob/<ref>/…/Batch.daml"
    }
  ],
  "pairedOracles": [],
  "reformulated": false
}
```

Oracles (`pairedOracles`) are best-effort and only join on bundle `paired_template` metadata. Empty is fine — do not invent paired tests when the list is empty.

Frozen field rules live in the private repo: `docs/internal/TOOL_CONTRACT.md` (Phase A).

---

[← What it is](01-what-it-is.md) · [Phase B →](03-phase-b.md)
