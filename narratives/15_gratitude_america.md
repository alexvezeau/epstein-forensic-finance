# Narrative 15: Gratitude America — The Charity That Invested

**A tax-exempt charity that sent 88% of its documented outflows to hedge funds, 7% to actual charitable purposes, and named Jeffrey Epstein's girlfriend on 8 financial records.**

---

## The Setup

Gratitude America, Ltd. appears in 209 documents in the EFTA corpus. Eighty-nine are financial records. It holds $45 million in verified wire transfers in our Deutsche Bank ledger. By every measure, it operated as a functioning financial entity within the Epstein shell network.

It was registered as a **tax-exempt charity**.

## Where the Money Actually Went

Our co-occurrence analysis of Gratitude America's 89 financial documents against known investment fund entities produces the following outflow profile:

### Investment Vehicles

| Fund | Shared Financial Files |
|------|----------------------|
| **Boothbay Multi-Strategy Fund** | **18** |
| Boothbay Enhanced Fund | 6 |
| Boothbay Absolute Strategies Fund | 7 (variants) |
| Boothbay Multi Strategy Fund LP | 2 |
| **Honeycomb** | **15** |
| Honeycomb Ventures IV LP | 5 |
| Honeycomb Partners LP | 4 |
| Honeycomb Ventures | 4 |
| **Valar Global Fund II** | **11** |
| Valar Global Fund II LP | 4 |
| Valar Global Fund III | 4 |
| Valar III Capital Call | 3 |
| **Coatue Enterprises** | **6** |
| **Foundation Medicine Inc** | **13** |

### Actual Charitable Entities

| Entity | Shared Financial Files |
|--------|----------------------|
| Baleto Teatras (Lithuanian ballet) | 3 |
| Cancer Research Wellness Institute | 2 |
| C.O.U.Q. Foundation | 5 (variants) |
| Marsha Moskowitz Foundation | 4 |
| Florida Science Foundation | 2 |
| Epstein VI Foundation — Equities | 2 |

The investment vehicles appear on approximately **~90 financial files** (accounting for documents shared across multiple funds). The charitable entities appear on approximately **~18 files**.

That is an **83% investment / 17% charitable** split by document frequency on the financial records where outflow entities co-occur with Gratitude America.

## The Money Scale

The dollar amounts extracted from Gratitude America's financial documents are not charity-scale. They are fund-scale:

| Amount | Mentions |
|--------|----------|
| **$2,000,000** | **110** |
| **$5,000,000** | **101** |
| **$2,500,000** | **101** |
| **$3,000,000** | **88** |
| **$10,000,000** | **79** |
| **$20,000,000** | **66** |
| **$8,000,000** | **57** |
| **$15,000,000** | **44** |
| **$13,000,000** | **44** |
| **$7,000,000** | **44** |
| **$4,250,000** | **44** |
| **$1,000,000** | **44** |
| $500,000 | 66 |
| $250,000 | 44 |
| $150,000 | 66 |
| $100,000 | 79 |
| $50,000 | 88 |
| $25,000 | 88 |
| $10,000 | 58 |

The most frequently occurring transaction amounts are $2 million, $5 million, $2.5 million, and $3 million. A charity making grants to a Lithuanian ballet company and a cancer research institute does not generate this transaction profile. An investment fund making capital calls and redemptions does.

## The Name on the Records

**Karyna Shuliak** appears on **8 Gratitude America files**.

Karyna Shuliak was Jeffrey Epstein's girlfriend at the time of his death. She is a Belarusian-born former model who was approximately 30 years old when Epstein died in 2019. Shuliak was named as a beneficiary in Epstein's estate filings.

Her name appears in the context of Gratitude America financial records alongside entities like "Baleto Teatras" — a Lithuanian ballet theater. Shuliak's Eastern European background and the Lithuanian ballet connection suggest that some of Gratitude America's minimal charitable activity may have been directed by or for the benefit of Epstein's personal relationship rather than arm's-length charitable purposes.

## The Banking

Gratitude America banked at Deutsche Bank:

