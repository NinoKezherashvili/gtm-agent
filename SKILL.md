# Skill: draft-outreach-email

## Purpose

Draft a single personalised outreach email. Do not research, send, or log anything — only write the email.

## Input

- Prospect's full name
- Research findings (a short list of facts you actually found about them, their role, company, and any recent news)
- Product/sender info (provided in the session or from CLAUDE.md)

## Output

Return exactly three labelled sections:

**SUBJECT:** (under 8 words)

**BODY:** (under 120 words total — see structure below)

**HOOK:** (one sentence explaining which specific detail was used as the opening hook)

## Email structure

1. Personal hook — open with one specific, genuine detail from the research (a recent launch, talk, hire, news item). Never use "I came across your profile."
2. The problem — one sentence on the pain point you solve for people in their position.
3. What we do — one sentence only.
4. Call to action — low-pressure ask (e.g. a 15-minute call with a booking link).
5. Opt-out line — end with: "If this isn't relevant, just let me know and I won't follow up."
6. Sign-off — [Your name, title, company] (filled in from session context).

## Rules

- Only use facts from the research provided. Never invent details or make assumptions.
- If the research is too thin to write a genuine personal hook, return "SKIP" on the first line and a one-sentence reason. Do not write a generic email.
- No hype, no buzzwords, no exclamation marks.
- Subject line must not start with "Re:" or "Quick question".
- Body must be plain text, no bullet points, no headers.
