# Ideal Day — Drift Tracker

A single-surface system for closing the gap between **your ideal day** and **your actual day**. Define the day you want, log whether you held it, name the drifts, and work corrections until they graduate to autopilot.

One page. No accounts. No backend. No AI (yet). Data stays in your browser.

## The core loop

```
Define your ideal day (once, in Settings)
        ↓
Each day: tap blocks as you hold them
        ↓
Tonight: write the verdict — matched or drifted?
        ↓
Name 1–3 drifts → turn them into corrections
        ↓
Hold corrections daily until they graduate to autopilot
```

This is **Phase 0** — manual, no intelligence. You collect the daily rows. The whole point is *using* it, not building it.

## The three concepts

### 1. Ideal-day template
Your definition of a perfect day — a list of time blocks, each with a label and what it holds. This is the **reference** you drift *from*. It's not a habit checklist; it's the shape of the day you're aiming for.

### 2. Nightly verdict
At the end of each day you answer one question: **did today match the ideal?**
- **Matched** — the day held.
- **Drifted** — name the 1–3 specific drifts (what pulled you off the ideal).

Plus a mood and a one-line note. This is the data you'll later compute baselines and drift patterns from.

### 3. Corrections queue
A drift becomes a **correction** — a temporary, active practice with an identity line:
> *correction:* "No phone in bedroom after 22:00"
> *identity:* "I am someone who protects his sleep like it's sacred"

You hold it daily. After **7 days held**, you can **graduate it to autopilot** — it leaves the active queue and joins the graduated list. The idea: you don't track habits forever. You fix a drift, hold it until it's automatic, then move on.

**Max 3 active corrections at a time.** This is deliberate — the document this system is built from warns against over-engineering. Three is enough to focus on; more is procrastination disguised as ambition.

## Features

### Today
- **Smart suggestions** — rule-based, derived from your data: what ideal block is NOW/next, correction streak risk, most-drifted block, protein behind pace, routine tasks pending, verdict reminder, never-miss-twice nudge. No AI — plain code.
- **Day-quality ring** — % of ideal blocks held, with a plain-language label
- **Ideal-day timeline** — your blocks as a vertical timeline, tap to mark held. Shows a live **NOW** pill on the current block and dims past unheld blocks.
- **Daily routine** — household and life-admin chores (laundry, trash, dishes, cleaning, groceries, inbox, finances…) scheduled by day of week. Shows only today's tasks with a progress counter. Tap to check off.
- **Active corrections** — up to 3 cards with identity lines, streaks, hold toggles, graduate/retire
- **Fuel panel** — daily protein & calorie targets calculated from your body profile (Mifflin-St Jeor). Log meals from a built-in food database, track protein/calories consumed vs target, and get smart food suggestions to close the protein gap.
- **Nightly verdict** — match/drift toggle, 1–3 named drifts (one-tap convert to correction), mood, note
- **Identity line** — rotates daily from your statements

### History
- **Consistency heatmap** — 12 weeks, colored by % of ideal blocks held; green = matched ideal
- **Recent verdicts** — last 10 days with drifts and notes
- **Graduated to autopilot** — corrections you've successfully installed

### Settings
- **Ideal-day editor** — add/edit/remove/reorder time blocks
- **Daily routine editor** — add/edit/remove household and life-admin tasks, schedule each by day of week (tap day chips to toggle; empty = every day)
- **Identity statements** — "I am someone who…" lines, one per line
- **North Star** — 10 / 20 / 30 year vision
- **Body profile** — weight, height, age, sex, activity level, goal (cut/maintain/gain). Drives the nutrition calculations.
- **Export / import** — JSON backup
- **Reset** — double-confirmed wipe

## Smart suggestions engine

All suggestions are **deterministic, rule-based code** — no LLM. They're computed fresh each render from your current state:

| Suggestion | Trigger |
|---|---|
| "Now: [block]" | Current time falls within an ideal block's window and it's not held |
| "Next up: [block] in Xh" | There's an upcoming ideal block today |
| "X blocks unheld today" | All blocks have passed and some are unheld |
| "Correction not held — streak at risk" | After 8pm, an active correction isn't marked held |
| "Hold [correction] today" | Afternoon, an active correction isn't held yet |
| "[block] drifts most for you" | A block appears in 2+ drift verdicts in the last 14 days |
| "Protein behind pace" | Logged protein < 70% of expected (target × day progress) |
| "N routine tasks pending" | After 4pm, today's routine items aren't all done |
| "Write tonight's verdict" | After 8pm, no verdict logged |
| "Yesterday drifted — hold one block" | Yesterday was a drift day, today has nothing held |

