# Application Rules

## Mode

- Selected mode: **Volume** (provisional default).
- Promote an unusually high-fit or high-value posting to Precision after user review.

## First Trial Boundary

- Selected boundary: **Lead finding only**.
- Find, screen, classify, and update the dashboard. 

## Prioritize

- Primary role families: Quantitative Trading / Research; Risk Analytics / Quantitative Risk.
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

## Never Guess

- Legal identity, current employment status, notice period, or unconfirmed availability.
- Work authorization or sponsorship beyond the exact facts and question mappings already recorded.
- Compensation outside the confirmed answer-bank range or any required base-versus-total distinction not already confirmed.
- Binding relocation commitments, unsupported education or employment dates, non-compete matters, references, or background details.
- Voluntary self-identification beyond the exact confirmed answer-bank values and their clear equivalents.

## Default Form Behavior

- Prefer `Apply Manually`; do not choose resume parsing or `Autofill with Resume` when a manual path exists.
- Upload the tailored PDF only as an attachment. Populate identity, employment, education, projects, skills, and websites from `candidate_profile.json`, not from text extracted from the PDF.
- If parsing is unavoidable, reconcile every parsed field against `candidate_profile.json` before saving: correct missing company/title/location/date fields, remove departments from titles, remove contact details and URLs from descriptions, and keep projects separate from work experience.
- Treat source conflicts as `Needs user`; never resolve conflicting dates or titles by guessing.
- Use `answer_bank.md` as the single source for reusable form answers and confirmed dropdown fallbacks. Use an answer only when the form question has the same meaning and scope as the recorded pattern.
- Choose the closest semantically equivalent dropdown value, not merely the first option. Ask the user when the wording combines categories, materially broadens the recorded question, conflicts with verified data, or provides no clear equivalent.
- Draft an unlisted custom answer from verified sources and obtain confirmation before recording it for reuse.
- Count an application as Submitted only after explicit confirmation evidence.
- Reuse candidate facts and structured resume/application data only from `candidate_profile.json`; use `answer_bank.md` for confirmed response wording and fallbacks.
- For `Why this company?`, follow the research and drafting procedure in `answer_bank.md`, use official company sources, and include the completed text in the pre-submit preview.
- When a configured education fallback is used, leave the underlying education records unchanged and disclose the substitution in the pre-submit summary.
- Fill ATS `Skills`, `Add Skills`, `Type to Add Skills`, and equivalent tag fields automatically from `candidate_profile.json.skills.verified_inventory`; use only the aliases recorded in `answer_bank.md`. Rank verified skills that match required JD terms first, then preferred JD terms, then the routed role-family priority list in `resume_routing.md`; never add a JD keyword that is absent from the verified inventory and mappings.
- Use the ATS field's stated limit; when no limit is visible, add at most 15 skills. Avoid duplicates. For a controlled suggestion list, select the real offered option and try configured aliases when needed; skip the skill if no verified equivalent is offered. For a true free-text tag field, enter the canonical verified name.
- Verify that every skill appears as a committed tag rather than unsubmitted text, and include the selected skill list in the pre-submit summary.

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
- Sponsorship compatibility: screen each posting against the current work-authorization and sponsorship facts in `answer_bank.md`; skip explicit conflicts and hand off ambiguous eligibility language.
- Industries: no exclusions currently.
- Sources: LinkedIn, Handshake, Indeed, and official company career sites.

## Account Policy

- Use only the configured account identifiers in `candidate_profile.json`.
- If a different account appears, stop and ask.
- When an ATS requires an account, first try the configured email and determine whether an account already exists without guessing credentials.
- If no account exists, open the ATS account-creation flow and fill verified non-secret fields automatically.
- Never read, expose, copy into project files, log, screenshot, or request the user's password.
- When account creation requires a password, use password manager's native strong-password generator and save function. The automation agent must not inspect or extract the generated password or operate password-manager approval prompts.
- If generation, filling, or saving is unavailable or fails, pause for the user to resolve it; do not generate or retain a fallback password in the project.
- Stop immediately before the final `Create Account` / registration action and obtain action-time confirmation. Account creation is not consent to submit the job application; final application submission requires a separate confirmation.
- Hand off email verification codes, 2FA, CAPTCHA, Cloudflare, and other identity or anti-bot checks unless an explicitly authorized safe verification integration is available.

## Answer Ownership and Routing

- `answer_bank.md` owns reusable question patterns, concrete answers, option mappings, explanations, and form-specific fallbacks.
- `candidate_profile.json` owns stable candidate facts and structured identity, education, experience, project, skill, and website data.
- `application_rules.md` owns screening, routing, safety, verification, escalation, and submission-control rules. Do not copy concrete reusable answers into this file.
- Before reusing an answer, match the question's meaning, timeframe, employer scope, and requested level of detail to the corresponding `answer_bank.md` entry.
- If sources conflict or the question is broader than a confirmed pattern, stop and ask rather than choosing the most convenient answer.
- When the user confirms a new or changed reusable answer, update `answer_bank.md`; update this file only if the operating rule itself changes.
