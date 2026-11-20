# Job Search Pipeline

## Purpose

Keep the user's job search pipeline current and act on it: gate new postings against the user's bar, prepare and review application materials, submit under the user's standing authority, and track where every application stands. All parameters (pay floor, locations, target role families, autonomy settings, standing answers) come from the user's profile, set during intake and kept in memory. Nothing in this skill assumes a particular user.

## The fit bar

A posting is worth flagging only if it clears all of these:

- It belongs to one of the user's target role families.
- Location passes the user's location rules (their cities, remote rules, relocation stance).
- Pay clears or plausibly clears the user's floor. If no range appears in the summary fields, run the full-text pay scan below before calling it "comp unverified."
- It is verified live on the employer's official careers page. Aggregators go stale; never rely on them.

## Gate posture

- **Hard drops, no exceptions:** pay below the user's floor with no meaningful upside exception (see below); location outside the user's rules; a dead posting, or one whose liveness cannot be confirmed on the official site.
- **Never auto-drops:** experience-evidence gaps, seniority stretches, and "preferred background" requirements (a named prior industry, a named prior role type). These route to the Pipeline for the user's call, or proceed under the user's autonomy setting. Years-of-experience requirements are not a gate; judge whether the user can evidence the role's substance.
- **Absolute blocks:** never fabricate; a required question that cannot be answered truthfully from the user's fact sheet parks the role (do not submit); no duplicate submissions.
- **Unusual consents** (waivers, non-competes, contracts beyond standard attestations) are never a drop and never signed without the user. Surface them clearly; only the consent step waits.
- **Upside exception:** base below the floor at an early-stage company with meaningful equity or bonus upside is a judgment call for the user, never an auto-drop, if the user's profile enables this exception. The floor applies in full where upside is absent or trivial.

## Pay resolution: full-text scan

Many jurisdictions require employers above a size threshold to include the pay scale in job postings. ATS summary fields and aggregator extracts routinely show pay as unposted while the full posting text carries the range in its body or footer. Therefore: before any role is labeled "comp unverified," fetch the full official posting text and scan body and footer for a disclosed range. A range found this way counts as posted pay for the floor gate; record it in the tracker. Only a role whose full official text discloses no range anywhere may be held as comp-unverified, and its Pipeline note should state the likely reason (small employer, a jurisdiction without a disclosure law, or a confidential search).

## Workflow

1. Load the watch list and the pipeline state file (`references/pipeline-status.md`: seen, applied, dead, submitted).
2. Check official careers pages and feeds for postings matching the fit bar (the sourcing skill does the broad discovery; this skill verifies).
3. Compare against the state file. Only surface what is new or changed.
4. For each new fit, report: company, title, location, posted pay, direct link to the official posting, one line on why it fits.
5. Update the state file on every run so the pipeline survives between sessions.

## Application submission

Under the user's standing authority (granted during intake; scope recorded in their profile):

1. Apply on the employer's official careers site only; verify liveness first (see Posting liveness).
2. **One identity on every portal.** Every portal account uses the user's application email as the username and the same password everywhere, stored as a verified username-plus-password pair in the secure vault. A password-only vault entry cannot be used by a sign-in service; never report a login as saved until the pair has been checked together. Never type a password into chat, and never leave password fields for the user unless they explicitly ask for the manual step.
3. **Check the inbox before parking on a saved login.** When an application is blocked on a login, search the application email inbox for an account-setup or welcome email from that portal or employer. No setup email means no account exists: create it and complete the application in the same session. A setup email means the account exists and a rejected sign-in is a password problem.
4. **Complete email verification yourself.** Portals commonly block sign-in until a verification email is completed. After account creation, find the verification message in the inbox (check the sender is the genuine portal domain first) and complete it: follow the link directly, or use the one-time-code flow for the current sign-in step.
5. **A CAPTCHA that rejects the automated session:** after a small capped number of attempts, park the role, tell the user, and hand them the prepared materials so they can apply by hand in a few minutes if they want to. Do not hammer the portal.
6. Fill the form with the tailored materials and the user's standing answers. Accept only the consents the user's profile pre-approves (standard truthfulness attestations; binding arbitration and interview-transcription consent only if the user opted in during intake). An unusual consent is never signed without the user and never drops the role; only that step waits.
7. **"Why this company" free-text fields take the cover letter.** When a form requires a personal free-text answer of the why-us type and has no cover letter field, answer with the package's approved cover letter text. Bespoke essays that go beyond a why-us answer still park for the user's own words.
8. **Check the inbox for the ATS confirmation before writing the status.** A submission attempt that ends on an error, anti-spam, or unclear screen is not yet a failed submission. Search the application inbox for a confirmation message from the ATS or employer for that company and role, covering the attempt window through the following morning. If a confirmation exists, the role is Submitted: record it, update the tracker, and never submit the package again (a second submission is a duplicate, an absolute block). Only when no confirmation is found may the role be recorded as parked or blocked, and the report must say the inbox check ran. Run the same check before any resubmission and before any report describes a role as not submitted.
9. After a confirmed submission: record it in the tracker, clear the role from Pipeline, update the state file.

