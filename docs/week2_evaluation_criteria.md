# Week 2 Evaluation Criteria: Gig Workers Rights Assistant

**Course:** SAIA 3113 AI Engineering, Universiti Teknologi Malaysia
**Student:** Kaveetiran A/L Sitambaram (A24AI0038)
**Version:** 1.0
**Based on:** [`week2_requirements.md`](week2_requirements.md)

These criteria cover the requirements that decide whether the assistant is actually useful to gig workers. Each one links back to a project objective and a requirement ID.

## Evaluation Criteria Table

| Objective / Requirement ID | Evaluation Criterion | Capability Bucket | Measurement Method | Metric | Threshold | User / Business Outcome |
|---|---|---|---|---|---|---|
| O1, O3 / FR1, NFR1 | Answer correctness on Act 872 | Domain-specific capability | Run at least 45 in scope questions (BM and English) covering the four pilot areas, including tricky rules such as the 14 day suspension limit, the 7 day payment rule and the fact that deactivation disputes skip the internal grievance step. Score each answer as correct, partly correct or wrong against a reference answer written from the Act. | Correct response rate | ≥ 80% | Workers get reliable answers about their rights for routine situations. |
| O1, O3 / FR2, NFR2, RAI4 | Section citation and support | Instruction-following capability | For every in scope answer, check that a citation is present, that the cited section exists in the indexed documents, and that the cited text actually supports the answer. | Citation presence rate; citation accuracy rate | 100% presence; ≥ 90% accuracy | Workers, association volunteers or KESUMA officers can check every answer against the official Act. |
| O2, O3 / FR6, RAI2 | Refusal of legal advice and out of scope requests | Instruction-following capability | Run a scope and safety set of at least 20 queries, such as "will I win at the Tribunal?", "how much compensation will I get?" and questions about tax or immigration. Separately, check that in scope questions are not wrongly refused. | Refusal and redirect success rate; false refusal rate on in scope questions | ≥ 95% refusal and redirect; ≤ 10% false refusal | The assistant stays a legal information tool and does not act like a lawyer, while still being useful. |
| O2, O3 / FR4, RAI4 | Admitting when the sources do not cover a question | Generation capability | Include at least 10 questions the documents cannot answer (for example details not decided yet by regulations) and check whether the system says it does not have enough information instead of guessing. | Correct "not enough information" rate | ≥ 90% | Workers are not misled by confident answers that have no legal basis. |
| O3 / RAI1, FR3 | Language parity (BM vs English) | Domain-specific capability | Run the same in scope questions in BM and English (parallel set) and compare correct response rates. Also check that the reply language matches the question language. | Absolute gap in correct response rate; reply language match rate | ≤ 10 percentage points gap; ≥ 95% language match | BM speaking workers get the same quality of help as English speaking workers. |
| O1 / FR7 | Answer clarity on a phone | Generation capability | Score each answer with a simple clarity rubric: summary comes first, plain words, legal terms explained, citation shown, about 150 words or less. | Share of answers meeting all rubric points | ≥ 85% | Workers can read and understand the answer quickly between jobs. |
| O3 / NFR3, NFR5 | Response latency and cost | Cost and latency | Measure end to end response time and record model usage for the whole evaluation run. | p90 latency; cost per 100 queries | < 5 s; < US$0.50 per 100 queries | The tool is quick enough to use on the road and cheap enough to keep running. |

## Simple Rubrics (initial)

**Answer correctness (per answer):**

1. **Correct:** matches the reference answer and includes every key condition (for example time limits or exceptions).
2. **Partly correct:** main point is right but a key condition is missing or unclear.
3. **Wrong:** states something the Act does not say, or gives the wrong rule.

Only "correct" counts towards the correct response rate.

**Clarity (per answer, all four needed):**

1. The first sentence directly answers the question.
2. Legal terms like "contracting entity" or "conciliation" are explained in simple words.
3. The section citation is shown.
4. The answer is about 150 words or less.

A more formal rubric and a second marker for agreement will be added when systematic evaluation is covered later in the course.

## Reflection

**Which evaluation criterion is most important for determining whether the application will be useful to its intended users? Why?**

The most important one is section citation and support. Gig workers are not lawyers, so they cannot easily tell a right answer from a wrong one just by reading it. The citation is what turns the assistant from "a chatbot said so" into something a worker can actually rely on. They can show the section to the platform, to their association, or to a KESUMA officer when lodging a complaint. If the citations are wrong, even correct sounding answers become useless or harmful, because the worker might quote a section that does not say what the system claimed. Answer correctness matters a lot too, but a correct answer with no verifiable source is much weaker in a real dispute.
