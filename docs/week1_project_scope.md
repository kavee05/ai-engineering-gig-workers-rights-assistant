# Week 1 Project Scope: Gig Workers Rights Assistant

**Course:** SAIA 3113 AI Engineering, Universiti Teknologi Malaysia
**Student:** Kaveetiran A/L Sitambaram (A24AI0038), Group 5
**Status:** First draft. I will refine this in the coming topics.

---

## 1. Project Name and Domain

**Project name:** Gig Workers Rights Assistant (working title)

**Domain:** Labour rights and legal information for gig workers in Malaysia.

**Short description:** An assistant that helps gig workers in Malaysia understand their rights under the new Gig Workers Act 2025 (Act 872). Workers can ask questions in Bahasa Malaysia (BM) or English, in their own words, and get a short answer in simple language that cites the exact section of the Act or regulation it is based on. It also tells them what they can do next, for example lodging a complaint through eAduan Gig or going for conciliation. Technically it is a retrieval augmented generation (RAG) system built only on official documents from the Ministry of Human Resources (KESUMA).

**Pilot scope:** The Act is long, so the first version focuses on the four areas that affect workers most in daily work:

1. Account deactivation and suspension (Section 14)
2. Earnings, deductions and earnings slips (Sections 11 to 13)
3. How to resolve a dispute: internal grievance, conciliation and the Gig Workers Tribunal (Parts IV and V)
4. Social security protection with PERKESO (Part VIII and the Social Security Regulations 2026)

The assistant gives legal information, not legal advice. It will not predict the outcome of a case or replace a lawyer or a KESUMA officer.

**Possible extension (later weeks, if time allows):** letting a worker paste a clause from their service agreement or a suspension notice, and having the system point out which parts of the Act are relevant to it.

---

## 2. Problem Statement

**The problem:** Malaysia's Gig Workers Act 2025 came into force on 31 March 2026. For the first time, it gives gig workers clear rights over things like account suspension, earnings slips, deductions and dispute resolution. But a right only helps if the worker knows about it. The information is spread across the Act itself (112 sections in 10 parts), four sets of regulations, several Director General determinations and an 83 page FAQ that is only in BM. Most riders and drivers do not have the time to read legal documents, and a lot of what they hear comes from WhatsApp groups and other riders.

A good example is account suspension. Under Section 14, a platform can suspend a worker for up to 14 days while it investigates, must notify the worker in writing, must give the worker the right to be heard, and if it finds no reason to deactivate, must reactivate the account and pay half of the worker's average daily earnings for the suspended period. A rider who gets suspended is unlikely to know any of this.

**Who faces this problem:** Platform gig workers such as food and parcel delivery riders (p-hailing) and e-hailing drivers, plus non-platform gig workers like freelancers, translators and photographers who are also covered by the Act. Many depend on gig work as their main income and cannot afford to lose days of work over a dispute.

**Why AI makes sense here:**

1. Workers describe their situation in everyday language, often mixing BM and English ("akaun kena suspend 3 hari, boleh claim tak?"). Keyword search in a legal PDF does not handle this.
2. A language model combined with retrieval can find the right section and explain it in simple words.
3. Because every answer cites the section number, the worker (or a KESUMA officer helping them) can check it against the official text.

**Why it needs careful engineering:** Legal information that sounds confident but is wrong can make a worker give up a valid claim or file the wrong complaint. Research also shows that even commercial legal AI tools built with RAG still make things up (see R4 below). So the main work in this project is the system around the model: the documents, retrieval, citation checking, guardrails, evaluation and keeping up with new regulations.

---

## 3. Evidence of the Problem

