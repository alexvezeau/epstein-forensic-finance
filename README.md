# EFTA Financial Forensics Pipeline

**The largest independent corpus and the only automated financial extraction pipeline built against the DOJ Epstein Files Transparency Act release.**

| Metric | This Project | DOJ Release | Next Largest Independent |
|--------|-------------|-------------|------------------------|
| **Files indexed** | 1,831,659 | ~1,400,000 | ~1,385,000 |
| **Pages processed** | 6,900,000+ | 3,500,000 | ~2,770,000 |
| **Fund flow records extracted** | 23,832 | Not provided | 1,489 |
| **Named entities (NLP)** | 11,400,000+ | Not provided | ~4,000 |
| **Persons identified** | 734,000+ | Not provided | ~1,200 |
| **Datasets** | 19 | 12 | 14 |
| **Database size** | 6.9 GB (SQLite) | N/A | ~4 GB |

---

## What This Is

A forensic financial analysis pipeline that processes the full EFTA corpus — all 12 DOJ datasets plus 7 supplementary sources — and extracts, classifies, and cross-references every financial transaction against known Suspicious Activity Report (SAR) filings.

The DOJ released 3.5 million pages of Epstein-related evidence. They did not organize, classify, or cross-reference any of it. This pipeline does.

**This is not a search engine.** Other projects index the documents for keyword search. This project reconstructs the financial ledger — who sent money to whom, through which banks, in what amounts, and whether those transactions appear in known SAR filings.

## Author

**Randall Scott Taylor**
Director of Finance Administration, large municipal government agency
BS Network & Cyber Security, Wilmington University
MS Applied Data Science, Syracuse University

Professional background in multi-affiliate financial reconciliation, budget auditing, and large-scale fiscal operations. Builds automated classification and exception reporting systems for institutional financial data. This project applies the same methodology used in professional public-sector financial auditing to the EFTA corpus.

## Database Schema

The pipeline produces a 6.9 GB relational SQLite database with 28+ tables. Key analytical tables:

### Financial Forensics
| Table | Records | Description |
|-------|---------|-------------|
| `fund_flows` | 24,623 | Directional money movements: entity_from → entity_to with amount, date, confidence |
| `fincen_transactions` | — | FinCEN SAR data cross-referenced against corpus extractions |
| `fincen_bank_connections` | — | Bank relationship mapping from suspicious activity filings |
| `financial_hits` | — | Raw dollar amount extraction markers with source context |
| `financial_redactions` | — | Redacted financial content specifically tracked and cataloged |

### Entity Intelligence
| Table | Records | Description |
|-------|---------|-------------|
| `entities` | 11,400,000+ | NLP-extracted entities (persons, organizations, locations, dates, amounts) |
| `poi_rankings` | — | Persons of interest scored by corpus frequency and financial involvement |
| `evidence_index` | — | Evidentiary chain linking entities to source documents |

### Redaction Analysis
| Table | Records | Description |
|-------|---------|-------------|
| `redaction_markers` | — | Systematic redaction location and type tracking |
| `redaction_recovery` | — | Content recovered from beneath failed redaction overlays |
| `redaction_summary` | — | Per-document redaction density and pattern analysis |

### Cross-Reference Sources
| Table | Description |
|-------|-------------|
| `icij_entities` | Panama Papers / Paradise Papers offshore entity cross-reference |
| `icij_officers` | Offshore company officer registry |
| `icij_relationships` | Offshore entity relationship mapping |
| `faa_master` | FAA aircraft registration (Epstein fleet tracking) |
| `faa_engine` / `faa_acftref` | Aircraft specification cross-reference |
| `media_evidence` | DS10 image/video catalog (941K serials registered) |
| `dates_found` | Temporal mapping across entire corpus |

## Dataset Inventory

| ID | Source | Files | Description |
|----|--------|-------|-------------|
| DS1–DS8 | DOJ EFTA | ~57,000 | FBI interviews, Palm Beach PD reports (2005–2008) |
| DS9 | DOJ EFTA | 531,284 | Email evidence, DOJ internal correspondence, NPA documents |
| DS10 | DOJ EFTA | 503,000+ | 180K images + 2K videos from seized devices |
| DS11 | DOJ EFTA | 331,659 | Financial ledgers, flight manifests, property seizures, 475K emails |
| DS12 | DOJ EFTA | ~150 | Late productions requiring extended legal review |
| DS98 | FBI Vault | 1,037 | FOIA releases predating EFTA |
| DS99 | House Oversight | 56,421 | Estate documents, congressional subpoena production |
| DS100 | DOJ Supplemental | 92 | December 2025 early release batch |
| DS101 | DOJ Supplemental | 92 | Additional December 2025 materials |
| DS102 | DOJ Supplemental | 67 | Pre-January supplemental filings |
| DS103 | House Oversight | 41,231 | Trump financial disclosures — excluded from financial pipeline |
| DS104 | House Oversight | 29,718 | Additional congressional production |

**Total: 1,831,659 files across 19 datasets.**

## Pipeline Architecture (v18)

