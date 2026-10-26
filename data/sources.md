# Data Sources

All documents are official, publicly available files from the Ministry of Human Resources (KESUMA) Act 872 portal: https://www.mohr.gov.my/aktapekerjagig2025/download.html

| No. | Document | Language | URL | Accessed |
|---|---|---|---|---|
| D1 | Gig Workers Act 2025 (Act 872) | English | https://www.mohr.gov.my/aktapekerjagig2025/assets/documents/Act%20872.pdf | 24 Oct 2026 |
| D1b | Akta Pekerja Gig 2025 (Akta 872) | BM | https://www.mohr.gov.my/aktapekerjagig2025/assets/documents/Akta%20872.pdf | 24 Oct 2026 |
| D2 | Gig Workers (Social Security) Regulations 2026, P.U.(A) 143/2026 | BM and English | https://www.mohr.gov.my/aktapekerjagig2025/assets/documents/PUA143_2026%20-%20PERATURAN%20PEKERJA%20GIG%20(KESELAMATAN%20SOSIAL).pdf | 24 Oct 2026 |
| D3 | Soalan Lazim Akta Pekerja Gig 2025 (FAQ) | BM | https://www.mohr.gov.my/aktapekerjagig2025/assets/documents/faq.pdf | 24 Oct 2026 |
| D4 | Gig Workers (Conciliation Proceedings) Regulations 2026, P.U.(A) 146/2026 | BM and English | https://www.mohr.gov.my/aktapekerjagig2025/assets/documents/PUA146_2026%20-%20PERATURAN%20PEKERJA%20GIG%20(PROSIDING%20PENDAMAIAN).pdf | 26 Oct 2026 |
| D5 | Gig Workers (Gig Workers Tribunal) Regulations 2026, P.U.(A) 144/2026 | BM and English | https://www.mohr.gov.my/aktapekerjagig2025/assets/documents/PUA144_2026%20-%20PERATURAN%20PEKERJA%20GIG%20(TRIBUNAL%20PEKERJA%20GIG).pdf | 26 Oct 2026 |
| D6 | Director General determination on earnings slips (Slip Pendapatan) | BM | https://www.mohr.gov.my/aktapekerjagig2025/assets/documents/Slip%20Pendapatan%20-%20Penentuan%20Ketua%20Pengarah%20Tenaga%20Kerja%20Akta%20Pekerja%20gig.pdf | 26 Oct 2026 |
| D7 | Director General determination on earnings deductions (Potongan Pendapatan) | BM | https://www.mohr.gov.my/aktapekerjagig2025/assets/documents/Potongan%20Pendapatan%20-%20Penentuan%20Ketua%20Pengarah%20Tenaga%20Kerja%20Akta%20Pekerja%20gig.pdf | 26 Oct 2026 |

## Which document covers which pilot area

| Pilot area | Main source (law) | Details |
|---|---|---|
| Account deactivation and suspension | Act 872, Section 14 | FAQ section H |
| Earnings, deductions and earnings slips | Act 872, Sections 11 to 13 | D6, D7, FAQ section G |
| Dispute resolution | Act 872, Sections 17 to 19 and Part V | D4, D5, FAQ sections K and L |
| Social security | Act 872, Part VIII | D2 (1.25% deduction), FAQ section O |

The Act is always the main source. The regulations and Director General determinations fill in details the Act leaves open, and the FAQ is supporting guidance only.

## Notes for parsing (Week 3 preparation)

1. The Act uses numbered sections, subsections like (1) and (2), and paragraphs like (a) and (b). Splitting by section number should keep each rule together.
2. Page headers repeat on every page ("Laws of Malaysia", "Act 872" and the page number), so they need to be removed before splitting.
3. Cross references are common, for example Section 18(3)(b) refers back to Section 14(9). The section number should be kept with each chunk so these can be followed.
4. The regulations PDF has BM and English text in the same document.
5. The FAQ is a question and answer list grouped by topic (sections A to P), which is also useful for building test questions.
