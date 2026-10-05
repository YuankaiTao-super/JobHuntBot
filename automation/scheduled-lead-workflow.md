# Scheduled Lead-Finding Workflow

Timezone: `America/New_York`
Email account and recipient: `yuankaitao0909@gmail.com`

Both scheduled runs must read the current `SKILL.md`, `application_rules.md`, `candidate_profile.json`, `resume_routing.md`, `experience_bank.md`, all files under `submitted-lists/`, and the dashboard CSV files before acting. Current project rules always take precedence over this orchestration file.

## 09:00 Daily Search

1. Run in lead-finding-only mode. Never open an application flow, create an ATS account, upload a resume, fill an application, or submit anything.
2. Rebuild the submitted-company exclusion set from every `.xlsx` and `.csv` under `submitted-lists/`, then exclude those companies and existing job-pool duplicates before deeper research.
3. Find 8-10 currently open internships that satisfy the latest screening rules. Prefer the freshest postings within the configured freshness window. Verify each role from the official company posting and use web search only as corroboration.
4. For each lead capture: company, title, provisional role family, level, location, remote policy, official URL, posted date when available, priority, resume route, fit summary, eligibility/sponsorship notes, and recommended next action.
5. Write the shortlist to `automation/daily-lead-review.json` with today's date, `status: "pending_user"`, and the complete staged candidate records. Do not modify `dashboard/job_pool.csv`, `dashboard/daily_dashboard.csv`, or `dashboard/application_log.csv` at this stage.
6. Present the numbered shortlist in the scheduled-task result and ask the user to confirm it or identify specific numbers to replace before 09:25.
7. Send an email from the connected personal Gmail account to `yuankaitao0909@gmail.com` with subject `JobHuntBot 09:00 岗位待确认 - YYYY-MM-DD`, including the numbered shortlist and a reminder to confirm or request replacements before 09:25.

If fewer than 8 valid roles can be verified, report the actual number and the limiting rule; never pad the list with weak, closed, duplicate, submitted-company, or fabricated roles.

## User Review Between 09:00 and 09:25

- If the user confirms, commit only the latest staged candidates to `dashboard/job_pool.csv`, classify them under the current role-family rules, update `dashboard/daily_dashboard.csv`, and set the state to `confirmed_committed`.
- If the user rejects N identified leads, remove them, find exactly N replacements under the same rules, update the staged JSON, and present the revised numbered list. Do not commit until the user confirms or the cutoff task runs.
- Deduplicate by official URL and conservative company/title matching before every write.

## 09:25 Reminder and Cutoff

1. Read `automation/daily-lead-review.json` and verify that its date is today.
2. Send an email from the connected personal Gmail account to `yuankaitao0909@gmail.com` with subject `JobHuntBot 09:25 岗位确认提醒 - YYYY-MM-DD`. State whether the shortlist is awaiting confirmation, already committed, or unavailable.
3. Post the same concise status reminder in the scheduled-task result.
4. If today's state is `pending_user`, commit the latest staged candidates to `dashboard/job_pool.csv`, classify them, update `dashboard/daily_dashboard.csv`, and set the state to `auto_committed` with a timestamp.
5. If today's state is already `confirmed_committed` or `auto_committed`, do not add duplicate rows. If there is no valid current-day state, report the blocker and do not invent jobs.
6. Never modify `dashboard/application_log.csv` and never open or submit an application.

## Git Sync After Local Updates

- After any successful local file update from the 09:00 search, user-confirmation flow, replacement flow, or 09:25 cutoff, stage only the files changed by that run.
- Verify that `dashboard/application_log.csv` was not modified unless a separate, explicitly authorized application workflow changed it.
- Commit the scoped changes on the current branch with a concise message that includes the run date, then push that branch to the `origin` GitHub remote.
- Never include unrelated working-tree changes in the commit. If commit or push fails, preserve the local changes or local commit and report the exact blocker; do not claim that GitHub is up to date.

## Scheduled Task Definitions

Create both tasks for this local project in the current chat:

- `JobHuntBot 09:00 Daily Lead Search`
  - Schedule: `RRULE:FREQ=DAILY;BYHOUR=9;BYMINUTE=0`
  - Prompt: `Read automation/scheduled-lead-workflow.md and execute only the section "09:00 Daily Search" for today's date. Return to this chat.`
- `JobHuntBot 09:25 Review Cutoff`
  - Schedule: `RRULE:FREQ=DAILY;BYHOUR=9;BYMINUTE=25`
  - Prompt: `Read automation/scheduled-lead-workflow.md and execute only the section "09:25 Reminder and Cutoff" for today's date. Return to this chat.`
