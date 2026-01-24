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

- A Prompt Pattern Catalog to Enhance Prompt Engineering with ChatGPT — [arXiv](https://arxiv.org/abs/2302.11382)
- Conversational Automated Program Repair — [arXiv](https://arxiv.org/abs/2301.13246)
- Keep the conversation going: Fixing 162 out of 337 bugs for $0.42 each using
  chatgpt — [arXiv](https://arxiv.org/abs/2304.00385)
- Language models are few-shot
  learners — [NeurIPS](https://proceedings.neurips.cc/paper_files/paper/2020/file/1457c0d6bfcb4967418bfb8ac142f64a-Paper.pdf)
- Quantifying language models’ sensitivity to spurious features in prompt design or: How I learned to start worrying
  about prompt formatting — [arXiv](https://arxiv.org/abs/2310.11324)
- Negated and Misprimed Probes for Pretrained Language Models: Birds Can Talk, But Cannot
  Fly — [arXiv](https://arxiv.org/abs/1911.03343)

## 1. Guidelines from Readings

> **Note:** Guidelines should be actionable, specific, and usable during real coding tasks.

### Guideline 1: Design a structured context prompt [1, 6, 11, 12]

**Description:**  
Design a prompt that gives the "job description" to the LLM before asking it to generate requirements or questions.

**Reasoning:**  
This serves two purposes.

- **First**, the process of designing this prompt forces you to think about the structure of the
  output, the type of language you want used, the process you want followed, and the standards to which you want the job
  done [1].
- **Second**, You make the LLM consider all of these expectations before its work begins.

Also, previous prompt pattern research [6] has shown that structured prompts outperform free-text prompts in creating
correct output.

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

### Guideline 2: Converse with the LLM [2, 10]

**Description:**  
Before creating requirements, talk to the LLM back and forth to refine the problem domain.

**Reasoning:**  
The process of back-and-forth conversation helps the model uncover missing constraints, assumptions, and edge cases.
This process has been demonstrated to improve the effectiveness of LLMs for bug fixing [10], and is one of the main
techniques used to generate specifications in SpecGen [2].

**Example:**

1. "Pretend you're a client. Talk to me about you would desire from a system that does X."
2. Converse for a while, save transcript
3. In a new session: "You are a senior requirements engineer creating a set of requirements based on this conversation"

---

### Guideline 3: Assign a role/persona to the LLM [2, 3, 4, 11]

**Description:**  
Tell the model what it is (e.g. "senior requirements engineer", "technical interviewer for Google", "end-user") before
asking it to do something.

**Reasoning:**  
The language used and professionalism of the LLM will vary based on the role it has to play [2, 4]. Explicitly defined
roles will also give additional context about the problem domain [2].

**Example:**  
"You are an INTERVIEWER. Your job is to ask follow-up questions to clarify goals, constraints, assumptions, and
tradeoffs. Do not propose solutions."

---

### Guideline 4: Provide few-shot examples [2, 3, 9, 11]

**Description:**  
When attempting to describe desired behavior of a program or system, give 1-3 examples of desired output.

**Reasoning:**  
Few-shot examples have been shown to reliably improve adherence to format and improve performance in LLMs [9]. These
examples also double as tests for your requirements.

**Example:**  
"Example Requirement:
Upon authenticating the signal, the system SHALL cause the garage door to open within 10 seconds"

---

### Guideline 5: Capitalize role identifiers [3, 7]

**Description:**  
When providing context (such as a transcript), capitalize the role identifiers such as "INTERVIEWER" and "INTERVIEWEE".

**Reasoning:**  
When reading transcripts, LLMs can sometimes misclassify which person was responsible for saying what, which leads to
all sorts of errors [3]. Luckily, capitalizing role identifiers has been found to significantly reduce this
classification error [3, 7].

**Example:**  
Preprocess input transcript as follows before giving it as context:

_Before_

- Interviewer: ...
- Interviewee: ...

_After_

- INTERVIEWER: ...
- INTERVIEWEE: ...

---

### Guideline 6: Reduce usage of Negation [3, 8]

**Description:**  
Avoid the use of double-negatives when expressing ideas in prompts.

**Reasoning:**  
LLM performance has been shown to be poor in the presence of negation [8]. That is, pretrained language models
have had trouble distinguishing between terms like "can" and "cannot" in text [8].

**Example:**  
Express as "remember to do X" rather than "don't forget to do X".

---

### Guideline 7: Treat the output as a draft, not as a final product [11, 12, 13, 14]

**Description:**
Do not treat the output of your LLM as a finished product. Treat it like a draft given to you for review by a colleague.

**Reasoning:**  
LLMs are powerful, but not perfect. Their outputs may contain senior engineer-level insights, but can also easily
contain amateur-level mistakes. Many LLM researchers for RE advocate for human oversight in their
studies of LLMs for requirements engineering, and object to LLMs as final authorities [11, 12, 13, 14].

**Example:**  
N/A

---

### Guideline 8: Base your prompting pattern on the RE task being performed [12, 13]

**Description:**  
Select your LLM prompting pattern based on the task.

**Reasoning:**  
Different methods of prompting LLMs ('prompt patterns') have been shown to be effective in different parts of the RE
process [12]. For instance, making the LLM ask the user questions as needed created better performance on binary
classification compared to making the LLM act as an RE expert [12].

**Example:**  
Pattern 1: "Cognitive Verifier"

"Classify the given list of requirements into functional (labelled as F) and non-functional requirements (labelled as
NF). Ask me questions if needed to break the given task into smaller subtasks. All the outputs to the smaller subtasks
must be combined before you generate the final output." [12]

Pattern 2: "Persona"

"Act as a requirements engineering domain expert and classify the given list of requirements into functional (labelled
as F) and non-functional requirements (labelled as NF)." [12]

---

### Guideline 9: Use multiple runs and majority vote for robustness [13]

**Description:**  
For important decisions, try running the LLM on the same prompt several times and taking the majority vote.

**Reasoning:**  
LLMs outputs are stochastic (assuming temperature != 0). This means that they can go either way when asked to decide yes
or no on something. Taking several runs gives both an idea of the uncertainty and a more robust answer [13].

**Example:**  
"Classify this sample as category A or category B. Explain your reasoning."
Repeat 10 times
Count the number of A's and B's
Think

---

### Guideline 10: Avoid yes/no without explanation [13]

**Description:**  
Do not ask a LLM to give binary responses without explanation.

**Reasoning:**  
Reasoning given by LLMs can often be fuzzy or based on hallucinations. If you ask for a decision without explanation,
you may receive a result based on broken logic, but you can no longer verify the deranged reasoning [13].

**Example:**  
"Classify these samples into category A or category B. For each categorization, explain your reasoning"

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

[4] C. S. Xia and L. Zhang, “Keep the conversation going: Fixing 162 out of 337 bugs for $0.42 each using chatgpt,”
arXiv preprint arXiv:2304.00385, 2023.

[5] T. Brown, B. Mann, N. Ryder, M. Subbiah, J. D. Kaplan, P. Dhariwal, A. Neelakantan, P. Shyam, G. Sastry, A. Askell
et al., “Language models are few-shot learners,” Advances in neural information processing systems, vol. 33, pp.
1877–1901, 2020.

[6] J. White, Q. Fu, S. Hays, M. Sandborn, C. Olea, H. Gilbert, A. Elnashar, J. Spencer-Smith, D. C. Schmidt, “A Prompt
Pattern Catalog to Enhance Prompt Engineering with ChatGPT”, arXiv preprint arXiv:2302.11382, 2023.

[7] M. Sclar, Y. Choi, Y. Tsvetkov, and A. Suhr. “Quantifying language models’ sensitivity to spurious features in
prompt design or: How I learned to start worrying about prompt formatting.” In arXiv preprint arXiv:2310.11324, 2023.

[8] N. Kassner and H. Sch ̈utze. “Negated and Misprimed Probes for Pretrained Language Models: Birds Can Talk, But
Cannot Fly.” In Proceedings of the 58th Annual Meeting of the Association for Computational Linguistics, pages
7811–7818, Online. Association for Computational Linguistics, 2020.

[9] T. Brown, B. Mann, N. Ryder, M. Subbiah, J.D. Kaplan, P. Dhariwal, A. Neelakantan et al. “Language models are
few-shot learners.” Advances in neural information processing systems 33: 1877-1901, 2020.

[10] C. S. Xia and L. Zhang, “Conversational automated program repair,” arXiv preprint arXiv:2301.13246, 2023.

[11] Arora, C., Grundy, J., Abdelrazek, M. (2024). Advancing Requirements Engineering Through Generative AI: Assessing
the Role of LLMs. In: Nguyen-Duc, A., Abrahamsson, P., Khomh, F. (eds) Generative AI for Effective Software Development.
Springer, Cham. https://doi.org/10.1007/978-3-031-55642-5_6

[12] K. Ronanki, B. Cabrero-Daniel, J. Horkoff, and C. Berger, “Requirements Engineering using Generative AI: Prompts
and Prompting Patterns,” arXiv preprint arXiv:2311.03832, Nov. 2023. doi: 10.48550/arXiv.2311.03832.

[13] M. Borg, K. Wnuk, and A. Ferrari, “Requirements Satisfiability with In-Context Learning,” arXiv preprint arXiv:
2404.12576, Apr. 2024. doi: 10.48550/arXiv.2404.12576.

[14] A. M. Author et al., “An Automated Model of Software Requirement Engineering Using GPT-3.5,” 2023.


---

