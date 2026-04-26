---
tags: [moc, prayer, analytics]
---
# 🕌 সালাহ অ্যানালিটিক্স — Prayer Analytics MOC

> [!quote] "নিশ্চয়ই সালাত মুমিনদের উপর নির্দিষ্ট সময়ে ফরজ।" — সূরা আন-নিসা: ১০৩

---

## 📊 সামগ্রিক পরিসংখ্যান (গত ৩০ দিন)

```dataview
TABLE WITHOUT ID
  round((sum(rows.fajr) / length(rows)) * 100, 1) + "%" AS "ফজর হার",
  round((sum(rows.dhuhr) / length(rows)) * 100, 1) + "%" AS "যোহর হার",
  round((sum(rows.asr) / length(rows)) * 100, 1) + "%" AS "আসর হার",
  round((sum(rows.maghrib) / length(rows)) * 100, 1) + "%" AS "মাগরিব হার",
  round((sum(rows.isha) / length(rows)) * 100, 1) + "%" AS "এশা হার",
  round((sum(rows.sunnah_prayers) / length(rows)) * 100, 1) + "%" AS "সুন্নাহ হার",
  round((sum(rows.qiyam_layl) / length(rows)) * 100, 1) + "%" AS "কিয়াম হার"
FROM "01_Daily_Action_Plans"
WHERE file.ctime >= date(today) - dur(30 days)
GROUP BY "সালাহ সামগ্রিক"
```

---

## 🎯 সাপ্তাহিক ট্রেন্ড

```dataview
TABLE fajr AS "ফজর", dhuhr AS "যোহর", asr AS "আসর", maghrib AS "মাগরিব", isha AS "এশা", qiyam_layl AS "কিয়াম"
FROM "01_Daily_Action_Plans"
WHERE file.ctime >= date(today) - dur(7 days)
SORT file.name DESC
```

---

## ⚠️ মিসড প্রেয়ার অ্যালার্ট

```dataview
LIST "❌ ফজর মিসড" 
FROM "01_Daily_Action_Plans"
WHERE fajr = false
WHERE file.ctime >= date(today) - dur(7 days)
SORT file.name DESC
```

```dataview
LIST "❌ কিয়াম লাইল মিসড"
FROM "01_Daily_Action_Plans"
WHERE qiyam_layl = false
WHERE file.ctime >= date(today) - dur(7 days)
SORT file.name DESC
```

---

## 🏆 স্ট্রিক ট্র্যাকার

### ফজর স্ট্রিক (পরপর কতদিন)

```dataview
TABLE fajr AS "সম্পন্ন?", file.day AS "তারিখ"
FROM "01_Daily_Action_Plans"
WHERE file.ctime >= date(today) - dur(30 days)
SORT file.name DESC
LIMIT 30
```

*গণনা করুন: পরপর কতদিন ফজর সম্পন্ন হয়েছে*

---

## 📈 মাসিক প্রোগ্রেস চার্ট

### এই মাসের সালাহ সংখ্যা

```dataview
TABLE WITHOUT ID
  sum(rows.fajr) AS "ফজর",
  sum(rows.dhuhr) AS "যোহর",
  sum(rows.asr) AS "আসর",
  sum(rows.maghrib) AS "মাগরিব",
  sum(rows.isha) AS "এশা"
FROM "01_Daily_Action_Plans"
WHERE file.ctime >= date(today) - dur(30 days)
GROUP BY "মোট সালাহ"
```

---

## 🎯 লক্ষ্য ও উন্নতি

### আমার সালাহ লক্ষ্য

- [ ] ফজর ১০০% (প্রতিদিন)
- [ ] সপ্তাহে ৫ দিন জামাতে
- [ ] সুন্নাহ সালাহ ৮০%+
- [ ] সপ্তাহে ৩ দিন কিয়ামুল লাইল

### উন্নতির জন্য পদক্ষেপ

1. ফজরের জন্য একাধিক অ্যালার্ম সেট করা
2. ঘুমাতে যাওয়ার আগে উযু করা
3. কিয়ামুল লাইলের জন্য নিয়াত করা
4. মসজিদে যাওয়ার অভ্যাস তৈরি করা

---

## 🔗 সম্পর্কিত নোটস

- [[MOC_Main_Hub|🗺️ Main Hub]] — কেন্দ্রীয় হাব
- [[MOC_Habit_Tracking|📊 Habit Tracking]] — সব হ্যাবিট ট্র্যাকিং
- [[03_Goals_and_Life_Wheel/Goal_Setting|🎯 Goals]] — আত্মিক লক্ষ্য দেখুন
- [[00_Dashboard/Dashboard|🏠 Dashboard]] — ড্যাশবোর্ড

---

## 📝 সালাহ রিমাইন্ডার

> [!tip] প্রোডাক্টিভ টিপ
> ফজর সালাহ পড়ার পর ১৫ মিনিট কুরআন তিলাওয়াত করুন। এটি আপনার দিনের শুরুটা অসাধারণ করবে।
