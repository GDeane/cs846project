## 1. Evaluation Criteria

The following criteria apply to this topic:
- Correct identification of Functional Requirements (FR) versus Non-Functional Requirements (NFR)
- Clear and logical reasoning
- Understanding of how prompt quality affects AI-assisted analysis
- Recognition of the limitations of AI and the need for human oversight.

## 2. Evaluation Criteria

The following criteria apply to this topic:
- Correct reasoning about requirements satisfiability
- Clear justification based on the provided design
- Ability to propose a practical design improvement
- Awareness of the role of human judgment in evaluating system designs

## 3. Evaluation Criteria

The following criteria apply to requirements elicitation problems in this topic:
- Ability to design relevant and well-scoped elicitation questions
- Clear distinction between survey and interview questions
- Awareness of question quality attributes (clarity, specificity, relevance)
- Ability to critically review and improve AI-assisted outputs
- Recognition of the need for human judgment in requirements elicitation

---

## 2. Evalation specifically for Example Problems

### Problem C_1: Functional vs Non-Functional Requirement Classification with AI Awareness

**Evaluation Description:**  
This problem is evaluated across three tasks.

Task 1 – Manual Requirement Classification

Good Solution:
- Correctly classifies:
- FR: appointment booking, reminders
- NFR: security (encryption), performance (2 seconds), compliance, usability
- Demonstrates understanding of the difference between:
- what the system does (FR) and
- how well or under what constraints it operates (NFR)

Bad Solution:
- Random or inconsistent classification
- Misclassifies security, performance, usability, or compliance requirements as FR
- Shows no clear reasoning or conceptual understanding

Task 2 – Prompt Design Reflection

Good Solution:
- Identifies Prompt B as better designed
- Provides a valid justification, such as:
- clearer instructions
- explicit output expectations
- requirement for justification
- reduced ambiguity for the AI

Bad Solution:
- Treats both prompts as equivalent
- Selects Prompt A without justification
- Provides vague or irrelevant reasoning

Task 3 – Human Oversight Reflection

Good Solution:
- Clearly explains at least one valid reason why human review is required, such as:
- AI may misinterpret requirements
- AI lacks full domain context
- AI can produce inconsistent or incorrect classifications

Bad Solution:
- Assumes AI output is always correct
- States that human review is unnecessary
- Provides overly brief or unsupported responses

**Code:**  
Not applicable (conceptual Requirements Engineering problem).
but
Student code should implement:
- classify_requirement(text) -> "FR" or "NFR"
- Good Code:
- Case-insensitive matching (uses .lower()).
- Returns only "FR" or "NFR".
- Produces reasonable outputs for the list.

- Bad Code:
- Hard-codes answers by index/order.
- Returns other labels (e.g., “functional”).
- Case-sensitive logic that fails on capitalization.

### Problem C_2: Requirements Satisfiability Reasoning

**Evaluation Description:**  
This problem is evaluated across three tasks.

Task 1 – Satisfiability Decision

Good Solution:
- Correctly answers No, recognizing that username/password authentication alone does not fully ensure that only authorized users can access sensitive records.

Bad Solution:
- Answers Yes without qualification
- Assumes basic authentication is sufficient without considering security risks

Task 2 – Reasoning

Good Solution:
- Clearly explains why the design is insufficient (e.g., weak authentication, lack of additional verification, higher risk of unauthorized access).
- Reasoning is directly tied to the stated requirement.

Bad Solution:
- Provides vague or generic security statements
- Does not connect the explanation to the requirement or design details

Task 3 – Design Improvement

Good Solution:
- Proposes a reasonable improvement, such as:
- multi-factor authentication
- role-based access control
- stronger authentication mechanisms
- Explains how the change improves satisfiability.

Bad Solution:
- Suggests unrelated changes
- Proposes improvements without explanation
- Provides no actionable design modification

**Code:**  
Not applicable (conceptual Requirements Engineering problem).but
Student code should implement:
- check_satisfiability(design) -> (bool, explanation)

- Good Code:
- Returns a tuple (True/False, "reason")
- For:{"username_password_login": True, "multi_factor_authentication": False}
it should return False with a reason mentioning MFA/RBAC or stronger authorization.

    •	Bad Code:
    •	Returns only True/False (no explanation).
    •	Ignores the design dictionary.
    •	Checks unrelated features.

### Problem C_3: Requirements Elicitation Question Generation with AI Assistance

**Evaluation Description:**  
This problem is evaluated across four tasks.

Task 1 – Survey Question Design

Good Solution:
- Provides three survey questions appropriate for general users (drivers).
- Questions are concise and easy to answer.
- Questions relate to usage patterns, feature importance, performance, or satisfaction.

Bad Solution:
- Provides fewer than three questions.
- Questions are vague, overly technical, or irrelevant to end users.
- Questions are written as interview-style open discussions instead of surveys.

Task 2 – Interview Question Design

Good Solution:
- Provides three interview questions suitable for a city transportation administrator.
- Questions address system management, constraints, policy, security, or scalability.
- Questions are open-ended and encourage detailed responses.

Bad Solution:
- Questions are too generic or user-focused.
- Questions lack relevance to administrative or organizational concerns.
- Questions are phrased as simple yes/no questions.

Task 3 – Question Quality Review

Good Solution:
- Correctly identifies a meaningful weakness, such as:
- ambiguity
- lack of scope
- missing non-functional considerations
- Demonstrates awareness of requirement quality attributes.

Bad Solution:
- Identifies a trivial or unrelated issue.
- Fails to explain why the issue is a weakness.
- States that no improvement is needed.

Task 4 – Question Improvement

Good Solution:
- Rewrites one question to improve clarity, scope, or specificity.
- The revised question clearly addresses the identified weakness.

Bad Solution:
- Makes minimal or no meaningful changes.
- Does not address the identified weakness.
- Produces a less clear question than the original.

**Code:**  
Not applicable (conceptual Requirements Engineering problem).
but
Student code should:
- Correctly replace {domain} with the given domain (no leftover {domain} in the output).
- Produce exactly 3 survey questions and 3 interview questions.
- Print or store:
- one clear weakness statement, and
- one improved question addressing that weakness.

Bad Code:
- Prints question templates without formatting or domain replacement.
- Produces an incorrect number of questions.
- Does not include a weakness statement or an improved question

## 3. References

[1] K. Ronanki, B. Cabrero-Daniel, J. Horkoff, and C. Berger,
“Requirements Engineering using Generative AI: Prompts and Prompting Patterns,”
arXiv:2311.03832, 2023.
[2] M. Borg, K. Wnuk, and A. Ferrari,
“Requirements Satisfiability with In-Context Learning,” arXiv:2404.12576, 2024.
[3] A. M. Author et al.,
“An Automated Model of Software Requirement Engineering Using GPT-3.5,” 2023.
