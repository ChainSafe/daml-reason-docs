# Daml Reason - developer guide

**About ten minutes.** Use the left nav, or walk the links below in order.

| | |
|--|--|
| **Tool** | `daml_reason` (MCP) |
| **Docs** | [daml-reason-docs](https://github.com/ChainSafe/daml-reason-docs) |
| **For** | Anyone wiring an agent or CI job to this tool |

## Why this exists (in one breath)

Today, every vibecoding session tends to invent its own private reading of Canton: whatever the model could synthesize from whatever docs and snippets happened to land in context. Ten developers can meet the same subtlety in DAML authorization and leave with ten “close enough” answers. Nothing shared gets corrected once.

Daml Reason flips that. A **promoted corpus** holds a curated, fixable interpretation of how Canton and DAML actually look in practice. The tool searches and **gates** against that commons. When the corpus is wrong or thin, you improve the corpus once; every later session inherits the fix. That is why this is infrastructure for a developer community, not only “RAG for faster lookup.”

The rest of this guide stays practical: what the tool returns, how to call it, and when to stop and hand off to a human.

## Ten-minute path

1. [What it is](01-what-it-is.md) - one tool, two phases, who writes vs who gates  
2. [Phase A](02-phase-a.md) - sharp intent suggests; vague intent abstains  
3. [Phase B](03-phase-b.md) - fail, ready_to_compile, pass  
4. [Agent draft loop](04-agent-loop.md) - iterate until handoff  
5. [Try it locally](05-try-it.md) - server and a first call  
6. [Where next](06-further.md) - deeper private-repo docs  
7. [CI semantic gate](ci-daml-reason.md) - GitHub Actions via hosted MCP  

## One sentence

We do not generate Daml. We gate agents on a promoted corpus, and we abstain when unsure.

---

**Next:** [What it is →](01-what-it-is.md)
