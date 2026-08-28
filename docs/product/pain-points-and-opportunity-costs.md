# Pain points and opportunity costs

## Why quantify without inventing

The repository contains no production usage or outcome dataset. The framework below defines severity, frequency, consequences, formulas, and proxies to measure later; every actual baseline and target remains **TBD**.

## Pain chains

| Pain | Severity | Frequency to measure | Consequence chain | Evidence status |
|---|---|---|---|---|
| Manual per-owner drafting | Medium–high when owner count is large | Runs/week; recipients/run; rows/run | More recipients → repeated selection/copy/format → longer preparation → delayed follow-up | Inference from workflow |
| Wrong grouping or recipient | High | Mapping corrections/run; near-misses/run | Ambiguous identifier → wrong group → unrelated row in draft → privacy/trust incident | Risk implied by `SKILL.md` invariants |
| Closed/irrelevant items included | Medium | Included-row corrections/run | Status mismatch → noisy message → recipient rechecks tracker → lower attention to real ask | Inference |
| Missing owner or ambiguous alias | Medium | Exception rows / total rows | Unresolved row → skipped draft or guessed address → manual cleanup or misdelivery risk | Evidence: ambiguity warning in `SKILL.md` |
| Invisible partial failure | High | Failed drafts/run; reconciliation gaps | Tool fails mid-run → some drafts absent → coordinator assumes completion → owners not contacted | Hypothesis; end-to-end mail behavior not in repo |
| Generic tone | Low–medium | Drafts edited/run; edit distance | Template mismatch → extensive edits → automation savings erode | Hypothesis |

## Opportunity-cost statements

Use observed values only:

- **Preparation hours per run** = `(manual minutes per recipient × recipient count + reconciliation minutes) / 60`.
- **Automation time avoided** = `manual preparation minutes − (mapping + preview + exception repair + mailbox review minutes)`.
- **Correction burden** = `drafts edited for factual/grouping reasons / drafts created`.
- **Unresolved-row rate** = `rows skipped for missing/ambiguous recipient / source rows`.
- **Relevance rate proxy** = `included rows accepted without removal / included rows`.
- **Follow-up latency** = `draft-ready timestamp − source-export timestamp`.
- **Coverage gap** = `expected recipient groups − successfully created draft groups`.

No actual value is claimed for any formula.

## Risk of inaction

- Follow-up time grows roughly with recipient count under manual drafting.
- Coordinators may send broad tracker links to save time, increasing recipient effort and potential over-disclosure.
- Repetitive work may be deferred, leaving action status stale.
- A generic sender may be adopted instead, trading speed for weaker review controls.

## Measurement cautions

- Never log source row text, recipient addresses, or draft bodies for product analytics.
- Separate “draft created” from “message sent”; this product intentionally owns only the former.
- A low skipped-row rate is not automatically good if inference guessed incorrectly.
- Track corrections by reason, not employee identity.
- Use synthetic fixtures for isolation testing; do not replay confidential workbooks.

## Prioritization rubric

Score future pain evidence as `reach proxy × consequence × confidence`, where:

- reach proxy = affected runs or rows, not unique people unless privacy-approved;
- consequence = 1 (minor edit), 2 (rerun), 3 (missed follow-up), 5 (misdelivery/privacy);
- confidence = observed, reproduced, or hypothesized.

This rubric is a proposed decision aid, not a shipped model.