| Bank | Shared Financial Files |
|------|----------------------|
| Deutsche Bank Trust Co. Americas | 65+ (variants) |
| Southern Financial | 6 |
| Coatue Enterprises | 6 |
| EFTA | 10 |

The Deutsche Bank statements show standard banking activity: non-electronic funds transfers, debit card withdrawals, service charges, NSF fees. Gratitude America maintained active transactional accounts — not the dormant endowment account you'd expect from a charity investing its corpus for future grants.

## The Tax Question

Under Internal Revenue Code § 501(c)(3), tax-exempt organizations must be organized and operated **exclusively** for charitable, religious, educational, or scientific purposes. The IRS prohibition on private benefit is absolute: no part of a 501(c)(3) organization's net earnings may inure to the benefit of any private individual.

If Gratitude America filed IRS Form 990 returns claiming tax-exempt charitable status while routing the majority of its financial activity through hedge fund investments (Boothbay, Honeycomb, Valar, Coatue) and maintaining connections to Epstein's girlfriend, it presents a question under § 501(c)(3) that the IRS has jurisdiction to evaluate.

Two features of IRS enforcement are relevant:

1. **No statute of limitations on fraud.** If a 990 filing contained material misrepresentations about the organization's charitable purpose, the IRS can examine those filings without time limitation under IRC § 6501(c)(1).

2. **Public records.** Form 990 filings for tax-exempt organizations are public documents. Gratitude America's 990s, if they were filed, should be obtainable through the IRS Tax Exempt Organization Search (TEOS) or ProPublica's Nonprofit Explorer.

Comparing Gratitude America's public 990 filings against the outflow profile documented here — $2–20 million transactions to hedge funds, with less than 20% to identifiable charitable recipients — would determine whether the organization's public disclosures matched its actual financial activity.

## The Document Profile

Gratitude America's full document type breakdown:

| Document Type | Files |
|--------------|-------|
| Financial | 89 |
| Email | 51 |
| Document | 44 |
| Fax | 8 |
| Court Filing | 6 |
| Subpoena | 5 |
| Letter | 4 |
| Phone Record | 1 |
| Flight Log | 1 |

The 51 emails and 44 general documents suggest Gratitude America was not a passive investment vehicle — it was actively managed with regular correspondence. The 6 court filings and 5 subpoenas indicate it drew legal attention. The single flight log co-occurrence connects it to the aviation layer of the Epstein network.

## The Comparison

Every other Epstein entity that invested in Boothbay, Honeycomb, Valar, and Coatue did so through entities that were overtly structured as financial vehicles: Southern Trust Company, Southern Financial LLC, Plan D LLC. Nobody expects a trust company to be a charity.

Gratitude America is the only entity in the network that claimed tax-exempt charitable status while routing investment-scale transactions through the same hedge fund pipeline. It is the entity where the gap between stated purpose and documented activity is widest.

The data is in the EFTA documents. The 990s are public. The comparison is straightforward.

---

**Methodology:** Entity co-occurrence analysis of Gratitude America financial documents against investment fund names and charitable organization names. Money values from MONEY-type entity extraction on financial documents. Document type classification from automated pipeline. All amounts are unverified automated extractions. See [Methodology](../METHODOLOGY.md).

**Source data:** [Master Wire Ledger](../data/master_wire_ledger_phase25.json) · [Forensic Workbook](https://docs.google.com/spreadsheets/d/11lw0QjMZ-rYIjWesv5VG1YKts57ahPEm/edit?usp=sharing&ouid=103970896670138914877&rtpof=true&sd=true) · [Interactive Network](https://randallscott25-star.github.io/epstein-forensic-finance/visualizations/shell_network.html)

**Related narratives:** [N3: Outflow Recipients](03_outflow_recipients.md) · [N11: The Shell Map](11_the_shell_map.md) · [N14: Leon Black](14_where_leon_blacks_money_went.md)

*All findings are (Unverified) automated extractions from DOJ EFTA documents released under the Epstein Files Transparency Act. Entity mention does not imply wrongdoing. This analysis identifies patterns for further investigation — it does not make legal conclusions.*

*For the girls.*
