# Week 3 Data Inventory: Gig Workers Rights Assistant

**Course:** SAIA 3113 AI Engineering, Universiti Teknologi Malaysia
**Student:** Kaveetiran A/L Sitambaram (A24AI0038)
**Version:** 1.0
**Notebook:** [`notebooks/week3_pipeline.ipynb`](../notebooks/week3_pipeline.ipynb) (Cells 2, 3 and Step A3)

This project uses **real, official data**, not the dummy dataset. All sources are public PDF documents from the Ministry of Human Resources (KESUMA) Act 872 portal, so only **Pathway A (PDF / text)** is used.

---

## Step A1: From Topic 2 Requirements to Data Needs

| Requirement ID | Needed information | Candidate source | Why usable / constraint |
|---|---|---|---|
| FR1: answer questions on the four pilot areas from the Act | The actual legal text of Sections 11 to 14, 17 to 19, Part V and Part VIII | S01 Act 872 (English) | Official text published by the government. It is the main legal source, so it covers all four pilot areas. Constraint: publisher notice reserves all rights, so the full text is not republished on GitHub. |
| FR1: pilot area 4 (social security) | The contribution percentage that Section 83(d) leaves open | S02 P.U.(A) 143/2026 | Official regulation, Regulation 2 sets 1.25%. Without it the system cannot answer "how much is deducted for PERKESO?". |
| FR2, NFR2, RAI4: cite the exact section | Section number, section title, Part and page for every piece of text | Same sources (S01, S02), plus the Act's Arrangement of Sections | Section titles are read from the Act's own contents pages and used to check that every section was detected correctly. |
| NFR4 and freshness (ADR3) | Source URL, publication date and a fingerprint of each file | Same sources, PDF metadata and SHA-256 | The PDF metadata holds the legislation number and gazette publication date. The SHA-256 fingerprint shows whether KESUMA has replaced a file. |
| FR7, test set (Week 2 evaluation criteria) | Plain BM explanations and realistic questions | S03 KESUMA FAQ | Official guidance in BM. Inspected this week. It will be prepared in a later iteration, because it is guidance, not law, and has a different structure (questions and answers). |

---

## Step A4: Data Inventory

| Source ID | Filename / URL | Type and purpose | Version / date / owner | Access / rights | Inspection evidence |
|---|---|---|---|---|---|
| S01 | `act872_en.pdf` from https://www.mohr.gov.my/aktapekerjagig2025/assets/documents/Act%20872.pdf | Unstructured text (digital PDF, 59 pages, 439,389 bytes). Main legal source for FR1 and FR2. | Act 872, Gig Workers Act 2025. Royal Assent 16 Dec 2025, gazette publication 31 Dec 2025 (from PDF metadata and page 2). Owner: Government of Malaysia, printed by Percetakan Nasional Malaysia Berhad, hosted by KESUMA. SHA-256 `632727cc...d270ab`. | Publicly downloadable. Page 2 notice: "All rights reserved. No part of this publication may be reproduced ... without the prior permission of Percetakan Nasional Malaysia Berhad." Used for study and processing; full prepared text is **not** committed to GitHub. | 59 pages, 77,702 characters, 0 empty pages, 0 undecoded characters. Page 17 shows Section 14(3) to (8) as clean text. Running header on every page. Pages 1 to 8 are cover, copyright page and Arrangement of Sections. |
| S02 | `pua143_2026.pdf` from https://www.mohr.gov.my/aktapekerjagig2025/assets/documents/PUA143_2026%20-%20PERATURAN%20PEKERJA%20GIG%20(KESELAMATAN%20SOSIAL).pdf | Unstructured text (digital PDF, 3 pages, 269,365 bytes). Detail for pilot area 4. | P.U.(A) 143/2026, Gig Workers (Social Security) Regulations 2026. Published 30 Mar 2026, in force 31 Mar 2026. Owner: Attorney General's Chambers (publisher), made by the Minister of Human Resources. SHA-256 `5109d086...4dae9`. | Publicly downloadable official gazette. Treated the same as S01: prepared text is not republished in full. | 3 pages, 2,372 characters. Page 2 is BM, page 3 is English. Regulation 2 (page 3) states "one point two five percent". Some words have broken spacing in the PDF ("t he", "purpose s"). |
| S03 | `kesuma_faq.pdf` from https://www.mohr.gov.my/aktapekerjagig2025/assets/documents/faq.pdf | Unstructured text (digital PDF, 83 pages, 686,646 bytes). Supporting guidance and test question ideas. | Soalan Lazim Akta Pekerja Gig 2025, prepared by KESUMA. File created 30 Mar 2026 (PDF metadata, no version number printed). SHA-256 `dff1b30b...339f8`. | Publicly downloadable. Marked "Untuk kegunaan umum" (for general use) on page 2. Inspected only this week; no prepared output yet. | 83 pages, 79,563 characters, BM only. Page 2 is a contents page with topics A to P. Page 42 shows questions 53 and 54 on internal grievance and conciliation. About 127 numbered questions. |

