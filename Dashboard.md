---
banner: "https://images.unsplash.com/photo-1564769625905-50e93615e769?w=1400&q=80"
banner_y: 0.4
cssclass: dashboard
tags: [dashboard, home]
---

# 🌙 Productive Muslim Vault

> [!quote] "নিয়তের উপরেই কাজের ফলাফল নির্ভরশীল।" — সহীহ বুখারি ১

---

## 🚨 তাৎক্ষণিক মনোযোগ প্রয়োজন

> [!danger] ⚡ Q1 — এখনই করুন (Urgent + Important)
> ```dataview
> TASK FROM "01_Daily_Action_Plans"
> WHERE !completed AND contains(text, "[Q1]")
> WHERE file.ctime >= date(today) - dur(2 days)
> LIMIT 3
> ```

> [!warning] 📋 Q2 — শিডিউল করুন (Important, Not Urgent)
> ```dataview
> TASK FROM "01_Daily_Action_Plans"
> WHERE !completed AND contains(text, "[Q2]")
> WHERE file.ctime >= date(today) - dur(3 days)
> LIMIT 3
> ```

> [!caution] ⚠️ মিসড সালাহ — গত ৩ দিন
> ```dataview
> TABLE fajr AS "ফজর", dhuhr AS "যোহর", asr AS "আসর", maghrib AS "মাগরিব", isha AS "এশা"
> FROM "01_Daily_Action_Plans"
> WHERE (fajr = false OR dhuhr = false OR asr = false OR maghrib = false OR isha = false)
> WHERE file.ctime >= date(today) - dur(3 days)
> SORT file.name DESC
> LIMIT 3
> ```

> [!bug] 🛑 পুনরাবৃত্তি এরর — এই সপ্তাহ
> ```dataview
> TABLE friction_type AS "ধরন"
> FROM #log/error
> WHERE file.ctime >= date(today) - dur(7 days)
> SORT file.mtime DESC
> LIMIT 3
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

## 🔥 হিটম্যাপ — ৩০ দিনের সামঞ্জস্য

```dataviewjs
const cal = {
  year: moment().year(),
  colors: { teal: ["#E1F5EE","#9FE1CB","#5DCAA5","#1D9E75","#0F6E56"] },
  showCurrentDayBorder: true,
  defaultEntryIntensity: 0,
  entries: []
};
for (let p of dv.pages('"01_Daily_Action_Plans"').where(p => p.daily_points > 0)) {
  cal.entries.push({
    date: p.file.name,
    intensity: Math.min(Math.floor((p.daily_points ?? 0) / 5), 4),
    content: `✅ ${p.daily_points}pts | ⚡${p.productivity_level ?? "-"}`
  });
}
renderHeatmapCalendar(this.container, cal);
```

---

## ⚡ আইজেনহাওয়ার ম্যাট্রিক্স — অসম্পূর্ণ কাজ

```dataviewjs
const pages = dv.pages('"01_Daily_Action_Plans"')
  .where(p => p.file.ctime >= dv.date("today") - dv.duration("7 days"));

const quadrants = [
  {id:"Q1", label:"🔴 Q1 — এখনই করুন", color:"#FAECE7", border:"#D85A30"},
  {id:"Q2", label:"🟡 Q2 — শিডিউল করুন", color:"#FAEEDA", border:"#BA7517"},
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
  html += `<div style="background:${q.color};border:1.5px solid ${q.border};border-radius:10px;padding:12px">
    <div style="font-size:13px;font-weight:700;margin-bottom:8px;color:var(--text-normal)">${q.label}</div>
    ${tasks.length ? tasks.slice(0,3).map(t=>`<div style="font-size:12px;padding:3px 0;border-bottom:1px solid rgba(0,0,0,0.06)">${t}</div>`).join("") : '<div style="font-size:12px;color:var(--text-muted)">✓ সব সম্পন্ন</div>'}
  </div>`;
}
html += `</div>`;
dv.container.innerHTML = html;
```

---

## 🕌 সালাহ কনসিস্টেন্সি চার্ট — ৩০ দিন

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
  const c = pct>=90?"#1D9E75":pct>=70?"#378ADD":pct>=50?"#BA7517":"#D85A30";
  return `<div style="margin:6px 0;display:flex;align-items:center;gap:8px">
    <span style="width:80px;font-size:12px;font-weight:600">${p.label}</span>
    <div style="flex:1;background:var(--background-secondary);border-radius:6px;height:20px;overflow:hidden">
      <div style="width:${pct}%;background:${c};height:100%;border-radius:6px;display:flex;align-items:center;justify-content:flex-end;padding-right:6px">
        <span style="color:white;font-size:10px;font-weight:700">${pct}%</span>
      </div>
    </div>
    <span style="font-size:11px;color:var(--text-muted);width:45px">${done}/${total}</span>
  </div>`;
}).join("");
dv.container.innerHTML = `<div style="padding:8px 0">${bars}</div>`;
```

---

