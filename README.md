# Hour Rich

From trading hours for dollars to getting 5+ hours a week back — because AI is finally doing the heavy lifting across your life, your backend, and your clients.

---

## What Is This?

Hour Rich is a ready-to-use AI system built on Claude Code. You download this folder, run one setup command, and AI starts handling your:

- **Morning routine** — journal prompts, schedule, meal planning
- **Email** — inbox scanned, replies drafted in your voice
- **Content** — analytics pulled, performance reported
- **Ads** — spend monitored, winners/losers flagged
- **Files** — Downloads auto-sorted into the right folders
- **Clients** — onboarding, feedback synthesis, communication templates
- **Weekly reports** — full digest across everything, with time-saved estimates

You don't need to be technical. You don't need to know how to code. You answer questions, and the system configures itself.

---

## Installation (5 minutes)

### Step 1: Install Claude Code

If you don't have it yet:
- Go to https://claude.ai/code
- Download and install Claude Code
- You need a Max plan ($100/mo) for automated scheduling, or Pro plan for manual use

### Step 2: Download Hour Rich

Download this folder and put it on your Desktop (or anywhere you want).

### Step 3: Open Claude Code in this folder

Open your terminal / command prompt:

```
cd ~/Desktop/hour-rich
claude
```

### Step 4: Run the setup wizard

Type:

```
/hour-rich
```

That's it. The wizard asks you ~20 questions about your life, business, and clients. Takes about 15 minutes. After that, everything is configured and running.

---

## What Happens After Setup

### Automated (runs without you doing anything)

| What | When | What it does |
|------|------|-------------|
| Morning Brief | Every day at your chosen time | Email drafts, content stats, journal prompt, schedule, client updates |
| Meal Planner | Every Monday (or your chosen day) | Week's meals + grocery list |
| Weekly Report | Every Sunday (or your chosen day) | Full performance digest with time-saved estimate |

### On-Demand (type when you need it)

| Command | What it does |
|---------|-------------|
| `/journal` | Get a personalized reflection prompt |
| `/manage-email` | Re-scan inbox and draft replies |
| `/copy-editor` | Edit any text to sound like you |
| `/file-organizer` | Sort messy folders |
| `/ga-report` | Google Analytics report |
| `/client-comms` | Draft messages to clients |
| `/client-feedback` | Analyze client feedback patterns |
| `/client-delivery` | Create resources for clients |
| `/personal-admin` | Daily priorities and calendar check |

---

## The 3 Layers

### Layer 1: Life
AI helps you run your mornings, meals, journaling, and personal admin. Like having a personal assistant who handles the stuff that falls through the cracks.

### Layer 2: Business Backend
This is where the hours come back. Email drafting, content analytics, ad monitoring, Google Analytics, file organization, copy editing — all running in the background.

### Layer 3: Clients
The layer nobody teaches. Onboarding flows, feedback synthesis, communication templates, program delivery. Your clients get a better experience AND you get your time back.

---

## Requirements

**Required:**
- Claude Code installed (https://claude.ai/code)
- Claude Max plan (for automated schedules) or Pro plan (manual only)

**Optional (but recommended):**
- Gmail — for email scanning and draft creation
- Google Calendar — for schedule integration
- Google Analytics — for website traffic reports
- Meta Ads — for ad performance monitoring

The system works with whatever you have connected. If something isn't set up, it just skips that part. No errors, no problems.

---

## FAQ

**Do I need to know how to code?**
No. You answer questions and type commands. That's it.

**Does it work on Mac and Windows?**
Yes. Claude Code runs on both.

**What if I don't have clients?**
Skip Layer 3 during setup. You can add it later anytime.

**Can I customize it?**
Everything is in readable .md files. You can edit any skill to match your workflow.

**How much does it cost to run?**
Claude Max plan is $100/month. Each automated task uses tokens (Claude's fuel). Normal usage is well within Max plan limits.

**What if I want to turn something off?**
Just tell Claude: "stop the morning brief" or "disable meal planning" — it adjusts.

---

## File Structure

```
hour-rich/
├── README.md              <- you are here
├── CLAUDE.md              <- brain file (Claude reads this first)
├── .claude/
│   ├── settings.json      <- permissions
│   ├── skills/            <- all 13 automation skills
│   └── commands/          <- morning brief, email management
├── config/                <- your profile (generated during setup)
├── templates/             <- voice samples, email templates
└── reports/               <- all generated reports
```

---

## Support

Having issues? Open Claude Code in this folder and just ask:

"Something isn't working with [feature]. Can you help me fix it?"

Claude can read its own skills and troubleshoot.

---

Built with Claude Code.
