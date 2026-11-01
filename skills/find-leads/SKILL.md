---
name: find-leads
description: >
  This skill should be used when the user asks to "find leads in my email",
  "who in my inbox could be a client", "scan my Gmail for leads",
  "check my email for new business", "any potential clients this week",
  "qualify my inbox", or runs /find-leads. It scans Gmail, identifies anyone who
  could become a paying client, researches their company from the email domain,
  and returns a ranked lead list (Hot / Warm / Cold) with next steps.
metadata:
  version: "0.1.0"
---

# Find Leads in Gmail

Scan the user's Gmail, find every sender who could plausibly become a client, research who they are, and hand back a ranked, actionable lead list.

## Lead definition (broad by design)

Treat as a lead ANY sender who asks about, hints at, or could reasonably need work the user can do.

Read `references/my-services.md` to learn what the user sells and which sectors they serve. If that file still contains the placeholder text, or the user has said what they do earlier in the conversation, use that instead; if neither is available, assume a software/web/app development business and say so in one line at the top of the report. Include:

- Direct inquiries: "need a website", "can you build", "quote for", "how much for an app"
- Indirect signals: complaints about an existing site/app, "our current vendor…", "looking for a developer", referrals ("X said you could help")
- Replies to the user's own outreach or proposals
- Existing clients mentioning new or additional work (upsell)
- Job/contract platform messages (Upwork, Freelancer, LinkedIn, Toptal, etc.) with a concrete project
- Partnership or white-label/agency subcontract offers
- Event/networking follow-ups where the person runs a business

Exclude: newsletters, marketing blasts, receipts, OTPs, system notifications, no-reply senders, job-board recruiter spam for full-time roles (unless the user asks), vendors selling TO the user, and the user's own sent mail.

## Workflow

### 1. Set scope
- Default window: last 14 days. Respect any range the user gives ("today", "this month", "since Oct 1").
- Load Gmail tools via ToolSearch if deferred: `select:mcp__Gmail__search_threads,mcp__Gmail__get_thread,mcp__Gmail__get_message,mcp__Gmail__list_labels,mcp__Gmail__create_label,mcp__Gmail__label_thread,mcp__Gmail__create_draft`.

### 2. Search the inbox
Run several Gmail searches rather than one, then merge by thread ID. Use queries from `references/gmail-queries.md`. Always add `-category:promotions -category:social -from:noreply -from:no-reply` and the date filter (`newer_than:14d` or `after:YYYY/MM/DD`).

### 3. Read and classify
For each candidate thread, read enough of the thread to judge intent. Record:
- Sender name, email, domain
- What they want (one line, in plain words)
- Budget, timeline, or urgency if mentioned
- Whether the user has already replied, and who spoke last
- Days since last message

Drop anything that is clearly not a lead. When unsure, keep it as Cold rather than dropping it.

### 4. Research the sender (professional info only)
- Business domain (not gmail/yahoo/outlook/hotmail/rediffmail/icloud): use WebSearch and WebFetch on the domain to find what the company does, industry, location, approximate size, and the state of their current website (outdated, slow, no mobile version, none at all — these are opportunities).
- Personal email domain: rely on the signature, the email content, and any company name they mention; search that company if named. Mark confidence as Low if nothing can be found.
- Stay with company and professional-role information. Do not dig into personal social media, family, home address, or anything unrelated to whether they could hire the user.

### 5. Score
Apply the rubric in `references/scoring.md` to assign Hot / Warm / Cold and a 0–100 score. Every lead gets a one-line reason.

### 6. Report
Present results in chat, sorted by score, using this layout:

**Summary line:** "Scanned N threads from <window>. Found X Hot, Y Warm, Z Cold leads."

Then a table: `# | Lead | Company / What they do | What they want | Score | Last contact | Next step`

Below the table, for each Hot lead only, a short card:
- Who they are (2 lines from research)
- Why they're a fit (tie to the user's services)
- Risks or unknowns (e.g. no budget mentioned, personal email)
- Suggested reply angle (one sentence)

Flag separately: "Waiting on you" — leads where the sender spoke last and the user hasn't replied in 2+ days.

### 7. Offer actions (never act without a yes)
After the report, offer in one line:
- Apply Gmail labels `Lead/Hot`, `Lead/Warm`, `Lead/Cold` (create labels if missing)
- Draft replies for the Hot leads (as Gmail drafts, never sent)
- Export the list to a sheet / tracker

Only perform these after the user confirms. Never send, forward, archive, or delete email.

## Output rules
- Keep it scannable; no long prose per lead.
- Do not paste whole email bodies; summarize intent in the user's terms.
- If zero leads are found, say so plainly and suggest widening the date window.
- If Gmail tools are unavailable, tell the user to connect Gmail in claude.ai connector settings.
