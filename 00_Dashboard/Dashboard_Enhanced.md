---
banner: "https://images.unsplash.com/photo-1564769625905-50e93615e769?w=1400&q=80"
banner_y: 0.4
cssclass: dashboard-enhanced
tags: [dashboard, home]
---

# 🌙 Productive Muslim Vault — Enhanced Dashboard

> [!quote|gold-green] "নিয়তের উপরেই কাজের ফলাফল নির্ভরশীল। প্রতিটি দিন একটি নতুন সুযোগ।" — সহীহ বুখারি ১

---

## 🚨 তাৎক্ষণিক মনোযোগ প্রয়োজন

> [!danger|gold-green] ⚡ **Q1 — এখনই করুন** (Urgent + Important)
> ```dataview
> TASK FROM "01_Daily_Action_Plans"
> WHERE !completed AND contains(text, "[Q1]")
> WHERE file.ctime >= date(today) - dur(2 days)
> LIMIT 3
> ```

> [!warning|gold-green] 📋 **Q2 — শিডিউল করুন** (Important, Not Urgent)
> ```dataview
> TASK FROM "01_Daily_Action_Plans"
> WHERE !completed AND contains(text, "[Q2]")
> WHERE file.ctime >= date(today) - dur(3 days)
> LIMIT 3
> ```

> [!caution|gold-green] 🍅 **আজকের পোমোডোরো লক্ষ্য**
> ```dataview
> TABLE total_pomodoros AS "লক্ষ্য", completed_pomodoros AS "সম্পন্ন", (completed_pomodoros / (total_pomodoros || 1) * 100) AS "হার %"
> FROM "03_Pomodoro_Tracker"
> WHERE file.name = dateformat(date(today), "yyyy-MM-dd")
> ```

> [!bug|gold-green] 🛑 **গত ৭ দিনের পুনরাবৃত্তি ফ্রিকশন**
> ```dataview
> TABLE file.link AS "দিন", friction_type AS "ধরন", count(rows) AS "সংখ্যা"
> FROM #log/error
> WHERE file.ctime >= date(today) - dur(7 days)
> GROUP BY friction_type
> SORT rows DESC
> ```

---

## 📊 ৩০ দিনের পারফরম্যান্স স্ন্যাপশট

```dataview
TABLE WITHOUT ID
  sum(rows.daily_points) AS "🏆 মোট পয়েন্ট",
  length(rows) AS "📅 সক্রিয় দিন",
  round(average(rows.productivity_level),1) AS "⚡ গড় লেভেল",
  round(average(rows.water_intake),1) AS "💧 গড় পানি",
  round(average(rows.quran_pages),1) AS "📖 কুরআন গড়"
FROM "01_Daily_Action_Plans"
WHERE file.ctime >= date(today) - dur(30 days)
GROUP BY "সারাংশ"
```

---

## 🔥 হিটম্যাপ — ৩০ দিনের সামঞ্জস্য (গোল্ডেন-গ্রীন থিম)

```dataviewjs
const cal = {
  year: moment().year(),
  colors: { 
    "gold-green": [
      "#F0E68C",  // Light Gold
      "#DAA520",  // Goldenrod
      "#B8960F",  // Gold
      "#6BA83F",  // Light Green
      "#2D5016"   // Dark Green
    ]
  },
  showCurrentDayBorder: true,
  defaultEntryIntensity: 0,
  entries: []
};

for (let p of dv.pages('"01_Daily_Action_Plans"').where(p => p.daily_points > 0)) {
  const intensity = Math.min(Math.floor((p.daily_points ?? 0) / 25), 4);
  cal.entries.push({
    date: p.file.name,
    intensity: intensity,
    content: `✅ ${p.daily_points}pts | ⚡${p.productivity_level ?? "-"}`
  });
}
renderHeatmapCalendar(this.container, cal);
```

---

## ⚡ আইজেনহাওয়ার ম্যাট্রিক্স — অসম্পূর্ণ কাজ (Q1-Q4)

