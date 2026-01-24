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

**Additional (academic) sources explored beyond assigned readings**

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

### Guideline 1: Design a structured context prompt [1, 6, 10, 11]

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

### Guideline 2: Converse with the LLM [2, 9]

**Description:**  
Before creating requirements, talk to the LLM back and forth to refine the problem domain.

**Reasoning:**  
The process of back-and-forth conversation helps the model uncover missing constraints, assumptions, and edge cases.
This process has been demonstrated to improve the effectiveness of LLMs for bug fixing [9], and is one of the main
techniques used to generate specifications in SpecGen [2].

**Example:**

1. "Pretend you're a client. Talk to me about you would desire from a system that does X."
2. Converse for a while, save transcript
3. In a new session: "You are a senior requirements engineer creating a set of requirements based on this conversation"

---

### Guideline 3: Assign a role/persona to the LLM [2, 3, 4, 10]

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

### Guideline 4: Provide few-shot examples [2, 3, 10]

**Description:**  
When attempting to describe desired behavior of a program or system, give 1-3 examples of desired output.

**Reasoning:**  
Few-shot examples have been shown to reliably improve adherence to format and improve performance in LLMs [5]. These
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

### Guideline 7: Treat the output as a draft, not as a final product [10, 11, 12, 13]

**Description:**
Do not treat the output of your LLM as a finished product. Treat it like a draft given to you for review by a colleague.

**Reasoning:**  
LLMs are powerful, but not perfect. Their outputs may contain senior engineer-level insights, but can also easily
contain amateur-level mistakes. Many LLM researchers for RE advocate for human oversight in their
studies of LLMs for requirements engineering, and object to LLMs as final authorities [10, 11, 12, 13].

**Example:**  
N/A

---

### Guideline 8: Base your prompting pattern on the RE task being performed [11, 12]

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

### Guideline 9: Use multiple runs and majority vote for robustness [12]

**Description:**  
For important decisions, try running the LLM on the same prompt several times and taking the majority vote.

**Reasoning:**  
LLMs outputs are stochastic (assuming temperature != 0). This means that they can go either way when asked to decide yes
or no on something. Taking several runs gives both an idea of the uncertainty and a more robust answer [12].

**Example:**  
"Classify this sample as category A or category B. Explain your reasoning."
Repeat 10 times
Count the number of A's and B's
Think

---

### Guideline 10: Avoid yes/no without explanation [12]

**Description:**  
Do not ask a LLM to give binary responses without explanation.

**Reasoning:**  
Reasoning given by LLMs can often be fuzzy or based on hallucinations. If you ask for a decision without explanation,
you may receive a result based on broken logic, but you can no longer verify the deranged reasoning [12].

**Example:**  
"Classify these samples into category A or category B. For each categorization, explain your reasoning"

---

## 2. Guidelines from any related research/grey literature like practitioner or developer tool blogs

### Guideline 1: Analyze the problem before writing the requirements documentation [14, 15, 16]

**Description:**  
Before drafting any requirements, use the LLM to collaboratively explore and understand the problem space. This
includes:

* Analyzing the underlying business or user problem
* Summarizing and synthesizing existing documentation
* Identifying and fleshing out candidate requirements
* Detecting contradictions or inconsistencies
* Clarifying ambiguities, assumptions, and open questions

**Reasoning:**  
This guideline mirrors established requirements elicitation practices, where understanding the problem precedes formal
specification. Starting with a high-level exploration ensures that requirements evolve cohesively from a shared
understanding of goals, constraints, and context. Using an LLM at this stage helps avoid fragmented or contradictory
requirements and reduces rework caused by premature specification.

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

---

### Guideline 2: Roleplaying [17]

**Description:**  
Identify a job title which is associated with knowledge in the field and assign it to the LLM to "roleplay" as. This
guides the model to reason, prioritize, and communicate from a specific expert viewpoint rather than a generic assistant
perspective. The role can be switched between chats to get differing perspectives for a broader and more thorough
process.

**Reasoning:**  
Role assignment anchors the LLM’s responses in domain-specific reasoning patterns and professional norms. By instructing
the model to roleplay as an expert, the output reflects appropriate terminology, depth, and decision-making criteria.
Improving alignment with industry standards, reducing superficial responses, and increases the usefulness of generated
requirements artifacts.

**Example:**  
Bad: *Review these user stories and suggest improvements.*

Good: *You are a senior product manager with 10+ years of experience in enterprise software development and familiarity
with ISO/IEC/IEEE standards. Review the following user stories and suggest improvements.*

*Focus on:*

* *Clarity and comprehensive unambiguous language*
* *Testability and verifiability*
* *Alignment with requirements engineering best practices*
* *Avoiding scope creep or solution bias*
  *Do not introduce new features beyond what is implied.*

---

### Guideline 3: Structured Outputs [16]

**Description:**  
Explicitly define the structure, format, and constraints of the expected output. This may include templates, schemas,
fixed phrasing, ordering rules, or formatting standards that the AI must follow. The goal is to ensure the generated
content is consistent, predictable, and directly usable in requirements artifacts.

