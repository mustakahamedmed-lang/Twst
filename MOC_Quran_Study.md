---
tags: [moc, quran, study]
---
# 📖 কুরআন স্টাডি MOC

> [!quote] "নিশ্চয়ই এই কুরআন সর্বোত্তম পথের দিকে হিদায়াত করে।" — সূরা ইসরা: ৯

---

## 📊 কুরআন তিলাওয়াত — গত ৩০ দিন

```dataview
TABLE quran_pages AS "পৃষ্ঠা", hadith_study AS "হাদিস?", file.day AS "তারিখ"
FROM "01_Daily_Action_Plans"
WHERE file.ctime >= date(today) - dur(30 days)
SORT file.name DESC
LIMIT 14
```

### মাসিক মোট তিলাওয়াত

```dataview
TABLE WITHOUT ID
  sum(rows.quran_pages) AS "মোট পৃষ্ঠা",
  round(average(rows.quran_pages), 1) AS "দৈনিক গড়"
FROM "01_Daily_Action_Plans"
WHERE file.ctime >= date(today) - dur(30 days)
GROUP BY "কুরআন সারাংশ"
```

---

## 🧠 ফ্ল্যাশকার্ড লাইব্রেরি

```dataview
TABLE file.ctime AS "যোগ করা হয়েছে", source AS "উৎস", category AS "ক্যাটাগরি"
FROM "04_Spaced_Repetition_Library"
SORT file.ctime DESC
```

---

## 🎯 কুরআন মুখস্থ লক্ষ্য

- [ ] এই মাসে ৫টি নতুন আয়াত মুখস্থ করা
- [ ] প্রতিদিন ১ পৃষ্ঠা তিলাওয়াত (ন্যূনতম)
- [ ] সপ্তাহে সূরা কাহাফ তিলাওয়াত (জুমা)

---

## 🔗 এম্বেডেড: সর্বশেষ ফ্ল্যাশকার্ড

![[04_Spaced_Repetition_Library/Example_Surah_Al-Fatiha]]

---

## 🔗 সম্পর্কিত নোটস

- [[06_MOCs/MOC_Main_Hub|🗺️ Main Hub]]
- [[06_MOCs/MOC_Prayer_Analytics|🕌 সালাহ অ্যানালিটিক্স]]
- [[03_Goals_and_Life_Wheel/Goal_Setting|🎯 আত্মিক লক্ষ্য]]
