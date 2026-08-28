# Product brief

## Why

Bulk follow-up is deceptively risky. Copying rows into messages is repetitive, but a single grouping mistake can disclose another owner's work. Automating the final send removes the last safety checkpoint. The product should compress preparation while preserving review and recipient isolation.

**Evidence:** the skill requires one recipient on `To`, only that recipient's rows, and drafts rather than sends (`SKILL.md`).
**Inference:** trust and controllability are more important than maximum throughput.

## Product thesis

If a coordinator can map a familiar table, preview exceptions, and create isolated drafts in one guided flow, then follow-up preparation becomes faster and safer without surrendering editorial control.

## What

A table-to-draft workflow that:

1. reads CSV, XLSX, or already-parsed rows;
2. identifies recipient, display-name, status, and item fields;
3. filters to actionable rows;
4. groups rows by recipient;
5. renders one HTML draft payload per group; and
6. hands payloads to a mail draft surface, never a send surface.

**Evidence:** steps 1–5 exist across `SKILL.md`, `scripts/build_draft_payloads.py`, and `scripts/templates/default.html`.
**Assumption:** a compatible mail-draft tool is available for end-to-end draft creation.

## Scope

- Guided column mapping and explicit ambiguity handling.
- Per-recipient isolation, open-item filtering, subject/deadline templating.
- Preview, validation summary, and draft-only creation.
- Counts for drafts, included rows, and skipped rows.

## Non-goals

- Sending or scheduling messages.
- Determining organizational policy, escalation severity, or recipient authority.
- Inventing missing context, outcomes, deadlines, or email addresses.
- Editing the source workbook or becoming an action-item system of record.
- Measuring message opens or employee performance.

## Principles

1. **Draft, never send.** Preserve a human checkpoint.
2. **Isolation before convenience.** A recipient sees only their rows.
3. **Exceptions are product states.** Ambiguity must be visible, not guessed away.
4. **Source fidelity.** Render supplied facts; do not embellish.
5. **Reversible by default.** Users can inspect or discard drafts.
6. **Minimal disclosure.** Summaries expose counts and blockers, not confidential row content.

## Product risks

| Risk | Current control | Remaining question |
|---|---|---|
| Wrong recipient mapping | Explicit mapping and ambiguity warning in `SKILL.md` | Hypothesis: a preview catches most mapping errors before drafting |
| Cross-recipient data leakage | Grouping by recipient in `build_draft_payloads.py` | Need automated isolation tests before broader use |
| Closed work included | Status inference/filtering | Custom status vocabularies may be misclassified |
| User mistakes draft for sent mail | Draft-only invariant | UI copy must make “created, not sent” unmistakable |
| Sensitive rows appear in chat/logs | Skill says summarize counts and blockers | Tooling should redact row values from telemetry |

## Decisions still requiring evidence

- Which table shapes and status vocabularies dominate real use.
- Whether users prefer correcting mappings before or after a sample preview.
- Acceptable unresolved-recipient rate.
- Whether one draft per owner remains useful for very large owner groups.
