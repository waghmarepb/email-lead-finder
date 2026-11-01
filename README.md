# Email Lead Finder

A Claude plugin that scans your Gmail for anyone who could become a client, researches their company from their email domain, and ranks them **Hot / Warm / Cold** with a suggested next step.

Built for freelancers, agencies and small businesses who don't want leads buried in their inbox.

## What it does
1. Runs several targeted Gmail searches: quote requests, project inquiries, referrals, Upwork/LinkedIn messages, replies to your proposals, and existing clients asking for more.
2. Filters out newsletters, receipts, OTPs, notifications and no-reply mail.
3. Looks up each sender's company from their email domain (professional info only).
4. Scores each lead 0–100 and groups them Hot / Warm / Cold, with a one-line reason.
5. Flags leads that are waiting on your reply.
6. With your OK, labels threads `Lead/Hot|Warm|Cold` and drafts replies as Gmail drafts.

**It never sends, forwards, archives or deletes email.**

## Requirements
- Claude with the **Gmail** connector enabled
- Web search enabled (for company research)

## Install

**Claude Code**
```
/plugin marketplace add waghmarepb/email-lead-finder
/plugin install email-lead-finder@email-lead-finder
```

**Claude app**
Download this repo as a ZIP, rename it to `email-lead-finder.plugin`, and open it in Claude — or add the repo as a plugin source from Claude's plugin settings.

## Make it yours (2 minutes)
Edit [`skills/find-leads/references/my-services.md`](skills/find-leads/references/my-services.md) with:
- the services you offer
- the sectors you already serve
- what you're not interested in

The plugin uses this to decide who counts as a lead and how well they fit.

## Usage
- `/find-leads` — scan the last 14 days
- "Find leads in my email from this month"
- "Who in my inbox could be a client?"

## Example output
| # | Lead | Company | Wants | Score | Last contact | Next step |
|---|------|---------|-------|-------|--------------|-----------|
| 1 | Dr. A. Patil | City Clinic — 3-branch clinic | Online booking app, quote | 86 Hot | 2 days ago | Send quote today |
| 2 | R. Mehta | Mehta Industries — CNC parts maker | "Our site looks old" | 58 Warm | 5 days ago | Offer redesign call |

## Customize further
- `skills/find-leads/references/scoring.md` — scoring rubric
- `skills/find-leads/references/gmail-queries.md` — search terms

## Privacy
Everything runs inside your own Claude session using your own Gmail connector. The plugin researches only company and professional information about senders.

## License
MIT © Pradip Waghmare