| No. | Evidence | Source |
|---|---|---|
| E1 | About 1.64 million people work in Malaysia's gig economy (MDEC estimate for 2024), with 246 platforms registered with ministries and agencies. ISEAS puts this at almost 10% of total employment. | KESUMA, *Soalan Lazim Akta Pekerja Gig 2025* (FAQ), Section A, https://www.mohr.gov.my/aktapekerjagig2025/assets/documents/faq.pdf and Lee Hwok Aun (2026), *Gig Workers in Malaysia: Is the New Law a Good Deal?*, ISEAS Perspective 2026/48, https://www.iseas.edu.sg/wp-content/uploads/2026/07/ISEAS-Perspective_2026_48.pdf |
| E2 | The Gig Workers Act 2025 (Act 872) came into force on 31 March 2026, together with its regulations. KESUMA launched the eAduan Gig online complaints system the next day and aims to resolve complaints within 21 working days. | Bernama, 31 Mar 2026, *Act 872 Provides Greater Protection To 1.64 Million Gig Workers*, https://bernama.com/en/news.php?id=2539439 and P.U.(A) 143/2026, which states it comes into operation on 31 March 2026, https://www.mohr.gov.my/aktapekerjagig2025/download.html |
| E3 | The legal material a worker would need to read is large and scattered: the Act itself, four regulations (P.U.(A) 143 to 146 of 2026), Director General determinations on earnings slips and deductions, and an 83 page FAQ in BM. | KESUMA Act 872 download page, https://www.mohr.gov.my/aktapekerjagig2025/download.html |
| E4 | Social protection uptake has been low. Only 26% of gig workers were in PERKESO's Self Employment Social Security Scheme in May 2025. As of 5 August 2025, 133,481 p-hailing and 189,450 e-hailing workers were contributing. | ISEAS Perspective 2026/48 (link above) and KESUMA FAQ, Section A (link above) |
| E5 | Many gig workers are financially vulnerable. Gig work is the main income for 74% of p-hailing riders (DOSM 2022 survey), and 30.7% of p-hailing riders still earn below the RM1,500 minimum wage. | ISEAS Perspective 2026/48 (link above), citing DOSM data |
| E6 | Disputes are already reaching the new Tribunal. The first Gig Workers Tribunal hearing was held on 1 September 2026 in Kuching, between an e-hailing driver and GrabCar Sdn Bhd, over issues like saver trips, cashback incentives and advance booking. | Human Resources Online, 3 Sep 2026, https://www.humanresourcesonline.net/malaysia-s-gig-workers-tribunal-hears-first-case |

Put together, this shows a large group of workers (E1) who just gained new legal rights (E2), but the information is hard to get through (E3), many have not taken up the protections that already exist (E4), many cannot afford to lose income (E5), and real disputes are already happening (E6).

**Note to myself:** I could not find a survey that directly measures how many gig workers understand Act 872. For Week 2 I want to look for one (KESUMA, PERKESO, DOSM or rider associations). If none exists, I could run a small survey of riders myself as part of the requirements stage.

---

## 4. Initial Related Work

| No. | Work or existing solution | What it does | Limitation for my project |
|---|---|---|---|
| R1 | **KESUMA Act 872 portal and FAQ** | The official site has the Act in BM and English, the regulations, an info kit, slides and an 83 page FAQ. https://www.mohr.gov.my/aktapekerjagig2025/ | Everything is static. The worker has to know which document to open and read it themselves. The FAQ is only in BM and covers general questions, not the worker's specific situation. |
| R2 | **AIFA, the Sebenarnya.my chatbot** (MCMC, launched 28 Jan 2025) | A general AI fact check assistant on WhatsApp and the web, in BM, English, Mandarin and Tamil. | It is built for checking news and general information on any topic. It is not designed to answer from the text of Act 872, and there is no public evaluation of how well it handles legal questions. Source: Bernama, https://www.bernama.com/en/news.php?id=2387450 |
| R3 | **MyGOV Malaysia agentic AI** (Digital Ministry, beta since August 2026) | AI chat in the MyGOV app that understands requests in simple language and guides users through government transactions, like paying a police fine. | It is for finding and completing government services, not for explaining a worker's legal rights. Source: Bernama, 10 Aug 2026, https://www.bernama.com/en/news.php?id=2592746 |
| R4 | **Magesh et al. (2025)**, *Hallucination Free? Assessing the Reliability of Leading AI Legal Research Tools*, Journal of Empirical Legal Studies 22, 216 | The first preregistered evaluation of commercial legal AI tools from LexisNexis and Thomson Reuters, which use RAG. | Even these professional tools made things up 17% to 33% of the time. They are also built for US lawyers, not for workers asking about Malaysian law in BM. This shows why my project needs strict citation checking and proper evaluation. Source: https://doi.org/10.1111/jels.12413 |
| R5 | **Dahl et al. (2024)**, *Large Legal Fictions: Profiling Legal Hallucinations in Large Language Models*, Journal of Legal Analysis 16, 64 | Tests how often general LLMs like ChatGPT 4 give wrong legal information. | General LLMs hallucinated at least 58% of the time on legal questions and often went along with wrong assumptions in the user's question. This is the risk if a worker just asks a normal chatbot. Source: https://doi.org/10.1093/jla/laae003 |

