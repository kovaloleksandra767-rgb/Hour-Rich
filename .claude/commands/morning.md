---
name: morning
description: Daily morning briefing across all 3 layers (Life, Business, Clients) — personal admin, journal prompt, email triage with drafts, content/ad stats, client updates, and task priorities. The unified Hour Rich morning brief.
---

# Morning Briefing — Hour Rich Edition

Your daily command center. Runs modules across all 3 layers (Life, Business, Clients), presents a single unified briefing.

---

## Config

| Key | Value |
|-----|-------|
| Timezone | America/Sao_Paulo (BRT, UTC-3) |
| Output | Terminal only |

---

## Process

### Module 0: Life Layer (Personal)

**Run FIRST — sets the tone for the day.**

**0A: Personal Admin (from /personal-admin)**
1. Check Google Calendar (if connected) for today's events and tomorrow's prep
2. Surface any personal reminders or time-sensitive items (bills, appointments, birthdays)

**0B: Journal Prompt (from /journal)**
1. Generate one personalized reflection prompt based on day of week and current context
2. Keep it to 2-3 lines max

**0C: Meal Plan Check (Mondays only, from /meal-planner)**
1. If it's Monday, generate this week's meal plan + grocery list
2. Other days: skip this section

**Output for briefing:**
```
## Life

### Schedule
- [time] — [event] (if any)
- No events today (if empty)

### Journal
> [Single reflection prompt]

### Meals (Mondays only)
- This week's plan ready — see reports/meal-plan-[date].md
- Grocery list: [X] items
```

---

### Module 1: Full Email Triage

**This is NOT a scan — run the FULL `/manage-email` process:**

1. Search Gmail for last 48 hours using **multiple queries** to catch everything:
   - `is:unread in:inbox` (all unread inbox — NO category filters)
   - `newer_than:2d subject:collab OR subject:partnership OR subject:sponsor OR subject:paid` (brand deal keywords)
2. **Deduplicate** results by message ID
3. **Read the full content** of every email using `gmail_read_message` — not just subject lines
4. Categorize every email into these buckets:
   - **Brand Deals** — partnership offers, paid collabs, sponsorships
   - **Revenue** — new Skool customers, payments received, subscription notifications
   - **Important** — calls booked, replies from active threads, team emails
   - **Community** — Skool notifications, NoeAI messages, community member questions
   - **Noise** — n8n error alerts, login notifications, digests, marketing
5. **Draft replies** for all brand deal emails (CC Mo at Mkmmediaagency@gmail.com)

**CRITICAL: Do NOT use `-category:` filters.** These exclude Skool notifications, payment confirmations, and other important emails that Gmail auto-categorizes. Search `is:unread in:inbox` to get EVERYTHING.

**Output for briefing:**
```
## Email

### Brand Deals ([count]) — drafts created
- **[Brand]** ([Contact]) — [what they want] — Draft ready

### Revenue ([count])
- **[Source]** — [who paid / what] — $XX

### Important ([count])
- **[From]** — [Subject] — [action needed]

### Community ([count])
- [summary of Skool/NoeAI activity]

### Noise ([count])
- [n8n errors, login alerts, digests — one-line summary]
```

**Do NOT skip reading emails.** The whole point is that Noe opens Claude and his email is handled.

### Module 2: AI & Claude Code News

Check for new releases, features, and announcements from the last 24-48 hours.

**Sources to scrape (use WebFetch + WebSearch):**

1. **Claude Code Changelog:** WebFetch `https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md` — extract latest entries
2. **Anthropic Blog:** WebSearch for `site:anthropic.com/news` + current month/year
3. **General AI news:** WebSearch for `AI news ChatGPT Claude Gemini update release launch` + today's date
4. **Releasebot:** WebFetch `https://releasebot.io/updates/anthropic/claude-code` — latest release notes

**For EACH news item, provide 3 things with clear spacing between items:**

