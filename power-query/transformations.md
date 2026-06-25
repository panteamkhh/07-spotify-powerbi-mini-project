# Power Query Transformations Log

## 🟢 stage 1 — Data Profiling

### Profiling Tools Used

* Column Quality
* Column Distribution
* Column Profile

### Data Validation

Verified data types for all 21 columns.

Examples:

* popularity → Whole Number
* duration_ms → Whole Number
* danceability → Decimal Number
* energy → Decimal Number
* acousticness → Decimal Number

No significant data type issues were identified.

### Duplicate Investigation

Duplicate checks were performed using:

* artists
* track_name
* album_name

The investigation confirmed the presence of duplicate song records that would be addressed during the cleaning phase.

### Distribution Analysis

Popularity statistics:

* Minimum: 0
* Maximum: 100
* Mean: 33.23
* Standard Deviation: 22.3

Observation:

Popularity values are concentrated in lower ranges with fewer highly popular tracks.

---

## 🟡 stage 2 — Data Cleaning & Transformation

### Duplicate Removal

Deduplication fields:

* artists
* track_name
* album_name

Results:

* Rows before cleaning: 114,000
* Rows after cleaning: 89,378
* Removed records: 24,622

### Conditional Column

Created:

* popularity_category

Rules:

* 0–30 → Low
* 31–70 → Medium
* 71–100 → High

### Group By Operation

Grouping field:

* track_genre

Generated metrics:

* Track Count
* Average Popularity

Results:

* 113 unique genres

Example:

* Spanish

  * Track Count: 937
  * Average Popularity: 39.82

### Unpivot Practice

Audio feature columns were unpivoted to understand data reshaping techniques and prepare data structures for advanced visualizations.

### Final Output

The resulting dataset is:

* Cleaned
* Deduplicated
* Categorized
* Aggregated
* Ready for dashboard development
