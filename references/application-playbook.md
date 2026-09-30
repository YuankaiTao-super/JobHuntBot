# Application Playbook

Use this reference for browser-based job applications, LinkedIn Easy Apply, Simplify, Greenhouse, Lever, Ashby, Workday, and other ATS pages.

## Global Rules

- Count only confirmed submissions.
- Prefer short, reliable paths over long custom forms.
- Close each completed or skipped job tab before moving on.
- Keep only tabs that need user handoff.
- Record every outcome in the dashboard.
- Stop rather than bypass verification or guess high-impact answers.
- Do not create separate "test" and "normal" behavior modes. Use one default behavior: automate clear low-risk fields, ask focused questions for missing high-impact facts, and always stop before final submit.
- Prefer `Apply Manually` over `Autofill with Resume`. The resume is an attachment, not a form-data source.

## Form Answer Defaults

- Basic fields with clear profile values can be filled automatically: name, email, phone, LinkedIn, location, resume upload, and start date.
- Populate structured employment, education, project, skill, and website fields from `ats_profile.json`. Do not derive them live from PDF reading order.
- Work authorization, sponsorship, and compensation can be filled only when wording matches the profile or answer bank closely.
- Voluntary self-ID defaults to blank, "Prefer not to say", or decline/skip when available unless the user configured exact answers.
- Custom questions should use answer-bank patterns when available. If no pattern exists, draft the specific answer and ask the user to confirm it.
- Final submit always requires user approval. Show a concise summary before the final click.

## Low-Friction Applications

Volume mode and first real application tests should prefer low-friction applications:

- No new account creation.
- Not Workday, Oracle, or another long enterprise ATS by default.
- No video, long writing sample, or mandatory portfolio submission.
- At most one custom question.
- Clear resume upload and final confirmation path.
- No CAPTCHA, Cloudflare, login, or 2FA interruption.

This is a prioritization rule, not a permanent ban. In Precision mode, a high-value role may justify Workday, Oracle, long forms, or deeper custom work after the user confirms it is worth the extra time.

## Automation Ladder

Use the fastest reliable method first, then escalate only when needed:

1. Browser automation / Playwright-style control: best for batch work, normal buttons, form fields, tab cleanup, and repeatable ATS flows.
2. DOM plus keyboard repair: use Escape, Tab, Enter, arrow keys, and real option selection when dropdowns or overlays misbehave.
3. Visual or computer-use control: use when the page state matters visually, buttons are covered, dropdowns are custom, uploads are silent, or DOM state and visible state disagree.
4. User handoff: use for CAPTCHA, Cloudflare, login, 2FA, sensitive legal questions, missing materials, or permission prompts.

Playwright is an implementation detail, not the user-facing concept. Describe it to users as fast browser automation unless they ask for the technical details.

## Manual ATS Entry Contract

1. Choose `Apply Manually` whenever the ATS offers it.
2. Fill identity/contact fields from `candidate_profile.json` and structured resume fields from `ats_profile.json`.
3. Upload the routed PDF only in the attachment section and verify the displayed filename.
4. Keep `work_experiences`, `research_experiences`, `projects`, `education`, `skills`, and `websites` in their matching ATS sections. Never convert a project into employment merely because an ATS lacks a project section.
5. Departments belong in a department field or role description, never in company or job title. URLs belong only in website/social fields.
6. Before leaving an experience page, verify each visible record has the expected company, title, location, dates, current-role flag, and description.
7. If an ATS forces PDF parsing, overwrite its output from the structured sources and delete parser artifacts before saving.

### ATS Skills and Tag Fields

Use the structured `skills` object in `ats_profile.json`; do not extract a new skill inventory from the PDF or copy every keyword from the JD.

1. Identify the routed role family and its priority list.
2. Build the candidate list from verified inventory only: JD required matches first, JD preferred matches second, then remaining role-family priorities.
3. Respect the ATS limit. If no limit is shown, add no more than 15 skills and stop when relevant verified skills are exhausted.
4. For typeahead or controlled dropdowns, type one skill at a time, wait for suggestions, and click the exact canonical skill or a configured alias. If neither appears, skip it.
5. For genuine free-text tag inputs, enter the canonical skill and use the field's supported action such as Enter or comma to commit it.
6. Do not add duplicates, proficiency levels, years of experience, C++, Java, credentials, or other claims unless the structured profile explicitly supports them.
7. Before continuing, verify that the field displays committed tags rather than raw text. Add the final selected-skill list to the pre-submit summary.

## The 10 Common Cardpoints

### 1. Permissions

Before long runs, verify that the agent can click, read pages, switch tabs, and upload files. Also verify browser extension permissions for the target websites.

If permissions fail mid-run, record the exact permission needed and stop that application.

### 2. Dropdowns That Look Selected But Are Not

ATS dropdowns may show a value visually while internal validation still fails.

Try:

- Press Escape to close autofill overlays.
- Click the real dropdown option text.
- Use keyboard navigation.
- Use visual/computer control if ordinary DOM interaction fails.
- After fixing, verify that the site no longer reports the field invalid.

If the same field repeatedly fails, record a blocker instead of burning time.

Education field-of-study dropdowns:

