# Health Info Navigator

A chatbot that answers general health questions in English and Bahasa Malaysia, using only official documents from the Ministry of Health Malaysia (KKM) and the World Health Organization (WHO). Every answer comes with a source so the user can check it.

> **Not medical advice.** This is a university project. It does not diagnose, give medicine dosages or replace a doctor. In an emergency, call 999 or go to the nearest hospital.

**Course:** SAIA 3113 AI Engineering, Faculty of Artificial Intelligence, Universiti Teknologi Malaysia
**Student:** Kaveetiran A/L Sitambaram (A24AI0038)
**Status:** Week 1, project scoping

---

## About the project

This is my semester project for AI Engineering. The idea is to build the full system around a language model, not just the model: collecting the documents, retrieval, prompts, safety guardrails, evaluation and monitoring.

To keep the first version manageable, I am starting with three topics: dengue, vaccination, and when to see a doctor for common illnesses.

## Problem statement

Many people in Malaysia get health information from social media, WhatsApp and random websites, where reliable and unreliable content is mixed together. KKM and WHO publish good guidance, but it is spread across many websites and PDFs, and it is not always easy to understand or available in the language people prefer. An AI assistant based on these official documents could help, but only if it is reliable and safe, because a wrong answer about health can hurt someone.

## Evidence of the problem

1. In NHMS 2019, 35% of Malaysian adults had limited health literacy, and it was much higher for older adults and lower income households. ([Jaafar et al., 2021, IJERPH](https://doi.org/10.3390/ijerph18115813))
2. A Malaysian study of 1,194 online health information entries found that 23.3% contained misinformation and only about half were trusted appropriately. ([Lim et al., 2025, Digital Health](https://doi.org/10.1177/20552076251334438))
3. WHO warns that false and misleading information during outbreaks causes confusion and risky behaviour that can harm health. ([WHO, Infodemic](https://www.who.int/health-topics/infodemic))
4. Malaysia had 123,133 dengue cases in 2023, up 86.3% from 2022. ([KKM statement ME52/2023](https://www.moh.gov.my/en/media-kkm/media-statement/2024/kenyataan-media-ketua-pengarah-kesihatan-situasi-semasa-demam-denggi-di-malaysia-minggu-epidemiologi-52-2023-24-30-disember-2023))
5. The Health Director General said delay in seeking treatment is one of the main causes of dengue deaths. ([The Sun, Dec 2023](https://thesun.my/local_news/health-dg-dengue-cases-drop-slightly-three-deaths-recorded-in-me49-DA11887712))

The full evidence table is in [`docs/week1_project_scope.md`](docs/week1_project_scope.md).

## Related work

| Work | Main limitation |
|---|---|
| WHO S.A.R.A.H. (2024) | Gave wrong and outdated answers, and is not based on Malaysian guidance. |
| Semigran et al. (2015), symptom checker audit, BMJ | Correct diagnosis listed first in only 34% of cases, and appropriate triage in only 57%. |
| Xiong et al. (2024), MedRAG and MIRAGE, Findings of ACL | Shows RAG helps, but only on English exam style questions, not public health guidance. |
| Wang et al. (2025), MedCite, Findings of ACL | A research method for medical citations, not a complete system for the public. |

More details and links are in [`docs/week1_project_scope.md`](docs/week1_project_scope.md).

## Engineering gap

I could not find an existing tool that does all of these together: answers based only on official Malaysian and WHO sources, citations the user can check, support for English and BM, clear safety rules (no diagnosis or dosages, and urgent care messages for warning signs), and testing on several quality dimensions such as faithfulness, citation correctness, safety and response time.

## Objectives

1. **O1:** Build a RAG pipeline over official KKM and WHO documents for the pilot topics, where every answer shows its source.
2. **O2:** Create a test set of at least 50 questions (including safety cases) and evaluate faithfulness, citation correctness, refusal behaviour and response time.
3. **O3:** Build and test safety guardrails that refuse diagnosis and dosage requests and send warning sign cases to urgent care.

## Target users

Members of the public in Malaysia looking for general health information, especially parents and caregivers, people who prefer BM, and people with limited health literacy. It is not meant for doctors making clinical decisions or for emergencies.

## Data sources

1. WHO, Dengue and severe dengue fact sheet: https://www.who.int/news-room/fact-sheets/detail/dengue-and-severe-dengue
2. Ministry of Health Malaysia (KKM): https://www.moh.gov.my
3. iDengue portal (KKM and the Malaysian Space Agency): https://idengue.mysa.gov.my/ide_v3/introduction.html
4. Malaysia open data portal: https://data.gov.my

I will only use publicly accessible documents, and I will record the source, URL and access date for each one.

## Repository structure

```
ai-engineering-health-info-navigator/
├── README.md
├── docs/
│   ├── week1_observation_sheet.md   group observation sheet (Part A)
│   ├── week1_system_map.png         group system map (Part B)
│   └── week1_project_scope.md       my project scope (Part C)
├── data/          source lists and small public samples
├── src/           application code
├── notebooks/     experiments
├── evaluation/    test sets and results
└── prompts/       prompt templates
```

## Weekly progress

| Week | Focus | Progress | Evidence |
|---|---|---|---|
| 1 | AI Engineering landscape and project scoping | Done. Wrote the project scope, set up this repository, and added the group observation sheet and system map. | [`docs/`](docs/) |
| 2 | To be added | Planned | |
| 3 | To be added | Planned | |
| 4 | To be added | Planned | |
| 5 | To be added | Planned | |
| 6 | To be added | Planned | |
| 7 | To be added | Planned | |
| 8 | To be added | Planned | |

I will update this table every week as the project goes on.

## Security and privacy

No API keys, passwords or tokens are stored in this repository. Secrets are kept in a local `.env` file, which is listed in `.gitignore`.
