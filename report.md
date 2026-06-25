# Spotify Power BI Project Report

## 🟢 Phase 1 — Data Exploration & Profiling

### Dataset Overview

| Metric                            |   Value |
| --------------------------------- | ------: |
| Raw Rows                          | 114,001 |
| Rows After Removing Empty Records | 114,000 |
| Total Columns                     |      21 |

### Dataset Columns

* track_id
* artists
* album_name
* track_name
* popularity
* duration_ms
* explicit
* danceability
* energy
* key
* loudness
* mode
* speechiness
* acousticness
* instrumentalness
* liveness
* valence
* tempo
* time_signature
* track_genre

### Data Quality Assessment

#### Data Types

All columns were reviewed and validated. Numeric and text fields were correctly assigned.

#### Missing Values

No significant missing values were detected after removing empty records.

#### Duplicate Investigation

Duplicate records were investigated using:

* artists
* track_name
* album_name

The analysis revealed a substantial number of duplicate song records in the dataset.

### Popularity Analysis

| Statistic          | Value |
| ------------------ | ----: |
| Minimum            |     0 |
| Maximum            |   100 |
| Average            | 33.23 |
| Standard Deviation |  22.3 |

### Key Findings

* The dataset contains a wide range of popularity values.
* Popularity distribution is skewed toward lower values.
* Many tracks have low popularity scores.
* Audio features provide strong opportunities for exploratory analysis and dashboard creation.

### Phase 1 Conclusion

The dataset was successfully profiled and assessed for quality. Initial exploration confirmed that the data is suitable for analytics and dashboard development.

---

## 🟡 Phase 2 — Data Cleaning & Transformations

### Duplicate Removal

Duplicates were removed using the following fields:

* artists
* track_name
* album_name

| Metric                    |   Value |
| ------------------------- | ------: |
| Rows Before Deduplication | 114,000 |
| Rows After Deduplication  |  89,378 |
| Removed Rows              |  24,622 |

### Feature Engineering

#### Popularity Category

A new analytical column was created:

| Popularity Range | Category |
| ---------------- | -------- |
| 0–30             | Low      |
| 31–70            | Medium   |
| 71–100           | High     |

### Genre Aggregation

The dataset was grouped by:

* track_genre

Metrics generated:

* Track Count
* Average Popularity

### Example Result

| Genre   | Track Count | Average Popularity |
| ------- | ----------: | -----------------: |
| Spanish |         937 |              39.82 |

### Summary

* 113 unique genres identified.
* Genre-level aggregation prepared for dashboard visualizations.
* Dataset transformed into an analytics-ready structure.

### Phase 2 Conclusion

The dataset was cleaned, validated, enriched with analytical categories, and prepared for dashboard development.