---

## 5. Engineering Gap

From what I could find, existing options fall into three groups:

1. **Official static documents** (R1). They are accurate, but the worker has to find and read the right section alone.
2. **General government chatbots** (R2, R3). They are easy to use, but they are not built on the text of Act 872 and are not evaluated on legal questions.
3. **Legal AI research and tools** (R4, R5). They show that RAG reduces hallucination but does not remove it, and they are made for lawyers in other countries.

I did not find any tool that lets a Malaysian gig worker ask about their rights under Act 872 in their own words and get an answer tied to the actual section. Since the Act only came into force in March 2026, this is not surprising, but it also means the gap is real right now.

**The gap my project targets:** a complete AI system (not just a model) that

1. answers only from official KESUMA documents (the Act, its regulations and official guidance),
2. cites the exact section or regulation for every answer, and checks that the citation is correct,
3. works in both BM and English, including mixed language questions,
4. has clear safety rules (no personal legal advice, no predicting case outcomes, and points the worker to eAduan Gig, conciliation or the Tribunal when they need real help),
5. keeps track of which version of each document it is using, since new regulations and Tribunal decisions will keep coming, and
6. is tested on more than accuracy, including citation correctness, faithfulness to the source, refusal behaviour, response time and quality in both languages.

---

## 6. Project Objectives

| No. | Objective | First target (will be refined) |
|---|---|---|
| O1 | Build a RAG pipeline over Act 872 (BM and English), its regulations and official KESUMA guidance for the four pilot areas, where every answer cites the section it comes from. | All official documents from the KESUMA download page collected with version dates. Every answer includes at least one section or regulation citation. |
| O2 | Build a test set and evaluate the system on several quality dimensions. | At least 60 test questions in BM and English, including realistic worker scenarios and 15 safety or out of scope questions. Measure citation correctness, faithfulness, refusal behaviour, response time and the score gap between BM and English. |
| O3 | Build and test safety guardrails. | The system refuses requests for personal legal advice or case predictions, and points to the correct next step (eAduan Gig, conciliation or the Tribunal), in all safety test cases. |

---

## 7. Target Users

**Main users:** Platform gig workers in Malaysia, especially food and parcel delivery riders (p-hailing) and e-hailing drivers. They are the largest group covered by the Act, often depend on gig work as their main income (E5), and mostly use their phone while working, so answers need to be short and quick to read.

**Other users:**

1. Non-platform gig workers covered by the Act, such as freelancers, translators, photographers and people in film and music, who are less likely to have a rider community to ask.
2. Gig worker associations and volunteers who help their members with questions, and could use the assistant to find the right section faster.

**Language:** Many workers are more comfortable in BM or mix BM and English, so both have to work equally well.

**Not meant for:** Lawyers or platform companies looking for compliance advice, or workers who already have an active case and need representation. In these cases the assistant should point them to KESUMA, the Industrial Relations Department or legal aid.

---

## 8. Data Sources

All of these are official and publicly accessible from KESUMA's Act 872 portal (https://www.mohr.gov.my/aktapekerjagig2025/download.html).

| No. | Source | Notes |
|---|---|---|
| D1 | Gig Workers Act 2025 (Act 872), English version: https://www.mohr.gov.my/aktapekerjagig2025/assets/documents/Act%20872.pdf | Main legal text. Also available in BM (Akta 872). |
| D2 | Gig Workers Regulations 2026, P.U.(A) 143 to 146 (social security, Tribunal, compounding of offences, conciliation proceedings) | The detailed rules under the Act, for example the 1.25% social security deduction. |
| D3 | KESUMA FAQ, *Soalan Lazim Akta Pekerja Gig 2025*: https://www.mohr.gov.my/aktapekerjagig2025/assets/documents/faq.pdf | 83 pages of official answers in BM. Also useful as a starting point for the test set. |
| D4 | Director General determinations on earnings slips and earnings deductions | Official decisions on how earnings slips and deductions must work. |
| D5 | PERKESO information on social security for gig workers: https://www.perkeso.gov.my | For the social security part of the pilot. |

**How I plan to handle the data:**