**Reasoning:**  
Structured outputs reduce variability in LLM responses and improve consistency across generated requirements. By
enforcing a predefined format, the model produces outputs that are easier to review, validate, compare, and trace. This
is especially valuable in requirements engineering, where uniformity eases communication, tooling integration, and
downstream activities such as testing and design.

**Example:**  
Bad: *Generate user stories for the system.*

Good: *Generate user stories of exact format “As a [type of user], I want [an action] so that [a result].”*

---

### Guideline 4: Maximise prompt information density [17]

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

## 3. Guidelines from LLMs

### Guideline 1: Start with Role + Standards Frame

**Description:**

Tell the LLM what expert role to take and what standards to follow (e.g., ISO 29148, IEEE 29148, ISO/IEC 25010).

**Reasoning:**

Role + standards anchors vocabulary, rigor, and requirement quality expectations so outputs are more consistent and professional.

**Example:**

“Act as a senior requirements engineer. Follow ISO/IEC/IEEE 29148. Use testable SHALL statements.”

**Suggested by:**

Savira (GPT), Gavin (Gemini), Savira (Gemini)

---

### Guideline 2: Provide Project Ecosystem Context First

**Description:**

Before asking for requirements, provide scope, stakeholders, goals, constraints, and any risks.

**Reasoning:**

Missing context causes generic requirements and wrong assumptions. Context helps the model tailor requirements to the real situation.

**Example:**

“Goal: reduce customer support calls 40%. Users: customers + agents. Constraints: must integrate with CRM; PII data; budget limit.”

**Suggested by:**

Artemiy (Copilot), Savira (Claude), Savira (DeepSeek)

---

### Guideline 3: Separate Problem Space from Solution Space

**Description:**

First elicit goals/needs; only later discuss design/implementation.

**Reasoning:**

LLMs tend to jump to solutions; separating spaces prevents premature design decisions and keeps requirements focused on needs.

**Example:**

“Phase 1: ask clarifying questions only. Do NOT propose architecture or tools yet.”

**Suggested by:**

Savira (GPT)

---

### Guideline 4: Use a Structured Prompt Format (Role–Goal–Context–Output–Constraints–Examples)

**Description:**

Write prompts in a consistent structure: Role, Goal, Context, Output format, Constraints, Examples.

**Reasoning:**

Structure reduces ambiguity, improves repeatability, and makes outputs easier to evaluate and compare.

**Example:**

    • Role: “Product Manager”
    • Goal: “Elicit NFRs for privacy”
    • Output: “Table with ID, SHALL, Rationale, Acceptance Criteria”

**Suggested by:**

Artemiy (Copilot)

---

### Guideline 5: Use Explicit Requirement Templates

**Description:**

Require outputs to follow a fixed template: ID, Type, SHALL statement, Rationale, Acceptance Criteria, Priority (and optional Verification Method).

**Reasoning:**

Templates force completeness and produce requirements that are easier to test, trace, and review.

**Example (template row):**

ID: NFR-01 | Type: Security | SHALL: “The system SHALL encrypt PII at rest using AES-256.” | AC: “Verify encryption enabled in DB config.”

**Suggested by:**

Savira (GPT), Gavin (Gemini), Savira (Gemini)

---

### Guideline 6: Ban Vague Words Unless Quantified

**Description:**

Forbid terms like “fast,” “robust,” “user-friendly,” “secure” unless measurable.

**Reasoning:**

Vague language cannot be verified, causing weak requirements and disputes later.

**Example:**

Bad: “System shall be fast.”
Good: “System SHALL respond within 2 seconds for 95% of requests.”

**Suggested by:**

Savira (GPT), Savira (Claude)

---

### Guideline 7: Enforce RFC-2119 Modal Verbs (SHALL/SHOULD/MAY)

**Description:**

Require SHALL for mandatory requirements; SHOULD for recommended; MAY for optional—and flag anything that can’t be stated clearly.

**Reasoning:**

Standard modality reduces ambiguity and helps prioritize and test requirements.

**Example:**

“If a requirement cannot be written as SHALL, rewrite it or mark it ambiguous.”

**Suggested by:**

Savira (GPT)

---

### Guideline 8: Decompose Complex Requirements into Atomic Ones

**Description:**

Split “and/or” and multi-part requirements into single, testable statements.

**Reasoning:**

Atomic requirements improve traceability, testing, and reduce hidden scope.

**Example:**

Bad: “The system shall store and share user data securely.”
Good: (1) store data with encryption; (2) share data only with user consent.

**Suggested by:**

Savira (Claude), Gavin (Gemini), Savira (Gemini)

---

### Guideline 9: Work in RE-Aligned Phases (Elicit → Analyze → Validate → Manage Change)

**Description:**

Ask the LLM to follow phases instead of producing everything at once.

**Reasoning:**

Phased workflows reduce hallucination, improve focus, and mirror real RE processes.

**Example:**

“Step 1: Extract atomic requirements. Step 2: classify FR/NFR. Step 3: add verification method.”

**Suggested by:**

Savira (DeepSeek), Gavin (Gemini), Savira (Gemini)

