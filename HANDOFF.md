# HANDOFF — Data Slide Deck

> **Status: NOT YET MIGRATED.** This file is a template. The original work lives in a
> local Claude Code session on Adam's laptop that ran out of context. Fill every
> `<<FILL>>` before an agent can usefully continue.

Last updated: <<DATE>> by <<WHO>>

---

## 1. The ask (one paragraph)

<<FILL: What is this deck for? Audience, occasion, decision it must drive, deadline.>>

## 2. Data

| File | Source | Rows/period | Cleaned? | Notes |
|---|---|---|---|---|
| `data/raw/<<FILE>>` | <<where it came from>> | <<N rows, date range>> | no | <<gotchas>> |

Known data quirks: <<FILL: nulls, duplicated IDs, timezone, currency, mislabeled cols>>

## 3. Deck state

- Target format: <<pptx / Google Slides / Gamma / HTML>>
- Slide count target: <<N>>
- Done: <<slides finished>>
- In progress: <<slide currently being built and what's wrong with it>>
- Not started: <<remaining slides>>

## 4. Decisions already made (do not re-litigate)

- <<e.g. "Revenue is net of refunds">>
- <<e.g. "Q3 excluded — partial data">>
- <<e.g. "Brand colours: #xxxxxx / #xxxxxx">>

## 5. Dead ends (already tried, don't repeat)

- <<FILL>>

## 6. Next 3 actions

1. <<FILL>>
2. <<FILL>>
3. <<FILL>>

## 7. Environment

- Python: <<version>> — deps in `requirements.txt`
- Setup: `python -m venv .venv && . .venv/bin/activate && pip install -r requirements.txt`
- Regenerate processed data: `python scripts/<<script>>.py`
- Build deck: `python scripts/<<build>>.py`

## 8. Open questions for Adam

- <<FILL>>
