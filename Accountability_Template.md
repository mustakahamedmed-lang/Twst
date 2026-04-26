---
tags: [accountability]
---
# 🤝 জবাবদিহিতা নোট — <% tp.file.title %>

> এই নোটের স্ক্রিনশট নিয়ে আপনার অ্যাকাউন্টেবিলিটি পার্টনারকে শেয়ার করুন।

---

## 🏆 এই সপ্তাহের শীর্ষ ৩টি জয়

```dataview
TABLE daily_points, productivity_level
FROM "01_Daily_Action_Plans"
WHERE file.ctime >= date(today) - dur(7 days)
SORT daily_points DESC
LIMIT 3
```

**আমার ৩টি জয়:**
1. 
2. 
3. 

---

## 🛑 প্রধান ফ্রিকশন (এই সপ্তাহ)

```dataview
LIST FROM #log/error
WHERE file.ctime >= date(today) - dur(7 days)
```

**সারসংক্ষেপ:**

---

## 📊 এই সপ্তাহের স্ট্যাটস

```dataview
TABLE WITHOUT ID
  sum(rows.daily_points) AS "পয়েন্ট",
  round(average(rows.productivity_level), 1) AS "গড় প্রোডাক্টিভিটি",
  round(average(rows.water_intake), 1) AS "গড় পানি (গ্লাস)"
FROM "01_Daily_Action_Plans"
WHERE file.ctime >= date(today) - dur(7 days)
GROUP BY "সাপ্তাহিক"
```

---

## 🎯 পরের সপ্তাহের অঙ্গীকার

আমি পরের সপ্তাহে নিশ্চিতভাবে করবো:
1. 
2. 
3. 

---

## 🔗 সম্পর্কিত নোটস
- সাপ্তাহিক রিভিউ: [[02_Weekly_Monthly_Reviews/]]
- লক্ষ্যমালা: [[03_Goals_and_Life_Wheel/Goal_Setting]]