1. Read the verified major from `ats_profile.json` and search for that exact option first.
2. If the field accepts free text, enter the verified major and do not use a fallback.
3. If a required dropdown does not contain the verified major, check `field_of_study_form_fallbacks` in `ats_profile.json` and select only the mapped value. The confirmed mappings are `Operations Research` -> `Statistics` and `Quantitative Finance` -> `Finance`.
4. Do not edit the canonical education record to match the dropdown. Record the substituted display value for the pre-submit summary.
5. If no exact or configured fallback option is available, stop and ask the user rather than improvising another major.

### 3. Address and Option Matching

Address fields may require full names, abbreviations, city, state, country, or localized text.

Try in this order, adapted to the user's profile:

1. Full city, state, country.
2. City only.
3. State only.
4. Country full name.
5. Country abbreviation.
6. Local-language variant if relevant.

For autocomplete fields, type, wait for candidates, then select a candidate. Do not submit raw typed text unless the site accepts free text.

### 4. Simplify or Extension Overlay Blocks Buttons

If Next, Review, or Submit does not respond:

- Close the Simplify side panel or other overlay.
- Focus the button and press Enter.
- Retry once.
- If still blocked, record a blocker.

Do not count an application as submitted unless the confirmation rule passes.

### 5. Close Completed Windows or Tabs

After each job is submitted, skipped, or blocked, close no-longer-needed tabs. This keeps memory, page scripts, and agent context under control.

Only keep tabs open when the user must act, such as CAPTCHA, login, upload, or final manual review.

### 6. Define Submission Success Strictly

Submission evidence can include:

- Visible text like `Application submitted`, `Application sent`, or `Thank you for applying`.
- A thank-you page.
- URL patterns like `thanks`, `thank-you`, `submitted`, or `confirmation`.
- A platform status that clearly says the application was sent.

Do not count:

- Saved jobs.
- Job trackers.
- Simplify quick apply labels.
- Autofill completion.
- A clicked submit button with no confirmation.

### 7. Email Verification vs CAPTCHA / Cloudflare

Email security codes may be handled if the user has connected an email tool and authorized code retrieval.

CAPTCHA, hCaptcha, reCAPTCHA, Cloudflare, and anti-bot checks must be treated as user handoff. Do not bypass them.

### 8. Login Sessions and Account Choice

If a login page appears, stop and record `Login required` or `Session expired`.

Do not attempt automatic login unless the user explicitly instructs it and the flow is safe. If multiple LinkedIn or email accounts exist, use the account specified in the candidate profile or rules.

When the user has enabled ATS account creation for a focused application:

1. Try the configured email first and determine whether an account already exists.
2. If it does not, open the registration form and fill only verified, non-secret profile fields.
3. Pause while the user enters the password and confirmation password directly in the browser. Never store, log, screenshot, generate, or ask the user to send the password through chat.
4. Obtain action-time confirmation immediately before clicking the final `Create Account` or equivalent registration control.
5. Treat email verification, 2FA, CAPTCHA, Cloudflare, and other identity or anti-bot checks as handoff points unless an explicitly authorized safe verification integration is available.
6. After account creation succeeds, continue the application, but still stop separately before the final job-application submission.

### 9. Resume Upload Verification

After uploading a resume, verify the file is attached before submitting.

Watch for:

- Sites that accept PDF only.
- Custom upload widgets.
- Silent upload failure.
- Wrong resume variant attached.
- Browser permission failure.

If upload cannot be verified, mark `Needs user` or `Blocked`; do not submit without a resume unless the user explicitly allows it.

Resume upload and resume parsing are separate decisions. Upload the correct routed PDF, but decline parsing/autofill when a manual-entry path exists.

### 10. Goal Mode Expectations

Goal-style runs are best for volume mode and short application flows.

Expect the agent to skip or defer:

- Workday or Oracle account-heavy flows.
- Long custom applications.
- Forms requiring missing materials.
- Login, 2FA, CAPTCHA, or Cloudflare.

For high-value target roles, use a focused run instead of a volume goal.

## Common ATS Notes

### LinkedIn Easy Apply

- Prefer fresh filters and direct apply flows.
- Close overlays before clicking Next, Review, or Submit.
- Count only after visible submitted/sent confirmation.

### Greenhouse

- Dropdown validation may be stale even when the page looks correct.
- Confirm required fields visually before retrying submit.
- If invalid state persists, record exact field and blocker.

Greenhouse email security code SOP:

- Use only when the user authorized email access.
- Read the latest Greenhouse security code from email.
- Locate each single-character security input when possible.
- Clear each box before typing.
- Enter one character per box using focused keypresses rather than bulk paste.
- Read the values back and verify the joined code exactly matches the email code.
- Submit only after verification.
- If characters duplicate, show as `undefined`, fail to clear, or cannot be verified, stop and hand off to the user.

### Lever

- Watch for hCaptcha or final confirmation pages.
- Count only explicit confirmation or thank-you page.

### Ashby

- Often requires resume upload.
- Verify upload before continuing.
- Record file permission blockers exactly.

### Workday / Oracle / Enterprise ATS

- Skip or defer long login-heavy flows unless fit is strong.
- Record maintenance, account creation, or login blockers.
