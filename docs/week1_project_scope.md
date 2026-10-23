# Week 1 Project Scope: Health Info Navigator

**Course:** SAIA 3113 AI Engineering, Universiti Teknologi Malaysia
**Student:** Kaveetiran A/L Sitambaram (A24AI0038), Group 5
**Status:** First draft. I will refine this in the coming topics.

---

## 1. Project Name and Domain

**Project name:** Health Info Navigator (working title)

**Domain:** Public health information for the general public in Malaysia.

**Short description:** A chatbot that answers general health questions in English and Bahasa Malaysia (BM). It only uses official documents from the Ministry of Health Malaysia (KKM) and the World Health Organization (WHO), and every answer shows where the information came from. Technically it is a retrieval augmented generation (RAG) system.

**Pilot scope:** I am starting small so the first version can actually be tested properly. It will cover three areas:

1. Dengue (prevention, symptoms, warning signs and when to get treatment)
2. Vaccination (schedules and general facts)
3. When to see a doctor for common illnesses (general guidance only)

The chatbot will not diagnose anyone, will not give medicine dosages and is not a replacement for a doctor.

---

## 2. Problem Statement

**The problem:** A lot of people in Malaysia get their health information from social media, WhatsApp groups and random websites, where good and bad information are mixed together. KKM and WHO do publish reliable guidance, but it is spread over many websites, PDFs and fact sheets. For an ordinary person it is not easy to find the right answer quickly, in simple words, and in the language they are comfortable with.

**Who faces this problem:** The general public, especially parents and caregivers (for example a parent checking dengue warning signs for a sick child), older adults, and people with limited health literacy who mostly rely on their phone for information.

**Why AI makes sense here:**

1. People ask questions in everyday language, often mixing English and BM. Normal keyword search does not handle this well.
2. A language model combined with retrieval can find the right part of an official document and explain it in simple words.
3. Because the answer is based on official documents and shows the source, the user can check it. A normal chatbot answering from memory cannot do this.

**Why it needs careful engineering:** This is health information, so a wrong answer can actually hurt someone. So the main work in this project is not just calling a model. It is building the whole system around it: the documents, retrieval, guardrails, testing and monitoring. This follows the main idea from Topic 1 that the system around the model matters as much as the model itself.

---

## 3. Evidence of the Problem

| No. | Evidence | Source |
|---|---|---|
| E1 | In the National Health and Morbidity Survey (NHMS) 2019, 35% of Malaysian adults had limited health literacy. It was much higher among people aged 75 and above (68%), people with no formal education (64.8%) and households earning below RM1,000 (49.5%). | Jaafar et al. (2021), *Malaysian Health Literacy: Scorecard Performance from a National Survey*, International Journal of Environmental Research and Public Health, 18(11), 5813. https://doi.org/10.3390/ijerph18115813 |
| E2 | A study of 270 patients at a primary care clinic in Malaysia recorded 1,194 pieces of online health information they came across. 23.3% contained misinformation, only 30.8% were rated good or excellent quality, and only about half (51.5%) were trusted appropriately. Information from social media was trusted less appropriately than information from websites. | Lim et al. (2025), *Appropriate trust in online health information is associated with information platform, commercial status, and misinformation in patients with high cardiovascular risk*, Digital Health, 11. https://doi.org/10.1177/20552076251334438 |
| E3 | WHO describes an "infodemic" as too much information, including false or misleading information, during a disease outbreak, and says it causes confusion and risk taking behaviour that can harm health. | WHO, Infodemic (health topic page). https://www.who.int/health-topics/infodemic |
| E4 | Malaysia recorded 123,133 dengue cases in 2023, an increase of 86.3% compared to 2022, based on the Health Director General's statement for epidemiological week 52/2023. | KKM media statement, ME52/2023 (5 Jan 2024): https://www.moh.gov.my/en/media-kkm/media-statement/2024/kenyataan-media-ketua-pengarah-kesihatan-situasi-semasa-demam-denggi-di-malaysia-minggu-epidemiologi-52-2023-24-30-disember-2023 and news report by The Sun: https://thesun.my/news/malaysia-news/health-dg-dengue-cases-down-68-in-me52-four-deaths-reported-jn11949099/ |
| E5 | The Health Director General said that delay in seeking treatment at health facilities is one of the main factors leading to dengue deaths, and asked the public to get treatment early when they have symptoms. | The Sun (Bernama), 19 Dec 2023, ME49 update. https://thesun.my/local_news/health-dg-dengue-cases-drop-slightly-three-deaths-recorded-in-me49-DA11887712 |
| E6 | WHO states that early detection and access to proper medical care greatly lower the fatality rate of severe dengue. | WHO, Dengue and severe dengue fact sheet (updated 21 Aug 2025). https://www.who.int/news-room/fact-sheets/detail/dengue-and-severe-dengue |

