# 🖥️ Dashboard Design Notes

Supplementary notes for `spotify-dashboard.pbix`, expanding on the Phase 4 summary in `../report.md`.

---

## 🎯 Design Goals

- Read in under 10 seconds by someone who has never seen the dataset
- One page, no scrolling, no tab-hopping between multiple report pages
- KPI cards first, detail visuals second — executive-summary layout, not an exploratory notebook

---

## 🎨 Visual Theme

| Element | Choice |
|---|---|
| Background | Dark theme (near-black) |
| Accent palette | Spotify-inspired green, with 2–3 supporting neutrals for contrast |
| Typography | Single consistent font family across all visuals; larger weight for KPI numbers, lighter weight for labels |
| Chart borders | Minimal / none — separation via spacing and background contrast instead of boxes |
| Data labels | Shown only where they aid reading (e.g., top bars); suppressed where they'd clutter (e.g., scatter plot) |

**Rationale:** a dark theme with a single accent color reads as "product dashboard" rather than "default Power BI report," and reduces visual competition between the 7 visuals on one page.

---

## 📊 KPI Card Row

| KPI | Value | Source |
|---|---:|---|
| Total Tracks | 89.74K | `spotify_clean` (post-deduplication) |
| Total Artists | 31.43K | `spotify_clean` |
| Total Genres | 113 | `spotify_clean` / `genre_summary` |
| Average Popularity | 33.20 | `spotify_clean` |

Placed top-of-page, left-to-right, so scale (tracks/artists/genres) is established before any detail visual is read.

---

## 🖱️ Interactivity

- **Cross-filtering:** clicking a genre in the Genre Analysis bar chart filters every other visual on the page (Popularity Distribution, Top Artists, Top Tracks, Audio Feature Comparison)
- **Tooltips:** default tooltips retained on the scatter plot (Q6) to surface track name/artist on hover, since the visual has no data labels
- **Sort control:** Top Artists and Top Tracks are sorted descending by default, with the field well left open for the viewer to re-sort by a different measure if needed

---

## 📈 Visual-by-Visual Notes

**Q1 — Popularity Distribution (Donut):** buckets `popularity_category` (Low/Medium/High) rather than raw popularity, so the shape of the catalog is legible at a glance instead of a dense histogram.

**Q2 — Genre Analysis (Horizontal Bar):** horizontal orientation chosen because genre names are long strings — vertical bars would force rotated axis labels, which are harder to scan.

**Q3 — Top Artists (Horizontal Bar):** capped to a top-N view (not the full 31.43K artists) — the point is ranking, not a complete listing.

**Q4 — Top Tracks (Table):** kept as a table rather than a chart since the ask here is precise lookup (exact track/artist/score), not pattern recognition.

**Q5 — Audio Feature Comparison (Horizontal Bar, from `audio_features_long`):** the unpivoted long format is what makes a single bar chart able to compare all 8 audio features side-by-side, instead of needing 8 separate visuals.

**Q6 — Audio Features vs Popularity (Scatter):** deliberately left without a trend line — the underlying relationship isn't strongly linear (see `../report.md`, Phase 5), and a trend line would overstate the relationship.

**Q7 — Genre vs Audio Features (Matrix, from `audio_features_long`):** matrix chosen over a chart because it's a genre × feature grid — this is inherently tabular, and conditional-formatting-style shading (if enabled) does the pattern-spotting work that a chart would otherwise need multiple small multiples to do.

---

## 🖼️ Screenshots

See `screenshots/` for exported page views. (Add updated exports here whenever the dashboard visuals change materially.)

---

## 🔭 Possible Follow-ups

- Add a genre slicer pinned to the top of the page instead of relying solely on bar-chart cross-filtering
- Add bookmarks for 2–3 pre-set "views" (e.g., "High popularity only", "By decade" if a date field is added)
- Revisit color contrast for accessibility (WCAG) once the palette is finalized
