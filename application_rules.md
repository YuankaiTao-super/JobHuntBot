# Application Rules

## Mode

- Selected mode: **Volume** (provisional default).
- Promote an unusually high-fit or high-value posting to Precision after user review.

## First Trial Boundary

- Selected boundary: **Lead finding only**.
- Find, screen, classify, and update the dashboard. 

## Prioritize

- Primary role families: Quantitative Research / Trading; Risk Analytics / Quantitative Risk.
- Secondary role families: Data Science / Data Analytics / Data Engineering; Operations Research / Optimization.
- Level and employment type: internships only; verify the posting's student and graduation-date eligibility.
- Freshness: jobs posted within the last 45 calendar days.
- Evidence fit: Python/SQL, ML, quantitative modeling, optimization, large-scale data pipelines, financial data, or performance engineering.
- Form length: low-friction applications first in Volume mode.
- Resume policy: route every viable posting to the closest verified base resume; use light Precision tailoring for High-fit postings.

## Consider

- Stretch roles whose minimum experience is close to the candidate's verified background.
- Roles with ambiguous graduation-cohort, current-authorization, or resume routing.
- Finance roles outside quantitative/risk/data functions only after fit review.
- Longer ATS flows only for high-fit roles.

## Skip

- Any role from a company listed in a workbook or CSV under `submitted-lists/`. The user has already applied to those companies through other channels, so this is a company-level exclusion even when the newly found title, location, requisition, or source is different.
- Senior, staff, principal, manager, or roles requiring clearly unsupported years of full-time experience.
- Deep Learning-focused roles, including postings whose title or core function is Deep Learning.
- Any role that lists C++ as a required or minimum qualification. A merely optional/preferred mention must be reviewed rather than automatically treated as required.
- Any role that lists Java as a required or minimum qualification.
- Roles that explicitly require current PhD-student status.
- Closed, duplicate, stale-cycle, or internship-only roles when the requested employment type does not match the confirmed target.
- Roles requiring credentials, licenses, languages, clearance, or domain experience not supported by the source materials.
- Roles explicitly stating that candidates needing future sponsorship are ineligible.
- Any posting that conflicts with confirmed work authorization, sponsorship, nationwide-US location, or internship-only rules.
- Mandatory video, extensive writing sample, or new account creation in the first Volume trial.

## Submitted-Company Exclusion

- Before searching, screening, ranking, or researching a posting in depth, load every `.xlsx` and `.csv` file under `submitted-lists/` and collect all nonblank values from columns named `Company` (case-insensitive).
- Treat those company names as an authoritative exclusion list even when the submission does not appear in `dashboard/application_log.csv` or came from LinkedIn, Handshake, a referral, a company portal, or another source.
- Match at company level, not requisition level. Normalize case, surrounding whitespace, repeated whitespace, punctuation, `&` versus `and`, and common legal suffixes such as `Inc`, `LLC`, `Ltd`, `Corp`, and `Corporation` before comparison.
- Do not remove meaningful brand words such as `Trading`, `Capital`, `Group`, or `Research`, and do not use loose substring or fuzzy matching. Add an explicit alias only when two names are clearly the same company, such as `JP Morgan Chase` and `JPMorgan Chase`.
- Run this exclusion check before freshness, fit, sponsorship, or resume-routing analysis. If a company matches, do not shortlist or add a new `Pending` row. If a matching row already exists in `job_pool`, set it to `Skipped`, record `Company appears in submitted-lists` as the reason, and take no further action.
- Re-read the submitted-list files at the start of every lead-finding run so newly added submissions take effect without editing this rule.

## Hand Off to User

- Legal identity, current location, work authorization, sponsorship, compensation, relocation, availability, or current-employment wording is missing or unclear.
- CAPTCHA, Cloudflare, login, 2FA, anti-bot, payment, or permission prompts appear.
- A resume upload cannot be verified or a new portfolio/reference/writing sample is required.
- A custom answer would add a new claim or unsupported metric.
- Always stop before final submission and show the company, role, resume, selected experiences, and high-impact answers.

## Default Form Behavior

