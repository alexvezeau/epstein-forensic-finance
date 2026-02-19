# Forensic Financial Analysis of the DOJ EFTA Corpus

**Independent research**

An automated forensic financial analysis of the full Department of Justice disclosure under the Epstein Files Transparency Act (Public Law 118-299). Built from scratch by a single independent researcher in 12 days using Python and SQLite.

---

## Key Findings

- **1.83 million files** ingested across 12 DOJ datasets plus community-sourced archives
- **$1.10 billion** in financial activity classified across **24,623 transactions**
- **18 transaction categories** including wire transfers, shell corporations, real estate, aviation, legal fees, and victim/trafficking indicators
- **Three-tier confidence model** separating court-confirmed amounts from dataset-sourced and entity-matched estimates
- **59.2% SAR coverage** against known Suspicious Activity Reports — identifying a **$322 million unclassified gap**
- **296 of 303 names** (97.7%) from the DOJ's "politically exposed persons" list matched to source documents with hyperlinked evidence

---

## Pipeline Overview

The analysis pipeline processes raw government PDFs through extraction, classification, and cross-referencing:

```
Corpus Assembly  →  Indexed 1.83M files from DOJ site, torrents, ZIP archives, manifests
Text Extraction  →  PyMuPDF native text + Tesseract OCR fallback on scanned documents
Entity Recognition  →  spaCy NLP across full corpus (11.4M entities, 734K persons)
Financial Classification  →  885-keyword system with 3-tier confidence scoring
Fund Flow Mapping  →  Entity-to-entity transaction reconstruction
Person-of-Interest Ranking  →  Weighted composite scoring with news-source filtering
DOJ 303 Cross-Reference  →  Navigation tool with dual hyperlinks to source files
```

---

## Deliverables

| Deliverable | Description |
|---|---|
| **Financial Summary** | $1.10B classified across 18 categories with confidence tiers and SAR benchmarks |
| **Person-of-Interest Rankings** | Scored entity list filtered for false positives, news contamination, and OCR artifacts |
| **DOJ 303 Cross-Reference** | 296/303 names matched with signal-level scoring and hyperlinked source documents |
| **Methodology Documentation** | Pipeline architecture, classification logic, deduplication rules, known limitations |

All deliverables use SSFS (Staff-Friendly Spreadsheet) formatting — designed for non-technical readers with sortable columns, plain-language headers, and embedded navigation.

---

## Corpus Statistics

| Metric | Count |
|---|---|
| Total files indexed | 1,830,154 |
| PDFs in corpus | 1,828,246 |
| Text extractions | 1,852,060 |
| Entities extracted | 11,438,106 |
| Unique persons identified | 734,122 |
| Financial transactions | 24,623 |
| Total classified value | $1,102,152,148 |
| DOJ 303 names matched | 296 / 303 |

---

## Technical Notes

**Database:** SQLite with WAL mode (~4.7 GB). Concurrent read/write architecture supporting extraction, NLP, and analysis simultaneously.

**Classification system:** 885 financial keywords across 18 categories. Three-tier confidence model: Tier 1 (court-confirmed via DB-SDNY), Tier 2 (dataset-sourced with document context), Tier 3 (entity-matched through co-occurrence). Deduplication prevents double-counting across tiers.

**Noise filtering:** 40+ false-positive exclusion patterns for aviation entities, geographic names, media article contamination, and OCR artifacts. Person-of-interest rankings require ≥2 non-news file appearances.

**SAR benchmarks:** JPMorgan Chase ($1.1B), Deutsche Bank ($400M), Bank of New York Mellon ($378M). Coverage analysis identifies which classified transactions fall within known SAR filings versus the unclassified gap.

---

## Scope and Limitations

This analysis covers financial patterns and entity relationships. It does not attempt to establish guilt, assign criminal liability, or substitute for law enforcement investigation. All findings carry appropriate confidence disclaimers per the methodology documentation.

The DOJ EFTA corpus contains known gaps, including documents withdrawn after release and redacted content. Financial totals represent a lower bound — actual activity likely exceeds classified amounts.

---

## About

**Randall Scott**
MS Applied Data Science, Syracuse University
BS Network & Cyber Security, Wilmington University
ORCID: [0009-0000-1773-2572](https://orcid.org/0009-0000-1773-2572)

This research was conducted independently with no institutional affiliation or funding, using only publicly available government records.

---

## License

This repository contains findings and methodology documentation only. The underlying pipeline, database, and source code are not included. Inquiries from qualified researchers may be directed through GitHub.