```dataviewjs
const pages = dv.pages('"01_Daily_Action_Plans"')
  .where(p => p.file.ctime >= dv.date("today") - dv.duration("7 days"));

const quadrants = [
  {id:"Q1", label:"🔴 Q1 — এখনই করুন", color:"#FAECE7", border:"#D85A30"},
  {id:"Q2", label:"🟡 Q2 — শিডিউল করুন", color:"#FAEEDA", border:"#B8960F"},
  {id:"Q3", label:"🟠 Q3 — ডেলিগেট করুন", color:"#E6F1FB", border:"#378ADD"},
  {id:"Q4", label:"⚪ Q4 — বাদ দিন", color:"var(--background-secondary)", border:"var(--background-modifier-border)"},
];

let html = `<div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;margin:10px 0">`;
for (const q of quadrants) {
  const tasks = [];
  for (const p of pages) {
    for (const t of (p.file.tasks ?? [])) {
      if (!t.completed && t.text.includes(`[${q.id}]`)) tasks.push(t.text.replace(`[${q.id}]`,"").trim());
    }
  }
  html += `<div style="background:${q.color};border:2px solid ${q.border};border-radius:12px;padding:14px">
    <div style="font-size:14px;font-weight:700;margin-bottom:10px;color:var(--text-normal)">${q.label}</div>
    ${tasks.length ? tasks.slice(0,3).map(t=>`<div style="font-size:12px;padding:4px 0;border-bottom:1px solid rgba(0,0,0,0.08);margin-bottom:4px">${t}</div>`).join("") : '<div style="font-size:12px;color:var(--text-muted);font-style:italic">সম্পূর্ণ বা খালি</div>'}
  </div>`;
}
html += `</div>`;
dv.container.innerHTML = html;
```

---

## 🕌 সালাহ কনসিস্টেন্সি চার্ট — ৩০ দিন (গোল্ডেন-গ্রীন)

```dataviewjs
const pages = dv.pages('"01_Daily_Action_Plans"')
  .where(p => p.file.ctime >= dv.date("today") - dv.duration("30 days"));
const total = pages.length || 1;
const prayers = [
  {key:"fajr",label:"ফজর 🌅"},{key:"dhuhr",label:"যোহর ☀️"},
  {key:"asr",label:"আসর 🌤️"},{key:"maghrib",label:"মাগরিব 🌆"},
  {key:"isha",label:"এশা 🌙"},{key:"qiyam_layl",label:"কিয়াম ⭐"}
];
const bars = prayers.map(p => {
  const done = pages.where(pg => pg[p.key] === true).length;
  const pct = Math.round((done/total)*100);
  const c = pct>=90?"#1D9E75":pct>=70?"#6BA83F":pct>=50?"#B8960F":"#D85A30";
  return `<div style="margin:8px 0;display:flex;align-items:center;gap:10px">
    <span style="width:90px;font-size:12px;font-weight:600">${p.label}</span>
    <div style="flex:1;background:var(--background-secondary);border-radius:8px;height:22px;overflow:hidden">
      <div style="width:${pct}%;background:${c};height:100%;border-radius:8px;display:flex;align-items:center;justify-content:flex-end;padding-right:8px">
        <span style="color:white;font-size:11px;font-weight:700">${pct}%</span>
      </div>
    </div>
    <span style="font-size:11px;color:var(--text-muted);width:50px">${done}/${total}</span>
  </div>`;
}).join("");
dv.container.innerHTML = `<div style="padding:10px 0">${bars}</div>`;
```

---

## 🍅 পোমোডোরো পারফরম্যান্স — এই সপ্তাহ

```dataviewjs
const pages = dv.pages('"03_Pomodoro_Tracker"')
  .where(p => p.file.ctime >= dv.date("today") - dv.duration("7 days"))
  .where(p => p.file.name !== "Pomodoro_Analytics" && p.file.name !== "Pomodoro_Log_Template")
  .sort(p => p.file.name, "asc");

const bars = pages.map(p => {
  const day = p.file.name.slice(-5);
  const completed = p.completed_pomodoros ?? 0;
  const planned = p.total_pomodoros ?? 1;
  const pct = Math.round((completed / planned) * 100);
  const color = pct >= 80 ? "#1D9E75" : pct >= 60 ? "#6BA83F" : pct >= 40 ? "#B8960F" : "#D85A30";
  
  return `<div style="display:flex;flex-direction:column;align-items:center;gap:6px;flex:1;min-width:50px">
    <span style="font-size:12px;font-weight:700;color:${color}">${completed}/${planned}</span>
    <div style="width:36px;background:var(--background-secondary);border-radius:6px;height:70px;display:flex;align-items:flex-end;overflow:hidden">
      <div style="width:100%;height:${pct}%;background:${color};border-radius:6px;transition:height 0.3s"></div>
    </div>
    <span style="font-size:10px;color:var(--text-muted)">${day}</span>
  </div>`;
}).join("");