## Materials preparation: the four-pass review

Every role that reaches the application stage goes through four passes before anything is submitted. Single-pass materials are how framing mistakes ship unchecked.

1. **Writer.** Drafts the tailored resume (resume-tailor skill) and the cover letter (cover-letter-writer skill). Inputs: the full posting text, never a summary (fit failures are keyword- and concept-level); the user's fact sheet and bullet bank as ground truth; the reframing playbook entry for the role family if one exists (rejection-review skill); the unsupported-claims list; the user's standing answers. The writer's core job is concept mapping: for each of the posting's top requirements, frame the closest real analog from the user's background in the employer's language. Translate, never relabel: an honest analog passes; dressing one domain's metrics up as another domain's metrics fails.
2. **Reviewer.** Stress-tests the drafts against the posting and returns PASS or FAIL with specific, actionable objections, never impressions:
   - *Coverage:* the posting's top 3 to 5 requirements appear in the top half of the resume, evidenced by real bullets. A requirement addressed only in the bottom third fails.
   - *Fabrication:* every claim traces to the fact sheet; every concept mapping is an honest analog, not a relabel; nothing on the unsupported-claims list appears.
   - *Framing:* the materials name the background-to-role translation explicitly instead of hoping the reader makes the leap.
   - *Bridgeable vs unbridgeable:* a remaining gap is either a framing problem (rewrite) or a substance gap no honest reframing closes. The latter is not a rewrite prompt and not an auto-drop: it escalates to the user on the Pipeline for their call.
   - *Section fidelity:* the tailored resume keeps the master resume's sections and placement. Rework bullets and summary; never move content across sections.
   - *Mechanical ATS check:* one page; all text selectable; standard section headers; no tables, text boxes, graphics, or multi-column layouts; the posting's keywords mirrored verbatim in summary, skills, and lead bullets.
   - *Style checklist:* past tense throughout, including the current role; every bullet leads with a strong action verb and no lead verb repeats in the document; quantified results retained wherever the record supports them; no personal pronouns; standard sections; one page. Report each item explicitly; a fail on any item blocks clearance.
   - The reviewer also covers application text answers, not just the documents.
3. **Loop.** The writer addresses each objection concretely; the reviewer re-checks. Max 3 rounds. If the package still fails, or the gap is declared unbridgeable, escalate to the user with the specific objections. Never submit a failed draft; never silently drop it.
4. **Cover letter critic.** After the reviewer passes the resume, a dedicated pass checks the letter: company specificity (could this letter only be for this company?), no generic flattery, human voice, no repetition of resume bullets, a real and grounded why-us. One trip back to the writer max.
5. **Screener (cold reader).** A final pass that reads the resume cold, with the posting but none of the internal context. In a six-second skim: what does this person do, and does the fit for this role land? Minor fixes only, one trip back to the writer max. A structural problem found here means the reviewer's framing checks were too generous; fix the materials and note the pattern for the playbook.
6. **Audit.** Periodically re-run the reviewer against already-submitted materials to keep the reframing playbook honest.

## Posting liveness

Verify open roles against official sources instead of trusting the tracker's last-seen state:

- **Rung 1 (scripted, cheap):** the official ATS APIs (Greenhouse, Lever, Ashby board and posting endpoints) for roles hosted there.
- **Rung 2 (uncertain):** bot-defended portals, aggregator-sourced URLs, custom boards, roles with no posting URL. These get browser verification, never trust.
- Closure requires positive evidence from the official source: an explicit not-found or expired response from the employer's own ATS, an official page stating the role is closed, or an official board listing checked twice with the role absent both times.
- A failed fetch, timeout, bot-defense response, empty board, or any other rung-2 result is an *uncertain* verdict, never a closure. Record uncertain roles as uncertain, leave them in Pipeline for a later recheck, and report them as their own count, never folded into drops.
- Confirm every rung-1 negative a second way before closing the role, and record the evidence (the official URL checked and what it returned) in the dropped-roles entry so the drop can be audited later.
- One pass of negative or uncertain output is not proof a posting died. False drops have to be rebuilt by hand; closures are the expensive mistake, so they carry the burden of proof.

## Output contract

New opportunities as a short list, one line each: **Company, Title** (location, pay), then the official link. Lead with the strongest fits. Do not pad with borderline roles. Mark "comp unverified" where the range is genuinely missing after the full-text scan.
