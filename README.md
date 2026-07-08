# 🎧 Spotify Power BI Analytics

![Power BI](https://img.shields.io/badge/Power%20BI-Analytics-F2C811?logo=powerbi)
![Status](https://img.shields.io/badge/Status-Completed-success)
![Type](https://img.shields.io/badge/Project-Data%20Analytics-blue)

---

## 📌 Project Overview

An end-to-end **Power BI analytics project** built on a public Spotify tracks dataset (114,000 rows / 21 columns).

The project was built as a hands-on introduction to the Power BI ecosystem — going from raw, duplicated data all the way to a structured semantic model and an interactive dashboard. It intentionally covers the parts of the workflow that come *before* dashboarding (profiling, cleaning, reshaping, modeling), which is where most of the real analytical decisions happen.

> **Scope note:** This project focuses on Power Query (M) and data modeling fundamentals. DAX measures/calculated columns are **not** used yet — all KPIs and aggregations are produced upstream in Power Query. This is a deliberate scoping decision, not an oversight, and is called out as a "Next Steps" item below.

---

## 🧭 Project Roadmap (5 Phases)

### 🟢 Phase 1 — Data Understanding & Profiling
📂 [`power-query/transformations.md`](power-query/transformations.md)

- Dataset structure review (114,000 rows × 21 columns)
- Data type validation (no issues found)
- Column quality / distribution / profile checks
- Statistical overview of `popularity` (min, max, mean, std dev, distinct count)
- Duplicate detection at full-dataset and column level

### 🟡 Phase 2 — Data Cleaning & Feature Engineering
📂 [`power-query/transformations.md`](power-query/transformations.md)

- Duplicate removal using a composite business key (`artists`, `track_name`, `album_name`)
- Conditional column: `popularity_category` (Low / Medium / High)
- Genre-level aggregation via Group By
- Unpivot of 8 audio-feature columns into a long/tidy format

### 🔵 Phase 3 — Data Modeling
📂 [`report.md`](report.md)

- Star-schema-inspired model with one fact table and two supporting tables
- `spotify_clean[track_genre]` → `genre_summary[track_genre]`
- `spotify_clean[track_id]` → `audio_features_long[track_id]`
- One-to-many, single-direction relationships (Model view, no manual Merge joins)
- Two supplementary technique demos included for reference:
  - [`power-query/merge-demo.md`](power-query/merge-demo.md) — Merge Queries walkthrough
  - [`power-query/append-demo.md`](power-query/append-demo.md) — Append Queries walkthrough

### 🟣 Phase 4 — Dashboard Development
📂 [`dashboard/`](dashboard/)

- 4 executive KPI cards
- 7 business-oriented visuals (popularity, genre, top artists/tracks, audio features)
- Consistent dark theme, business-focused layout
- Design rationale documented in [`dashboard/dashboard-notes.md`](dashboard/dashboard-notes.md)

### 🟠 Phase 5 — Insights & Storytelling
📂 [`report.md`](report.md)

- Key findings translated into plain-language insights
- Interpretation of genre popularity patterns and audio-feature relationships
- Full write-up in the project report

---

## 📊 Datasets Produced

| Dataset | Description |
|---|---|
| `spotify_clean` | Cleaned, deduplicated fact table (~89,961 rows) |
| `genre_summary` | Genre-level aggregated metrics (track count, avg. popularity) |
| `audio_features_long` | Unpivoted, long-format audio feature dataset |

---

## 💡 Key Insights

- Most tracks fall in the low-to-medium popularity range
- Genre popularity varies significantly across the catalog
- Audio features enable deeper track-level analysis beyond popularity alone
- Relationships between audio features and popularity can be explored visually
- Interactive dashboards materially speed up analytical exploration vs. static reports

---

## 🛠️ Tools Used

- Power BI Desktop
- Power Query (M Language)
- Excel / CSV Dataset
- Git & GitHub

---

## 📁 Repository Structure

```text
spotify-powerbi-analytics/
│
├── data/
│   └── spotify.csv
│
├── power-query/
│   ├── append-demo.md
│   ├── merge-demo.md
│   └── transformations.md
│
├── dashboard/
│   ├── spotify-dashboard.pbix
│   ├── screenshots/
│   └── dashboard-notes.md
│
├── report.md
└── README.md
```

---
