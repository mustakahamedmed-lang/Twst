---
tags: [moc, habits, tracking]
---
# 📊 হ্যাবিট ট্র্যাকিং — Habit Tracking MOC

> [!quote] "ছোট ছোট পদক্ষেপই বড় পরিবর্তন আনে।"

---

## 🎯 সামগ্রিক হ্যাবিট স্কোর (গত ৩০ দিন)

```dataview
TABLE WITHOUT ID
  round((sum(rows.exercise) / length(rows)) * 100, 1) + "%" AS "🏃 ব্যায়াম",
  round((sum(rows.journaling) / length(rows)) * 100, 1) + "%" AS "📝 জার্নাল",
  round((sum(rows.family_time) / length(rows)) * 100, 1) + "%" AS "👨‍👩‍👧 পরিবার",
  round((sum(rows.book_reading) / length(rows)) * 100, 1) + "%" AS "📚 বই",
  round((sum(rows.sleep_adequate) / length(rows)) * 100, 1) + "%" AS "😴 ঘুম",
  round((sum(rows.morning_adhkaar) / length(rows)) * 100, 1) + "%" AS "🌅 সকালের যিকির",
  round((sum(rows.evening_adhkaar) / length(rows)) * 100, 1) + "%" AS "🌆 বিকালের যিকির"
FROM "01_Daily_Action_Plans"
WHERE file.ctime >= date(today) - dur(30 days)
GROUP BY "হ্যাবিট সামগ্রিক"
```

---

## 📈 সাপ্তাহিক ট্রেন্ড

```dataview
TABLE 
  exercise AS "ব্যায়াম",
  water_intake AS "পানি",
  book_reading AS "বই",
  journaling AS "জার্নাল",
  family_time AS "পরিবার"
FROM "01_Daily_Action_Plans"
WHERE file.ctime >= date(today) - dur(7 days)
SORT file.name DESC
```

---

## 💧 পানি পান ট্র্যাকার

### দৈনিক গড় (গত সপ্তাহ)

```dataview
TABLE WITHOUT ID
  round(average(rows.water_intake), 1) AS "গড় গ্লাস/দিন",
  max(rows.water_intake) AS "সর্বোচ্চ",
  min(rows.water_intake) AS "সর্বনিম্ন",
  sum(rows.water_intake) AS "মোট (৭ দিন)"
FROM "01_Daily_Action_Plans"
WHERE file.ctime >= date(today) - dur(7 days)
GROUP BY "পানি সারসংক্ষেপ"
```

### দৈনিক ব্রেকডাউন

```dataview
TABLE water_intake AS "গ্লাস", file.day AS "তারিখ"
FROM "01_Daily_Action_Plans"
WHERE file.ctime >= date(today) - dur(7 days)
SORT file.name DESC
```

---

## 📚 বই পড়ার ট্র্যাকার

### এই মাসে বই পড়ার দিন

```dataview
TABLE book_reading AS "পড়েছি?", file.day AS "তারিখ"
FROM "01_Daily_Action_Plans"
WHERE file.ctime >= date(today) - dur(30 days)
WHERE book_reading = true
SORT file.name DESC
```

*মোট: `= length(filter(pages, (p) => p.book_reading = true))` দিন*

---

## 🏃 ব্যায়াম ট্র্যাকার

### এই সপ্তাহে ব্যায়ামের দিন

```dataview
TABLE exercise AS "ব্যায়াম?", file.day AS "তারিখ"
FROM "01_Daily_Action_Plans"
WHERE file.ctime >= date(today) - dur(7 days)
SORT file.name DESC
```

---

## 👨‍👩‍👧 পরিবারের সময়

### মাসিক ট্রেন্ড

```dataview
TABLE family_time AS "পরিবার সময়", file.day AS "তারিখ"
FROM "01_Daily_Action_Plans"
WHERE file.ctime >= date(today) - dur(30 days)
WHERE family_time = true
SORT file.name DESC
```

---

## 🎯 হ্যাবিট লক্ষ্য

### স্বল্পমেয়াদী (এই মাস)

- [ ] প্রতিদিন ৮ গ্লাস পানি পান (১০০%)
- [ ] সপ্তাহে ৫ দিন ব্যায়াম (৭০%+)
- [ ] প্রতিদিন ১৫ মিনিট বই পড়া (৮০%+)
- [ ] প্রতিদিন জার্নালিং (৯০%+)

### দীর্ঘমেয়াদী (৬ মাস)

- [ ] নিয়মিত ব্যায়ামের রুটিন স্থাপন
- [ ] মাসে ২টি বই সম্পূর্ণ করা
- [ ] পরিবারের সাথে সাপ্তাহিক কোয়ালিটি টাইম
- [ ] ৭–৮ ঘণ্টা ঘুমের অভ্যাস তৈরি

---

## ⚠️ চ্যালেঞ্জিং হ্যাবিট (উন্নতি প্রয়োজন)

```dataview
TABLE WITHOUT ID
  round((sum(rows.exercise) / length(rows)) * 100, 1) AS "ব্যায়াম %",
  round((sum(rows.sleep_adequate) / length(rows)) * 100, 1) AS "পর্যাপ্ত ঘুম %",
  round((sum(rows.book_reading) / length(rows)) * 100, 1) AS "বই পড়া %"
FROM "01_Daily_Action_Plans"
WHERE file.ctime >= date(today) - dur(30 days)
GROUP BY "চ্যালেঞ্জিং"
```

*যেকোনো হ্যাবিট যার স্কোর ৫০% এর নিচে তা উন্নতি প্রয়োজন।*

---

## 🔗 সম্পর্কিত নোটস

- [[MOC_Main_Hub|🗺️ Main Hub]] — কেন্দ্রীয় হাব
- [[03_Goals_and_Life_Wheel/Personal_Checklist|✅ Personal Checklist]] — হ্যাবিট প্ল্যানিং
- [[03_Goals_and_Life_Wheel/Goal_Setting|🎯 Goals]] — দীর্ঘমেয়াদী লক্ষ্য
- [[00_Dashboard/Dashboard|🏠 Dashboard]]

---

## 💡 হ্যাবিট বিল্ডিং টিপস

> [!tip] ৩টি সহজ নিয়ম
> 1. **ছোট শুরু করুন** — ৫ মিনিট থেকে শুরু করুন, ৩০ মিনিট নয়
> 2. **স্ট্যাকিং করুন** — নতুন হ্যাবিট পুরনো হ্যাবিটের সাথে যুক্ত করুন
> 3. **ট্র্যাক করুন** — প্রতিদিন চেক করুন এবং ছোট জয় উদযাপন করুন