dv.container.innerHTML = `<div style="display:flex;align-items:flex-end;gap:8px;padding:12px 0;height:110px;justify-content:space-around">${bars || '<p style="color:var(--text-muted)">কোনো ডেটা নেই</p>'}</div>`;
```

---

## 📊 হ্যাবিট চার্ট — ৩০ দিন (গোল্ডেন-গ্রীন রঙ)

```dataviewjs
const pages = dv.pages('"01_Daily_Action_Plans"')
  .where(p => p.file.ctime >= dv.date("today") - dv.duration("30 days"));
const total = pages.length || 1;
const habits = [
  {key:"exercise",label:"🏃 ব্যায়াম"},{key:"book_reading",label:"📚 বই পড়া"},
  {key:"journaling",label:"📝 জার্নাল"},{key:"family_time",label:"👨‍👩‍👧 পরিবার"},
  {key:"morning_adhkaar",label:"🌅 সকালের যিকির"},{key:"sleep_adequate",label:"😴 ঘুম"},
  {key:"volunteer_sadaqah",label:"💚 সাদাকাহ"},{key:"hadith_study",label:"📜 হাদিস"}
];
const bars = habits.map(h => {
  const done = pages.where(p => p[h.key] === true).length;
  const pct = Math.round((done/total)*100);
  const c = pct>=80?"#1D9E75":pct>=60?"#6BA83F":pct>=40?"#B8960F":"#D85A30";
  return `<div style="margin:6px 0;display:flex;align-items:center;gap:10px">
    <span style="width:140px;font-size:12px;font-weight:500">${h.label}</span>
    <div style="flex:1;background:var(--background-secondary);border-radius:6px;height:18px;overflow:hidden">
      <div style="width:${pct}%;background:${c};height:100%;border-radius:6px;transition:width 0.3s"></div>
    </div>
    <span style="font-size:11px;color:var(--text-muted);width:40px;text-align:right">${pct}%</span>
  </div>`;
}).join("");
dv.container.innerHTML = `<div style="padding:10px 0">${bars}</div>`;
```

---

## 💧 পানি ট্র্যাকার চার্ট — গত ৭ দিন

```dataviewjs
const pages = dv.pages('"01_Daily_Action_Plans"')
  .where(p => p.file.ctime >= dv.date("today") - dv.duration("7 days"))
  .sort(p => p.file.name, "asc");
