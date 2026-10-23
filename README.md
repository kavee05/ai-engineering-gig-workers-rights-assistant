# Gig Workers Rights Assistant

An assistant that helps gig workers in Malaysia understand their rights under the Gig Workers Act 2025 (Act 872). Workers can ask in Bahasa Malaysia or English, in their own words, and get a simple answer that cites the exact section of the Act or regulation behind it, plus the next step they can take.

> **Legal information, not legal advice.** This is a university project. It does not replace a lawyer or an officer from the Ministry of Human Resources (KESUMA). For a real dispute, use eAduan Gig (https://eaduan-gig.mohr.gov.my/) or visit the nearest KESUMA office.

**Course:** SAIA 3113 AI Engineering, Faculty of Artificial Intelligence, Universiti Teknologi Malaysia
**Student:** Kaveetiran A/L Sitambaram (A24AI0038)
**Status:** Week 1, project scoping

---

## About the project

This is my semester project for AI Engineering. The idea is to build the full system around a language model, not just the model: collecting the official documents, retrieval, prompts, citation checking, safety guardrails, evaluation and monitoring.

To keep the first version manageable, it covers four areas of the Act: account deactivation and suspension, earnings and deductions, how to resolve a dispute, and social security with PERKESO.

## Problem statement

The Gig Workers Act 2025 came into force on 31 March 2026 and gives about 1.64 million gig workers new rights, for example over account suspension, earnings slips and dispute resolution. But the information is spread across the Act (112 sections), four sets of regulations, several official determinations and an 83 page FAQ that is only in BM. Most riders and drivers do not have time to read legal documents, so many may not know what they are entitled to. A normal chatbot is not a safe answer either, because general LLMs often get legal questions wrong.

## Evidence of the problem

1. About 1.64 million people work in the gig economy, almost 10% of total employment. ([KESUMA FAQ](https://www.mohr.gov.my/aktapekerjagig2025/assets/documents/faq.pdf); [ISEAS Perspective 2026/48](https://www.iseas.edu.sg/wp-content/uploads/2026/07/ISEAS-Perspective_2026_48.pdf))
2. Act 872 came into force on 31 March 2026, and KESUMA opened the eAduan Gig complaints system the next day. ([Bernama, 31 Mar 2026](https://bernama.com/en/news.php?id=2539439))
3. The legal material is large and scattered: the Act, regulations P.U.(A) 143 to 146 of 2026, official determinations and an 83 page FAQ in BM. ([KESUMA download page](https://www.mohr.gov.my/aktapekerjagig2025/download.html))
4. Only 26% of gig workers were in PERKESO's Self Employment Social Security Scheme in May 2025. ([ISEAS Perspective 2026/48](https://www.iseas.edu.sg/wp-content/uploads/2026/07/ISEAS-Perspective_2026_48.pdf))
5. Gig work is the main income for 74% of p-hailing riders, and 30.7% earn below the minimum wage. ([ISEAS Perspective 2026/48](https://www.iseas.edu.sg/wp-content/uploads/2026/07/ISEAS-Perspective_2026_48.pdf))
6. The first Gig Workers Tribunal hearing took place on 1 September 2026, between an e-hailing driver and GrabCar. ([Human Resources Online](https://www.humanresourcesonline.net/malaysia-s-gig-workers-tribunal-hears-first-case))

The full evidence table is in [`docs/week1_project_scope.md`](docs/week1_project_scope.md).

## Related work

| Work | Main limitation |
|---|---|
| KESUMA Act 872 portal and FAQ | Accurate but static. Workers must find and read the right document themselves, and the FAQ is only in BM. |
| AIFA, the Sebenarnya.my chatbot (MCMC) | General fact checking on any topic, not built on the text of Act 872 or evaluated on legal questions. |
| MyGOV Malaysia agentic AI (beta, 2026) | Helps complete government transactions, not explain legal rights. |
| Magesh et al. (2025), Journal of Empirical Legal Studies | Commercial legal AI tools using RAG still hallucinated 17% to 33% of the time. |
| Dahl et al. (2024), Journal of Legal Analysis | General LLMs hallucinated at least 58% of the time on legal questions. |

More details and links are in [`docs/week1_project_scope.md`](docs/week1_project_scope.md).

## Engineering gap

From what I could find, there is no tool that lets a Malaysian gig worker ask about their rights under Act 872 in their own words and get an answer tied to the actual section. The official documents are accurate but hard to use, general government chatbots are not built on this law, and research shows legal AI still makes things up unless it is carefully grounded and tested. This project targets a system that answers only from official KESUMA documents, cites and checks the exact section, works in BM and English, refuses personal legal advice, tracks document versions, and is evaluated on citation correctness, faithfulness, safety, response time and language parity.

## Objectives

1. **O1:** Build a RAG pipeline over Act 872, its regulations and official KESUMA guidance for the four pilot areas, where every answer cites its section.
2. **O2:** Build and test guardrails that refuse personal legal advice and case predictions, admit when the sources are not enough, and point workers to eAduan Gig, conciliation or the Tribunal.
3. **O3:** Evaluate the system on a test set of at least 85 BM and English questions for answer correctness, citation correctness, refusal behaviour, response time and the gap between languages.

The objectives were refined in Week 2. Details are in [`docs/week2_requirements.md`](docs/week2_requirements.md).

## Target users

Platform gig workers in Malaysia, mainly food and parcel delivery riders and e-hailing drivers, who often rely on gig work as their main income and use their phone while working. It is also for non-platform gig workers such as freelancers, and for gig worker associations that help their members. It is not meant for lawyers, for platform companies seeking compliance advice, or for workers who need representation in an active case.

## Data sources

All from KESUMA's official Act 872 portal: https://www.mohr.gov.my/aktapekerjagig2025/download.html

1. Gig Workers Act 2025 (Act 872), in English and BM
2. Gig Workers Regulations 2026, P.U.(A) 143 to 146
3. KESUMA FAQ, *Soalan Lazim Akta Pekerja Gig 2025*
4. Director General determinations on earnings slips and deductions
5. PERKESO information on social security for gig workers: https://www.perkeso.gov.my

I will record the source, URL, version and access date for each document.

## Repository structure

```
ai-engineering-gig-workers-rights-assistant/
├── README.md
├── docs/
│   ├── week1_observation_sheet.md   group observation sheet (Part A)
│   ├── week1_system_map.png         group system map (Part B)
│   ├── week1_project_scope.md       my project scope (Part C)
│   ├── week2_requirements.md        framing, scope, FR, NFR and RAI requirements
│   ├── week2_evaluation_criteria.md evaluation criteria table
│   ├── week2_architecture_v1.png    V1 conceptual architecture
│   └── week2_architecture_decisions.md  ADRs and traceability matrix
├── data/          source lists and download scripts
├── src/           application code
├── notebooks/     experiments
├── evaluation/    test sets and results
└── prompts/       prompt templates
```

## Weekly progress

| Week | Focus | Progress | Evidence |
|---|---|---|---|
| 1 | AI Engineering landscape and project scoping | Done. Wrote the project scope, set up this repository, and added the group observation sheet and system map. | [`docs/`](docs/) |
| 2 | Planning: requirements, evaluation criteria and V1 architecture | Done. Refined the project framing and scope, wrote 7 functional, 5 non-functional and 5 Responsible AI requirements, defined evaluation criteria with thresholds, and designed the V1 architecture with 4 architecture decisions and a traceability matrix. | [`week2_requirements.md`](docs/week2_requirements.md), [`week2_evaluation_criteria.md`](docs/week2_evaluation_criteria.md), [`week2_architecture_v1.png`](docs/week2_architecture_v1.png), [`week2_architecture_decisions.md`](docs/week2_architecture_decisions.md) |
| 3 | To be added | Planned | |
| 4 | To be added | Planned | |
| 5 | To be added | Planned | |
| 6 | To be added | Planned | |
| 7 | To be added | Planned | |
| 8 | To be added | Planned | |

I will update this table every week as the project goes on.

## Security and privacy

No API keys, passwords or tokens are stored in this repository. Secrets are kept in a local `.env` file, which is listed in `.gitignore`.
