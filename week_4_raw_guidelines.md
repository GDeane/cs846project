# Week 4 Raw Guidelines: Requirements

**Authors:** [Gavin Deane, Artemiy Vishnyakov, Savira Umar]  
**Readings Assigned:**

- Advancing Requirements Engineering through Generative AI: Assessing the Role of
  LLMs — [PDF](https://arxiv.org/pdf/2310.13976)
- Investigating ChatGPT’s Potential to Assist in Requirements Elicitation
  Processes — [arXiv](https://arxiv.org/abs/2307.07381)
- SpecGen: Automated Generation of Formal Program Specifications via Large Language
  Models — [arXiv](https://arxiv.org/abs/2401.08807)
- Requirements Elicitation Follow-Up Question Generation — [arXiv](https://arxiv.org/abs/2507.02858)
- Requirements Engineering using Generative AI: Prompts and Prompting
  Patterns — [arXiv](https://arxiv.org/abs/2311.03832)
- Requirements Satisfiability with In-Context Learning — [arXiv](https://arxiv.org/abs/2404.12576)
- An Automated Model of Software Requirement Engineering Using
  GPT-3.5 — [IEEE](https://ieeexplore.ieee.org/document/10459458)

**Additional sources explored beyond assigned readings**

- a
- b
- c

## 1. Guidelines from Readings

> **Note:** Guidelines should be actionable, specific, and usable during real coding tasks.

### Guideline 1: Design a context prompt [1]

**Description:**  
Design a prompt that gives the "job description" to the LLM before asking it to generate requirements or questions.

**Reasoning:**  
This serves two purposes. First, the process of designing this prompt forces you to think about the structure of the
output, the type of language you want used, the process you want followed, and the standards to which you want the job
done.

**Example:**  
"Act as a senior systems engineer following IEEE 29148.
First ask clarifying questions about goals, stakeholders, constraints, and risks.
Do not propose solutions yet.

Once clarified:

- Produce functional and non-functional requirements using "The system SHALL..."
- Each requirement must be atomic, testable, and free of design decisions
- Include acceptance criteria and verification method
- List assumptions and potential conflicts
- Identify out-of-scope items
- Provide a traceability matrix

Finally, critique the requirements for ambiguity and testability and revise as needed."


---

### Guideline 2: [Short, Actionable Title]

(Repeat the same structure for each guideline.)

---

### Guideline N: [Short, Actionable Title]

(Repeat the same structure for each guideline.)

---

## 2. Guidelines from any related research/grey literature like practitioner or developer tool blogs

> **Note:** Guidelines should be actionable, specific, and usable during real coding tasks.

### Guideline 1: [Short, Actionable Title]

**Description:**  
State the guideline clearly and concretely.

**Reasoning:**  
Explain *why* this guideline is important, referencing readings and external sources where relevant.

**Example:**  
Provide a brief illustrative example (code or pseudo-code if helpful).

---

### Guideline 2: [Short, Actionable Title]

(Repeat the same structure for each guideline.)

---

### Guideline N: [Short, Actionable Title]

(Repeat the same structure for each guideline.)

---

## 3. Guidelines from LLMs

> **Note:** Guidelines should be actionable, specific, and usable during real coding tasks.

### Guideline 1: [Short, Actionable Title]

**Description:**  
State the guideline clearly and concretely.

**Reasoning:**  
Explain *why* this guideline is important, referencing readings and external sources where relevant.

**Example:**  
Provide a brief illustrative example (code or pseudo-code if helpful).

---

### Guideline 2: [Short, Actionable Title]

(Repeat the same structure for each guideline.)

---

### Guideline N: [Short, Actionable Title]

(Repeat the same structure for each guideline.)

---

## 4. References

[1] K. Ronanki, C. Berger, and J. Horkoff, “Investigating ChatGPT’s Potential to Assist in Requirements Elicitation
Processes,” Jul. 14, 2023, arXiv: arXiv:2307.07381. doi: 10.48550/arXiv.2307.07381.

[2] L. Ma, S. Liu, Y. Li, X. Xie, and L. Bu, “SpecGen: Automated Generation of Formal Program Specifications via Large
Language Models,” Feb. 25, 2025, arXiv: arXiv:2401.08807. doi: 10.48550/arXiv.2401.08807.

[3] Y. Shen, A. Singhal, and T. Breaux, “Requirements Elicitation Follow-Up Question Generation,” Jul. 03, 2025, arXiv:
arXiv:2507.02858. doi: 10.48550/arXiv.2507.02858.

[4] Jules White and Quchen Fu and Sam Hays and Michael Sandborn and Carlos Olea and Henry Gilbert and Ashraf Elnashar
and Jesse SpencerSmith and Douglas C. Schmidt. A Prompt Pattern Catalog to Enhance Prompt Engineering with ChatGPT,

2023.

[5] C. S. Xia and L. Zhang, “Keep the conversation going: Fixing 162 out of 337 bugs for $0.42 each using chatgpt,”
arXiv preprint arXiv:2304.00385, 2023.

[6] T. Brown, B. Mann, N. Ryder, M. Subbiah, J. D. Kaplan, P. Dhariwal, A. Neelakantan, P. Shyam, G. Sastry, A. Askell
et al., “Language models are few-shot learners,” Advances in neural information processing systems, vol. 33, pp.
1877–1901, 2020.

[7] J. White, Q. Fu, S. Hays, M. Sandborn, C. Olea, H. Gilbert, A. Elnashar, J. Spencer-Smith, D. C. Schmidt, “A Prompt
Pattern Catalog to Enhance Prompt Engineering with ChatGPT”, arXiv preprint arXiv:2302.11382, 2023.

[8] M. Sclar, Y. Choi, Y. Tsvetkov, and A. Suhr. “Quantifying language models’ sensitivity to spurious features in
prompt design or: How I learned to start worrying about prompt formatting.” In arXiv preprint arXiv:2310.11324, 2023.

[9] N. Kassner and H. Sch ̈utze. “Negated and Misprimed Probes for Pretrained Language Models: Birds Can Talk, But
Cannot Fly.” In Proceedings of the 58th Annual Meeting of the Association for Computational Linguistics, pages
7811–7818, Online. Association for Computational Linguistics, 2020.

[10] T. Brown, B. Mann, N. Ryder, M. Subbiah, J.D. Kaplan, P. Dhariwal, A. Neelakantan et al. “Language models are
few-shot learners.” Advances in neural information processing systems 33: 1877-1901, 2020.



---

