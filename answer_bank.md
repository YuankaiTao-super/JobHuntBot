# Answer Bank

Status: initialized draft. High-impact answers are intentionally blocked pending user confirmation.

## Work Authorization

- Status: **F-1 student**.
- CPT: eligible to apply for CPT for a qualifying internship; the user reports no anticipated CPT eligibility issue.
- I-20 program end date: **December 17, 2027**.
- Employer-specific boundary: work may begin only after CPT is approved for that employer and dates and appears on the updated I-20.
- `Are you at least 18 years old?`: **Yes**.
- `Are you legally authorized to work in the United States?`: **Yes** .
- `Do you have legal authorization to work in the country in which you are applying`:**Yes**
- `Are you authorized to work for any employer without restriction?`: **No**.

## Sponsorship

- Confirmed fact: **Future sponsorship is required.**
- `Will you require sponsorship for this CPT internship/current internship position?`: **No**.
- `Do you require sponsorship now?`: **No**.
- `Will you require sponsorship now or in the future?`: **Yes**.
- `Will you require sponsorship in the future?`: **Yes**.
- `Does the employer need to file a visa petition or pay sponsorship fees for this CPT internship?`: **No**.
- If a single question combines unrestricted authorization, current employer-specific authorization, and future sponsorship unclearly, ask the user rather than guessing.

Reusable explanation when a text field is provided:

> I am eligible to apply for CPT for a qualifying internship and expect to obtain employer-specific work authorization before the internship start date. CPT does not require the employer to file an employment-based visa petition. I may require employment visa sponsorship in the future.

## Location and Relocation

- Current address: `1025 Spring St NW, Atlanta, GA 30309, United States`.
- Search geography: United States nationwide.
- Work-location preference question: select **New York, NY** and **Chicago, IL** when available. If only one selection is allowed, choose **New York, NY** first, then **Chicago, IL**. If these two cities not available, choose the first selection.
- Relocation: open to locations across the United States; ask if a binding relocation commitment is required.
- `Are you willing to relocate?`: **Yes**.
- Remote/hybrid/onsite: no preference; all are acceptable.

## Compensation

- Default range: **20000 to 40000**.
- Deferral wording: “I am open to discussing compensation based on the role's scope, location, and total package.”
- Use that wording only when deferral is accepted; otherwise ask the user.

## Start Date

- Default answer: **2027-05-17**

## Prior Employment With the Applicant Company

- Status: **Confirmed by the user on 2026-09-30; reuse automatically.**
- Question patterns include:
  - `Have you previously worked for [Company]?`
  - `Have you ever been employed by [Company]?`
  - `Are you a former employee of [Company]?`
- Default answer: **No**.
- Use **No** without asking again when the question refers only to prior employment by the current applicant company.
- Truthfulness check: before answering automatically, compare the applicant company and any explicitly named affiliate against the verified employers in `ats_profile.json`. If there is an exact or clearly equivalent match, or the question expands employment to contractors, temporary workers, vendors, subsidiaries, or affiliates in a way that could include a verified experience, stop and ask the user instead of using the default.

## How You Heard About This Opportunity

- Status: **Confirmed by the user on 2026-09-30; reuse automatically.**
- Question patterns include:
  - `How did you hear about this opportunity?`
  - `How did you learn about this position?`
  - `Source of application` / `Source` / `Referral source` when the field is asking for the discovery channel.
- Default answer: **Indeed**.
- If the dropdown contains `Indeed`, select it.
- If `Indeed` is not available but a generic `Job board`, `Online job board`, or equivalent option is available, select that option and enter **Indeed** in any accompanying detail field.
- Do not select `Employee referral`, `Recruiter`, `University`, or another materially different channel when `Indeed` or a truthful generic job-board option is available.

## Education Field-of-Study Dropdown Fallbacks

- Status: **Confirmed by the user on 2026-09-30; reuse automatically.**
- Always search for and select the verified `field_of_study` from `ats_profile.json` first.
- If the ATS dropdown does not offer **Operations Research**, select **Statistics**.
- If the ATS dropdown does not offer **Quantitative Finance**, select **Finance**.
- These are form-option fallbacks only. Do not replace the true majors in `ats_profile.json`, `candidate_profile.json`, a resume, a free-text field, or an application summary.
- If a free-text field is available, enter the true major rather than the fallback.
- If neither the true major nor the configured fallback is available, stop and ask the user instead of choosing another field of study.

## Why This Company

- Search the company's official homepage and relevant official About, product, research, or values pages.
- Write and directly fill **3-4 concise sentences** connecting specific company facts with the candidate's verified quantitative, finance, data, optimization, or risk experience and the selected experiences for that role.
- Do not invent company facts or personal claims. No separate approval is required before filling; include the text in the final pre-submit preview.

## Background Defaults

- Relatives employed by the applicant company or its named affiliates: **No**.
- Criminal, conviction, offense, or unlawful-conduct history questions: **No**.
- Confirmed by the user on 2026-10-03; reuse automatically. If a question requests details beyond the yes/no fact, stop and ask rather than inventing details.

## Why This Role

Reusable draft pattern: “This role combines [verified strength 1] and [verified strength 2]. In [selected experience], I [verified action/result], and in [selected project], I [verified action/result]. That background fits the role's focus on [JD-specific responsibility].”

## Portfolio / Work Samples

- Homepage: `https://yuankaitao-super.github.io/`
- GitHub: `https://github.com/YuankaiTao-super`
- LinkedIn: `https://www.linkedin.com/in/yuankai-tao-211788328/`
- Ask before selecting a repository or presenting any work as a formal sample.

## Voluntary Self-ID

- Status: **Confirmed by the user on 2026-09-30; fill automatically and reuse without asking again.**
- Gender identity: select **Man**. If the equivalent option is `Male` or `Cisgender man`, select that equivalent.
- Sex, when asked separately from gender identity: select **Male**.
- Sexual orientation: select **Straight** or **Heterosexual**.
- Race or ethnicity: select **Asian**. If the form offers a more specific equivalent, select **East Asian**.
- Military status: select **Never served**, **No military service**, or the equivalent option meaning the candidate has not served in the armed forces.
- Veteran status: select **Not a veteran** or **Not a protected veteran**, according to the form's wording.
- Disability status: select **No, I do not have a disability**, **No disability**, or the equivalent non-disabled option.
- `Do you identify as part of the LGBTQ+ community?`: select **No**.
- Do not select `Prefer not to say` when an equivalent confirmed option is available.
- If a form combines categories unusually, asks for medical details or past disability history beyond the confirmed `No disability` answer, or offers no clearly equivalent option, stop and ask the user instead of guessing.
- These answers are private form data. Do not add them to resumes, cover letters, public profiles, or repository documentation intended for sharing.

## Custom Questions

| Question pattern | Reusable answer or pattern | When to customize |
|---|---|---|
| Relevant quantitative experience | Select 2–4 verified items from `experience_bank.md`; connect methods and results to the JD | Every job |
| Relevant data/ML experience | Select the closest pipeline/modeling/project evidence; do not list the full inventory | Every job |
| Leadership | Use UCSD/FMSbonds or SEC 10-K team-lead evidence where relevant | When leadership is requested |
