# Project Atlas — Diligence Data and Problem Statements

This repository contains the Project Atlas v0.1 synthetic dataset under [data/project-atlas/](data/project-atlas/) and possible problem statements for an evidence-backed diligence agent. Due diligence means checking a company's claims, financial performance, contracts, technology and risks before an investment or acquisition. A virtual data room (VDR) contains the documents and records used for that investigation.

## What is Project Atlas?

Project Atlas is a **fictional AI data and infrastructure company acquisition**, designed as a public teaching and development case. It is not a real company's confidential deal room. Its illustrative enterprise value is **$1.8 billion**, a scenario assumption rather than a valuation conclusion.

The local pack contains **89 files**, including **66 VDR documents**, **14 canonical data files**, **3 worked-answer files** and **6 root metadata/documentation files**. It describes six entities, 500 customers/contracts, 1,200 employees and 4,096 GPUs. There are 36 monthly financial snapshots spanning September 2023 through August 2026.

The documents represent management claims, agreements, financial snapshots and evidence updates. The structured tables provide the records against which claims can be checked. Management assertions can be wrong; the pack identifies its structured tables as canonical.

```text
data/project-atlas/
├── README.md                 Dataset orientation and limitations
├── LICENSE.md                Dataset reuse permission
├── data_dictionary.json      Units, joins and modeling limits
├── manifest.json             Document metadata and line locators
├── SHA256SUMS                Published file hashes
├── data/                     10 CSV files and 4 JSON files
├── vdr/                      66 Markdown documents in 14 folders
└── worked_answers/           Public findings, updates and redaction labels
```

### Structured records

The following row counts were inspected locally; CSV counts exclude headers.

| File under `data/project-atlas/data/` | Rows | Purpose |
| --- | ---: | --- |
| `entities.csv` | 6 | Corporate entities and assumed jurisdictions. |
| `customers.csv` | 500 | Customer identity, product, recurring fees and contract links. |
| `contracts.csv` | 500 | Fees, dates, obligations and transfer/consent fields. |
| `invoices.csv` | 18,036 | Invoiced, recognized and collected amounts, including invoice kind. |
| `cash_receipts.csv` | 17,535 | Receipts linked to invoices. |
| `ledger.csv` | 107,358 | Signed journal entries for accounting reconciliation. |
| `monthly_finance.csv` | 36 | Monthly financial totals and balances. |
| `cost_allocations.csv` | 18,000 | Customer/month GPU, power, support and retry costs. |
| `assets.csv` | 4,096 | Asset ownership, location, vendor and lease references. |
| `employees.csv` | 1,200 | Synthetic employee roles and monthly salaries. |

The four JSON files contain opening balances, closing balances, a dependency graph and post-close scenario events. Post-close projections must be kept separate from historical booked results.

**Data conventions:** monetary amounts use integer USD cents; divide by 100 for dollar presentation. Ledger signs are positive for debits and negative for credits. Join using identifiers such as `customer_id`, `contract_id`, `invoice_id`, `entity_id` and `journal_id`. Dates use UTC, monthly periods use `YYYY-MM`, and finance effective dates on day 28 are cutoff labels rather than transaction dates. See the [data dictionary](data/project-atlas/data_dictionary.json).

### VDR evidence and stages

The 14 VDR folders cover index/policy, corporate, finance, commercial, AI/data/IP, infrastructure, security, privacy, legal, people, tax, environment, deal thesis and post-close integration. Documents record IDs, versions, entities, stages, effective dates and observation times.

| Stage | Date | Example and intended behavior |
| --- | --- | --- |
| T0 | August 31, 2026 | Initial evidence snapshot; identify issues using information available at this point. |
| T1 | September 6, 2026 | Security remediation/retest evidence; retire the resolved open vulnerability while retaining the separate scope gap. |
| T2 | September 10, 2026 | Customer change-of-control consent supplement; resolve that consent request while retaining the separate data-license consent issue. |

Gate retrieval by evidence availability, not merely filename or effective date. The manifest includes document text in its line locators: exposing an unfiltered manifest can leak later-stage evidence even if the later document files are excluded.

## Possible problem statements

These are candidate project directions, not claims of implemented capabilities. The examples below reveal teaching-case facts and should count as answer exposure when documenting evaluation.

