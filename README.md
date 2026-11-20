# Job Search Autopilot: Skill Pack

A set of Muse skills that run an end-to-end job search: sourcing, gating, tailored application materials, submission, tracking, inbox watch, interview prep, rejection analysis, and offer review. The pack is generic. Every personal setting (target roles, pay floor, locations, standing answers) comes from the user's own intake, never from these files.

## How to install

Give this repository to Muse and say:

> Install the skills from this repository as custom skills, then run the job search autopilot setup.

Muse should:

1. Copy each folder under `skills/` into the user's custom skills directory, intact, including any `references/` files.
2. Security-scan each `SKILL.md` before installing (for example with NVIDIA SkillSpector or an equivalent skill scanner) and show the user the scores. Do not install a skill that scores at the scanner's highest risk tier without the user's explicit go-ahead.
3. Then follow the companion setup document, maintained in this repository as `SETUP.md`, for intake: it collects the user's resume, targets, pay floor, locations, autonomy settings, and standing answers, and confirms a summary before any application is submitted.
4. This pack is maintained in this repository. An installed system records the version it installed from, checks this repository weekly, and pulls security-scanned updates automatically, so fixes pushed here reach it without a reinstall. Updates change procedure only, never the user's settings.

## What is in the pack

| Skill | What it does |
| --- | --- |
| `job-search-sourcing` | Finds new postings: watch-list company feeds first, keyword sweeps second, aggregators as discovery only. Dedupes and fit-filters. |
| `job-search-pipeline` | The operating core: hard gates, pay verification, liveness checks, the four-pass materials review, submission rules, and the tracker. |
| `verify-before-recommending` | The discipline that no role is recommended or queued until its full official posting has been read and checked for pay, liveness, and craft fit. |
| `resume-tailor` | Builds a one-page, posting-specific resume variant from the user's verified facts only. |
| `cover-letter-writer` | Drafts and debates a company-specific cover letter for each application. |
| `interview-prep` | Prep plans, a story bank, scored practice sessions, debriefs, and a company red-flag check. |
| `rejection-review` | Turns each rejection into a diagnosis and a reframing playbook entry, so the next application in that role family is stronger. |
| `offer-stage` | Offer arithmetic, a clause-by-clause contract walk that produces questions for a lawyer, and negotiation talking points. Never advises signing or declining; never legal advice. |
| `write-like-a-person` | The standing voice pass for everything written on the user's behalf (application answers, recruiter emails, letters, thank-you notes): removes AI writing patterns without changing what the text says. |
| `resume-review` | A standalone audit of the master resume: recruiter first-scan test, the style checklist item by item, defects separated from taste calls, before-and-after rewrites, and a JD-match mode. |
| `system-upkeep` | The maintenance mandate: when a feed, run, or submission flow breaks, diagnose the real cause, repair it inside scope, and verify the repair before reporting it healed. Repairs restore the system; they never widen its permissions or edit the user's rules. |

## Ground rules baked into every skill

- Never fabricate. Application content comes only from the user's verified fact sheet and bullet bank.
- Official source or it did not happen. Aggregator listings are leads; a posting counts only when confirmed live on the employer's own careers site.
- No duplicates. The tracker is reconciled before every run.
- Secrets live in the secure vault, never in chat, files, or these skills.
- Unusual legal consents, unanswerable required questions, and bespoke essays park for the user. Everything else inside the user's rules runs automatically.
- Reports ship as PDFs: a short chat note plus the full daily report as a styled PDF attachment, never a wall of text.
- The sponsor never reaches in. This repository is a one-way channel for workflow fixes. It cannot see or change any user's profile, targets, pay floor, or settings; those belong to the user alone, and their Muse changes them only on the user's own instruction.

## License and provenance

These skills distill a working personal job search system into a reusable template. Adapt them freely. Released under the MIT License (see the LICENSE file). Settings marked as coming "from the user's profile" are set during intake by the companion setup document.
