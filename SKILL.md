---
name: action-item-email-drafter
description: "Turns a spreadsheet, CSV, or table of owners/action items into individualized Outlook draft emails. Use when the user wants templated per-person reminders, follow-ups, outcome requests, action-item chasers, or personalized draft emails from a workbook/export. The skill groups rows by recipient, renders a concise HTML template with only that recipient's action items, and creates drafts only; it never sends mail automatically."
---

# Action Item Email Drafter

Use this skill to transform a workbook/export/table into one personalized Outlook draft per recipient.

## Safety invariants

- **Never send automatically.** Create drafts only.
- Put each recipient on the **To:** line only unless the user explicitly provides CC/BCC rules.
- Each draft must include only that recipient's rows/action items.
- If recipient resolution is ambiguous, create the draft with the best available address/alias and warn the user to review before sending.
- Do not include confidential spreadsheet rows in chat output; summarize counts and blockers instead.

## Required inputs

Ask one question at a time if missing:

1. **Input source**: spreadsheet link/path, CSV, pasted table, or already-parsed rows.
2. **Recipient column**: alias, email, owner, PoC, reviewer, manager, or equivalent.
3. **Action item columns**: the fields to show in the email body.
4. **Subject pattern**: default to `[Action Required] Outstanding items - {{Count}} pending`.
5. **Deadline**: optional, but include it prominently when provided.

## Recommended column mapping

Infer these names case-insensitively when possible:

| Purpose | Common column names |
|---|---|
| Recipient | `Owner`, `Alias`, `Email`, `Reviewer`, `PoC`, `AssignedTo`, `Assignee` |
| Display name | `Name`, `DisplayName`, `OwnerName`, `ReviewerName` |
| Service/team | `Service`, `Team`, `Area`, `Component`, `Workload` |
| Action item | `ActionItem`, `Action`, `Task`, `RequiredAction`, `NextStep` |
| Status | `Status`, `State`, `Outcome`, `Decision` |
| Due date | `DueDate`, `Deadline`, `TargetDate` |
| Notes/link | `Notes`, `Details`, `Link`, `Url`, `Evidence` |

If the mapping is uncertain, show the candidate columns and ask the user to choose.

## Workflow

1. Import rows from the source. If the source is an Excel/SharePoint link and a direct workbook reader is available, use it. Otherwise ask the user to export/download as `.xlsx` or `.csv`.
2. Normalize recipient values:
   - Trim whitespace.
   - Strip trailing `*` markers from aliases.
   - If the value lacks `@`, treat it as a resolvable Microsoft alias/name.
3. Filter rows:
   - Keep rows with open/outstanding/incomplete/action-required status.
   - If no status column exists, keep all rows unless the user gives a filter.
4. Group by recipient.
5. Render one HTML draft per recipient using `scripts/templates/default.html`.
6. Apply `Anti-Slop.md` before creating drafts:
   - Start with the ask.
   - Use the row's concrete service/item/status/deadline.
   - Remove generic filler and banned words.
   - Do not invent missing context.
7. Create drafts with the mail draft tool when available:
   - `to`: single recipient
   - `subject`: rendered subject
   - `contentType`: `HTML`
   - `body`: rendered HTML
8. Summarize:
   - Number of drafts created
   - Number of recipients
   - Number of skipped rows
   - Any unresolved/ambiguous recipients

## Helper script

For local row processing, use:

```bash
python3 ~/.copilot/skills/action-item-email-drafter/scripts/build_draft_payloads.py \
  --input /path/to/input.csv \
  --recipient-column Owner \
  --subject "[Action Required] Outstanding items - {{Count}} pending" \
  --deadline "2026-06-30" \
  --output /tmp/action-item-drafts.json
```

The script accepts `.csv` and `.xlsx` files. For `.xlsx`, it uses `openpyxl` if installed; otherwise ask the user to export as CSV or install `openpyxl`. The script emits draft payloads that can be passed to the mail draft tool. It does **not** send or create mail by itself.
