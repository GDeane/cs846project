# Week X Raw Guidelines: [Topic Title]

**Authors:** [Student Name 1, Student Name 2, Student Name 3]  
**Readings:**   
- [Additional sources explored beyond assigned readings]


## 2. Guidelines from from any related research/grey literature like practitioner or developer tool blogs

> **Note:** Guidelines should be actionable, specific, and usable during real coding tasks.

### Guideline 1: Analyze the problem before writing the requiremets documentation [1, 2, 3]
**Description:**  
Before drafting any requirements, use the LLM to collaboratively explore and understand the problem space. This includes:
* Analyzing the underlying business or user problem
* Summarizing and synthesizing existing documentation
* Identifying and fleshing out candidate requirements
* Detecting contradictions or inconsistencies
* Clarifying ambiguities, assumptions, and open questions

**Reasoning:**  
This guideline mirrors established requirements elicitation practices, where understanding the problem precedes formal specification. Starting with a high-level exploration ensures that requirements evolve cohesively from a shared understanding of goals, constraints, and context. Using an LLM at this stage helps avoid fragmented or contradictory requirements and reduces rework caused by premature specification.

**Example:**  
Bad: *Write user stories for the login feature.*
* No analysis of the problem

Good: *You are a senior requirements engineer. Before writing any user stories, analyze the following project description:*
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

### Guideline 2: Roleplaying [4]

**Description:**  
Identify a job title which is associated with knowledge in the field and assign it to the LLM to "roleplay" as. This guides the model to reason, prioritize, and communicate from a specific expert viewpoint rather than a generic assistant perspective. The role can be switched between chats to get differing perspectives for a broader and more thorough process.

**Reasoning:**  
Role assignment anchors the LLM’s responses in domain-specific reasoning patterns and professional norms. By instructing the model to roleplay as an expert, the output reflects appropriate terminology, depth, and decision-making criteria. Improving alignment with industry standards, reducing superficial responses, and increases the usefulness of generated requirements artifacts.

**Example:**  
Bad: *Review these user stories and suggest improvements.*

Good: *You are a senior product manager with 10+ years of experience in enterprise software development and familiarity with ISO/IEC/IEEE standards. Review the following user stories and suggest improvements.*

*Focus on:*
* *Clarity and comprehensive unambiguous language*
* *Testability and verifiability*
* *Alignment with requirements engineering best practices*
* *Avoiding scope creep or solution bias*
*Do not introduce new features beyond what is implied.*

---

### Guideline 3: Structured Outputs [3]

**Description:**  
Explicitly define the structure, format, and constraints of the expected output. This may include templates, schemas, fixed phrasing, ordering rules, or formatting standards that the AI must follow. The goal is to ensure the generated content is consistent, predictable, and directly usable in requirements artifacts.

**Reasoning:**  
Structured outputs reduce variability in LLM responses and improve consistency across generated requirements. By enforcing a predefined format, the model produces outputs that are easier to review, validate, compare, and trace. This is especially valuable in requirements engineering, where uniformity eases communication, tooling integration, and downstream activities such as testing and design.

**Example:**  
Bad: *Generate user stories for the system.*

Good: *Generate user stories of exact format “As a [type of user], I want [an action] so that [a result].”*

---

### Guideline 4: Maximise prompt information density [4]

**Description:**  
Provide sufficient and relevant context to the LLM to fully constrain the problem space. The prompt should explicitly state assumptions, scope, constraints, and expected output format, while avoiding unnecessary or unrelated information. This minimizes ambiguity and prevents the model from making implicit assumptions.

**Reasoning:**  
High information density prompts guide the LLM toward producing precise, domain-appropriate outputs. By clearly specifying context and constraints, the model avoids defaulting to generic or boilerplate responses and instead generates results that are aligned with stakeholder intent, system boundaries, and verification needs. This leads to higher quality, consistent, and more testable requirements artifacts.

**Example:**  
*As an expert in software testing, review the following requirements and identify any gaps, along with their potential impact, providing actionable pointers for improvement in tabular format.*

Bad: *Explain the login requirement and generate acceptance criteria*

Good as an intermediary data: *As a registered user, I want to be able to log in to my account so that I can access personalized content and features*

Good: *You are assisting with requirements engineering for a consumer-facing web application based on the following user story: ""As a registered user, I want to be able to log in to my account so that I can access personalized content and features". Generate clear, testable acceptance criteria using Given When Then format.*

*Assumptions and constraints:*
* *Users authenticate using email and password*
* *The system must comply with basic security best practices (password hashing, failed login handling)*
* *Login is performed via a web browser*
* *Include both successful and unsuccessful login scenarios*
* *Do not invent features beyond authentication and session access*

NOTE: look at [6] for information on Given-When-Then test case format
---

## 4. References

[1] F. Sosa, “Transforming Specifications into Requirements: Leveraging Copilot for Optimal Results,” LinkedIn, Apr. 23, 2025. [Online]. Available: https://www.linkedin.com/pulse/transforming-specifications-requirements-leveraging-copilot-sosa-7ze2e.

[2] S. U. Shah, “Revolutionizing Software Requirements Engineering with LLMs,” Medium, Jun. 23, 2024. [Online]. Available: https://medium.com/@samiullah6799/revolutionizing-software-requirements-engineering-with-llms-db90551a3965

[3] “A Developer’s Guide to Leveraging LLMs in the Software Development Lifecycle,” Apecton, May 2025. [Online]. Available: https://apecton.com/ai/a-developers-guide-to-leveraging-llms-in-the-software-development-lifecycle/

[4] D. Divekar, “How to use ChatGPT for Requirement Analysis?” LinkedIn, Apr. 20, 2024. [Online]. Available: https://www.linkedin.com/pulse/how-use-chatgpt-requirement-analysis-dnyaneshwar-divekar-qvzjf. 

[5] B. Böckeler, A. K. P., S. Mukhopadhyay, R. Sivadass, and J. B., “Using AI for requirements analysis: A case study,” Thoughtworks, Sept. 17, 2024. [Online]. Available: https://www.thoughtworks.com/en-us/insights/blog/generative-ai/using-ai-requirements-analysis-case-study.

[6] https://ebgconsulting.com/blog/using-given-when-then-to-discover-and-validate-requirements-2/


---