| Candidate | Problem to solve | Evidence and expected output |
| --- | --- | --- |
| Revenue quality and ARR verifier | Does management's annual recurring revenue claim match recurring contracts? | Reconcile contracts, invoices and ledger with `ARR-v1.md`. The document states $202m ARR includes $22m nonrecurring services; $15m contracted monthly recurring revenue annualizes to $180m. Distinguish ARR from recognized revenue and accept the correct `CLEAN-v1.md` bridge. |
| Customer contribution-margin analyst | Which customers generate revenue but poor margins after AI infrastructure costs? | Join invoices and customer/month cost allocations. Produce reproducible margin calculations and evidence requests. Avoid adding the $1.2m monthly lease commitment again: the capacity document says it is already included in GPU allocations. |
| Contract and data-rights investigator | Which customer or dataset rights could affect the acquisition or model use? | Check contracts, consent versions, license/IP documents and model dependencies. Distinguish missing assignment evidence from proof of infringement; update customer consent status at T2 without resolving unrelated data rights. |
| Security evidence lifecycle agent | Can an agent maintain accurate findings as remediation evidence arrives? | Combine security scope, vulnerability versions and dependency records. Revise at T1, retain unresolved scope questions and avoid equating a scanner finding with proven exploitation. |
| Infrastructure ownership verifier | Does management's GPU ownership claim match the asset register? | Compare `OWNERSHIP-v1.md` with assets: 4,096 GPUs comprise 3,072 owned and 1,024 leased. Cite the discrepancy without treating an inventory count as proof of legal title. |
| Acquisition evidence memo | How do commercial consent, customer economics and technical/data-rights issues affect the acquisition thesis? | Connect commercial, financial and technical evidence, quantify supported implications, rank evidence requests and regenerate the memo after staged updates. |
| Version-aware diligence evaluator | Can a grader distinguish correct findings, false alarms and stale conclusions? | Freeze material/control/update cases; score evidence accuracy, calculations and revision behavior against documented baselines. Keep public worked answers outside agent inputs. |

**Suggested starting scope:** Revenue-quality verification. It has structured inputs, a clear material discrepancy and an explicit clean control. Add a staged customer-consent case to test whether the agent revises its assessment of revenue exposure when evidence changes; consent does not itself change booked revenue or ARR.

## Limitations, answer exposure and licensing

Project Atlas is a public teaching preview with expert realism review pending. Its worked answers are public labels, **not hidden test answers**. Declare exposure to the documents, worked labels and examples in this README; removing labels from retrieval does not turn familiar cases into unseen evaluation. Use separately authored/versioned cases for stronger generalization claims and document their provenance.

The model uses group-only accounts and simplified cash timing, service recognition and staffing. Tax, FX, interest, working-capital aging, intercompany transactions and GAAP lease accounting are not modeled. Some topics have placeholder scope documents rather than substantive modeled evidence. OCR scans, live collectors, real security assessments, production agents and an implemented permission service are absent. Do not claim these capabilities from results on this pack.

Attribute **Apex Growth Systems LLC / Project Atlas v0.1**, link to the [source repository](https://github.com/AAH20/project-atlas-due-diligence), preserve synthetic-data/limitation notices and identify modifications. The local [dataset license](data/project-atlas/LICENSE.md) permits attributed research, education and evaluation reuse under its terms. Commercial integration or resale requires a separate agreement. This permission does not license project code or private application software. The upstream `DATA_LICENSE.md` is referenced by the dataset but is not included at that path in this local pack.

Outputs are decision support requiring qualified human review, not investment recommendations, legal opinions or compliance certificates. Only publish data and artifacts that you have rights to disclose.

## Dataset sources

Dataset descriptions and counts above were checked against the local files on September 20, 2026.

- [Standalone Project Atlas dataset](https://www.kaggle.com/datasets/ahmedalaahassan/project-atlas-synthetic-m-and-a-due-diligence-vdr)
- [Upstream repository and generation/validation/reference-run resources](https://github.com/AAH20/project-atlas-due-diligence) — these tools are not included in this local dataset-only download.
- [Local dataset README](data/project-atlas/README.md), [VDR scope](data/project-atlas/vdr/00_index/INDEX-v1.md), [data dictionary](data/project-atlas/data_dictionary.json) and [license](data/project-atlas/LICENSE.md).
