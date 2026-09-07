# Ample

Working repo for the data-driven slide deck build.

## Layout

| Path | Purpose |
|---|---|
| `HANDOFF.md` | Live state of the task. **Read this first.** Any agent picking up work updates it before stopping. |
| `data/raw/` | Source data exactly as exported. Never edited by hand. |
| `data/processed/` | Cleaned/derived tables produced by scripts in `scripts/`. |
| `scripts/` | Reproducible transforms: raw -> processed -> chart inputs. |
| `slides/` | Deck source (outline, per-slide content, generated deck files). |
| `docs/` | Notes, references, decisions. |

## Rules

1. Every number on a slide traces back to a file in `data/` via a script in `scripts/`.
2. No secrets in git. Check `.gitignore` before adding anything.
3. Update `HANDOFF.md` at the end of every working session.
