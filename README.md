# 🚀 Productive Muslim Vault — Setup Guide

> Built from: **Productive Ramadan Daily Planner** (প্রোডাক্টিভ মুসলিম ডেইলি প্ল্যানার) by Hamid Siraji
> Vault Architect: Claude (Anthropic)

---

## 📁 Vault Structure

```
00_Dashboard/
  └── Dashboard.md              ← Pin this as your home screen
01_Daily_Action_Plans/
  └── (auto-generated daily notes)
02_Weekly_Monthly_Reviews/
  └── (weekly + monthly review notes)
03_Goals_and_Life_Wheel/
  ├── Goal_Setting.md            ← 6m/1yr/5yr goal horizons
  ├── Life_Balance_Wheel.md      ← 8-category wheel tracker
  ├── Personal_Checklist.md      ← Your custom recurring items
  └── Productive_Inner_Dialogue.md ← 10 mindset affirmations
04_Spaced_Repetition_Library/
  └── (Quran verses + Duas flashcards)
05_Friction_and_Error_Logs/
  └── (auto-tagged with #log/error)
99_Templates/
  ├── Daily_Template.md
  ├── Weekly_Review_Template.md
  ├── Monthly_Review_Template.md
  ├── Flashcard_Template.md
  └── Accountability_Template.md
```

---

## 🔌 Required Plugins (Settings → Community Plugins)

| Plugin | Key Setting |
|---|---|
| **Templater** | Template folder: `99_Templates` · Enable "Trigger on new file creation" |
| **Periodic Notes** | Daily folder: `01_Daily_Action_Plans` · Template: `Daily_Template.md` |
| **Dataview** | Enable · No extra config needed |
| **Tasks** | Global task filter: `#task` |
| **Spaced Repetition** | Flashcard tag: `#flashcard` |
| **Smart Random Note** | Enable · Drag dice icon to left sidebar |
| **Heatmap Calendar** | Enable · Powers the Dashboard heatmap |
| **Banners** (optional) | Enable · Add banner image path to Dashboard frontmatter |

---

## ✅ Go-Live Sequence

1. Create the 7 folders above
2. Install all 8 plugins
3. Configure Templater (folder + trigger on new file)
4. Configure Periodic Notes (daily folder + template)
5. Open `00_Dashboard/Dashboard.md` → right-click tab → **Pin**
6. Fill in `03_Goals_and_Life_Wheel/Goal_Setting.md` with your goals
7. Click the Periodic Notes calendar icon to generate today's daily note
8. Add your first flashcard in `04_Spaced_Repetition_Library/`
9. Drag the Smart Random Note dice icon to your left sidebar

---

## 🏆 Gamification — Points System

Each completed item in the daily note frontmatter = **1 point**

| Points | Reward |
|---|---|
| 50 | 1 hour halal recreation |
| 100 | Favourite meal or book |
| 250 | Family outing |
| 500 | Short trip or retreat |
| 1000 | Your personal dream reward |

Update `daily_points` in each daily note's frontmatter. The Dashboard aggregates your total automatically.

---

## 💡 Gaps Incorporated (Beyond the Original Plan)

1. **Productivity Level (1–5)** — `productivity_level` frontmatter key + heatmap intensity mapping
2. **Water Intake Tracker** — `water_intake` frontmatter + weekly average on Dashboard
3. **Visual Dashboard** — 6-box monthly event/deadline grid in Monthly Review
4. **Goal Horizon Table** — 6m/1yr/5yr across 9 life categories in `Goal_Setting.md`
5. **Personal Checklist** — Separate note embeddable in any note with `![[Personal_Checklist]]`
6. **Productive Inner Dialogue** — 10 book affirmations + custom slots in `Productive_Inner_Dialogue.md`
7. **Error Categorisation** — `friction_type` field in error log entries for Weekly/Monthly pattern analysis
8. **Accountability Template** — Weekly snapshot with top 3 wins + friction for sharing with accountability partner
