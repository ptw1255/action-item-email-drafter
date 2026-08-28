# Value proposition

## Why

The value is not “AI writes email.” The valuable unit is a correctly isolated, reviewable draft built from source rows. That distinction determines both differentiation and proof.

## Value proposition canvas

### Customer profile: coordinator

| Jobs | Pains | Desired gains |
|---|---|---|
| Convert a tracker into targeted asks | Copy/paste effort; mapping uncertainty; leakage risk | Faster preparation; consistent format; visible exceptions |
| Keep follow-up grounded in current rows | Stale or invented context | Traceable content and explicit deadline |
| Maintain editorial control | Fear of automatic sending | Editable drafts and a review gate |

### Value map

| Product/service | Pain reliever | Gain creator |
|---|---|---|
| Column inference plus confirmation | Reduces header-mapping effort without hiding uncertainty | Reusable flow across common exports |
| Status filter and per-recipient grouping | Reduces irrelevant/closed rows and cross-owner exposure | One focused draft per owner |
| HTML template | Avoids hand-formatting | Predictable, scannable message |
| Exception and count summary | Makes skipped work visible | Quick reconciliation against the source |
| Draft-only handoff | Prevents irreversible automatic send | Preserves human tone/policy review |

## Current alternatives

| Alternative | Strength | Tradeoff |
|---|---|---|
| Manual email per owner | High control; no setup | Slow and inconsistent at scale |
| Generic mail merge | Mature and familiar | Often assumes clean one-row-per-recipient data; weak exception visibility |
| Send full tracker/link | Minimal preparation | Burdens recipient and may over-disclose |
| Workflow automation that sends | High throughput | Irreversible and harder to review |
| Do nothing / periodic group reminder | Low effort | Low relevance and weak accountability |

## Differentiation

1. **Recipient isolation is a safety contract**, not merely a personalization feature (`SKILL.md`).
2. **Draft-only is structural**, leaving sending to the human (`SKILL.md`).
3. **Deterministic row processing** makes grouping/filtering inspectable (`scripts/build_draft_payloads.py`).
4. **Exceptions are summarized** rather than silently discarded (`draftCount`, `skippedRowCount`, and mappings in helper output).

## Proof available now

- **Evidence:** source code shows recipient normalization, grouping, filtering, HTML escaping, and payload counts (`scripts/build_draft_payloads.py`).
- **Evidence:** the skill documents draft-only and disclosure constraints (`SKILL.md`).
- **Evidence:** the helper has no Outlook/Graph connection and writes JSON only (module docstring and `main` in `scripts/build_draft_payloads.py`).

There is no repository evidence for adoption, time saved, lower error rates, recipient satisfaction, or successful delivery.

## Assumptions and hypotheses

- **Assumption:** source tables contain a stable recipient identifier.
- **Assumption:** users can access a mail-draft tool after payload generation.
- **Hypothesis:** a mapping preview lowers correction effort versus discovering errors in mailbox drafts.
- **Hypothesis:** exception-first review increases trust more than a single “drafts created” count.
- **Hypothesis:** recipients act faster on isolated tables than on a shared tracker link.

## Positioning

For coordinators who follow up from tabular action trackers, Action Item Email Drafter is a draft-preparation workflow that isolates each recipient's outstanding rows and surfaces exceptions. Unlike automatic senders or generic bulk mail, it keeps source fidelity and human review as non-negotiable boundaries.
