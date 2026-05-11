# Hour Rich

AI system that runs your Life, Business, and Clients — so you can close your laptop at 2pm.

---

## How It Works

This project has 3 layers of AI automation:

- **Layer 1 — Life:** Journal prompts, meal planning, personal admin, morning routine
- **Layer 2 — Business:** Email drafting, content analytics, ad monitoring, Google Analytics, file organization, copy editing
- **Layer 3 — Clients:** Onboarding, feedback synthesis, client communication, program delivery

## First Time Setup

Run `/hour-rich` — the setup wizard will interview you and configure everything.

## Daily Usage

- `/morning` — your unified morning brief (runs automatically if cron is set)
- All other skills available on-demand (see Quick Reference below)

---

## Quick Reference

### Automated (runs on schedule after setup)
| Command | What it does | Schedule |
|---------|-------------|----------|
| `/morning` | Full morning brief across all 3 layers | Daily |
| `/weekly-report` | Weekly performance digest | Weekly |
| `/meal-planner` | Meal plan + grocery list | Weekly |

### On-Demand (type when you need it)
| Command | Layer | What it does |
|---------|-------|-------------|
| `/journal` | Life | Personalized reflection prompt |
| `/personal-admin` | Life | Daily priorities, calendar, reminders |
| `/manage-email` | Business | Scan inbox, draft replies in your voice |
| `/copy-editor` | Business | Edit any text in your voice |
| `/file-organizer` | Business | Sort Downloads into correct folders |
| `/ga-report` | Business | Google Analytics report |
| `/client-comms` | Clients | Draft client messages in your voice |
| `/client-feedback` | Clients | Synthesize client feedback into insights |
| `/client-delivery` | Clients | Create resources for your clients |

### Setup
| Command | What it does |
|---------|-------------|
| `/hour-rich` | Master setup wizard (run this first) |
| `/my-business` | Update your profile and business config |

---

## Folder Structure

```
hour-rich/
├── CLAUDE.md              <- you are here
├── .claude/
│   ├── skills/            <- all automation skills
│   │   ├── hour-rich/     <- setup wizard
│   │   ├── meal-planner/
│   │   ├── journal/
│   │   ├── personal-admin/
│   │   ├── manage-email/
│   │   ├── copy-editor/
│   │   ├── file-organizer/
│   │   ├── ga-report/
│   │   ├── weekly-report/
│   │   ├── client-feedback/
│   │   ├── client-comms/
│   │   ├── client-delivery/
│   │   └── my-business/
│   └── commands/
│       ├── morning.md     <- daily morning brief
│       └── manage-email.md
├── config/
│   └── my-profile.md      <- generated during /hour-rich setup
├── templates/
│   └── email-voice.md     <- your voice samples (generated during setup)
└── reports/               <- all generated reports land here
```

---

## Requirements

- Claude Code (Max plan recommended for automated cron triggers)
- Gmail MCP (for email features) — optional but recommended
- Google Calendar MCP (for schedule features) — optional
- Google Analytics access (for GA reports) — optional

Not everything needs to be connected. The system works with whatever you have — just skip what you don't.
