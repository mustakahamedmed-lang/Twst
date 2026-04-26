---
date: <% tp.file.title %>
fajr: false
dhuhr: false
asr: false
maghrib: false
isha: false
sunnah_prayers: false
qiyam_layl: false
quran_pages: 0
hadith_study: false
morning_adhkaar: false
evening_adhkaar: false
family_time: false
halal_entertainment: false
volunteer_sadaqah: false
career_business: false
journaling: false
istighfar: false
shukr: false
goal_visualising: false
exercise: false
sleep_adequate: false
book_reading: false
productive_habit: false
water_intake: 0
productivity_level: 3
daily_points: 0
tags: [daily]
---
# 📅 <% tp.file.title %>

<< [[<% tp.date.now("YYYY-MM-DD", -1, tp.file.title, "YYYY-MM-DD") %>]] | [[<% tp.date.now("YYYY-MM-DD", 1, tp.file.title, "YYYY-MM-DD") %>]] >> | [[00_Dashboard/Dashboard|🏠]] | [[06_MOCs/MOC_Main_Hub|🗺️]] | [[03_Goals_and_Life_Wheel/Goal_Setting|🎯]] | [[06_MOCs/MOC_Prayer_Analytics|🕌]]

> [!quote] আজকের অ্যাফার্মেশন → [[03_Goals_and_Life_Wheel/Productive_Inner_Dialogue|ইনার ডায়ালগ পড়ুন]]

---

## ⚡ টাইম ম্যাট্রিক্স — আজকের কাজ

> **নিয়ম:** প্রতিটি task-এর আগে `[Q1]`, `[Q2]`, `[Q3]`, বা `[Q4]` লিখুন → Dashboard ম্যাট্রিক্স স্বয়ংক্রিয়ভাবে আপডেট হবে

### 🔴 Q1 — এখনই করুন (Urgent + Important)
- [ ] #task [Q1] MIT: 

### 🟡 Q2 — শিডিউল করুন (Important, Not Urgent)
- [ ] #task [Q2] 
- [ ] #task [Q2] 

### 🟠 Q3 — ডেলিগেট করুন (Urgent, Not Important)
- [ ] #task [Q3] 

### ⚪ Q4 — বাদ দিন বা এলিমিনেট করুন
- [ ] #task [Q4] 

---

## 🕌 সালাহ ট্র্যাকার

| সালাহ | সময়মতো? | জামাতে? | সুন্নাহ? |
|---|---|---|---|
| ফজর 🌅 | ☐ | ☐ | ☐ |
| যোহর ☀️ | ☐ | ☐ | ☐ |
| আসর 🌤️ | ☐ | ☐ | ☐ |
| মাগরিব 🌆 | ☐ | ☐ | ☐ |
| এশা 🌙 | ☐ | ☐ | ☐ |
| কিয়ামুল লাইল ⭐ | ☐ | — | — |

*সম্পন্ন প্রতিটির জন্য frontmatter-এ `true` করুন → [[06_MOCs/MOC_Prayer_Analytics|চার্টে দেখুন]]*

---

## 📖 কুরআন ও হাদিস

- **তিলাওয়াত:** পৃষ্ঠা: ______ *(frontmatter `quran_pages` আপডেট করুন)*
- **হাদিস অধ্যয়ন:** 
- **নতুন মুখস্থ:** → [[04_Spaced_Repetition_Library/|ফ্ল্যাশকার্ড লাইব্রেরি]] | [[06_MOCs/MOC_Quran_Study|কুরআন হাব]]

---

## 💧 পানি — `= this.water_intake` গ্লাস

`○` `○` `○` `○` `○` `○` `○` `○` *(frontmatter `water_intake` আপডেট করুন → [[06_MOCs/MOC_Habit_Tracking|হ্যাবিট চার্টে দেখুন]])*

---

## 🌿 লাইফ-ব্যালেন্স চেকলিস্ট

| আইটেম | ✓ | আইটেম | ✓ |
|---|---|---|---|
| পরিবার ও সম্পর্ক | ☐ | সকালের যিকির | ☐ |
| হালাল বিনোদন | ☐ | সন্ধ্যার যিকির | ☐ |
| সাদাকাহ | ☐ | ব্যায়াম | ☐ |
| ক্যারিয়ার/বিজনেস | ☐ | পর্যাপ্ত ঘুম | ☐ |
| জার্নালিং | ☐ | বই পড়া | ☐ |
| ইস্তিগফার | ☐ | গোল ভিজুয়ালাইজিং | ☐ |
| শোকর | ☐ | প্রোডাক্টিভ হ্যাবিট | ☐ |

*→ [[03_Goals_and_Life_Wheel/Personal_Checklist|পারসোনাল চেকলিস্ট]] | [[03_Goals_and_Life_Wheel/Life_Balance_Wheel|লাইফ হুইল আপডেট করুন]]*

---

## 📅 অ্যাপয়েন্টমেন্ট
📞 ফোন: &emsp; 📧 ইমেইল: &emsp; 🤝 মিটিং:

---

## 🛑 ফ্রিকশন লগ #log/error
- **friction_type:** *(distraction / procrastination / health / spiritual / planning)*
- **কী হলো:** 
- **পরবর্তীবার:** 

*→ [[05_Friction_and_Error_Logs/|এরর লগ ফোল্ডার]] | [[06_MOCs/MOC_Main_Hub|মাস্টার হাবে প্যাটার্ন দেখুন]]*

---

## 📝 দিনশেষ রিভিউ
- **আজকের প্রধান অর্জন:** 
- **অসম্পূর্ণ কাজ ও পরবর্তী পদক্ষেপ:** 
- **আজকের শিক্ষা:** 

---

## 🏆 পয়েন্ট: `= this.daily_points` | লেভেল: `= this.productivity_level`/5

*→ [[00_Dashboard/Dashboard|Dashboard-এ মোট ও রিওয়ার্ড দেখুন 🏠]]*