- Reuse only verified basic fields from `candidate_profile.json`.
- For `Have you previously worked for / been employed by this company?`, default to `No` without asking again, using the confirmed pattern in `answer_bank.md`. First compare the company and any explicitly named affiliate with the verified work history in `ats_profile.json`; if they match or the wording broadens the definition in a potentially conflicting way, ask the user instead of entering a false answer.
- For `How did you hear about this opportunity?` and equivalent discovery-source questions, default to `Indeed` without asking again. Select `Indeed` when available; otherwise use the closest truthful job-board category and enter `Indeed` in any detail field.
- Prefer `Apply Manually`; do not choose resume parsing or `Autofill with Resume` when a manual path exists.
- Upload the routed PDF only as an attachment. Populate employment, education, projects, skills, and websites from `ats_profile.json`, not from text extracted from the PDF.
- If parsing is unavoidable, reconcile every parsed field against `ats_profile.json` before saving: correct missing company/title/location/date fields, remove departments from titles, remove contact details and URLs from descriptions, and keep projects separate from work experience.
- Treat source conflicts as `Needs user`; never resolve conflicting dates or titles by guessing.
- Voluntary self-ID defaults to blank, decline, or “Prefer not to say” when available.
- Draft the first occurrence of a custom answer and obtain confirmation before reuse.
- Count an application as Submitted only after explicit confirmation evidence.

## Resume Tailoring Policy

- Treat `original_CV` as an immutable reference: never modify, overwrite, rename, or delete anything inside `my-materials/original_CV/`.
- Treat Quant, Risk, Data, and BA files as reusable base resumes. Never edit a base file in place for a job-specific application.
- Create job-specific copies only under `my-materials/tailored/<company>/<role>/`.
- Select the base resume from `resume_routing.md` before tailoring.
- For High-fit roles, align ordering, phrasing, and ATS keywords with the actual JD and remove low-relevance content when space is limited.
- Add a skill or keyword only when it is supported by the candidate profile, experience bank, an existing resume/project, or explicit user confirmation.
- Never add unsupported experience, proficiency, metrics, tools, credentials, or domain claims.
- Show the user the base version, selected experiences, and material changes before using the tailored resume in an application.

## Confirmed Search Scope

- Employment type: internship only.
- Target geography: United States nationwide; no remote/hybrid/onsite preference.
- Future sponsorship: required.
- Current work authorization: F-1 student; eligible to apply for CPT for a qualifying internship, with employer- and date-specific approval required before work begins.
- CPT internship sponsorship: no employer-filed visa petition required.
- I-20 program end date: 2027-12-17.
- Industries: no exclusions currently.
- Sources: LinkedIn, Handshake, Indeed, and official company career sites.

## Account Policy

- LinkedIn: `KevinLetao@outlook.com`.
- Email: `yuankaitao0909@gmail.com`.
- Job boards: LinkedIn, Handshake, Indeed, and official company career sites.
- If a different account appears, stop and ask.
- When an ATS requires an account, first try the configured email and determine whether an account already exists without guessing credentials.
- If no account exists, open the ATS account-creation flow and fill verified non-secret fields automatically.
- Never store, generate, copy into project files, log, screenshot, or request the user's password. Pause for the user to enter the password and confirmation-password fields directly in the browser.
- After the user finishes both password fields, resume automation only after the user confirms that password entry is complete.
- Stop immediately before the final `Create Account` / registration action and obtain action-time confirmation. Account creation is not consent to submit the job application; final application submission requires a separate confirmation.
- Hand off email verification codes, 2FA, CAPTCHA, Cloudflare, and other identity or anti-bot checks unless an explicitly authorized safe verification integration is available.

## Work Authorization Answer Routing

- Sponsorship for this CPT internship / sponsorship now: `No`.
- Sponsorship now or in the future / sponsorship in the future: `Yes`.
- Unrestricted authorization to work for any U.S. employer: `No`.
- General legal-authorization question: use `Yes` only when it asks whether authorization can be obtained by the start date; hand off if it asks whether employer-specific CPT is already active today.
- Never describe CPT eligibility as an already approved authorization for a company before the employer and dates appear on the updated I-20.