Put together, these show three things. Many Malaysians struggle to understand health information (E1). A good amount of the health information people find online is wrong or poor quality (E2, E3). And for something like dengue, getting the right information and acting early really matters (E4 to E6).

**Note to myself:** For E4 I still want to read the full PDF attached to the KKM statement, and I should check whether data.gov.my has the yearly dengue numbers as a dataset.

---

## 4. Initial Related Work

| No. | Work or existing solution | What it does | Limitation for my project |
|---|---|---|---|
| R1 | **WHO S.A.R.A.H.** (Smart AI Resource Assistant for Health), launched April 2024 | An AI health promotion assistant available 24/7 in several languages, covering topics like healthy eating, mental health and smoking. | It gave wrong or outdated answers. For example it said the Alzheimer's drug lecanemab was still in clinical trials even though the FDA approved it in January 2023. It was reportedly built on GPT 3.5 with data only up to September 2021, and WHO itself warned that answers "may not always be accurate". It is also not based on Malaysian guidance. Source: https://gulfnews.com/technology/media/whos-new-ai-powered-chatbot-is-giving-wrong-medical-answers-1.1713437247946 |
| R2 | **Semigran et al. (2015)**, *Evaluation of symptom checkers for self diagnosis and triage: audit study*, BMJ 351:h3480 | Tested 23 online symptom checkers using 45 patient cases. | The correct diagnosis was listed first in only 34% of cases, and triage advice was appropriate in only 57%. These tools try to diagnose, which is the part I think should not be automated for the public, and they do not point users to official guidance. Source: https://doi.org/10.1136/bmj.h3480 |
| R3 | **Xiong et al. (2024)**, *Benchmarking Retrieval Augmented Generation for Medicine* (MIRAGE and MedRAG), Findings of ACL 2024 | Tested RAG on 7,663 medical questions from five datasets and found retrieval improved accuracy by up to 18% compared to chain of thought prompting alone. | It is tested on exam style medical questions in English, not on health guidance for the public. It does not look at local sources or at safety behaviour like refusing to diagnose. Source: https://aclanthology.org/2024.findings-acl.372 |
| R4 | **Wang et al. (2025)**, *MedCite: Can Language Models Generate Verifiable Text for Medicine?*, Findings of ACL 2025 | Proposes a framework for generating and evaluating citations in medical question answering. | It shows that most medical LLM systems do not generate or check citations. But it is a research method, not a working system for the public, and it does not cover Malaysian sources or BM. Source: https://aclanthology.org/2025.findings-acl.967 |

---

## 5. Engineering Gap

From what I found, existing options fall into three groups:

1. **General global tools** like S.A.R.A.H., which have had accuracy and freshness problems and are not based on local guidance.
2. **Symptom checkers**, which focus on diagnosis. For a public information tool this is exactly the part I want to avoid.
3. **Research benchmarks** like MedRAG and MedCite, which prove that retrieval and citations help, but are not built into a complete system that has been tested end to end.

**The gap my project targets:** a complete AI system (not just a model) that

1. answers only from official KKM and WHO documents,
2. shows a citation the user can check for every answer,
3. works in both English and BM,
4. has clear safety rules (no diagnosis, no dosages, and a "go to a clinic or hospital now" message for warning signs), and
5. is tested on more than accuracy, including faithfulness to the source, citation correctness, safety behaviour and response time.

---

## 6. Project Objectives

| No. | Objective | First target (will be refined) |
|---|---|---|
| O1 | Build a RAG pipeline over official KKM and WHO documents for the three pilot topics, where each answer shows its source. | At least 20 official documents collected. Every answer has at least one citation. |
| O2 | Build a test set and evaluate the system on several quality dimensions. | At least 50 test questions, including 15 safety or out of scope questions. Measure faithfulness, citation correctness, refusal behaviour and response time (target around 5 seconds, to be confirmed later). |
| O3 | Build and test safety guardrails. | The system refuses diagnosis and dosage requests and shows an urgent care message for warning signs in all safety test cases. |

---

## 7. Target Users

**Main users:** Members of the public in Malaysia who want general, reliable health information about dengue, vaccination and common illnesses.

**Groups I especially have in mind:**

1. Parents and caregivers looking up information for a child or an elderly family member, for example checking dengue warning signs.
2. People who are more comfortable asking in BM, or who mix English and BM when they type.
3. People with limited health literacy, who the NHMS 2019 results show are a large part of the population (E1). This is why answers need to be short and in simple language.

**Not meant for:** Doctors or nurses making clinical decisions, emergencies, or anyone looking for a diagnosis or treatment plan. In these cases the system should tell the user to go to a clinic, a hospital or call 999.

---

## 8. Data Sources

All of these are publicly accessible official sources.

