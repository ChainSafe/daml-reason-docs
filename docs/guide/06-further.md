# 6. Where next

**About one minute**

If the guide clicked, you already have the mental model: one commons, two phases, abstain when unsure, compile on the client, hand off when the corpus is done helping.

Deeper material stays in the **private** repository under `docs/internal/` (not on this public site):

| Path | When you need it |
|------|------------------|
| `docs/internal/TOOL_CONTRACT.md` | Frozen outcomes and field musts |
| `docs/internal/DAML_REASON.md` | One-page capability brief |
| `docs/internal/DEVELOPING.md` | Auth, Postgres, sidecar, corpus bind |
| `docs/internal/DEMO.md` / `DEMO_CHAT.md` | Rehearse gates and the draft loop |
| `docs/internal/COMPARE.md` | Recall regression vs the Python sidecar |
| `docs/internal/PORT_PLAN.md` | Sprint and cutover status |
| `docs/internal/VALUE_NARRATIVE.md` | External and press framing |

### How we evaluate (v1)

Public CI already carries a **labeled** regression set on the promoted `corpus_v2` bundle with the cross-encoder path:

- Phase A tables (`//go:build corpus`) — vague abstains, sharp settlement suggests, honest IOU/DvP abstain-or-propose.
- Phase B fail-and-help — aligned drafts must not `fail`; mismatched domains `fail`; compile-failed attaches patterns when recall is strong.

That is the **v1 evaluation set**: outcome classes under honest retrieval, not a published confusion matrix. Deeper alignment research (labeled tasks, matrices) continues on the private eval-lab branch when needed — it is not a separate public issue for day-to-day product work.

### Still small?

Yes. One tool, two phases, a handful of outcomes, and a clear agent loop. If this guide ever needs more than about fifteen minutes, split “operators” from “agent authors” instead of bloating the ten-minute path.

### Thesis (again)

We do not generate Daml. We gate agents on a promoted corpus, and we abstain when unsure. That is how vibecoding sessions stop diverging and start inheriting the same corrected practice.

---

[← Try it](05-try-it.md) · [Back to start](index.md)