## 📊 হ্যাবিট চার্ট — ৩০ দিন

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
  const c = pct>=80?"#1D9E75":pct>=60?"#378ADD":pct>=40?"#BA7517":"#D85A30";
  return `<div style="margin:4px 0;display:flex;align-items:center;gap:8px">
    <span style="width:130px;font-size:12px">${h.label}</span>
    <div style="flex:1;background:var(--background-secondary);border-radius:5px;height:16px;overflow:hidden">
      <div style="width:${pct}%;background:${c};height:100%;border-radius:5px"></div>
    </div>
    <span style="font-size:11px;color:var(--text-muted);width:32px;text-align:right">${pct}%</span>
  </div>`;
}).join("");
dv.container.innerHTML = `<div style="padding:8px 0">${bars}</div>`;
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
  const c = val>=8?"#1D9E75":val>=6?"#378ADD":"#BA7517";
  const day = p.file.name.slice(5); // MM-DD
  return `<div style="display:flex;flex-direction:column;align-items:center;gap:4px;flex:1">
    <span style="font-size:11px;font-weight:600;color:${c}">${val}</span>
    <div style="width:28px;background:var(--background-secondary);border-radius:4px;height:60px;display:flex;align-items:flex-end;overflow:hidden">
      <div style="width:100%;height:${pct}%;background:${c};border-radius:4px;transition:height 0.3s"></div>
    </div>
    <span style="font-size:10px;color:var(--text-muted)">${day}</span>
  </div>`;
}).join("");
dv.container.innerHTML = `<div style="display:flex;align-items:flex-end;gap:6px;padding:8px 0;height:100px">${bars}
  <div style="font-size:10px;color:var(--text-muted);writing-mode:vertical-lr;transform:rotate(180deg);padding-bottom:4px">গ্লাস/দিন</div>
</div>`;
```

---

## 🔄 সাম্প্রতিক পরিবর্তন (সর্বশেষ ৫টি করে)

### 📅 দৈনিক নোট
```dataview
TABLE daily_points AS "পয়েন্ট", productivity_level AS "⚡", quran_pages AS "📖"
FROM "01_Daily_Action_Plans"
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

### 🧠 ফ্ল্যাশকার্ড ও MOC
```dataview
TABLE file.folder AS "বিভাগ"
FROM "04_Spaced_Repetition_Library" OR "06_MOCs"
SORT file.mtime DESC
LIMIT 5
```

---

## 🎁 রিওয়ার্ড প্রোগ্রেস

```dataviewjs
const pts = dv.pages('"01_Daily_Action_Plans"').map(p=>p.daily_points??0).reduce((a,b)=>a+b,0);
const tiers=[{p:50,l:"🥉 হালাল বিনোদন"},{p:100,l:"🥈 পছন্দের বই/খাবার"},{p:250,l:"🥇 পরিবারের আউটিং"},{p:500,l:"💎 ছোট ট্রিপ"},{p:1000,l:"👑 স্বপ্নের পুরস্কার"}];
const next=tiers.find(t=>t.p>pts)??tiers[4];
const pct=Math.min(Math.round((pts/next.p)*100),100);
dv.container.innerHTML=`<div style="padding:14px;background:var(--background-secondary);border-radius:12px;border:1px solid var(--background-modifier-border)">
  <div style="font-size:32px;font-weight:800;background:linear-gradient(135deg,#1D9E75,#378ADD);-webkit-background-clip:text;-webkit-text-fill-color:transparent">${pts} pts</div>
  <div style="font-size:12px;color:var(--text-muted);margin:6px 0">পরবর্তী: <b>${next.l}</b> (${next.p} pts দরকার)</div>
  <div style="background:var(--background-primary);border-radius:20px;height:12px;overflow:hidden;margin-top:8px">
    <div style="width:${pct}%;background:linear-gradient(90deg,#1D9E75,#378ADD);height:100%;border-radius:20px"></div>
  </div>
  <div style="font-size:11px;color:var(--text-muted);margin-top:5px">${pct}% — আরও ${next.p-pts} পয়েন্ট বাকি</div>
</div>`;
```

---

## 🔗 দ্রুত নেভিগেশন

| 📅 পরিকল্পনা | 📊 বিশ্লেষণ | 🎯 লক্ষ্য | 📚 শিক্ষা |
|---|---|---|---|
| [[01_Daily_Action_Plans/\|আজকের প্ল্যান]] | [[06_MOCs/MOC_Prayer_Analytics\|সালাহ চার্ট]] | [[03_Goals_and_Life_Wheel/Goal_Setting\|লক্ষ্যমালা]] | [[04_Spaced_Repetition_Library/\|ফ্ল্যাশকার্ড]] |
| [[02_Weekly_Monthly_Reviews/\|রিভিউ]] | [[06_MOCs/MOC_Habit_Tracking\|হ্যাবিট চার্ট]] | [[03_Goals_and_Life_Wheel/Life_Balance_Wheel\|লাইফ হুইল]] | [[06_MOCs/MOC_Quran_Study\|কুরআন হাব]] |
| [[06_MOCs/MOC_Main_Hub\|মাস্টার হাব 🗺️]] | [[05_Friction_and_Error_Logs/\|এরর লগ]] | [[03_Goals_and_Life_Wheel/Personal_Checklist\|চেকলিস্ট]] | [[03_Goals_and_Life_Wheel/Productive_Inner_Dialogue\|ইনার ডায়ালগ]] |