| No. | Source | URL | Notes |
|---|---|---|---|
| D1 | WHO, Dengue and severe dengue fact sheet | https://www.who.int/news-room/fact-sheets/detail/dengue-and-severe-dengue | Symptoms, warning signs, treatment and prevention. |
| D2 | Ministry of Health Malaysia (KKM) official portal | https://www.moh.gov.my | Media statements, guidelines and health information. I will pick the specific documents in Week 2. |
| D3 | iDengue portal (KKM with the Malaysian Space Agency) | https://idengue.mysa.gov.my/ide_v3/introduction.html | Official dengue information and hotspot data for the public. |
| D4 | Malaysia open data portal | https://data.gov.my | Government datasets. I still need to check which health datasets are available and their licence terms. |

**How I plan to handle the data:**

1. Check each website's terms of use and robots.txt before downloading anything.
2. Record the source, URL and date accessed for every document so I can trace where each answer came from.
3. Only commit material that is fine to share publicly. For large documents I will commit a download script and a list of sources instead of the files.

---

## 9. Comparison with EduAdvisor

| Aspect | EduAdvisor (lecture example) | Health Info Navigator |
|---|---|---|
| Basic idea | RAG over approved university documents, with citations. | Same idea, but over approved KKM and WHO documents. |
| Stack layers | Application (chat interface, retrieval, guardrails), model (foundation and embedding models), infrastructure (API, vector database, monitoring). | Same three layers. |
| Example failure | Makes up a course prerequisite. | Gives wrong health advice, like a wrong warning sign, a wrong vaccine schedule or telling someone it is safe to wait. |
| Risk level | Lower. A wrong prerequisite is annoying but fixable. | Higher. A wrong answer could delay treatment, so safety rules are a core part of the design. |
| What it answers | Questions about courses and requirements. | Has to actively refuse some questions (diagnosis, dosage) and redirect others (warning signs) to urgent care. |
| Language | Mainly English. | English and BM, including mixed language questions, so both languages need to be tested. |
| How often data changes | Handbooks change about once a year. | Health guidance and outbreak numbers change more often, so I need to track document dates and update them. |
| Evaluation focus | Correct prerequisites and grounded answers. | Faithfulness, correct citations, safety behaviour and similar quality in both languages. |

---

## 10. Responsible AI Risks

| No. | Risk | Possible impact | What I plan to build | How I will check it |
|---|---|---|---|---|
| RAI 1 | **Wrong or made up health information** | Someone follows a wrong answer and delays getting treatment. | Answer only from retrieved official text, refuse when nothing relevant is found, and always include citations. | Faithfulness and citation scores on the test set. |
| RAI 2 | **Unsafe advice** (diagnosing, giving dosages, or missing an emergency) | Someone treats the chatbot like a doctor, or does not get urgent care in time. | Guardrails on input and output that refuse diagnosis and dosage questions, plus detection of warning signs that triggers an urgent care message. | All safety test cases must pass. Guardrail triggers are logged. |
| RAI 3 | **Outdated information** | The system quotes old guidance or old numbers. | Store the date and source of every document, update documents regularly and show a "last updated" date with each answer. | Freshness checks in the test set and a document list with access dates. |
| RAI 4 | **Privacy** | Users type personal health details that end up saved in logs. | Never ask for personal data, avoid logging personal details and show a short privacy notice. | Review the logs and run a test for personal data in logs. |
| RAI 5 | **Unequal quality between languages** | BM or mixed language users get worse answers than English users. | Build a test set in both languages and compare the results. | Separate scores for each language. |
| RAI 6 | **Prompt injection or misuse** | A user, or text inside a document, tries to get around the safety rules. | Treat retrieved text as information only, never as instructions, and include attack style questions in testing. | Pass rate on the adversarial test questions. |

---

## Planned Architecture (rough idea, will change)

1. User asks a question in English or BM.
2. Input check: is it an emergency, a diagnosis or dosage request, or out of scope?
3. Retriever searches the KKM and WHO documents (embeddings and a vector database).
4. The prompt is built from the instructions, the retrieved passages and the rule to always cite.
5. The foundation model writes the answer (through an API).
6. Output check: no diagnosis or dosage, and a citation is present.
7. The user sees the answer with its sources and a short disclaimer.
8. Everything is logged for monitoring and feedback.

| Stack layer | Components |
|---|---|
| Application | Chat interface, retrieval workflow, prompts, guardrails, evaluation |
| Model | Foundation model (not chosen yet) and embedding model |
| Infrastructure | API hosting, vector database, logging and monitoring |

---

## Week 1 files in this repository

1. `docs/week1_observation_sheet.md`: our group observation sheet for Claude.ai (Part A)
2. `docs/week1_system_map.png`: our group conceptual system map (Part B)
3. `docs/week1_project_scope.md`: this document (Part C)
