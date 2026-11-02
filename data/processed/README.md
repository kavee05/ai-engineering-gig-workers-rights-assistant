# Prepared Data (Week 3)

The prepared outputs are built by [`notebooks/week3_pipeline.ipynb`](../../notebooks/week3_pipeline.ipynb).

| File | What it is | In GitHub? |
|---|---|---|
| `prepared_act872_sections.jsonl` | 134 section level records from Act 872 (Part B output) | No, rebuilt by the notebook |
| `prepared_pua143_regulations.jsonl` | 4 records from P.U.(A) 143/2026, English page (Part B output) | No, rebuilt by the notebook |
| `evidence/prepared_act872_sections.evidence.jsonl` | Public evidence for the file above | Yes |
| `evidence/prepared_pua143_regulations.evidence.jsonl` | Public evidence for the file above | Yes |

**Why the full files are not here:** they reproduce the Act and the regulations word for word, and the Act carries a publisher notice that reserves all rights. Following the lab instruction for data that should not be redistributed, only non-sensitive evidence is committed.

**What the evidence files contain:** for every record, the record id, citation (for example "Act 872, Section 14"), section title, Part, pages, character count, source URL, source SHA-256, version, processing method, the SHA-256 of the record's full text and an 80 character preview.

**How to rebuild and verify:** run the notebook from top to bottom (Colab or local). It downloads the official PDFs, rebuilds the full files and writes new evidence files. The `text_sha256` values and the `prepared_sha256` values in [`data/week3_manifest.json`](../week3_manifest.json) should match.

**Record format (full files):**

```json
{
  "record_id": "S01-14-01",
  "source_id": "S01",
  "cite": "Act 872, Section 14",
  "section": "14",
  "title": "Deactivation under service agreement, etc.",
  "part": "Part III GIG WORKER",
  "piece": 1,
  "pieces": 3,
  "pages": [16, 17, 18],
  "text": "Act 872 Gig Workers Act 2025 | Part III GIG WORKER | Section 14: ... (part 1 of 3)\n14. (1) A platform provider shall ...",
  "char_count": 1019,
  "source": "act872_en.pdf",
  "source_url": "https://www.mohr.gov.my/aktapekerjagig2025/assets/documents/Act%20872.pdf",
  "source_sha256": "632727cc...",
  "source_version": "2025-12-31",
  "language": "en",
  "processing": "section-aware chunks (max 1200 chars; ...)"
}
```
