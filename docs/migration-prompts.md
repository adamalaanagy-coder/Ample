# Migrating the deck task off the laptop

Two steps. Step 1 runs **on the laptop** (that's the only machine with the data
folder). Step 2 runs in **ChatGPT Codex** against this repo.

---

## STEP 1 — Prompt for the laptop session (Claude Code CLI or Codex CLI, run in the folder with the data)

```
You are performing a session handoff. My previous session ran out of context while
building a data-driven slide deck from files in this folder. Another agent will pick
this up from a GitHub repo, with zero memory of our conversation. Your only job right
now is to make that possible. Do not continue building the deck.

Repo to push to: https://github.com/adamalaanagy-coder/Ample
Branch: main-handoff

Do this:

1. Inventory. List every file in this working folder that is part of the deck task:
   raw data exports, cleaned data, scripts, notebooks, the deck file itself, notes,
   images. For each, one line: path, what it is, whether it is an input, an output,
   or scratch.

2. Classify for git. Flag anything that must NOT be pushed: credentials, API keys,
   .env files, personally identifiable data, client-confidential rows, anything over
   50MB. List these separately and stop to ask me before including any of them.

3. Reconstruct state from evidence, not memory. Read the deck file and the scripts.
   Determine: which slides exist, which are finished, which are stubs, which numbers
   are hardcoded vs computed, and what the last thing being worked on was.

4. Write HANDOFF.md at the repo root covering, in this order:
   - The ask: audience, purpose, deadline, the decision this deck must drive.
   - Data inventory table: file, source, rows, date range, cleaned yes/no, quirks.
   - Deck state: target format, slide count, done / in-progress / not-started.
   - Decisions already locked (definitions, exclusions, colours, framing) so the
     next agent doesn't re-litigate them.
   - Dead ends already tried.
   - The next 3 concrete actions.
   - Environment: python version, exact install commands, how to regenerate the
     processed data, how to build the deck.
   - Open questions that need me to answer.
   Be specific. "Cleaned the data" is useless. "Dropped 412 rows with null
   customer_id; revenue is net of refunds; FY starts April" is useful.

5. Make it reproducible. Write requirements.txt (pinned versions) and make sure the
   scripts run end-to-end from raw data to deck with no manual steps. If a step is
   manual, say so explicitly in HANDOFF.md.

6. Structure into: data/raw/, data/processed/, scripts/, slides/, docs/. Add a
   .gitignore covering .env, venvs, __pycache__, node_modules, OS files.

7. Commit and push:
   git init (if needed)
   git remote add origin https://github.com/adamalaanagy-coder/Ample
   git checkout -b main-handoff
   git add -A && git commit -m "Handoff: deck task state, data, scripts"
   git push -u origin main-handoff

8. Report back the repo URL and a 5-bullet summary of what a fresh agent now knows.

If anything is ambiguous about what the deck is for, ask me before writing HANDOFF.md.
```

---

## STEP 2 — Prompt for ChatGPT Codex (cloud), pointed at adamalaanagy-coder/Ample

```
Repo: adamalaanagy-coder/Ample

Context: this repo is a handoff. A previous agent session ran out of context while
building a data-driven slide deck and pushed its state here. You are continuing that
work cold.

Before you write any code:
1. Read HANDOFF.md end to end. It is the source of truth for task state.
2. Read README.md for the repo layout and working rules.
3. Run the environment setup exactly as HANDOFF.md specifies, and verify you can
   regenerate data/processed/ from data/raw/. If that fails, fixing it is your
   first task — nothing downstream is trustworthy until it works.
4. Independently verify the top 5 numbers that appear on the deck against the raw
   data. Report any that don't reconcile. Do not carry forward a number you cannot
   trace to a file.

Then:
5. Restate the task back to me in 5 bullets, list the next 3 actions from
   HANDOFF.md, and tell me anything in HANDOFF.md that is missing, contradictory,
   or that you disagree with. Wait for my go-ahead.

Standing rules for this repo:
- Every number on a slide must be computed by a script in scripts/ from a file in
  data/. No hardcoded figures. If you hardcode one, comment why.
- Prefer fixing the pipeline over patching the slide.
- Before you stop working for any reason — task done, blocked, or running low on
  context — update HANDOFF.md with current state, next 3 actions, and open
  questions, then commit and push. Treat running low on context as a trigger to
  hand off cleanly, not to rush the work.
- Commit in small, described steps. Open a draft PR when there's something to review.
```

---

## If you'd rather skip the cloud entirely

Run Codex CLI (or Claude Code) **on the laptop** in the data folder and just paste
Step 2's "Standing rules" section plus a one-line task restatement. Local agents can
read the data folder directly — no migration needed. The repo push is still worth
doing as a backup and so any machine can pick the task up.
