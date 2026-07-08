# ➕ Power Query — Append Queries Demo

This document is a standalone technique reference. **Append is not part of the main `spotify_clean` pipeline** — the production model uses relationships (see `../report.md`, Phase 3) instead of physically stacking tables. This demo exists to show the technique was deliberately considered and understood, not accidentally skipped.

---

## 🎯 Purpose

Append Queries is used when you have **the same columns, different rows** — e.g., combining multiple exports of the same shape into one table. It is the Power Query equivalent of a SQL `UNION ALL`.

---

## 🧪 Demo Scenario

To exercise the technique against this dataset:

1. Split `spotify_clean` into two sample slices with identical columns:
   - `spotify_part_A` — first half of `track_genre` values (alphabetically)
   - `spotify_part_B` — remaining `track_genre` values
2. Use **Home → Append Queries → Append Queries as New** to combine them back into `spotify_appended`
3. Validate row count parity: `count(spotify_part_A) + count(spotify_part_B) = count(spotify_appended)`

---

## 🧩 Steps in Power Query Editor

1. `Home` → `Combine` → `Append Queries` → `Append Queries as New`
2. Choose **Two tables** (or **Three or more** if combining multiple batches)
3. Select the primary table, then the table(s) to stack underneath it
4. Power Query generates M code equivalent to:

```m
Table.Combine({SpotifyPartA, SpotifyPartB})
```

5. Confirm column names and types match exactly between sources — mismatched types will coerce or error
6. Rename the resulting query (e.g., `spotify_appended`) and load or reference downstream

---

## ⚠️ When Append Would Be the Wrong Choice Here

Appending `spotify_clean`, `genre_summary`, and `audio_features_long` directly would **not** make sense in this project, because those three tables have **different grains** (track-level, genre-level, feature-level) and mostly different columns. Stacking them would produce a table full of blanks and mismatched semantics. That's exactly why this project uses a **relationship model** instead — see Phase 3 in `../report.md`.

---

## ✅ When Append *Would* Be the Right Choice

- Monthly exports of the same Spotify extract format landing in separate CSVs
- Combining a "new releases" batch with the historical catalog before deduplication (Phase 2)
- Merging regional exports (e.g., `spotify_us.csv`, `spotify_uk.csv`) that share identical schema

---

## 📌 Takeaway

Append = **same shape, more rows**. It was evaluated for this project and consciously not used in the core pipeline, since the three analytical tables here differ in grain and are better connected via a relationship model.
