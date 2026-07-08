# 🔗 Power Query — Merge Queries Demo

This document is a standalone technique reference. **Merge is not used in the production model** — the final design uses native Power BI **relationships** between `spotify_clean`, `genre_summary`, and `audio_features_long` instead of flattening them with a Power Query Merge (see `../report.md`, Phase 3, and the "Modeling Principles" note there). This demo shows the technique was evaluated, and documents *why* relationships were chosen instead.

---

## 🎯 Purpose

Merge Queries is used when you have **different columns, a shared key** — e.g., enriching one table with columns from another. It is the Power Query equivalent of a SQL `JOIN`.

---

## 🧪 Demo Scenario

To exercise the technique against this dataset:

1. Take `spotify_clean` (track-level) and `genre_summary` (genre-level: Track Count, Avg Popularity)
2. Use **Home → Merge Queries** to join them on the shared key `track_genre`
3. Expand the `Avg Popularity` and `Track Count` columns from `genre_summary` into a new flattened query, `spotify_with_genre_stats`

---

## 🧩 Steps in Power Query Editor

1. Open `spotify_clean` → `Home` → `Combine` → `Merge Queries`
2. Select `genre_summary` as the table to merge with
3. Click the matching column in both tables: `track_genre` ↔ `track_genre`
4. Choose a join kind:

| Join Kind | Behavior |
|---|---|
| Left Outer | Keep all rows from `spotify_clean`, matched columns where available |
| Inner | Keep only tracks whose genre exists in `genre_summary` |
| Right Outer | Keep all genres from `genre_summary`, matched tracks where available |
| Full Outer | Keep everything from both sides |

5. For this demo, **Left Outer** is the natural choice — every track should be retained even if a genre-level stat is momentarily missing
6. Expand the new `genre_summary` column, selecting `Track Count` and `Avg Popularity`
7. Resulting M code is equivalent to:

```m
Table.NestedJoin(
    SpotifyClean, {"track_genre"},
    GenreSummary, {"track_genre"},
    "genre_summary", JoinKind.LeftOuter
)
```

---

## ⚠️ Why This Wasn't Used in the Production Model

Merging `genre_summary` (and similarly `audio_features_long`) directly into `spotify_clean` would:

- **Flatten the model to a single wide table**, which loses the ability to independently slice at the genre grain or the feature grain in Power BI visuals
- **Duplicate genre-level values** across every matching track row, inflating the apparent size of the dataset and making `Track Count` / `Avg Popularity` misleading if re-aggregated
- Make the model harder to maintain — any change to `genre_summary` would require re-running the merge, instead of Power BI simply re-evaluating the relationship

This is why the project uses **relationships in the Model view** instead (`spotify_clean[track_genre]` → `genre_summary[track_genre]`, and `spotify_clean[track_id]` → `audio_features_long[track_id]`) — same analytical outcome, without the row-duplication risk.

---

## ✅ When Merge *Would* Be the Right Choice

- One-off exports where the destination is a flat CSV/Excel file (not a Power BI model)
- Enriching a lookup table permanently before loading, when relationship modeling isn't available downstream
- Validating join cardinality during development, before deciding on a relationship-based design

---

## 📌 Takeaway

Merge = **different shape, shared key, flattened result**. It was evaluated for this project and consciously replaced by a relationship-based model to avoid duplication and keep each table at its natural grain.
