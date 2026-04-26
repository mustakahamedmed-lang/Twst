---
week: <% tp.file.title %>
spiritual_score: 0
health_score: 0
family_score: 0
career_score: 0
volunteer_score: 0
self_improvement_score: 0
recreation_score: 0
finances_score: 0
tags: [weekly-review]
---
# উইকলি প্রোডাক্টিভ রিভিউ — <% tp.file.title %>

<< [[]] | [[]] >>

---

## ⚖️ লাইফ-ব্যালেন্স হুইল (১–১০ রেটিং)

| বিভাগ | স্কোর (১–১০) | টীকা / উন্নতির পথ |
|---|---|---|
| আত্মিক (Spiritual) | | |
| সুস্বাস্থ্য (Health) | | |
| পরিবার ও সম্পর্ক (Family) | | |
| ক্যারিয়ার/বিজনেস (Career) | | |
| উম্মাহ ও কমিউনিটি (Volunteer) | | |
| আত্মোন্নয়ন (Self-Improvement) | | |
| ভ্রমণ/হালাল বিনোদন (Recreation) | | |
| অর্থ-সম্পদ (Finances) | | |

*→ [[03_Goals_and_Life_Wheel/Life_Balance_Wheel]] এ হুইল আপডেট করুন*

---

## 🎯 সপ্তাহের সবচেয়ে গুরুত্বপূর্ণ কাজের অর্জন


## 📋 গুরুত্বপূর্ণ অসম্পূর্ণ কাজ (গত ৭ দিন)

```dataview
TASK FROM "01_Daily_Action_Plans"
WHERE !completed
AND file.ctime >= date(today) - dur(7 days)
SORT file.name DESC
```

---

## 🛑 এরর ও ফ্রিকশন প্যাটার্ন বিশ্লেষণ (গত ৭ দিন)

```dataview
LIST FROM #log/error
WHERE file.ctime >= date(today) - dur(7 days)
SORT file.name DESC
```

### পুনরাবৃত্তিমূলক দুর্বলতা চিহ্নিত করুন:
- সবচেয়ে বেশি ঘটা friction_type: 
- প্যাটার্ন ভাঙার জন্য প্রয়োজনীয় পদক্ষেপ: 

---

## 📊 সপ্তাহের হ্যাবিট সারসংক্ষেপ

```dataview
TABLE fajr, dhuhr, asr, maghrib, isha, quran_pages, water_intake, daily_points, productivity_level
FROM "01_Daily_Action_Plans"
WHERE file.ctime >= date(today) - dur(7 days)
SORT file.name ASC
```

---

## 🔄 সাপ্তাহিক চেকলিস্ট
- [ ] নফল সিয়াম (সোম/বৃহস্পতি)
- [ ] জুমাবারের সুন্নাহ (সূরা কাহাফ তিলাওয়াত)
- [ ] দরুদ পাঠ
- [ ] মসজিদে সময়দান
- [ ] অসুস্থ ব্যক্তির সাক্ষাৎ
- [ ] পরিবারকে সময়দান
- [ ] আত্মীয়ের খোঁজখবর
- [ ] সাদাকার উদ্দেশে সঞ্চয়
- [ ] ক্ষুধার্তদের খাওয়ানো
- [ ] কুরআন মুখস্থ
- [ ] হাদিস মুখস্থ
- [ ] পারিবারিক হালাকা
- [ ] সপ্তাহের বই-পাঠ
- [ ] ক্যালেন্ডার চেকিং
- [ ] অ্যাপয়েন্টমেন্ট সেটিং

---

## 📈 সপ্তাহের প্রজেক্ট প্রোগ্রেস
`10%` — `20%` — `30%` — `40%` — `50%` — `60%` — `70%` — `80%` — `90%` — `100%`

প্রোডাক্টিভিটি বৃদ্ধির জন্য করণীয়:

---

## 🏆 জবাবদিহিতা সারসংক্ষেপ (Accountability Snapshot)
*(স্ক্রিনশট নিয়ে অ্যাকাউন্টেবিলিটি পার্টনারকে শেয়ার করুন)*

**এই সপ্তাহের শীর্ষ ৩টি জয়:**
1. 
2. 
3. 

**এই সপ্তাহের প্রধান ফ্রিকশন:**


---

## 💡 সপ্তাহের বিশেষ অভিজ্ঞতা ও শিক্ষা


## 🔄 পরের সপ্তাহের জন্য করণীয়


---

## 🔗 সম্পর্কিত নোটস
- গত সপ্তাহ: [[]]
- আগামী সপ্তাহ: [[]]
- মাসিক রিভিউ: [[02_Weekly_Monthly_Reviews/]]
- লক্ষ্য: [[03_Goals_and_Life_Wheel/Goal_Setting]]
