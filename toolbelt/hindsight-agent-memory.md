# Hindsight — Persistent Agent Memory

**Status:** ADDED TO TOOLBELT / APPROVED FOR CONTROLLED EVALUATION; NOT DEPLOYED
**Upstream:** https://github.com/vectorize-io/hindsight
**License:** MIT (verify upstream license and dependency obligations before production)
**Scope:** STS engineering agents, design framework and project memory — not client-facing production features by default.

## Why
Hindsight provides persistent, structured agent memory with three operations:
- **retain:** extract and store selected facts, decisions, experiences, and corrections.
- **recall:** retrieve relevant memories at task/session startup or on demand.
- **reflect:** synthesize accumulated experience into observations; treat reflections as hypotheses until validated.

Git remains the canonical source for code, documented standards, approved decisions and audit history. Hindsight is a **retrieval and learning layer**, not an authority that can supersede the repository, CI, owner instructions, or security policies.

## Recommended implementation
1. Pilot with Claude Code on a **non-sensitive STS lab repository**.
2. Evaluate upstream's coding-agent integration (documented command: `npx @vectorize-io/hindsight-coding-agents install claude-code`); review installer, hooks, permissions, storage, and dependencies **before executing**. Prefer pinned versions.
3. Use one isolated memory bank per repository, plus a separate curated **STS-global** bank for explicitly approved reusable principles.
4. On session start, recall applicable architecture, decisions, failure patterns and active work. Before committing a significant decision, read the authoritative file and confirm memory currency.
5. Retain concise, high-value summaries: user-approved rules, accepted/rejected designs, root causes, verified remediations and test outcomes. Attach source repository, file/commit or issue, timestamp, project, and verification status where supported.
6. Reflect periodically for recurring defects, repeated tool friction and process improvements; route suggested changes through owner approval, PR and testing before promoting them to governance.
7. Evaluate memory quality against a small test set: correct project recall, no cross-project leakage, stale-decision handling, correction retention, latency and operating cost.
8. Only after successful evaluation consider a shared service/MCP integration so Claude and other compatible agents can access the **same authorized bank**. ChatGPT access is **not automatic**.

## Rules / safeguards
- **No cross-client memory mixing.** STS, The Fun Frame, BDWS, and other clients/projects must remain separated. Global reusable patterns require explicit curation and sanitization.
- **Never store** API keys, passwords, tokens, private SSH keys, authentication codes, client personal data, legal matter content, production logs containing secrets or other sensitive material. Apply redaction and consent policies; verify cloud data retention before use.
- Prefer self-hosted deployment if privacy requirements demand it; self-hosting alone does not remove the need to assess outbound LLM calls, logging, backups, retention and access controls.
- Do not automatically ingest all conversations, git history or files from private projects before a source review and scope approval.
- For disagreement, owner directives, repository governance, current source code and verified tests outrank retrieved memory.
- Persist a decision's **status** (proposed, approved, retired), **time**, **source**, and **supersession**. Corrections must supersede stale memory, not coexist as equally current instructions.
- No automated repository changes, service deployment, external data transfer or memory-bank sharing without the appropriate project authorization.
- Keep the existing STS testing rule: targeted CI/security/visual smoke tests during implementation; comprehensive end-to-end Playwright and visual/responsive/accessibility QA at the integrated release gate.

## High-value STS use cases
- Claude Code remembers why architectural, UI, security and hosting choices were made.
- Design QA learns from owner acceptance/rejection and recurrent visual mistakes; do not treat aesthetic preferences as verified facts.
- RCA memory preserves failures and validated fixes for Vercel, GitHub Actions, Supabase and integrations.
- Handoff between development sessions without giant pasted transcripts.
- Future agent orchestration: distinct agents consult permitted project knowledge while the repository remains the source of truth.

## Boundaries
Hindsight is NOT native or automatic ChatGPT memory; a supported connector or custom bridge is required to make a deployed Hindsight bank available to ChatGPT. Hindsight installation and operational costs are not assumed free merely because its software is open source.

## First pilot acceptance criteria
- Scoped STS lab memory, no credentials or real client data.
- Correct retrieval of five known decisions across restarted coding sessions.
- Correct recognition of a superseded decision.
- No leakage when querying a different bank.
- Recall grounded to source evidence with an explicit uncertainty path.
- Easy disable/uninstall and export/deletion path.
- Measured cost, latency and storage footprint.
