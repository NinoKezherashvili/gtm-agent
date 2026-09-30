# GTM Outreach Agent

This project runs personalised cold outreach entirely inside Claude Code, using the Gmail MCP connector to send emails.

## Files

| File                                           | Purpose                                                                      |
| ---------------------------------------------- | ---------------------------------------------------------------------------- |
| `prospects.csv`                                | Input list. Columns: `email`, `first_name`, `last_name`                      |
| `sent.json`                                    | Tracker. Every email sent or skipped is logged here immediately after action |
| `.claude/skills/draft-outreach-email/SKILL.md` | Drafting skill — writing only, no research or sending                        |

## Sender & product info

- **Your name / title / company:** [Your Name, Title, Company]
- **Product name:** [Product name]
- **One-sentence description:** [What it does]
- **Target customer:** [Who you sell to]
- **Pain point:** [Problem you solve]
- **Proof point:** [Traction, grant, result]
- **Call to action:** [e.g. 15-min demo — https://cal.com/yourname/15min]

## How to run outreach

Say **"run outreach"** and follow these steps:

### Step 1 — Load & deduplicate

Read `prospects.csv` and `sent.json`. Build a list of prospects whose `email` does not appear in `sent.json`. If everyone is already logged, report that and stop.

### Step 2 — Research

For each new prospect, use web search to find:

- Their current role and company (confirm from email domain)
- A recent, specific fact: news item, product launch, hiring announcement, talk, blog post, or public quote
- Keep only facts you actually found — do not assume or invent

Limit: maximum **20** prospects per run.

### Step 3 — Draft

For each prospect, invoke the `draft-outreach-email` skill (`.claude/skills/draft-outreach-email/SKILL.md`) passing:

- The prospect's full name
- The research findings
- The sender & product info above

The skill returns SUBJECT / BODY / HOOK, or SKIP + reason.

### Step 4 — Review

Display all drafts (or skip reasons) in a clear numbered list. **Wait for explicit approval before sending anything.**

Format each draft like this:

```
--- Draft 1: Jane Smith <jane.smith@acmecorp.com> ---
SUBJECT: ...
BODY:
...
HOOK: ...
```

Ask: "Send these N emails? (yes / edit N / skip N)"

### Step 5 — Send

For approved drafts, send each email using the Gmail MCP connector. After each send (success or error), immediately append an entry to `sent.json`:

```json
{
  "email": "jane.smith@acmecorp.com",
  "name": "Jane Smith",
  "date_sent": "2026-09-30",
  "subject": "...",
  "hook_used": "...",
  "status": "sent",
  "reason": ""
}
```

For skipped prospects (SKIP from skill, or user chose to skip), log `"status": "skipped"` with the reason.

### Step 6 — Summary

End with a short summary:

```
Run complete.
Sent: N
Skipped: N (list names + reasons)
Errors: N (list names + errors)
```

## Rules

- Never email the same address twice — always check `sent.json` first.
- Max 20 emails per run.
- Never send without explicit user approval in Step 4.
- Write `sent.json` after every individual action, not just at the end — so a crash mid-run doesn't cause duplicates.
- Keep emails under 120 words; subjects under 8 words.
- Do not invent research facts.
