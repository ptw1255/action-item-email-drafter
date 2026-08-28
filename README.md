# Action Item Email Drafter

**Status:** Working skill and local payload builder; draft creation depends on an available mail-draft tool.

This repository turns tabular action-item exports into one reviewable Outlook draft payload per recipient. It is intentionally draft-only: it groups each owner's rows, filters open work when a status column exists, renders an HTML table, and never sends mail.

## Verified surface

- Workflow and safety contract: [`SKILL.md`](SKILL.md)
- CSV/XLSX grouping and rendering helper: [`scripts/build_draft_payloads.py`](scripts/build_draft_payloads.py)
- Default email template: [`scripts/templates/default.html`](scripts/templates/default.html)

Run `python3 scripts/build_draft_payloads.py --help` for the verified local interface. CSV works with the Python standard library; XLSX input requires `openpyxl`, as the helper reports when unavailable.

## Product portfolio

The product rationale, users, journeys, wireframes, roadmap, and measurement plan are in [`docs/product/README.md`](docs/product/README.md).