1. Check the terms of use of each site before downloading anything.
2. Record the source, URL, document version and date accessed for every document, so every answer can be traced back.
3. Only commit material that is fine to share publicly. For the PDFs I will commit a download script and a list of sources instead of the files themselves.

---

## 9. Comparison with EduAdvisor

| Aspect | EduAdvisor (lecture example) | Gig Workers Rights Assistant |
|---|---|---|
| Basic idea | RAG over approved university documents, with citations. | Same idea, but over official KESUMA legal documents. |
| Stack layers | Application (chat interface, retrieval, guardrails), model (foundation and embedding models), infrastructure (API, vector database, monitoring). | Same three layers. |
| Type of source | Handbooks and course catalogues written for students. | Legal text written for lawyers and officers, so the system has to explain it in simple words without changing the meaning. |
| Citation | Cites the handbook page. | Has to cite the exact section and subsection, which is easier to check automatically but also easier to get wrong. |
| Example failure | Makes up a course prerequisite. | Makes up a right the worker does not have, or misses a deadline or condition in the law. |
| Risk level | Lower. A wrong prerequisite is annoying but fixable. | Higher. A wrong answer could make a worker give up a valid claim or lose income. |
| What it answers | Questions about courses and requirements. | Has to refuse personal legal advice and point to the right official channel. |
| Language | Mainly English. | BM and English, including mixed language questions. |
| How often data changes | Handbooks change about once a year. | The law is new, so more regulations, determinations and Tribunal decisions are likely. Version tracking matters more. |

---

## 10. Responsible AI Risks

| No. | Risk | Possible impact | What I plan to build | How I will check it |
|---|---|---|---|---|
| RAI 1 | **Wrong or made up legal information** | A worker believes they have a right they do not have, or misses one they do have. | Answer only from retrieved official text, refuse when nothing relevant is found, and check that every cited section exists and supports the answer. | Citation correctness and faithfulness scores on the test set. |
| RAI 2 | **Acting like a lawyer** | A worker treats the answer as legal advice for their case and makes a bad decision. | Guardrails that refuse case specific advice and outcome predictions, plus a clear "legal information, not legal advice" notice and a pointer to eAduan Gig, conciliation or the Tribunal. | All safety test cases must pass. Guardrail triggers are logged. |
| RAI 3 | **Outdated law** | The system quotes an old version after new regulations or amendments come out. | Store the version and date of every document, update regularly, and show the document date in each answer. | Freshness checks in the test set and a document list with versions. |
| RAI 4 | **Privacy** | Workers paste agreements or notices with their name, IC number or account details, which end up in logs. | Never ask for personal data, mask personal details before logging, and show a short privacy notice. | Log review and a test for personal data in logs. |
| RAI 5 | **Unequal quality between groups** | BM users, or non-platform gig workers whose situations are less covered in the FAQ, get worse answers. | Build a test set that covers both languages and both types of gig worker, and compare the results. | Separate scores for each language and worker type. |
| RAI 6 | **Prompt injection** | Text pasted by a user (for example a service agreement) contains instructions that try to change how the system behaves. | Treat pasted and retrieved text as information only, never as instructions, and include attack style inputs in testing. | Pass rate on the adversarial test questions. |

---

## Planned Architecture (rough idea, will change)

1. Worker asks a question in BM or English.
2. Input check: is it in scope, is it asking for personal legal advice, does it contain personal data?
3. Retriever searches the Act, regulations and KESUMA guidance (embeddings and a vector database, split by section).
4. The prompt is built from the instructions, the retrieved sections and the rule to always cite.
5. The foundation model writes the answer (through an API).
6. Output check: the cited sections exist and support the answer, and no personal legal advice is given.
7. The worker sees the answer with section citations, the document date and the next step they can take.
8. Everything is logged (without personal data) for monitoring and feedback.

| Stack layer | Components |
|---|---|
| Application | Chat interface, retrieval workflow, prompts, guardrails, citation checker, evaluation |
| Model | Foundation model (not chosen yet) and embedding model |
| Infrastructure | API hosting, vector database, logging and monitoring |

---

## Week 1 files in this repository

1. `docs/week1_observation_sheet.md`: our group observation sheet for Claude.ai (Part A)
2. `docs/week1_system_map.png`: our group conceptual system map (Part B)
3. `docs/week1_project_scope.md`: this document (Part C)
