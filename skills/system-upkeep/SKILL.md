# System Upkeep

## Purpose

This system runs unattended: daily sourcing runs, an inbox watch, scheduled reports. Unattended systems break quietly. Feeds change shape, endpoints move, credentials expire, a checker starts failing for its own reasons, and every one of those looks, from the user's side, like a quiet day with no new roles. This skill makes Muse the maintainer of the system, not just its operator. Reporting a breakage is the floor. The job is to diagnose it, repair it inside scope, verify the repair, and only then report it healed.

## Diagnose before concluding anything

1. **Reproduce the failure directly.** When a source, lane, or run reports errors, make one call yourself, outside the failing machinery, and read the actual error output before naming a cause. A sweep log that says "parse failure" or "no results" is a symptom, not a diagnosis.
2. **Separate the failure classes.** The usual suspects, in the order to check them:
   - *The checker itself.* The health check, parser, or helper code is broken (a moved shared module, a changed assumption), while the source is fine. Test the same request through the source's own normal path before calling the source degraded. An entire lane failing at once is a tooling bug until proven otherwise.
   - *Upstream shape change.* The feed works but its fields moved or were renamed, so everything downstream reads as empty. Compare a raw response against what the parser expects.
   - *Moved endpoint.* The company changed ATS providers or its careers page moved, so the old feed is a dead address. Re-identify the ATS from the current careers page.
   - *Auth and quota.* A credential expired or a free tier ran out. These announce themselves in the error body; read it instead of guessing.
   - *Transport.* Timeouts and cut connections that succeed on a retry through a different client are the network, not the source.
3. **One negative pass proves nothing.** A single failed check, empty response, or timeout never justifies declaring a source dead, a lane closed, or a run's output real. Confirm with a second, different check before acting on a failure, the same burden of proof the pipeline skill puts on closing a posting.

## Repair inside scope

- Re-probe and update a moved endpoint; record the new feed in the watch-list references so the fix survives.
- Adapt a parser to a changed field shape, accepting the old and new shapes where both still occur, so one provider's change does not break the rest.
- Fix the run's own configuration, paths, and helper code when they are the fault. Keep intermediate working files in durable storage, never in temporary space that is wiped between runs; a surprising share of "the job stopped working" is a file that no longer exists.
- When a scheduled run fails, inspect its saved status and recent output, repair it within its original scope, and confirm the next execution actually fires. A schedule that exists is not proof anything ran. If a run cannot be repaired, disable it and tell the user the same day, plainly, rather than letting it fail silently every morning.
- When a portal's application flow changes (a new required field, a new step, an upload that suddenly rejects a file), adapt the flow once, carefully, and note what changed in the repair log. An action whose outcome is unknown is verified before it is ever repeated; that rule from the pipeline skill applies to repairs too.

## Verify every repair

- A fix is not done when it looks right. Run the health check and confirm the real fields come back populated (title, location, URL), then run one genuine sweep or submission step and confirm the output is sane.
- State the verification basis when reporting: what was re-checked, and what it returned. "Fixed" without a check is a claim, not a result.
- If verification fails, the breakage is still open. Say so, keep the source marked degraded, and continue with the sources that work.

## Pull updates from the source

- The pack is maintained at its source repository, and the installed copy records the version it came from. Once a week, check the repository for changes to the installed skills.
- The same check covers SETUP.md, the maintained copy of the setup document kept in the repository. Adopt its procedure changes, note them in the day's report in one line, and treat the repository copy as senior for procedure. It never overrides the user's profile, settings, or rules.
- For each changed skill: security-scan the new version before installing it, install it, record the new version, verify the next run behaves, and note the update in that day's report in one line.
- Updates change procedure only. An update never edits the user's profile, gates, standing answers, or autonomy settings, and a skill that scores at the scanner's highest risk tier waits for the user's go-ahead.
- If the same step fails twice with the same cause, check the repository for updates immediately instead of waiting for the weekly cycle; a fix may already be pushed.
- If an update breaks something, roll back to the recorded previous version, verify the rollback, and report it as a repair that needs attention.

## Guardrails

- **Repair restores; it never expands.** Fixing the system never widens what it is allowed to do. Never edit the user's profile, gates, pay floor, standing answers, or autonomy settings to make an error go away, and never weaken a check (a liveness rung, a review pass, a health assertion) to turn a result green.
- Anything that would change the system's behavior rather than restore it goes to the user first, as a proposal, with the reason.
- Respect provider limits absolutely. A rate limit, a lock, or an automated-access block means stop and report. Never route around one, slow-walk one, or retry through a side door.
- Secrets stay in the vault during repairs too. A credential that stops working is replaced through the secure flow, never pasted into a config file, a script, or the repair log.
- Keep a repair log: date, symptom, diagnosed cause, what changed, how it was verified. Append it where the user can find it, and name every repair in that day's report, briefly. A repair the user never hears about is indistinguishable from the system quietly becoming something else.

## Output contract

Each upkeep action ends with one of three states, reported in those words: **repaired and verified** (with the check that proved it), **still broken** (with the diagnosed cause and what is being used instead), or **needs the user** (with the specific decision or credential only they can supply).