```
### [Feature/Release Name]

**What:** [2-3 sentences explaining what it actually does]

**Why it matters:** [How this affects Noe's workflow, content, or business]

**Content angle:** [One specific video idea Noe can film about this]

---
```

**Evaluation criteria:**
- Is this actually new (last 48h)?
- Is it relevant to Noe's work (Claude Code, AI tools, automation, content creation)?
- Could Noe make content about this?
- Does this change how Noe works day-to-day?

If nothing new: "No major AI news in the last 24 hours."

### Module 3: Today's Tasks

Read the project's `TASKS.md` file. Identify:

1. What phase/section is marked as top priority?
2. What are the next 3-5 actionable tasks?
3. Any deadlines or time-sensitive items from email (contracts to sign, payments failing, etc.)?

**Output for briefing:**
```
## Tasks
**Priority:** [current top priority phase]
**Today's focus:**
- [ ] [Task 1]
- [ ] [Task 2]
- [ ] [Task 3]
**From email:**
- [ ] [Any urgent items surfaced from Module 1]
```

### Module 4: Account Stats

Pull latest account metrics from Supabase.

```sql
-- Latest follower counts (all platforms)
SELECT platform, follower_count, snapshot_date
FROM account_snapshots
WHERE platform IN ('instagram', 'tiktok', 'youtube')
  AND snapshot_date >= CURRENT_DATE - INTERVAL '2 days'
ORDER BY platform, snapshot_date DESC;

-- This month's top performing content
SELECT caption, views, likes, shares, saves, platform, post_date
FROM content
WHERE (handle = 'your-handle' OR handle = 'your-yt-handle')
  AND post_date >= date_trunc('month', CURRENT_DATE)
ORDER BY views DESC
LIMIT 5;
```

**Output for briefing:**
```
## Account
- IG: XX,XXX (+/- XX)
- TikTok: XX,XXX (+/- XX)
- YouTube: XXX (+/- XX)

Top content this month:
1. "caption..." — XX,XXX views (platform)
```

---

### Module 5: Client Layer

**Skip this module entirely if no clients/students are configured.**

1. Check for new client feedback (from Airtable, email, or forms)
2. Check for pending onboarding tasks
3. Check for clients who haven't been contacted in 7+ days

**Output for briefing:**
```
## Clients

### Activity
- New feedback: [X] responses
- Pending onboards: [X]
- Clients needing check-in: [names — haven't heard from in 7+ days]

### Action Needed
- [most urgent client item]
```

---

## Final Output

Combine all modules into one clean briefing:

```
# Morning Briefing — [Date] ([Day of Week])

## Life
[Module 0 output — schedule, journal prompt, meals if Monday]

## Email
[Module 1 output — full triage with all categories]

## AI News
[Module 2 output — detailed with content angles]

## Tasks
[Module 3 output — priorities + urgent items from email]

## Account
[Module 4 output]

## Clients
[Module 5 output — skip if no clients configured]

---
Actions available:
- /manage-email — Re-run email triage or handle new emails
- /post-content — Post videos from Dropbox queue
- /daily-content-researcher — Find today's content topics
- /journal — Get another reflection prompt
- /meal-planner — Generate/update meal plan
- /client-comms — Draft client messages
- /client-feedback — Synthesize client feedback
- /file-organizer — Sort your Downloads folder
```

---

## CRITICAL RULES

1. **Actually read every email.** Don't just scan subject lines. Use `gmail_read_message` on each one.
2. **Never use `-category:` Gmail filters.** They hide Skool, payment, and notification emails. Always search `is:unread in:inbox`.
3. **Actually draft replies.** Brand deal emails get a draft reply with Mo CC'd. No exceptions.
4. **Revenue is its own category.** New Skool customers, payments, subscriptions — Noe wants to see money coming in.
5. **AI News needs depth.** Every item gets: what it is, why it matters to Noe, and a content angle.
6. **If any module fails, skip it and note the error.** Don't block the whole briefing.
7. **AI News should be genuinely new.** Don't surface week-old announcements.
8. **Present everything in terminal.** No email delivery needed.