---

### Guideline 10: Use Hierarchical Decomposition Instead of “Write Full SRS”

**Description:**

Break big tasks into smaller subtasks: overview → extraction → classification → refinement.

**Reasoning:**

Asking for a full SRS often produces generic fluff; decomposition improves quality and reduces errors.

**Example:**

“First list stakeholders and goals. Then extract 15 atomic requirements. Then label FR/NFR/constraints.”

**Suggested by:**

Gavin (Gemini), Savira (Gemini)

---

### Guideline 11: Use Recursive Refinement (Generate → Critique → Refine)

**Description:**

Make the model critique its own output, then rewrite.

**Reasoning:**

First drafts are rarely good; critique/refine improves clarity, resolves conflicts, and increases testability.

**Example:**

Prompt 1: “Generate 10 requirements.”
Prompt 2: “Find 3 ambiguities + 2 conflicts.”
Prompt 3: “Rewrite requirements + add verification method.”

**Suggested by:**

Gavin (Gemini), Savira (Gemini)

---

### Guideline 12: Ask for Assumptions Explicitly

**Description:**

Require the LLM to list assumptions it made and identify missing info.

**Reasoning:**

Hidden assumptions cause requirement defects; surfacing them early improves correctness.

**Example:**

“List assumptions about users, data volume, and compliance rules.”

**Suggested by:**

Artemiy (Copilot), Savira (DeepSeek)

---

### Guideline 13: Generate Concrete Examples + Negative Scenarios

**Description:**

Ask for realistic examples and edge cases (failure/abuse cases).

**Reasoning:**

Examples ground the requirement and expose gaps; negative scenarios reveal missing constraints and NFRs.

**Example:**

“Give 2 misuse cases (e.g., brute-force login attempts) and the missing security requirements.”

**Suggested by:**

Artemiy (Copilot), Gavin (Gemini), Savira (Gemini)

---

### Guideline 14: Use Pre-Mortem Prompting for Risk-Driven Requirements

**Description:**

Ask the LLM to assume the system failed, then work backward to identify missing requirements.

**Reasoning:**

Pre-mortems create realistic, safety/security-focused requirements tied to real failure modes.

**Example:**

“Assume a data breach occurred. What privacy/security requirement was missing?”

**Suggested by:**

Gavin (Gemini), Savira (Gemini)

---

### Guideline 15: Elicit Non-Functional Requirements Separately

**Description:**

Prompt explicitly for NFR categories (performance, security, privacy, usability, reliability, scalability).

**Reasoning:**

NFRs are commonly missed unless asked directly; separating them ensures coverage.

**Example:**

“List security NFRs for handling PII. Output as SHALL statements with acceptance criteria.”

**Suggested by:**

Savira (Claude)

---

### Guideline 16: Require Testability Checks + Verification Method

**Description:**

For each requirement, require a testability judgment and a verification method (Test/Demo/Analysis/Inspection).

**Reasoning:**

Forces requirements to be verifiable and reduces vague statements.

**Example:**

“Add column: Verification Method = Test; AC = ‘95% requests < 2s’ measured in load test.”

**Suggested by:**

Savira (GPT), Gavin (Gemini), Artemiy (Copilot)

---

### Guideline 17: Produce Traceability Links (Requirement ↔️ Tests ↔️ Stakeholders)

**Description:**

Ask the LLM to link each requirement to stakeholders, rationale, and test cases.

**Reasoning:**

Traceability improves change impact analysis and helps ensure each requirement has a purpose and verification.

**Example:**

REQ-05 → Stakeholder: Patient → Test: TC-05 “Appointment booking happy path” → Rationale: reduce phone calls.

**Suggested by:**

Artemiy (Copilot)

---

### Guideline 18: Keep Outputs Small and Iterate

**Description:**

Ask for a small batch (5–10 requirements/questions), review, then expand.

**Reasoning:**

Iteration reduces errors, improves alignment, and avoids large hallucinated requirement lists.

**Example:**

“Start with 5 key requirements. Ask 5 clarifying questions. Then produce the next 10.”

**Suggested by:**

Artemiy (Copilot)

---

### Guideline 19: Use “Ask Clarifying Questions First” Mode

**Description:**

Instruct the model to ask clarifying questions before generating requirements.

**Reasoning:**

Better input quality leads to better output; clarifying questions reduce ambiguity early.

**Example:**

“Before drafting, ask 5 questions about stakeholders, latency, data sensitivity, and integrations.”

**Suggested by:**

Gavin (Gemini), Savira (GPT)

---

### Guideline 20: Keep Humans in the Loop (LLM as Facilitator, Not Final Authority)

**Description:**

Use the LLM to assist (brainstorm, critique, structure), but keep final decisions with human stakeholders/engineers.

**Reasoning:**

LLMs lack true domain accountability and can hallucinate; human validation is required for correctness and ethics.

**Example:**

Human drafts requirements → LLM flags ambiguity → human revises → stakeholders approve.

**Suggested by:**

Savira (DeepSeek), Artemiy (Copilot), Savira (GPT/Claude)

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

---
