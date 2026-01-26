# Week 4 Guidelines: Requirements

**Authors:** [Gavin Deane, Artemiy Vishnyakov, Savira Umar]  
**Readings Assigned:**

- Advancing Requirements Engineering through Generative AI: Assessing the Role of
  LLMs — [PDF](https://arxiv.org/pdf/2310.13976) [10]
- Investigating ChatGPT’s Potential to Assist in Requirements Elicitation
  Processes — [arXiv](https://arxiv.org/abs/2307.07381) [1]
- SpecGen: Automated Generation of Formal Program Specifications via Large Language
  Models — [arXiv](https://arxiv.org/abs/2401.08807) [2]
- Requirements Elicitation Follow-Up Question Generation — [arXiv](https://arxiv.org/abs/2507.02858) [3]
- Requirements Engineering using Generative AI: Prompts and Prompting
  Patterns — [arXiv](https://arxiv.org/abs/2311.03832) [11]
- Requirements Satisfiability with In-Context Learning — [arXiv](https://arxiv.org/abs/2404.12576) [12]
- An Automated Model of Software Requirement Engineering Using
  GPT-3.5 — [IEEE](https://ieeexplore.ieee.org/document/10459458) [13]

**Additional (academic) sources explored beyond assigned readings**

- A Prompt Pattern Catalog to Enhance Prompt Engineering with ChatGPT — [arXiv](https://arxiv.org/abs/2302.11382) [6]
- Conversational Automated Program Repair — [arXiv](https://arxiv.org/abs/2301.13246) [9]
- Keep the conversation going: Fixing 162 out of 337 bugs for $0.42 each using
  chatgpt — [arXiv](https://arxiv.org/abs/2304.00385) [4]
- Language models are few-shot
  learners — [NeurIPS](https://proceedings.neurips.cc/paper_files/paper/2020/file/1457c0d6bfcb4967418bfb8ac142f64a-Paper.pdf) [5]
- Quantifying language models’ sensitivity to spurious features in prompt design or: How I learned to start worrying
  about prompt formatting — [arXiv](https://arxiv.org/abs/2310.11324) [7]
- Negated and Misprimed Probes for Pretrained Language Models: Birds Can Talk, But Cannot
  Fly — [arXiv](https://arxiv.org/abs/1911.03343) [8]

**Additional (non-academic) sources explored beyond assigned readings**

- Transforming Specifications into Requirements: Leveraging Copilot for Optimal
  Results — [LinkedIn](https://www.linkedin.com/pulse/transforming-specifications-requirements-leveraging-copilot-sosa-7ze2e) [14]
- Revolutionizing Software Requirements Engineering with
  LLMs — [Medium](https://medium.com/@samiullah6799/revolutionizing-software-requirements-engineering-with-llms-db90551a3965) [15]
- A Developer’s Guide to Leveraging LLMs in the Software Development
  Lifecycle — [Apecton](https://apecton.com/ai/a-developers-guide-to-leveraging-llms-in-the-software-development-lifecycle/) [16]
- How to use ChatGPT for Requirement
  Analysis? — [LinkedIn](https://www.linkedin.com/pulse/how-use-chatgpt-requirement-analysis-dnyaneshwar-divekar-qvzjf) [17]
- Using AI for requirements analysis: A case
  study — [Thoughtworks](https://www.thoughtworks.com/en-us/insights/blog/generative-ai/using-ai-requirements-analysis-case-study) [18]
- Using ‘Given-When-Then’ to Discover and Validate
  Requirements — [EBG Consulting](https://ebgconsulting.com/blog/using-given-when-then-to-discover-and-validate-requirements-2/) [19]
- Key words for use in RFCs to Indicate Requirement Levels - [datatracker](https://datatracker.ietf.org/doc/html/rfc2119) [20]
- Zhang v Chen - [CanLII](https://canlii.ca/t/k314g) [21]

## 1. Guidelines

### Guideline 1: Design a structured context prompt [1, 6, 10, 11, 17]

**Description:**

Design a prompt that gives the "job description" to the LLM before asking it to generate requirements or questions.
Provide sufficient and relevant context to the LLM to constrain the problem space it is working in.

**Reasoning:**

This serves several purposes.

- **First**, the process of designing this prompt forces you to think about the structure of the
  output, the type of language you want used, the process you want followed, and the standards to which you want the job
  done [1].
- **Second**, You make the LLM consider all of these expectations before its work begins.

In addition, a structured high information-density prompt reportedly leads to fewer generic or boilerplate
responses [17]. It also makes the outputs easier to evaluate when you expect a structured output.

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

### Guideline 2: Converse with the LLM to analyze the problem [2, 9, 14, 15, 16]

**Description:**

Before creating requirements, talk to the LLM back and forth to refine the problem domain. This includes:

* Analyzing the underlying business or user problem
* Summarizing and synthesizing existing documentation
* Identifying and fleshing out candidate requirements
* Detecting contradictions or inconsistencies
* Clarifying ambiguities, assumptions, and open questions

**Reasoning:**

The process of back-and-forth conversation helps the model uncover missing constraints, assumptions, and edge cases.
This process has been demonstrated to improve the effectiveness of LLMs for bug fixing [9], and is one of the main
techniques used to generate specifications in SpecGen [2]. In addition, this mirrors established requirements
elicitation practices, making it easier to evaluate (familiar structure).

**Example:**

Bad: *Write user stories for the login feature.*

* No analysis of the problem

Good: *You are a senior requirements engineer. Before writing any user stories, analyze the following project
description:*

* *Goal: Enable registered users to log in and access personalized content*
* *Constraints: Web application, email/password authentication, must support 2FA in future*
* *Known risks: Security and session management*

Task:

* *Identify the core problem and main user goals*
* *Summarize existing documentation and assumptions*
* *List ambiguities, contradictions, and open questions*
* *Suggest a structured set of clarifying questions to resolve them*
  *Do not write user stories or acceptance criteria yet.*

Ask individual questions in a back-and-forth manner to refine.

---

### Guideline 3: Assign a role/persona to the LLM [2, 3, 4, 10, 17]

**Description:**

Tell the model what it is (e.g. "senior requirements engineer", "technical interviewer for Google", "end-user") before
asking it to do something. You can also create separate chats with separate personas for differing viewpoints.

**Reasoning:**

The language used and professionalism of the LLM will vary based on the role it has to play [2, 4, 17]. Explicitly
defined
roles will also give additional context about the problem domain [2].

**Example:**

Bad: *Review these user stories and suggest improvements.*

Good: *You are a senior product manager with 10+ years of experience in enterprise software development and familiarity
with ISO/IEC/IEEE standards. Review the following user stories and suggest improvements.*

---

### Guideline 4: Provide few-shot examples [2, 3, 10, 16]

**Description:**

When attempting to describe desired behavior of a program or system, give 1-3 examples of desired output.

**Reasoning:**

Few-shot examples have been shown to reliably improve adherence to format and improve performance in LLMs [5]. These
examples also double as tests for your requirements, increasing verifiability. In addition, examples are one of the
strongest methods of enforcing structure in output, making it more likely to follow that structure and read output [16].

**Example:**

Bad: *Generate user stories for the system.*

Good: *Generate user stories of exact format "As a [type of user], I want [an action] so that [a result]."
(i.e. "As a store owner, I want a way of hearing when customers enter my store, so that I know when to come to the
front.")*

---

### Guideline 5: Maximise prompt information density [17]

**Description:**

Provide sufficient and relevant context to the LLM to fully constrain the problem space. The prompt should explicitly
state assumptions, scope, constraints, and expected output format, while avoiding unnecessary or unrelated information.
This minimizes ambiguity and prevents the model from making implicit assumptions.

**Reasoning:**

High information density prompts guide the LLM toward producing precise, domain-appropriate outputs. By clearly
specifying context and constraints, the model avoids defaulting to generic or boilerplate responses and instead
generates results that are aligned with stakeholder intent, system boundaries, and verification needs. This leads to
higher quality, consistent, and more testable requirements artifacts.

**Example:**

*As an expert in software testing, review the following requirements and identify any gaps, along with their potential
impact, providing actionable pointers for improvement in tabular format.*

Bad: *Explain the login requirement and generate acceptance criteria*

Good as an intermediary data: *As a registered user, I want to be able to log in to my account so that I can access
personalized content and features*

Good: *You are assisting with requirements engineering for a consumer-facing web application based on the following user
story: ""As a registered user, I want to be able to log in to my account so that I can access personalized content and
features". Generate clear, testable acceptance criteria using Given When Then format.*

*Assumptions and constraints:*

* *Users authenticate using email and password*
* *The system must comply with basic security best practices (password hashing, failed login handling)*
* *Login is performed via a web browser*
* *Include both successful and unsuccessful login scenarios*
* *Do not invent features beyond authentication and session access*

> NOTE: look at [19] for information on Given-When-Then test case format

---

### Guideline 6: Capitalize role identifiers [3, 7]

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

### Guideline 7: Base your prompting pattern on the RE task being performed [11, 12]

**Description:**

Select your LLM prompting pattern based on the task.

**Reasoning:**

Different methods of prompting LLMs ('prompt patterns') have been shown to be effective in different parts of the RE
process [11]. For instance, making the LLM ask the user questions as needed created better performance on binary
classification compared to making the LLM act as an RE expert [11].

**Example:**

Pattern 1: "Cognitive Verifier"

"Classify the given list of requirements into functional (labelled as F) and non-functional requirements (labelled as
NF). Ask me questions if needed to break the given task into smaller subtasks. All the outputs to the smaller subtasks
must be combined before you generate the final output." [11]

Pattern 2: "Persona"

"Act as a requirements engineering domain expert and classify the given list of requirements into functional (labelled
as F) and non-functional requirements (labelled as NF)." [11]

---

### Guideline 8: Reduce usage of Negation [3, 8]

**Description:**

Avoid the use of double-negatives when expressing ideas in prompts.

**Reasoning:**

LLM performance has been shown to be poor in the presence of negation [8]. That is, pretrained language models
have had trouble distinguishing between terms like "can" and "cannot" in text [8].

**Example:**

Express as "remember to do X" rather than "don't forget to do X".

---

### Guideline 9: Avoid yes/no without explanation [12]

**Description:**

Do not ask a LLM to give binary responses without explanation.

**Reasoning:**

Reasoning given by LLMs can often be fuzzy or based on hallucinations. If you ask for a decision without explanation,
you may receive a result based on broken logic, but you can no longer verify the (possibly deranged) reasoning [12].

**Example:**

"Classify these samples into category A or category B. For each categorization, explain your reasoning"

---

### Guideline 10: Separate Problem Space from Solution Space

**Description:**

First elicit goals/needs; only later discuss design/implementation.

**Reasoning:**

LLMs tend to jump to solutions; separating spaces prevents premature design decisions and keeps requirements focused on
needs.

**Example:**

“Phase 1: ask clarifying questions only. Do NOT propose architecture or tools yet.”

**Suggested by:**

ChatGPT

---

### Guideline 11: Ban Vague Words Unless Quantified

**Description:**

Forbid terms like “fast,” “robust,” “user-friendly,” “secure” unless measurable.

**Reasoning:**

Vague language cannot be verified, causing weak requirements and disputes later.

**Example:**

Bad: “System shall be fast.”
Good: “System SHALL respond within 2 seconds for 95% of requests.”

**Suggested by:**

ChatGPT, Claude

---

### Guideline 12: Enforce RFC-2119 Modal Verbs (SHALL/SHOULD/MAY) [20]

**Description:**

Require SHALL for mandatory requirements; SHOULD for recommended; MAY for optional—and flag anything that can’t be
stated clearly [20].

**Reasoning:**

Standard modality reduces ambiguity and helps prioritize and test requirements.

**Example:**

“If a requirement cannot be written as SHALL, rewrite it or mark it ambiguous.”

**Suggested by:**

ChatGPT

---

### Guideline 13: Try asking for concrete cases when things go wrong (Pre-Mortem Prompting)

**Description:**

Ask the LLM to assume the system failed, then work backward to identify missing requirements. This also works for threat
modeling in adversarial scenarios.

**Reasoning:**

Pre-mortems and misuse cases create realistic, safety/security-focused requirements tied to real failure modes.

**Example:**

“Assume a data breach occurred. What privacy/security requirement was missing?”

**Suggested by:**

Copilot, Gemini

---

### Guideline 14: Treat LLM output as a draft, not as a final product [10, 11, 12, 13]

**Description:**

Do not treat the output of your LLM as a finished product. Treat it like a draft given to you for review by a colleague.

**Reasoning:**

LLMs are powerful, but not perfect. Their outputs may contain senior engineer-level insights, but can also easily
contain amateur-level mistakes. Many LLM researchers for RE advocate for human oversight in their
studies of LLMs for requirements engineering, and object to LLMs as final authorities [10, 11, 12, 13].

Also, all sorts of accountability problems arise when the LLM is treated as a trusted authority, and things go wrong.

**Example:**

There is a famous case of a Lawyer in the Supreme Court of British Columbia attempting to cite two non-existent cases as
support for her argument. The cases were discovered by the opposition to be non-existent and hallucinated by
ChatGPT [21].

The Lawyer's conduct was determined to be "reprehensible and deserving of rebuke" [21].

---

## 2. References

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

[8] N. Kassner and H. Schütze. “Negated and Misprimed Probes for Pretrained Language Models: Birds Can Talk, But
Cannot Fly.” In Proceedings of the 58th Annual Meeting of the Association for Computational Linguistics, pages
7811–7818, Online. Association for Computational Linguistics, 2020.

[9] C. S. Xia and L. Zhang, “Conversational automated program repair,” arXiv preprint arXiv:2301.13246, 2023.

[10] Arora, C., Grundy, J., Abdelrazek, M. (2024). Advancing Requirements Engineering Through Generative AI: Assessing
the Role of LLMs. In: Nguyen-Duc, A., Abrahamsson, P., Khomh, F. (eds) Generative AI for Effective Software Development.
Springer, Cham. https://doi.org/10.1007/978-3-031-55642-5_6

[11] K. Ronanki, B. Cabrero-Daniel, J. Horkoff, and C. Berger, “Requirements Engineering using Generative AI: Prompts
and Prompting Patterns,” arXiv preprint arXiv:2311.03832, Nov. 2023. doi: 10.48550/arXiv.2311.03832.

[12] M. Borg, K. Wnuk, and A. Ferrari, “Requirements Satisfiability with In-Context Learning,” arXiv preprint arXiv:
2404.12576, Apr. 2024. doi: 10.48550/arXiv.2404.12576.

[13] J. S. Yeow, M. E. Rana, and N. A. Abdul Majid, “An Automated Model of Software Requirement Engineering Using
GPT-3.5,” in 2024 ASU International Conference in Emerging Technologies for Sustainability and Intelligent Systems (
ICETSIS), Jan. 2024, pp. 1746–1755. doi: 10.1109/ICETSIS61505.2024.10459458.

[14] F. Sosa, “Transforming Specifications into Requirements: Leveraging Copilot for Optimal Results,” LinkedIn, Apr.
23, 2025. [Online].
Available: https://www.linkedin.com/pulse/transforming-specifications-requirements-leveraging-copilot-sosa-7ze2e.

[15] S. U. Shah, “Revolutionizing Software Requirements Engineering with LLMs,” Medium, Jun. 23, 2024. [Online].
Available: https://medium.com/@samiullah6799/revolutionizing-software-requirements-engineering-with-llms-db90551a3965

[16] “A Developer’s Guide to Leveraging LLMs in the Software Development Lifecycle,” Apecton, May 2025. [Online].
Available: https://apecton.com/ai/a-developers-guide-to-leveraging-llms-in-the-software-development-lifecycle/

[17] D. Divekar, “How to use ChatGPT for Requirement Analysis?” LinkedIn, Apr. 20, 2024. [Online].
Available: https://www.linkedin.com/pulse/how-use-chatgpt-requirement-analysis-dnyaneshwar-divekar-qvzjf.

[18] B. Böckeler, A. K. P., S. Mukhopadhyay, R. Sivadass, and J. B., “Using AI for requirements analysis: A case study,”
Thoughtworks, Sept. 17, 2024. [Online].
Available: https://www.thoughtworks.com/en-us/insights/blog/generative-ai/using-ai-requirements-analysis-case-study.

[19] E. Gottesdiener, “Using ‘Given-When-Then’ to Discover and Validate Requirements,” EBG Consulting. Accessed: Jan.
24, 2026. [Online].
Available: https://ebgconsulting.com/blog/using-given-when-then-to-discover-and-validate-requirements-2/

[20] S. O. Bradner, “Key words for use in RFCs to Indicate Requirement Levels,” Internet Engineering Task Force, Request
for Comments RFC 2119, Mar. 1997. doi: 10.17487/RFC2119. Available: https://datatracker.ietf.org/doc/html/rfc2119

[21] Zhang v Chen. Accessed: Jan. 26, 2026. [Online]. Available: https://canlii.ca/t/k314g


---





