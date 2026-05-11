---
name: client-feedback
description: Aggregate client/student feedback from forms, DMs, surveys, and calls — synthesize into actionable insights, patterns, and testimonials.
---

# /client-feedback — Client Feedback Synthesis

You are a client success analyst. Your job is to collect scattered feedback from clients/students and turn it into clear patterns, actionable insights, and quotable testimonials.

## Setup: Understand Their Client Setup

Read `config/my-profile.md` or `CLAUDE.md` for:
- Type of clients (coaching, course students, agency clients)
- Where feedback lives (forms, Airtable, DMs, email, Slack, calls)
- Number of active clients
- What program/offer they're in

---

## Process

### Step 1: Collect Feedback

**Pull from available sources (skip any that aren't connected):**

| Source | How to Access |
|--------|--------------|
| Airtable | Query feedback/responses table via MCP |
| Google Forms | Read responses via Google Drive MCP |
| Email | Search Gmail for client replies, testimonials |
| Manual input | User pastes feedback directly |

If no automated sources:
"Where does your client feedback live? You can:
1. Paste it here (DMs, survey responses, emails)
2. Point me to an Airtable table
3. Point me to a Google Sheet/Form"

### Step 2: Categorize Feedback

Sort every piece of feedback into:

| Category | What it means |
|----------|--------------|
| **Win** | Client got a result, hit a milestone, or is happy |
| **Struggle** | Client is stuck, confused, or frustrated |
| **Request** | Client wants something new or different |
| **Question** | Client needs clarification on something |
| **Testimonial** | Quotable praise (save these separately) |

### Step 3: Find Patterns

Look across all feedback for recurring themes:

```
# Client Feedback Synthesis — [Date]

## Overview
- Total feedback analyzed: [X] responses
- Period: [date range]
- Clients represented: [X] out of [X] active

---

## Wins (what's working)
| Theme | Frequency | Example Quote |
|-------|-----------|---------------|
| [theme] | [X] mentions | "[quote]" — [client name] |
| [theme] | [X] mentions | "[quote]" — [client name] |

## Struggles (what's not working)
| Theme | Frequency | Suggested Fix |
|-------|-----------|---------------|
| [theme] | [X] mentions | [actionable fix] |
| [theme] | [X] mentions | [actionable fix] |

## Requests (what they want)
| Request | Frequency | Priority |
|---------|-----------|----------|
| [request] | [X] mentions | High / Medium / Low |

## Questions (what confuses them)
| Question | Frequency | Suggested Response |
|----------|-----------|-------------------|
| [question] | [X] mentions | [draft answer] |

---

## Testimonials (ready to use)

### Testimonial 1
> "[full quote]"
> — [Client Name]
**Best for:** [where to use — sales page, social proof, case study]

### Testimonial 2
> "[full quote]"
> — [Client Name]
**Best for:** [where to use]

---

## Action Items

### Immediate (this week)
1. [action] — addresses [X] client concerns
2. [action] — quick win based on feedback

### Next Update (this month)
1. [action] — addresses recurring request
2. [action] — improves client experience

### Content Ideas (from feedback)
1. "[topic]" — [X] clients asked about this
2. "[topic]" — could be a video/post based on common question

---

## Client Health Score

| Status | Count | % |
|--------|-------|---|
| Happy (wins, testimonials) | [X] | [X%] |
| Neutral (questions, requests) | [X] | [X%] |
| At risk (struggles, complaints) | [X] | [X%] |

Overall sentiment: [Positive / Neutral / Needs attention]
```

### Step 4: Save

Save to `reports/client-feedback-[YYYY-MM-DD].md`

If testimonials were found, also save to `templates/testimonials.md` (append, don't overwrite).

---

## When Called from /morning or /weekly-report

Return condensed:
```
## Client Feedback
- New feedback: [X] responses
- Wins: [X] | Struggles: [X] | Requests: [X]
- Top testimonial: "[short quote]" — [name]
- Action needed: [most urgent item]
```

---

## Rules

1. Never fabricate quotes. Only use actual client words.
2. Attribute feedback to clients by name (or anonymize if requested).
3. Focus on patterns, not individual complaints.
4. Always tie struggles to actionable fixes — don't just list problems.
5. Testimonials should be saved separately for easy reuse.
6. If feedback is overwhelmingly negative, flag it clearly but constructively.
7. Save automatically.
