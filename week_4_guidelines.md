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
- Lost in the Middle: How Language Models Use Long
  Contexts — [arXiv](https://arxiv.org/abs/2307.03172) [22]
- LLMs Get Lost In Multi-Turn Conversation — [arXiv](https://arxiv.org/abs/2505.06120) [23]

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
- Key words for use in RFCs to Indicate Requirement
  Levels - [datatracker](https://datatracker.ietf.org/doc/html/rfc2119) [20]
- Zhang v Chen - [CanLII](https://canlii.ca/t/k314g) [21]

## 1. Guidelines

### Guideline 1: Design a structured context prompt [1, 6, 10, 11, 17]

**Description**

Create a compact, high-information “job brief” that tells the LLM its role in a requirements engineering task, the artifact expected, and the constraints to follow.

Focus on clearly specifying:

- the role of the model
- the task objective
- expected deliverables
- relevant constraints

**Reasoning**

Structured context prompts reduce ambiguity and guide the model toward task-relevant outputs [1, 6]. They improve task alignment and reduce misunderstanding of stakeholder intent.

**Example**
You are a requirements engineer evaluating a healthcare system design. Provide a structured analysis of the security requirement and its satisfaction.

---

### Guideline 2: Converse with the LLM to analyze the problem [2, 9, 14, 15, 16]

**Description:**

Before creating requirements, talk to the LLM back and forth to refine the problem domain. This includes:

- Analyzing the underlying business or user problem
- Summarizing and synthesizing existing documentation
- Identifying and fleshing out candidate requirements
- Detecting contradictions or inconsistencies
- Clarifying ambiguities, assumptions, and open questions

**Reasoning:**

The process of back-and-forth conversation helps the model uncover missing constraints, assumptions, and edge cases.
This process has been demonstrated to improve the effectiveness of LLMs for bug fixing [9], and is one of the main
techniques used to generate specifications in SpecGen [2]. In addition, this mirrors established requirements
elicitation practices, making it easier to evaluate (familiar structure).

**Example:**

Bad: _Write user stories for the login feature._

- No analysis of the problem

Good: _You are a senior requirements engineer. Before writing any user stories, analyze the following project
description:_

- _Goal: Enable registered users to log in and access personalized content_
- _Constraints: Web application, email/password authentication, must support 2FA in future_
- _Known risks: Security and session management_

Task:

- _Identify the core problem and main user goals_
- _Summarize existing documentation and assumptions_
- _List ambiguities, contradictions, and open questions_
- _Suggest a structured set of clarifying questions to resolve them_
  _Do not write user stories or acceptance criteria yet._

Ask individual questions in a back-and-forth manner to refine.

---

### Guideline 3: Assign a stakeholder or expert role/persona to the LLM [2, 3, 4, 10, 17]

**Description:**

Tell the model what it is (e.g. "senior requirements engineer", "technical interviewer for Google", "end-user") before
asking it to do something. You can also create separate chats with separate personas for differing viewpoints.

**Reasoning:**

The language used and professionalism of the LLM will vary based on the role it has to play [2, 4, 17]. Explicitly
defined roles will also give additional context about the problem domain [2].

**Example:**

Bad: _Review these user stories and suggest improvements._

Good: _You are a senior product manager with 10+ years of experience in enterprise software development and familiarity
with ISO/IEC/IEEE standards. Review the following user stories and suggest improvements._

---

### Guideline 4: Provide few-shot examples of good requirements or user stories [2, 3, 10, 16]

**Description:**

When attempting to describe desired behavior of a program or system, give 1-3 examples of desired output.

**Reasoning:**

Few-shot examples have been shown to reliably improve adherence to format and improve performance in LLMs [5]. These
examples also double as tests for your requirements, increasing verifiability. In addition, examples are one of the
strongest methods of enforcing structure in output, making it more likely to follow that structure and read output [16].

**Example:**

Bad: _Generate user stories for the system._

Good: _Generate user stories of exact format "As a [type of user], I want [an action] so that [a result]."
(i.e. "As a store owner, I want a way of hearing when customers enter my store, so that I know when to come to the
front.")_

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

_As an expert in software testing, review the following requirements and identify any gaps, along with their potential
impact, providing actionable pointers for improvement in tabular format._

Bad: _Explain the login requirement and generate acceptance criteria_

Good as an intermediary data: _As a registered user, I want to be able to log in to my account so that I can access
personalized content and features_

Good: _You are assisting with requirements engineering for a consumer-facing web application based on the following user
story: ""As a registered user, I want to be able to log in to my account so that I can access personalized content and
features". Generate clear, testable acceptance criteria using Given When Then format._

_Assumptions and constraints:_

- _Users authenticate using email and password_
- _The system must comply with basic security best practices (password hashing, failed login handling)_
- _Login is performed via a web browser_
- _Include both successful and unsuccessful login scenarios_
- _Do not invent features beyond authentication and session access_

> NOTE: look at [19] for information on Given-When-Then test case format

---

### Guideline 6: Capitalize role identifiers in transcripts and interviews [3, 7]

**Description**

When analyzing transcripts or multi-speaker interviews, capitalize role identifiers (e.g., **INTERVIEWER**, **CLIENT**).

**Important scope clarification**

This guideline applies only to transcript analysis or multi-speaker conversations.

It is not relevant for:

- classification tasks
- reasoning tasks
- structured requirement writing

**Reasoning**

Capitalization helps prevent speaker misattribution in transcripts [3, 7] but provides no benefit outside transcript contexts.

**Example:**

Preprocess input transcript as follows before giving it as context to an LLM:

_Before_

- Interviewer: Why do users avoid using the system?
- Client: They find it confusing.

_After_

- INTERVIEWER: Why do users avoid using the system?
- CLIENT: They find it confusing.

---

### Guideline 7: Base your prompting pattern on the RE task being performed [11, 12]

**Description:**

Select your LLM prompting pattern based on the task.

**Reasoning:**

Different methods of prompting LLMs ('prompt patterns') have been shown to be effective in different parts of the RE
process [11]. For instance, making the LLM ask the user questions as needed created better performance on binary
classification compared to making the LLM act as an RE expert [11].

**Example:**

Pattern 1: "Cognitive Verifier" (good for classification)

"Classify the given list of requirements into functional (labelled as F) and non-functional requirements (labelled as
NF). Ask me questions if needed to break the given task into smaller subtasks. All the outputs to the smaller subtasks
must be combined before you generate the final output." [11]

Pattern 2: "Persona"

"Act as a requirements engineering domain expert and classify the given list of requirements into functional (labelled
as F) and non-functional requirements (labelled as NF)." [11]

---

### Guideline 8: Reduce usage of Negation when providing requirements [3, 8]

**Description:**

Avoid the use of negation or double-negatives when expressing ideas in prompts.

**Reasoning:**

LLM performance has been shown to be poor in the presence of negation [8]. That is, pretrained language models
have had trouble distinguishing between terms like "can" and "cannot" in text [8].

**Example:**

Bad: _Don't forget to include an example of what the output format should look like_

Good: _Remember to include an example of what the output format should look like_

---

### Guideline 9: Avoid classification classification or yes/no answers without explanation [12]

**Description:**

Do not ask a LLM to give binary responses without explanation.

**Reasoning:**

Reasoning given by LLMs can often be fuzzy or based on hallucinations. If you ask for a decision without explanation,
you may receive a result based on broken logic, but you can no longer verify the (possibly deranged) reasoning [12].

**Example:**

Bad: _Classify these samples into category A or category B._

Good: _Classify these samples into category A or category B. For each categorization, explain your reasoning_

---

### Guideline 10: Separate Problem Space from Solution Space

**Description:**

First elicit and validate stakeholder goals, needs, success metrics, constraints, and assumptions. Delay
design/implementation discussion until the problem space is well understood and agreed.

**Reasoning:**

LLMs tend to jump to solutions; separating spaces prevents premature design decisions and keeps requirements focused on
needs.
This prevents premature commitment to architectures or features that don't meet real needs, produces verifiable
acceptance criteria and traceability from goals → requirements → design, and reduces rework, scope creep, and hidden
assumptions that lead to failed deliveries.

**Example:**

Bad: _For this task, give me a set of requirements that must be completed._

Good: _For this task, give me a set of requirements that must be completed. Do NOT propose implementation details such
as architecture or tools yet._

**Suggested by:**

ChatGPT

---

### Guideline 11: Ban Vague Words Unless Quantified

**Description**

Avoid vague terms such as fast, robust, secure, or user-friendly unless they are supported by realistic and meaningful measurements.

Measurements should be:

- achievable
- stakeholder-understandable
- relevant to the domain

**Important scope clarification**

This guideline applies only when writing measurable requirements.

It is not applicable to:

- requirement classification
- satisfiability reasoning
- question generation tasks

  **Reasoning**

Vague language reduces testability and may cause disputes during verification. Over-quantification can produce unrealistic or artificial requirements[10, 11]. The goal is clarity and verifiability, not unnecessary precision.

**Example**

Bad: System shall be fast.

Good: System SHALL respond within 2 seconds for 95% of requests.

---

### Guideline 12: Enforce RFC-2119 Modal Verbs (SHALL/SHOULD/MAY) [20]

**Description**

Use RFC-2119 modal verbs (SHALL / SHOULD / MAY) when writing requirements.

**Reasoning**
RFC-2119 modality reduces ambiguity and clarifies priority levels. It supports consistent interpretation across stakeholders and improves requirement precision.

**Example**
The system SHALL encrypt all patient data.

---

### Guideline 13: Assign priorities to user stories and requirements using the MoSCoW method or following the RFC-2119 Modal Verbs (SHALL/SHOULD/MAY) standard before giving them to the LLM.

**Description:**

To prioritize key requirements above desirable features label each user story or requirement with how necessary it is so
the LLMfocuses on creating the MVP before adding extra features.
To proritize key requirements above desirable features label each user story or requirement with how necessary it is so
the LLM focuses on creating the MVP before adding extra features.

**Reasoning:**

The Requirements Engineering process tends to be a non-linear, waterfall-like process. Client needs, available
resources, and domain specific factors change, get misinterpreted, and are clarified. Thus, it is important to
synchronize the software development teams' perception of the Minimum Viable Product with the client.

**Example:**

You are an experienced Software Requirement Engineer determining the Minimum Viable Product (MVP) for {Project
Name/Description}. To ensure full alignment between the development team and stakeholders and to avoid an expectation
gap at delivery, I need to categorize our User Stories using the MoSCoW method.
Please analyze the following requirements and generate a structured list. For every item, assign a priority label (M, S,
C, or W) and provide a brief 'Reasoning' to justify its placement based on {Time/Budget/Technical} constraints.
Categorization Rules:

- M (Must Have): Non-negotiable core functionality. Without these, the product is not viable.
- S (Should Have): Important but not vital for the initial launch.
- C (Could Have): Desirable 'bonus' features that will be included only if resources permit.
- W (Won't Have): Explicitly excluded from this release to protect the project scope.
  Input Requirements / User Stories:
  {user stories}

---

### Guideline 14: Treat LLM output as a draft, not as a final product [10, 11, 12, 13]

**Description:**

Treat any LLM-generated requirements text as a starting draft that must be reviewed, validated, and approved by humans
before becoming part of the requirements baseline.

**Reasoning:**

LLMs can surface useful wording and structure but may introduce ambiguity, incorrect domain assumptions, missing
constraints, or implementation bias.
Accepting LLM output unreviewed creates traceability, accountability, and compliance risks and can hide unstated
assumptions that break downstream design, testing, and delivery.

**Example:**

There is a famous case of a Lawyer in the Supreme Court of British Columbia attempting to cite two non-existent cases as
support for her argument. The cases were discovered by the opposition to be non-existent and hallucinated by
ChatGPT [21].

The Lawyer's conduct was determined to be "reprehensible and deserving of rebuke" [21].

---

### Guideline 15: DO NOT perform all steps of the RE process in a single context window

**Description:**

Do not do requirement brainstorming, stakeholder analysis, refinement and more in a single conversation with an LLM.
Instead, summarize the output artifacts of each step and make those the inputs for a fresh conversation.

**Rationale:**

It may be tempting to think that, since you just had a conversation with your LLM about all the context related to your
project, the LLM is better suited to subsequent problems. Unfortunately, LLMs have "attention span" problems.

More specifically, when you stretch an LLM's context across several prompts in the same chat window, it pays less
attention to any specific instruction, and is very likely to forget or ignore instructions from previous
prompts [22, 23].

In contrast, starting a fresh prompt allows the LLM to focus all of its considerable computational resources on the
single task you want done.

**Example:**

After applying Guideline 2 to analyze user goals and high-level requirements, you have a summary of user goals and
high-level requirements brainstormed using ChatGPT.

In a _new_ chat window:

"Here is a summary of user goals and high level requirements for a Web Application I am building, <summary>. Based on
these, please generate a comprehensive set of user stories using the following format:

As a [type of user], I want [some goal] so that [some reason]."

---

### Guideline 16: Use explicit task-tag structured prompting

**Description**

For structured evaluation or grading tasks, isolate the core objective inside `<task> … </task>` tags and enforce an explicit output template.

**Reasoning**

Task-tag prompting improves:

- format consistency
- reproducibility
- comparability across runs

Our experiments in Problems C1–C3 showed that task-tag isolation reduces output drift (e.g., progress logs, narration) and makes results easier to grade and compare. However, it mainly improves output control and evaluation stability, not necessarily reasoning quality.

This guideline is especially recommended for:

- grading exercises
- structured comparisons
- reproducible evaluation workflows

**Example**
<task>
Classify R1–R6 as FR or NFR and justify each in one sentence.
Then explain why AI-assisted classification needs human review.
</task>

---

### Problem A: Requirement Analysis

You may find the following guidelines more useful for each problem of exercise A. Not all of them should be used
simultaneously but due to the open-ended nature of the problem there are multiple correct approaches and solutions.

#### Problem 1:

- Guideline 6: Treat LLM output as a draft, not as a final product
- Guideline 7: Capitalize role identifiers
- Guideline 11: Separate Problem Space from Solution Space
- Guideline 13: Enforce RFC-2119 Modal Verbs (SHALL/SHOULD/MAY)

#### Problem 2:

- Guideline 1: Design a structured context prompt
- Guideline 2: Converse with the LLM to analyze the problem
- Guideline 4: Provide few-shot examples
- Guideline 11: Separate Problem Space from Solution Space
- Guideline 13: Enforce RFC-2119 Modal Verbs (SHALL/SHOULD/MAY)

#### Problem 3:

- Guideline 1: Design a structured context prompt
- Guideline 2: Converse with the LLM to analyze the problem
- Guideline 3: Assign a role/persona to the LLM
- Guideline 5: Maximise prompt information density
- Guideline 6: Treat LLM output as a draft, not as a final product
- Guideline 11: Separate Problem Space from Solution Space

#### Problem 4:

- Guideline 1: Design a structured context prompt
- Guideline 2: Converse with the LLM to analyze the problem
- Guideline 3: Assign a role/persona to the LLM
- Guideline 5: Maximise prompt information density
- Guideline 6: Treat LLM output as a draft, not as a final product
- Guideline 14: Try asking for concrete cases when things go wrong (Pre-Mortem Prompting)

### Problem B: Elicitation of Requirements from Problem Domain

You may find varying success with different combinations of guidelines for this problem. Given the open-endedness of the
problem and the desire for clear and unambiguous requirements, I would recommend:

First:

- Guideline 2: Converse with the LLM to analyze the problem

Then:

- Guideline 3: Assign a role/persona to the LLM
- Guideline 1: Design a structured context prompt
- Guideline 10: Separate Problem Space from Solution Space
- Guideline 11: Ban Vague Words Unless Quantified
- Guideline 12: Enforce RFC-2119 Modal Verbs (SHALL/SHOULD/MAY)
- Guideline 14: Treat LLM output as a draft, not as a final product

### Problem C:

## Problem C: Requirement Classification

- Guideline 1: Design a structured context prompt
- Guideline 7: Base prompting pattern on the RE task being performed
- Guideline 9: Avoid classification or yes/no answers without explanation
- Guideline 16: Use explicit task-tag structured prompting

## Problem 2: Requirement Satisfiability Evaluation

- Guideline 1: Design a structured context prompt
- Guideline 9: Avoid classification or yes/no answers without explanation
- Guideline 16: Use explicit task-tag structured prompting

## Problem 3: Requirements Elicitation Question Generation

- Guideline 1: Design a structured context prompt
- Guideline 2: Converse with the LLM to analyze the problem
- Guideline 16: Use explicit task-tag structured prompting
- Guideline 14: Treat LLM output as a draft, not as a final product
- Guideline 15: DO NOT perform all steps of the RE process in a single context window

---

## 3. References

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
and Prompting Patterns,” Nov. 07, 2023, arXiv: arXiv:2311.03832. doi: 10.48550/arXiv.2311.03832.

[12] S. Santos, T. Breaux, T. Norton, S. Haghighi, and S. Ghanavati, “Requirements Satisfiability with In-Context
Learning,” Apr. 19, 2024, arXiv: arXiv:2404.12576. doi: 10.48550/arXiv.2404.12576.

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

[22] N. F. Liu et al., “Lost in the Middle: How Language Models Use Long Contexts,” Nov. 20, 2023, arXiv: arXiv:
2307.03172. doi: 10.48550/arXiv.2307.03172.

[23]] P. Laban, H. Hayashi, Y. Zhou, and J. Neville, “LLMs Get Lost In Multi-Turn Conversation,” May 09, 2025, arXiv:
arXiv:2505.06120. doi: 10.48550/arXiv.2505.06120.

---
