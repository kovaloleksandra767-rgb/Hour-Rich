---
name: manage-email
description: Scan Gmail, categorize emails (brand deals, important, noise), draft partnership replies with manager CC, and manage your inbox. Use anytime you want to check or triage email — not just mornings.
---

# Manage Email

Inbox triage — scan recent emails, surface brand deal inquiries, draft templated replies that loop in your brand manager, highlight what matters, and flag the noise.

---

## Config

| Key | Value |
|-----|-------|
| Brand Manager Email | Mkmmediaagency@gmail.com |
| Brand Manager Name | Mo |
| Your Name | Noe |
| Scan Window | 24-48 hours |

---

## Process

### Step 1: Scan Recent Emails

Search Gmail for all emails from the last 48 hours using multiple queries in parallel:

**Query 1 — Brand deal keywords:**
```
newer_than:2d (collaboration OR partnership OR sponsorship OR sponsor OR "brand deal" OR "paid promotion" OR influencer OR campaign OR UGC OR "creator program" OR "paid collab" OR "paid partnership" OR "would love to work" OR "interested in working")
```

**Query 2 — All recent inbox emails:**
```
newer_than:2d in:inbox
```

Use `gmail_search_messages` for both queries. Paginate if needed to get all results.

### Step 2: Read and Categorize

Read the full content of each email using `gmail_read_message`. Categorize every email into one of three buckets:

#### Brand Deal / Partnership Inquiry
Emails from brands, agencies, or creators proposing paid collaborations, sponsorships, UGC deals, or influencer campaigns. Match on:
- Keyword hits from the brand deal search
- Context clues: mentions of "rate card", "deliverables", "compensation", product pitches with partnership intent
- Sender domain is a company/agency (not a personal Gmail unless clearly a brand rep)

#### Important (Action Needed)
Non-brand emails that still need attention:
- Client communication (Agency work)
- Team messages (Trevor, Drew)
- Financial / legal (invoices, contracts, bank)
- Platform notifications that require action (account issues, policy changes)
- Personal emails from known contacts

#### Noise (Skip/Archive)
- Marketing newsletters you didn't opt into
- Automated promotional emails
- Generic SaaS upsells
- Social media digest notifications
- Spam that made it through filters

### Step 3: Present the Summary

Output a structured report:

```
## Email Report — [Date]

### Brand Deal Inquiries ([count])
For each:
- **From:** [Name] <[email]> — [Company/Brand]
- **Subject:** [subject line]
- **Summary:** [1-2 sentence summary of what they want]
- **Draft reply:** Ready / Needs review

### Important ([count])
For each:
- **From:** [Name] — [Subject]
- **Why it matters:** [1 sentence]
- **Action needed:** [what to do]

### Noise ([count])
- [Sender — Subject] (x[count] if multiple from same sender)

### Stats
- Total emails scanned: X
- Brand deals: X | Important: X | Noise: X
```

### Step 4: Draft Brand Deal Replies

For EACH brand deal email, draft a Gmail reply using `gmail_create_draft`:

**Template:**
```
Hey [First Name],

Thanks for reaching out — appreciate the interest in working together.

I'm CCing my manager Mo (Mkmmediaagency@gmail.com) who handles all of my partnerships. He'll take it from here.

Hope to be working together soon!

Thanks,
Noe
```

**Draft settings:**
- Reply to the original message (use the message ID as `inReplyTo`)
- CC: Mkmmediaagency@gmail.com
- Keep the original subject line (Re: ...)

Present each draft for review before creating. If the user approves, create all drafts.

### Step 5: Inbox Cleanup & Organization (via n8n Webhooks)

After the user reviews the summary, take these actions with user confirmation.

**n8n Webhook URLs (LIVE — tested and working):**
- **Star messages:** `POST https://YOUR-N8N-INSTANCE.app.n8n.cloud/webhook/gmail-star` (workflow `YOUR_WORKFLOW_ID`)
- **Mark as read:** `POST https://YOUR-N8N-INSTANCE.app.n8n.cloud/webhook/gmail-mark-read` (workflow `YOUR_WORKFLOW_ID`)

**Payload format (both endpoints):**
```json
{"messageIds": ["id1", "id2", "id3"]}
```

**IMPORTANT: Use Bash with curl to call these. Do NOT use WebFetch (it only does GET).**
```bash
curl -s -X POST "https://YOUR-N8N-INSTANCE.app.n8n.cloud/webhook/gmail-star" \
  -H "Content-Type: application/json" \
  -d '{"messageIds": ["id1", "id2"]}'
```

**Actions:**
1. Collect all Brand Deal + Important message IDs → POST to `/webhook/gmail-star`
2. Collect ALL handled message IDs (Brand Deal + Important + Noise) → POST to `/webhook/gmail-mark-read`

Present the count before executing: "Ready to star X emails and mark Y as read. Proceed?"

---

## Edge Cases

- **Existing brand deal threads** (Hostinger, Chatly, Chatbase, Sticker) — flag these as "Active Deal Update" rather than new inquiry. Do NOT send the template reply to ongoing conversations.
- **Ambiguous emails** — If unclear whether brand deal or spam, include in the summary with a "?" flag and let the user decide.
- **No brand deals found** — Still present the Important vs Noise breakdown.
- **Duplicate threads** — Group by thread, don't list each reply separately.
