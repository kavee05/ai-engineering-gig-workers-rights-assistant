# Data Sources

All documents are official, publicly available files from the Ministry of Human Resources (KESUMA) Act 872 portal: https://www.mohr.gov.my/aktapekerjagig2025/download.html

| No. | Document | Language | URL | Accessed |
|---|---|---|---|---|
| D1 | Gig Workers Act 2025 (Act 872) | English | https://www.mohr.gov.my/aktapekerjagig2025/assets/documents/Act%20872.pdf | 24 Oct 2026 |
| D1b | Akta Pekerja Gig 2025 (Akta 872) | BM | https://www.mohr.gov.my/aktapekerjagig2025/assets/documents/Akta%20872.pdf | 24 Oct 2026 |
| D2 | Gig Workers (Social Security) Regulations 2026, P.U.(A) 143/2026 | BM and English | https://www.mohr.gov.my/aktapekerjagig2025/assets/documents/PUA143_2026%20-%20PERATURAN%20PEKERJA%20GIG%20(KESELAMATAN%20SOSIAL).pdf | 24 Oct 2026 |
| D3 | Soalan Lazim Akta Pekerja Gig 2025 (FAQ) | BM | https://www.mohr.gov.my/aktapekerjagig2025/assets/documents/faq.pdf | 24 Oct 2026 |

The other regulations (P.U.(A) 144 to 146 of 2026) and the Director General determinations are on the same download page and will be added as the pilot areas need them.

## Notes for parsing (Week 3 preparation)

1. The Act uses numbered sections, subsections like (1) and (2), and paragraphs like (a) and (b). Splitting by section number should keep each rule together.
2. Page headers repeat on every page ("Laws of Malaysia", "Act 872" and the page number), so they need to be removed before splitting.
3. Cross references are common, for example Section 18(3)(b) refers back to Section 14(9). The section number should be kept with each chunk so these can be followed.
4. The regulations PDF has BM and English text in the same document.
5. The FAQ is a question and answer list grouped by topic (sections A to P), which is also useful for building test questions.