```
Phase 5A: News-filtered entity extraction (40+ false-positive exclusions, OCR normalization)
     ↓
Phase 5B: Financial transaction classification
          ├── Tier 1: Direct bank evidence (DB-SDNY production documents)
          ├── Tier 2: Corpus-wide extraction (keyword + amount + context scoring)
          └── Tier 3: Entity-matched transactions (NLP entity ↔ financial record linkage)
     ↓
Phase 5C: SAR cross-reference (benchmark against known FinCEN filings)
     ↓
Phase 5D: Deduplication (composite key: amount + entity + date)
     ↓
Phase 5E: Confidence scoring and tier assignment
     ↓
Phase 6:  DOJ release gap analysis (303-name PEP list cross-reference)
```

### Current Pipeline Output

The pipeline's `fund_flows` table contains **23,832 directional fund flow records** — extracted transactions with sender, receiver, amount, and date — totaling $10.73B in extracted volume.

| Confidence | Entries | Amount | Description |
|------------|---------|--------|-------------|
| **High** | 675 | $267,244,458 | Anchored by bank production documents (DB-SDNY, JPM-SDNYLIT series) |
| Low | 23,157 | $10,460,970,150 | Corpus-wide extraction — contains duplication from same transactions appearing across multiple documents |
| **Total** | **23,832** | **$10,728,214,608** | |

**Important:** The $10.7B figure is **extracted volume**, not verified transaction volume. The same wire transfer may appear in a bank statement, an email confirmation, a wire request form, and a legal filing — generating multiple fund flow records. The high-confidence $267M represents the floor of verified, deduplicated financial activity. The network topology (who sent money to whom) is more reliable than the aggregate dollar amounts.

### Bank Routing (from fund_flows)

| Bank | Role | Records | Extracted Volume |
|------|------|---------|-----------------|
| Deutsche Bank | Sender | 2,311 | $1,475,373,584 |
| JPMorgan | Sender | 795 | $933,057,678 |
| JPMorgan | Receiver | 705 | $342,716,349 |
| Citibank | Sender | 165 | $198,209,007 |

### SAR Benchmark Context

| Bank | Known SAR Filing | Pipeline Extracted (as sender) | Ratio |
|------|-----------------|-------------------------------|-------|
| JPMorgan Chase | $1,100,000,000 | $933,057,678 | 0.85x |
| Deutsche Bank | ~$400,000,000 | $1,475,373,584 | 3.69x |
| BNY Mellon | $378,000,000 | In progress | — |

Deutsche Bank's extraction exceeds its known SAR filing by 3.7x. This does not mean the pipeline found $1.5B in unique transactions — it means Deutsche Bank appears as a sender in fund flow records totaling that amount, which likely includes duplication. However, the ratio suggests Deutsche Bank processed substantial Epstein-related activity beyond what it reported as suspicious.

## Findings

| # | Title | Status |
|---|-------|--------|
| [001](findings/FINDING_001_FUND_FLOW_NETWORK.md) | Reconstructing the Epstein Fund Flow Network: 23,832 Directional Records Across 19 Datasets | Published |

## Methodology

All analysis is performed on publicly released U.S. government records under the Epstein Files Transparency Act (Public Law 118-299). No data was obtained through leaks, hacking, or non-public channels.

- **Text extraction**: PyMuPDF (digital PDFs), Tesseract OCR (scanned documents and images)
- **Entity extraction**: spaCy NLP pipeline + custom Epstein-domain entity recognizer
- **Financial extraction**: Multi-pass regex with context scoring, false-positive filtering, sanity caps
- **Deduplication**: Composite keys (amount + entity + date) with quality tiers
- **Cross-referencing**: SAR benchmark data from Senate Finance Committee public filings
- **Victim protection**: No victim names, addresses, or identifying information in any published output

## Publication Policy

**This repository publishes findings, methodology, and source citations. It does not publish the database or pipeline code.**

Why:

- **Victim protection.** The EFTA corpus contains victim names, home addresses, phone numbers, and intimate images — much of which the DOJ itself failed to properly redact. Over 200 survivors have filed legal action over the DOJ's handling of this data. A structured, searchable database that indexes this material would compound that harm. This project will not contribute to it.

- **Professional standard.** Forensic financial analysis publishes findings with sufficient methodology for independent verification — not raw working papers. Every claim in every finding includes EFTA serial numbers that can be checked directly against the source documents on [justice.gov/epstein](https://www.justice.gov/epstein).

- **Active analysis.** The pipeline is under active development (v18, 19 versions over 70+ sessions). Code and schema will be evaluated for release after the analytical work is complete and victim-sensitive content can be properly separated.

Anyone can verify any finding by following the EFTA citations to the original DOJ documents. That is the standard this project holds itself to.

## Replication

All EFTA source documents are available at [justice.gov/epstein](https://www.justice.gov/epstein). Any EFTA citation can be verified:

```
https://www.justice.gov/epstein/files/DataSet {N}/EFTA{XXXXXXXX}.pdf
```

## Project Timeline

- **Started**: February 7, 2026
- **Development**: 200+ paired hours across 70+ sessions
- **Pipeline versions**: v1 through v19
- **Built from scratch**: DOJ document crawler, 19-dataset aggregator, 1.83M file corpus, full financial forensic pipeline

## License

Analysis of public government records. Underlying EFTA documents are U.S. government works. Structured analytical outputs are released into the public domain.
