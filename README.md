# job-scout

Personal job-search scout — **not** part of any Flink work project.

## What it does

A scheduled Claude routine searches public listings on LinkedIn, Stepstone.de, and
Indeed.de once a day for early-career data roles and delivers a digest of new postings.

- **Roles:** Junior Data Scientist, Junior Data Analyst, Intern/Praktikum Data Science,
  Intern/Praktikum Data Analyst (+ Werkstudent variants)
- **Location:** Berlin, or remote hireable from Germany
- **Recency:** postings from the last ~24h (stateless — no tracker needed; dedupe happens
  within each run)

## What it deliberately does NOT do

It does not submit applications. Auto-applying is against all three platforms' terms,
LinkedIn actively bans accounts for it, and form submissions need per-application
confirmation anyway. Applying stays a human step (optionally assisted interactively).

## Contents

- `digests/` — daily digest snapshots (the first one was generated manually on 2026-08-17)
- `routine-prompt.md` — the exact prompt the scheduled routine runs, kept here so it can
  be reviewed/edited and re-applied
