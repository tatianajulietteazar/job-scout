# job-scout

A daily, Claude-powered job scout for early-career data roles — set up as a personal
project (no Flink work content). Candidate profile: see `application-materials/`
(gitignored — this repo is a shareable blueprint, the personal data never leaves the
machine it runs on).

## What it does, every morning (~07:07)

A scheduled task in the Claude desktop app on this Mac:

1. **Sweeps public listings** — LinkedIn guest search (primary; works without login) and
   Indeed.de (secondary; German keywords) — for postings from the last 24 hours matching
   junior / intern / Praktikum / Werkstudent data scientist & data analyst roles, Berlin +
   remote Germany. Stepstone.de is excluded (blocks automated readers at network level);
   its inventory overlaps heavily with the other two.
2. **Writes a digest** to `digests/<date>-digest.md` and commits it here.
3. **Drafts a tailored cover letter** per core posting (DE/EN matching the ad), grounded
   strictly in the candidate CV — saved under `applications/<date>/` (gitignored).
4. **Emails digest + drafts** to the recipients configured in `routine-prompt.md`.

If the Mac or the Claude app is closed at 07:07, the run happens on next launch instead.

## What it deliberately does NOT do

**It never submits applications.** Auto-applying violates all three platforms' terms
(LinkedIn actively bans accounts for it), the platforms sit behind personal logins, and
an application is an irreversible outward action that needs a human decision. The scout
automates everything up to the click: finding, filtering, drafting. A human reviews and
submits — optionally in an assisted Claude session (Claude fills the forms in the
applicant's logged-in browser; the human confirms each submit).

## How to adjust it

Everything tunable lives in **`routine-prompt.md`** — roles/keywords, location, email
recipients, digest format, sources. The scheduled task re-reads it on every run, so an
edit applies from the next morning. No need to touch the task itself.

**Updating the CV:** drop the new PDF into `application-materials/` — the scout always
uses the most recently modified PDF there. Interim corrections (new job, new city) go in
`application-materials/profile-notes.md`, which overrides the CV until the new version
lands.

## How to share it / run your own

- **Just receive the digest:** get added to *Email recipients* in `routine-prompt.md`.
- **Run your own scout:** scheduled tasks are per-machine and per-Claude-account, so each
  person runs their own copy. Clone this repo (or copy `README.md` + `routine-prompt.md`),
  put your own CV in `application-materials/`, edit the search profile and recipients in
  `routine-prompt.md`, then open Claude Code in the folder and say:
  *"Set up the daily scheduled task described in routine-prompt.md."*
  Requirements: Claude desktop app + a connected Gmail connector.
- The repo is designed so nothing personal is committed — safe to share as a private
  GitHub repo with collaborators, or even publicly.

## History / design notes

- A claude.ai **cloud** routine was tried first and abandoned: the cloud sandbox's egress
  proxy blocks linkedin.com and indeed.de outright, and its Gmail connector is draft-only.
  The scout must run locally. (Disabled routine id: `trig_01SuJ2QUN1JTpybo8HsCdbtd`.)
- LinkedIn guest pages ignore the `f_E` experience-level filter — seniority is filtered by
  title keywords instead.
- The first digest (`digests/2026-08-17-digest.md`) was a manual 7-day backfill run.