const max = Math.max(...pages.map(p => p.water_intake ?? 0), 8);
const bars = pages.map(p => {
  const val = p.water_intake ?? 0;
  const pct = Math.round((val/max)*100);
  const c = val>=8?"#1D9E75":val>=6?"#6BA83F":"#B8960F";
  const day = p.file.name.slice(5);
  return `<div style="display:flex;flex-direction:column;align-items:center;gap:4px;flex:1">
    <span style="font-size:11px;font-weight:700;color:${c}">${val}</span>
    <div style="width:32px;background:var(--background-secondary);border-radius:5px;height:70px;display:flex;align-items:flex-end;overflow:hidden">
      <div style="width:100%;height:${pct}%;background:${c};border-radius:5px;transition:height 0.3s"></div>
    </div>
    <span style="font-size:10px;color:var(--text-muted)">${day}</span>
  </div>`;
}).join("");
dv.container.innerHTML = `<div style="display:flex;align-items:flex-end;gap:8px;padding:10px 0;height:110px;justify-content:space-around">${bars}</div>`;
```

---

## 🎁 রিওয়ার্ড প্রোগ্রেস (গোল্ডেন-গ্রীন গ্র্যাডিয়েন্ট)

```dataviewjs
const pts = dv.pages('"01_Daily_Action_Plans"').map(p=>p.daily_points??0).reduce((a,b)=>a+b,0);
const tiers=[
  {p:50,l:"🥉 হালাল বিনোদন"},
  {p:100,l:"🥈 পছন্দের বই/খাবার"},
  {p:250,l:"🥇 পরিবারের আউটিং"},
  {p:500,l:"💎 ভ্রমণ পরিকল্পনা"},
  {p:1000,l:"👑 আল্লাহর সন্তুষ্টি"}
];
const next=tiers.find(t=>t.p>pts)??tiers[4];
const pct=Math.min(Math.round((pts/next.p)*100),100);
dv.container.innerHTML=`<div style="padding:16px;background:var(--background-secondary);border-radius:14px;border:2px solid #B8960F">
  <div style="font-size:36px;font-weight:800;background:linear-gradient(135deg,#B8960F,#1D9E75);-webkit-background-clip:text;-webkit-text-fill-color:transparent;margin-bottom:8px">${pts} pts</div>
  <div style="font-size:13px;color:var(--text-normal);margin:8px 0;font-weight:600">পরবর্তী: <b>${next.l}</b></div>
  <div style="font-size:11px;color:var(--text-muted);margin-bottom:10px">${next.p} পয়েন্ট প্রয়োজন</div>
  <div style="background:var(--background-primary);border-radius:20px;height:14px;overflow:hidden;margin-bottom:8px;border:1px solid #B8960F">
    <div style="width:${pct}%;background:linear-gradient(90deg,#B8960F,#6BA83F,#1D9E75);height:100%;border-radius:20px;transition:width 0.5s"></div>
  </div>
  <div style="font-size:11px;color:var(--text-muted)">${pct}% সম্পূর্ণ — আরও ${next.p-pts} পয়েন্ট বাকি</div>
</div>`;
```

---

## 📈 সাম্প্রতিক পরিবর্তন (সর্বশেষ ৫টি করে)

### 📅 দৈনিক নোট
```dataview
TABLE daily_points AS "পয়েন্ট", productivity_level AS "⚡", quran_pages AS "📖", completed_pomodoros AS "🍅"
FROM "01_Daily_Action_Plans"
SORT file.mtime DESC
LIMIT 5
```

### 🍅 পোমোডোরো সেশন
```dataview
TABLE total_pomodoros AS "পরিকল্পিত", completed_pomodoros AS "সম্পন্ন", total_minutes AS "মিনিট"
FROM "03_Pomodoro_Tracker"
WHERE file.name != "Pomodoro_Analytics" AND file.name != "Pomodoro_Log_Template"
SORT file.mtime DESC
LIMIT 5
```

### 📋 রিভিউ ও লক্ষ্য
```dataview
TABLE file.folder AS "বিভাগ", file.mtime AS "পরিবর্তন"
FROM "02_Weekly_Monthly_Reviews" OR "03_Goals_and_Life_Wheel"
SORT file.mtime DESC
LIMIT 5
```

---

## 🔗 দ্রুত নেভিগেশন

| 📅 পরিকল্পনা | 📊 বিশ্লেষণ | 🎯 লক্ষ্য | 📚 শিক্ষা | 🍅 ফোকাস |
|---|---|---|---|---|
| [[01_Daily_Action_Plans/01_Daily_Action_Plans_README\|আজকের প্ল্যান]] | [[06_MOCs/MOC_Prayer_Analytics\|সালাহ চার্ট]] | [[03_Goals_and_Life_Wheel/Goal_Setting\|লক্ষ্য নির্ধারণ]] | [[04_Spaced_Repetition_Library/\|ফ্ল্যাশকার্ড]] | [[03_Pomodoro_Tracker/Pomodoro_Analytics\|পোমোডোরো হাব]] |
| [[02_Weekly_Monthly_Reviews/\|রিভিউ]] | [[06_MOCs/MOC_Habit_Tracking\|হ্যাবিট চার্ট]] | [[03_Goals_and_Life_Wheel/Life_Balance_Wheel\|লাইফ হুইল]] | [[06_MOCs/MOC_Quran_Study\|কুরআন স্টাডি]] | [[03_Pomodoro_Tracker/Pomodoro_Log_Template\|নতুন সেশন]] |
| [[06_MOCs/MOC_Main_Hub\|মাস্টার হাব]] | [[05_Friction_and_Error_Logs/\|এরর লগ]] | [[03_Goals_and_Life_Wheel/Personal_Checklist\|চেকলিস্ট]] | [[Improvement_Suggestions\|উন্নতি পরামর্শ]] | — |

---

## ✨ সাজেশন

> [!info|gold-green] **গোল্ডেন-গ্রীন থিম**
> সকল শিরোনাম, উদ্ধৃতি এবং গ্রাফ এখন গোল্ডেন-গ্রীন গ্র্যাডিয়েন্ট ব্যবহার করছে:
> - **Gold**: `#B8960F` (প্রধান)
> - **Light Green**: `#6BA83F` (মধ্য)
> - **Dark Green**: `#1D9E75` (জোর)

---

*সর্বশেষ আপডেট: 2026-04-26 | গোল্ডেন-গ্রীন থিম সক্রিয়*