The ingestion log with download time and HTTP status for each file is in [`data/ingestion_log.json`](../data/ingestion_log.json).

---

## Inspection Observations (two representative pages per source)

**S01 Act 872**

* **Page 2:** date of Royal Assent (16 December 2025), gazette publication (31 December 2025) and the publisher's copyright notice. This page tells me the version and the rights position.
* **Page 17:** the body of Section 14 (deactivation): subsection (3), the 14 day suspension limit, through to (8). The text is clean and subsection markers such as "(3)" start each line, which makes section aware splitting possible.
* Every page begins with a running header ("Gig Workers 17" on odd pages, "18" plus "Laws of Malaysia Act 872" on even pages) that must be removed.
* The marginal heading of each section (for example "Deactivation under service agreement, etc.") is extracted just before the section number, so it lands at the end of the previous section unless handled.
* Defined terms are written in curly quotes (“contracting entity” means ...).

**S02 P.U.(A) 143/2026**

* **Page 2:** BM version (Peratusan potongan caruman, "satu perpuluhan dua lima peratus").
* **Page 3:** English version (Percentage of contribution deduction, "one point two five percent"). Only page 3 is used so the knowledge source has one language per record for now.
* Signature lines ("Made 28 March 2026", reference number, Minister's name) are not legal rules and are removed.

**S03 KESUMA FAQ**

* **Page 2:** contents page listing topics A (Pengenalan) to P (Lain-lain), including H (deactivation), G (earnings), K and L (disputes and Tribunal) and O (social security), which match the four pilot areas.
* **Page 42:** questions 53 and 54, which explain that a worker must normally use the internal grievance mechanism first, unless the platform does not provide one. This matches Sections 17 and 18 of the Act and is a good source of realistic test questions.

---

## Raw vs Prepared Storage

| Item | Location | In GitHub? |
|---|---|---|
| Raw PDFs (S01 to S03) | `data/raw/` inside the notebook workspace (Colab `/content/week3_project` or local `week3_project/`) | No. Re-downloaded from the official URLs each run. |
| Full prepared text (Part B) | `data/processed/prepared_act872_sections.jsonl`, `data/processed/prepared_pua143_regulations.jsonl` | No (git-ignored). Rebuilt by running the notebook. |
| Full prepared text (Part C) | `data/pipeline_v1/documents/prepared_text.jsonl` | No (git-ignored). Rebuilt by running the notebook. |
| Public evidence of prepared outputs | `data/processed/evidence/*.evidence.jsonl`, `data/pipeline_v1/documents/prepared_text.evidence.jsonl` | Yes. Record ids, citations, pages, sizes, SHA-256 of each record's text and an 80 character preview. |
| Lineage manifests | `data/week3_manifest.json`, `data/pipeline_v1/documents/pipeline_manifest.json` | Yes |

The full prepared text is kept only in the notebook workspace on my own machine or Colab session (and my own private Google Drive if I need it between Colab sessions). It is not shared publicly. Anyone with access to the notebook can rebuild it exactly, and the SHA-256 values in the evidence files and manifests show that the rebuilt files match.

---

## Checkpoint A

**Which Topic 2 requirement needs this data?** FR1 needs the legal text of the four pilot areas (S01, plus S02 for the 1.25% rate). FR2, NFR2 and RAI4 need each piece of text to carry its section number, title and page, which the Act's own structure provides. NFR4 needs the URL, publication date and fingerprint of each file.

**Loaded sample (not just "file loaded"):** Step A3 in the notebook prints the page count, character count, metadata and the text of two pages from each source, including Section 14(3) from page 17 of the Act and Regulation 2 from page 3 of P.U.(A) 143/2026.
