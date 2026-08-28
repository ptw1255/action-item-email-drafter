# Roadmap and success metrics

## Why

The next investment should increase confidence before throughput. The repository proves deterministic payload construction, but not user adoption, error reduction, or mailbox draft reliability.

## Phased roadmap

| Phase | Outcome | Candidate work | Exit evidence |
|---|---|---|---|
| 0 — Baseline trust | Understand real table shapes safely | Synthetic fixture suite; mapping/error taxonomy; privacy-safe run events | Isolation and escaping tests pass; baseline task study completed |
| 1 — Guided review | Users can detect mapping/filter errors before drafts | Mapping confirmation, sample preview, exception queue, explicit empty states | Test users explain inclusion rules and catch seeded errors |
| 2 — Reliable draft handoff | Partial failures are visible and recoverable | Idempotency key proposal, per-group progress, retry failed only, duplicate warning | Synthetic mail-tool faults reconcile created/failed/pending groups |
| 3 — Reusable workflows | Repeat runs need less setup without hiding change | Saved column maps scoped to schema fingerprint; change diff; template variants | Reuse lowers setup time without increasing corrections |
| 4 — Scale with control | Large runs remain reviewable | Chunking experiment, sampling strategy, policy hooks | Guardrails stay within agreed thresholds at larger row counts |

Roadmap items are proposals, not commitments.

## Hypotheses

1. Showing a sample group before draft creation reduces factual/grouping corrections.
2. Explaining every skipped row increases completion confidence.
3. Schema-fingerprinted mappings reduce setup effort without applying stale mappings.
4. “Retry failures only” reduces duplicate drafts after partial tool failure.
5. Draft-only copy increases willingness to use the workflow for sensitive trackers.

## Metric model

| Type | Metric | Definition |
|---|---|---|
| Leading | Mapping completion rate | runs reaching confirmed mapping / runs started |
| Leading | Preview correction rate | runs with mapping/filter correction before creation / previewed runs |
| Leading | Exception resolution rate | exception rows resolved before creation / exception rows shown |
| Leading | Draft handoff coverage | successfully created groups / approved groups |
| Lagging | Preparation time | review-complete time − source-selected time |
| Lagging | Post-creation correction rate | drafts requiring factual/grouping edit / drafts created |
| Lagging | Repeat workflow rate | operators returning with same schema fingerprint within window / eligible operators |
| Guardrail | Cross-recipient isolation failures | groups containing a row for another recipient; target must be zero |
| Guardrail | Automatic sends | send operations initiated by product; target must be zero |
| Guardrail | Silent skip rate | skipped rows without surfaced reason / skipped rows; target must be zero |
| Guardrail | Sensitive telemetry events | events containing row text/address/body; target must be zero |

No baseline or target is asserted beyond invariants.

## Privacy-safe instrumentation

Proposed events:

| Event | Allowed properties |
|---|---|
| `source_read` | format, row-count bucket, sheet-count bucket, outcome, error category |
| `mapping_confirmed` | inferred/changed flags by role, confidence bucket, elapsed time |
| `grouping_previewed` | recipient-count bucket, included/skipped counts, exception categories |
| `draft_batch_started` | approved group count, template id, deadline-present boolean |
| `draft_group_result` | anonymous run/group sequence, success/error category, latency |
| `draft_batch_completed` | created/failed/pending counts, stopped boolean |

Never capture filenames, headers unless allow-listed, cell contents, names, aliases, addresses, subjects, or bodies.

## Experiments

| Experiment | Comparison | Success signal | Guardrail |
|---|---|---|---|
| Seeded-error usability test | Mapping form vs mapping + sample group | More seeded errors detected before creation | Task completion does not materially regress |
| Exception presentation | Inline count vs categorized exception queue | Higher correct resolution, lower abandonment | No row content in analytics |
| Status rule explanation | Hidden inference vs visible included/excluded examples using synthetic rows | Better rule comprehension | No increase in accidental include-all |
| Partial-failure recovery simulation | Full rerun vs failed-only retry | Fewer duplicate synthetic drafts | No missing successful group |

## Decision cadence

Review guardrails first, then user-correction evidence, then speed. A faster flow that weakens isolation or review fails the product thesis.
