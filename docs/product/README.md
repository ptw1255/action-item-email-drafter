# Product portfolio: Action Item Email Drafter

## Why this product exists

Action owners need precise follow-up, while coordinators need to avoid repetitive drafting, accidental cross-recipient disclosure, and an irreversible send. The repository encodes a safer middle path: deterministic per-recipient payloads plus human review before any message leaves the mailbox.

## From why to what

1. [Product brief](product-brief.md) — thesis, boundaries, principles, and evidence.
2. [Users and JTBD](users-and-jtbd.md) — personas, triggers, jobs, stories, forces, and journeys.
3. [Value proposition](value-proposition.md) — alternatives, value map, differentiation, proof, and assumptions.
4. [Pain points and opportunity costs](pain-points-and-opportunity-costs.md) — consequence chains and measurable proxies.
5. [Wireframes](wireframes.md) — proposed workflow and state coverage.
6. [Roadmap and success metrics](roadmap-and-success-metrics.md) — phases, hypotheses, instrumentation, and experiments.

## Evidence discipline

Statements use these labels:

- **Evidence** — directly supported by repository behavior or documentation.
- **Inference** — a product interpretation derived from that evidence.
- **Hypothesis** — a testable belief requiring user or usage data.
- **Assumption** — an unverified dependency or constraint.

### Evidence register

| Claim | Type | Repository source |
|---|---|---|
| The workflow creates drafts and must never auto-send. | Evidence | `SKILL.md` (“Safety invariants”) |
| Rows are grouped by normalized recipient and can be filtered by status. | Evidence | `scripts/build_draft_payloads.py` (`should_keep`, grouping loop) |
| CSV and XLSX are accepted; XLSX needs `openpyxl`. | Evidence | `scripts/build_draft_payloads.py` (`read_rows`) |
| Recipient ambiguity and missing mappings need review. | Evidence | `SKILL.md` (“Required inputs”, “Recommended column mapping”) |
| Coordinators are the likely primary operator. | Inference | `SKILL.md` workflow and helper CLI |

No shipped adoption, usability, time-saving, deliverability, or business-result claim is made in this portfolio.
