# Users and jobs to be done

## Why user understanding matters

The same automation that removes repetitive work can amplify a bad mapping. Personas are therefore defined by responsibility and risk, not by demographics.

## Personas

| Persona | Type | Goal | Constraint |
|---|---|---|---|
| Program coordinator or action owner | Primary | Prepare accurate, individualized follow-ups from a tracker | Many rows, uneven data quality, limited time |
| Recipient/action owner | Secondary | Understand exactly what needs attention and by when | Wants relevance, context, and no unrelated rows |
| Reviewer or approver | Secondary | Confirm wording, audience, and policy before sending | Needs traceability to the source |
| Autonomous bulk-mail operator | Negative | Upload a list and send immediately with no review | Conflicts with the draft-only safety invariant |
| Performance-monitoring analyst | Negative | Infer employee performance from response behavior | Outside purpose and creates surveillance risk |

**Inference:** personas follow the roles implied by the draft workflow in `SKILL.md`; no repository user research validates their prevalence.

## Contexts and triggers

- A review exports outstanding work to CSV/XLSX.
- A deadline approaches and each owner needs a tailored reminder.
- A coordinator needs outcome/blocker updates without exposing the entire tracker.
- A tracker has inconsistent owner/status headers and needs mapping before use.
- A rerun is needed after rows change, but prior drafts must not be silently overwritten.

## Jobs

**Functional**

- Segment actionable rows by the correct recipient.
- Produce concise, consistent drafts with source facts and optional deadline.
- Identify skipped, closed, missing-owner, and ambiguous rows.
- Review payloads before creating mailbox drafts.

**Emotional**

- Feel confident that no owner receives another person's items.
- Avoid the anxiety of a mass-send mistake.
- Preserve control over tone and final wording.

**Social**

- Appear organized and respectful of recipients' attention.
- Demonstrate that follow-up is based on an auditable tracker, not ad hoc pressure.

## Rigorous JTBD statements

1. **When** I receive an export with many owners, **I want to** map its columns and see a sample grouping, **so I can** trust that each person will receive only their own open items.
2. **When** a deadline is approaching, **I want to** generate consistent draft subjects and bodies from source rows, **so I can** follow up promptly without rewriting the same message.
3. **When** owner values are missing or ambiguous, **I want to** isolate those exceptions before draft creation, **so I can** correct them without risking misdelivery.
4. **When** drafts have been created, **I want to** see counts and unresolved blockers without row content in the summary, **so I can** verify completion while limiting disclosure.
5. **When** an action owner opens a reminder, **I want to** see the concrete item, state, and deadline in a compact table, **so I can** decide what to complete or explain.

## User stories with acceptance intent

- As a coordinator, I can confirm inferred columns before processing so that inference is never mistaken for approval.
- As a coordinator, I can choose “include all” explicitly so that bypassing status filtering is deliberate.
- As a reviewer, I can inspect a representative draft and exception list before any mailbox draft is created.
- As a recipient, I receive no rows belonging to another normalized recipient.
- As a privacy-conscious operator, I see aggregate completion counts rather than source row contents in the final summary.

## Forces of progress

| Push of current state | Pull of product | Anxiety | Habit/inertia |
|---|---|---|---|
| Repetitive copy/paste and formatting | One guided run creates consistent payloads | Wrong recipient or accidental send | Familiarity of hand-written email |
| Tracker contains more detail than each owner needs | Per-recipient isolation | Status inference may exclude/include wrong rows | Existing mail merge templates |
| Follow-up slips as lists grow | Counts and exception summary | Draft quality may feel impersonal | Manual review already “works” at small scale |

## Journeys

### Coordinator journey

| Stage | User question | Product response | Failure/edge state |
|---|---|---|---|
| Select | “Can this source be read?” | Show source type and sheet options | Unsupported type; missing `openpyxl` |
| Map | “Which columns mean what?” | Inference with explicit confirmation | No recipient match; duplicate/blank headers |
| Filter | “What will be included?” | Open-status rule and counts | Unknown/custom status values |
| Preview | “Is isolation correct?” | Recipient groups, sample draft, exceptions | Empty actionable set; unusually large group |
| Create | “What changed in Outlook?” | Draft progress only | Tool/auth failure; partial creation |
| Review | “Can I safely send?” | Mailbox drafts remain editable | Duplicate rerun; stale source |

### Recipient journey

Receive draft after human sends → scan ask/deadline → inspect only owned items → complete or reply with outcome/blocker. The repository supports draft composition, not delivery or response tracking (`SKILL.md`).
