# Resume Review

## Purpose

A standalone audit of the user's resume, run before the search starts and any time the master resume changes. Everything downstream (tailored variants, cover letters, application answers) is built from this document, so a defect here replicates into every application. This skill finds the defects. It reports and rewrites on request; it does not silently edit the master resume.

## Workflow

1. **Read the whole resume first.** No skimming, no comments until the full document is read. Note the user's field, level, and the story the document currently tells.
2. **Run the first-scan test.** Read it again the way a recruiter does: 6 to 8 seconds, top to bottom, no lingering. Report what a stranger takes away: what this person does, at what level, and the single strongest proof point. If the scan cannot answer those, that is the headline finding.
3. **Run the style checklist and report every item, pass or fail:**
   - Past tense throughout, including the current role.
   - Every bullet leads with a strong action verb, and no lead verb repeats anywhere in the document.
   - Tense and format are consistent across all roles (dates, punctuation, bullet style).
   - Results are quantified wherever the record supports a number, and every number is exact, never rounded into a different claim.
   - No personal pronouns.
   - Standard sections a parser expects: summary, experience, education, skills.
   - One page at the user's level, unless their field's norm is longer.
   - Any failure is a high-impact defect, not a nit. List each failure with the offending line.
4. **Separate factual defects from optional improvements.** Factual defects: wrong or inconsistent dates, titles that do not match the record, metrics that overstate, claims with no evidence behind them anywhere in the user's background. Optional improvements: ordering, wording, emphasis. Never present a taste call as a defect.
5. **Give a concrete before-and-after rewrite for every high-impact issue.** Show the original line and the replacement. A review that says "strengthen this bullet" without showing the stronger bullet has not done the work.
6. **Close with the prioritized fix list:** high-impact first, in the order the user should make them.

## JD-match mode

When the user provides a job description, add a match audit:

- List the posting's hard requirements in three groups: **matched** (evidenced on the resume), **missing** (no evidence anywhere in the user's record), and **mentioned without evidence** (the resume uses the word but no bullet backs it; screeners and interviewers both catch this).
- Mirror check: does the resume use the posting's own vocabulary for the things the user genuinely does? Where the same work is described in different words, show the swap.
- Flag any keyword whose honest use would require fabrication as **unusable**. Name it plainly. The answer to a missing requirement is a reframing of real experience (the rejection-review playbook) or accepting the gap, never a new claim.
- The match audit informs the resume-tailor skill; it does not replace it. Tailoring happens per application. This mode tells the user what tailoring can and cannot fix.

## Operating rules

- The master resume is ground truth for facts, but the review may question the resume itself: if a line on it cannot be evidenced, that is a factual defect and the most important kind.
- Never invent a metric, title, or scope to make a rewrite stronger. A rewrite uses only facts the user confirms.
- Report the checklist explicitly, item by item. A summary like "looks good overall" without the item results is not a review.
- Keep the report scannable: headline finding, checklist results, defects with rewrites, fix list. The user should be able to act on it without asking what to do first.