## Daily routine

Recurring household and life-admin tasks, scheduled by day of week. This is separate from the ideal-day template (which is about the shape of your day and who you're becoming) — routine is the maintenance layer that keeps life running.

**Ships with 8 defaults:**

| Task | Schedule |
|---|---|
| 🧺 Laundry | Mon, Thu |
| 🗑️ Take out trash | Tue, Fri |
| 🍽️ Do dishes | Every day |
| 🧹 Quick clean (15m) | Wed, Sat |
| 🛒 Groceries | Sat |
| 📧 Inbox to zero | Weekdays |
| 🪴 Water plants | Mon, Wed, Fri |
| 💳 Check finances | Sun |

**Scheduling:** In Settings, tap the day-of-week chips to toggle each day on/off. Empty = every day. The Today tab shows only the tasks scheduled for the current weekday, with a progress counter ("3 / 5 done"). Tap to check off.

Fully editable — add your own (watering garden, meal prep, car maintenance, calling mom, whatever recurring life tasks you have).

## Nutrition calculations

Uses the **Mifflin-St Jeor** equation:

- **BMR** = 10×weight(kg) + 6.25×height(cm) − 5×age + 5 (male) / −161 (female)
- **TDEE** = BMR × activity factor (1.2 sedentary → 1.9 very active)
- **Calorie target** = TDEE − 400 (cut) / TDEE (maintain) / TDEE + 300 (gain)
- **Protein target** = weight × 1.8 (cut) / 1.6 (maintain) / 2.0 (gain) g/kg

The food database has 12 common high-protein foods with per-serving protein and calories. The smart suggestion greedily picks the highest protein-density foods to close your remaining protein gap.

## PWA
- Installable on iOS/Android (Add to Home Screen)
- Works offline (service worker caches all assets)
- No build step, no dependencies, no backend

## Project structure
```
ideal-day/
├── index.html          # The entire app (HTML + CSS + JS)
├── manifest.json       # PWA manifest
├── service-worker.js   # Offline caching
└── README.md
```

## Deploy
Static site — push to GitHub and enable Pages, or drop on Vercel/Netlify. No build command needed.

## Roadmap — the phases

This system is designed in phases. **Do not skip ahead.** Each phase earns the next.

### Phase 0 — Manual surface (this)
No intelligence. You define the ideal day, log holds, write verdicts, manage corrections by hand. **Goal: use it daily for a few weeks. Collect rows.** If you're tweaking the system instead of using it, stop — that's the signal.

### Phase 1 — Manual + review
Same surface, but you've accumulated enough data to spot patterns yourself by eye. You graduate your first corrections. You notice which blocks drift most. Still no code beyond this app.

### Phase 2 — One agent (~100 lines)
A scheduled morning job:
```
cron 06:15 →
  load last N days from the store          (code)
  compute baselines, drifts, gap score     (code)
  → LLM call: "metrics + ideal-day template + active queue
     → return {verdict, corrections[1..3], adjusted_schedule}"   (the agent)
  render into today's surface              (code)
```
One agent. One prompt. Reversible output (it writes a note, it doesn't act). This is the *entire* AI surface. Everything else stays plain code.

The drift math (baselines, sneakiness sort, gap score) is **plain code** — only the final "read the metrics and write the verdict" step needs a model.

### Phase 3 (maybe) — Max-3 pipeline
Only if Phase 2 proves worth it. Split by cognitive role, not domain:
1. **Analyst** (mostly code) — baselines, drift detection, gap score
2. **Coach** (LLM) — writes identity-framed corrections + verdict in your voice
3. **Scheduler** (code) — drops corrections into your blocked day

A pipeline, not an office. No manager agent, no dynamic hiring. Adding a fourth requires justifying it against the over-engineering rule out loud.

## Principles (from the source document)
- **Manual before automated.** Don't build intelligence before you've felt the problem by hand.
- **A running v1 beats a perfect v3 that never ships.**
- **Designing the system is not using it.** If you're tweaking instead of logging, stop.
- **One artifact per day for one user.** This is not a content factory — don't wrap it in multi-agent orchestration.
- **Derived status, never stored.** Streaks, gap scores, queue position are computed from raw daily rows. Single source of truth.
- **Reversible output.** The agent writes a note; it doesn't take actions you can't undo.
