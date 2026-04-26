---
tags: [moc, hub]
cssclass: moc-page
---
# 🗺️ প্রোডাক্টিভ মুসলিম — মাস্টার হাব

> [!quote] আপনার সম্পূর্ণ প্রোডাক্টিভিটি সিস্টেমের কেন্দ্রীয় নেভিগেশন

---

## 📊 এক নজরে সম্পূর্ণ অবস্থা

### 🏆 এই মাসের পারফরম্যান্স

```dataview
TABLE WITHOUT ID
  sum(rows.daily_points) AS "মোট পয়েন্ট",
  length(rows) AS "সক্রিয় দিন",
  round(average(rows.daily_points), 1) AS "দৈনিক গড়",
  round(average(rows.productivity_level), 1) + "/5" AS "প্রোডাক্টিভিটি",
  round(average(rows.water_intake), 1) AS "পানি 💧",
  round(average(rows.quran_pages), 1) AS "কুরআন 📖"
FROM "01_Daily_Action_Plans"
WHERE file.ctime >= date(today) - dur(30 days)
GROUP BY "মাসিক সারাংশ"
```

### 🎯 আজকের লক্ষ্য অগ্রগতি

```dataview
TASK FROM "01_Daily_Action_Plans"
WHERE file.name = dateformat(date(today), "yyyy-MM-dd")
WHERE !completed
LIMIT 5
```

### 🛑 এই সপ্তাহের পুনরাবৃত্তি ফ্রিকশন

```dataview
TABLE file.link AS "দিন", friction_type AS "ধরন"
FROM #log/error
WHERE file.ctime >= date(today) - dur(7 days)
SORT file.name DESC
```

---

## 🗂️ প্রধান বিভাগসমূহ

### 📅 দৈনিক ও পর্যালোচনা
- [[00_Dashboard/Dashboard|🏠 Dashboard]] — আপনার হোম পেজ
- [[01_Daily_Action_Plans/|📆 Daily Plans]] — সব দৈনিক নোট
- [[02_Weekly_Monthly_Reviews/|📊 Reviews]] — সাপ্তাহিক ও মাসিক রিভিউ

### 🎯 লক্ষ্য ও ব্যালেন্স
- [[03_Goals_and_Life_Wheel/Goal_Setting|🎯 Goal Setting]] — ৬ মাস/১ বছর/৫ বছরের লক্ষ্য
- [[03_Goals_and_Life_Wheel/Life_Balance_Wheel|⚖️ Life Balance]] — ৮-ক্যাটাগরি হুইল
- [[03_Goals_and_Life_Wheel/Personal_Checklist|✅ Personal Checklist]] — কাস্টম চেকলিস্ট
- [[03_Goals_and_Life_Wheel/Productive_Inner_Dialogue|💬 Inner Dialogue]] — ১০ অ্যাফার্মেশন

### 📚 শিক্ষা ও স্মৃতি
- [[04_Spaced_Repetition_Library/|🧠 Flashcards]] — কুরআন ও হাদিস মুখস্থ
- [[MOC_Quran_Study|📖 Quran Study MOC]] — কুরআন অধ্যয়ন হাব

### 📈 বিশ্লেষণ ও উন্নতি
- [[05_Friction_and_Error_Logs/|🛑 Error Logs]] — ভুল প্যাটার্ন
- [[MOC_Habit_Tracking|📊 Habit Tracking MOC]] — হ্যাবিট ট্র্যাকিং হাব
- [[MOC_Prayer_Analytics|🕌 Prayer Analytics MOC]] — সালাহ বিশ্লেষণ

---

## 📈 প্রধান ট্রেন্ডস (গত ৩০ দিন)

### সালাহ কনসিস্টেন্সি রেট

```dataview
TABLE WITHOUT ID
  round((sum(rows.fajr) / length(rows)) * 100, 1) + "%" AS "ফজর",
  round((sum(rows.dhuhr) / length(rows)) * 100, 1) + "%" AS "যোহর",
  round((sum(rows.asr) / length(rows)) * 100, 1) + "%" AS "আসর",
  round((sum(rows.maghrib) / length(rows)) * 100, 1) + "%" AS "মাগরিব",
  round((sum(rows.isha) / length(rows)) * 100, 1) + "%" AS "এশা"
FROM "01_Daily_Action_Plans"
WHERE file.ctime >= date(today) - dur(30 days)
GROUP BY "সালাহ কনসিস্টেন্সি"
```

### হ্যাবিট কমপ্লিশন স্কোর

```dataview
TABLE WITHOUT ID
  round((sum(rows.exercise) / length(rows)) * 100, 1) + "%" AS "🏃 ব্যায়াম",
  round((sum(rows.journaling) / length(rows)) * 100, 1) + "%" AS "📝 জার্নালিং",
  round((sum(rows.family_time) / length(rows)) * 100, 1) + "%" AS "👨‍👩‍👧 পরিবার",
  round((sum(rows.book_reading) / length(rows)) * 100, 1) + "%" AS "📚 বই পড়া"
FROM "01_Daily_Action_Plans"
WHERE file.ctime >= date(today) - dur(30 days)
GROUP BY "হ্যাবিট স্কোর"
```

---

## 🔄 সাম্প্রতিক কার্যক্রম

### সর্বশেষ ৫টি দৈনিক নোট

```dataview
TABLE daily_points AS "পয়েন্ট", productivity_level AS "লেভেল", quran_pages AS "কুরআন পৃষ্ঠা"
FROM "01_Daily_Action_Plans"
SORT file.name DESC
LIMIT 5
```

### সর্বশেষ রিভিউ

```dataview
LIST
FROM "02_Weekly_Monthly_Reviews"
SORT file.mtime DESC
LIMIT 3
```

---

## 🎯 দ্রুত অ্যাকশন

- [ ] আজকের দৈনিক নোট তৈরি করুন
- [ ] এই সপ্তাহের রিভিউ সম্পন্ন করুন
- [ ] লাইফ-ব্যালেন্স হুইল আপডেট করুন
- [ ] নতুন ফ্ল্যাশকার্ড যোগ করুন
- [ ] পারসোনাল চেকলিস্ট রিভিউ করুন

---

## 🔗 বহিরাগত রিসোর্স

- [Productive Muslim](https://productivemuslim.com)
- [Quran.com](https://quran.com)
- [Sunnah.com](https://sunnah.com)

---

## 📝 নোটস ও টিপস

> এই MOC আপনার সম্পূর্ণ সিস্টেমের ওভারভিউ। প্রতিদিন এই পেজটি খুলুন এবং আপনার অগ্রগতি দেখুন।
