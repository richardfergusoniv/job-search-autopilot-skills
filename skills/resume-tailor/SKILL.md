# Resume Tailor

Build a one-page resume variant tailored to a specific job description. Every fact must be verified against the user's master resume and bullet bank; rephrase and reorder freely, never invent.

## Workflow

1. **Read the posting.** Pull the full text from the employer's careers page, never an aggregator snippet. Extract:
   - The 8 to 12 hard requirements (methods, tools, domain knowledge).
   - The exact vocabulary the posting uses. Mirror it verbatim.
   - The top 3 responsibilities; these dictate bullet order.
2. **Rewrite the summary** (2 to 3 lines) to mirror the role: current title, years, the posting's core domain in its own words, one differentiator. Name the target function the way the posting names it.
3. **Select and order bullets** from the bullet bank by posting relevance. Lead each employer block with its most relevant bullet. Rephrase bullets into the posting's vocabulary where the underlying fact supports it.
4. **Tune the skills lines** to echo the posting's tools and methods, but only with tools the user actually uses (the bank lists them). Never add a tool they do not.
5. **Render** in the user's established resume format (their template, fonts, and layout live with their resume files; keep the format identical across variants so every application looks like the same person's resume).
6. **Verify:** one page, all text selectable (no images of text), standard section headers intact, no invented numbers, titles, or scope. Run the writing-style pass (below) over the final text.

## ATS-era rules

- Mirror posting keywords verbatim in the summary, skills, and lead bullets. Modern screeners do semantic matching, but exact terms still win ties.
- Standard headers only: SUMMARY, EXPERIENCE, EDUCATION, SKILLS, INTERESTS. No tables, text boxes, graphics, or multi-column layouts.
- Dense, plain-text bullet formatting that parses as normal text.
- File name pattern: `<Lastname>_Resume_<Company>_<Role>.pdf`.

## Style rules

- Past tense throughout, including the current role. Every bullet leads with a strong past-tense action verb, and no lead verb repeats anywhere in the document.
- Quantified results wherever the master resume supports them. Where the master gives a number, keep the number exact; never round, restate, or reinterpret a metric into a different claim (a count of models built is not a count of assets valued).
- No personal pronouns. No em dashes.
- Desired compensation never appears on a resume.

## Hard constraints

- The master resume is ground truth. Where the bullet bank or any other note conflicts with it, the master wins, and the bank gets corrected.
- Maintain a forbidden-claims list in the bullet bank: things the user does not do, has not done, or cannot evidence. The tailor never uses them, and the pipeline reviewer checks against the list.
- **Section fidelity:** the tailored resume keeps the master resume's layout, same sections, same placement of content. The job is reworking bullets and summary to tell the posting's story. Bullets may mention skills or tools from other sections, but items never move into new sections.
- Role-specific standing preferences (for example, which credential or coursework lines appear on which kind of resume) live in the user's profile, set during intake, and are applied from there, never assumed.
