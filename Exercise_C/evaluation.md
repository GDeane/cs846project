## 1. Evaluation specifically for Example Problems

### Problem C_1: Functional vs Non-Functional Requirement Classification with AI Awareness

The following criteria apply to this topic:

- Correct identification of Functional Requirements (FR) versus Non-Functional Requirements (NFR)
- Clear and logical reasoning
- Recognition of the limitations of AI and the need for human oversight.

**Evaluation Description:**  
This problem is evaluated across two tasks.

Task 1 – Manual Requirement Classification

Good Solution:

- Correctly classifies:
    - FR:
        - appointment booking - (describes an action the user can do with the system),
        - reminders - (describes a behavior the system performs for the users)
    - NFR:
        - encryption - (not something the user can do with the system. Not an action or behavior),
        - 2 seconds - (this is a performance constraint on how something is done, not an action or behavior),
        - compliance - (regulatory compliance is a constraint. Not an action or behavior),
        - usability - (this is a quality constraint, not an action or behavior).
- Demonstrates understanding of the difference between:
    - what the system does (FR) and
    - how well or under what constraints it operates (NFR)

Bad Solution:

- Random or inconsistent classification
- Misclassifies security, performance, usability, or compliance requirements as FR
- Shows no clear reasoning or conceptual understanding

Task 2 – Human Oversight Reflection

Good Solution:

- Clearly explains at least one valid reason why human review is required, such as:
    - AI may misinterpret requirements
    - AI lacks full domain context
    - AI can produce inconsistent or incorrect classifications
    - AI cannot be held responsible for harm caused

Bad Solution:

- Assumes AI output is always correct
- States that human review is unnecessary
- Provides overly brief or unsupported responses

### Problem C_2: Requirements Satisfiability Reasoning

The following criteria apply to this topic:

- Correct reasoning about requirements satisfiability
- Clear justification based on the provided design
- Ability to propose a practical design improvement
- Awareness of the role of human judgment in evaluating system designs

**Evaluation Description:**  
This problem is evaluated across three tasks.

Task 1 – Satisfiability Decision

Good Solution:

- Correctly answers No, recognizing that username/password authentication alone does not fully ensure that only
  authorized users can access sensitive records.

Bad Solution:

- Answers Yes without qualification
- Assumes basic authentication is sufficient without considering security risks

Task 2 – Reasoning

Good Solution:

- Clearly explains why the design is insufficient (e.g., weak authentication, lack of additional verification, higher
  risk of unauthorized access).
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

### Problem C_3: Requirements Elicitation Question Generation with AI Assistance

> A note on GenAI contribution:
> - Example solutions were written by GPT-5.2, with edits when the context didn't make sense

The following criteria apply to requirements elicitation problems in this topic:

- Ability to design relevant and well-scoped elicitation questions
- Clear distinction between survey and interview questions
- Awareness of question quality attributes (clarity, specificity, relevance)
- Ability to critically review and improve AI-assisted outputs
- Recognition of the need for human judgment in requirements elicitation

**Evaluation Description:**  
This problem is evaluated across four tasks.

Task 1 – Survey Question Design

Good Solution:

- Provides three survey questions appropriate for general users (drivers).
- Questions are concise and easy to answer.
- Questions relate to usage patterns, feature importance, performance, or satisfaction.

Example:

1) "How often do you use parking apps per week?"
2) "How important is knowing space availability in real-time when choosing parking?" (scale: extremely important - not
   important at all)
3) "How satisfied are you with the current time it takes you to find parking downtown?" (scale: extremely satisfied -
   not satisfied at all)

Bad Solution:

- Provides fewer than three questions.
- Questions are vague, overly technical, or irrelevant to end users.
- Questions are written as interview-style open discussions instead of surveys.

Task 2 – Interview Question Design

Good Solution:

- Provides three interview questions suitable for a city transportation administrator.
- Questions address system management, constraints, policy, security, or scalability.
- Questions are open-ended and encourage detailed responses.

Example:

1) "What policies or constraints govern data sharing and privacy for parking usage analytics?"
2) "How do you prioritize enforcement, revenue, and congestion goals when managing parking zones?"
3) "What scalability or uptime requirements do you have for a citywide parking system during the busiest times?"

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

Example:
"The initial survey questions might miss non-functional aspects, like acceptable false positive (app says parking when
no parking) or false negative (app says no parking when there is parking)"

Bad Solution:

- Identifies a trivial or unrelated issue.
- Fails to explain why the issue is a weakness.
- States that no improvement is needed.

Task 4 – Question Improvement

Good Solution:

- Rewrites one question to improve clarity, scope, or specificity.
- The revised question clearly addresses the identified weakness.

Example:
(replace question 2)
"Which one would bother you more?

- An app saying there is no available parking when really there is, or
- an app saying there is available parking when really there isn't?"

Bad Solution:

- Makes minimal or no meaningful changes.
- Does not address the identified weakness.
- Produces a less clear question than the original.

## 2. References

[1] K. Ronanki, B. Cabrero-Daniel, J. Horkoff, and C. Berger,
“Requirements Engineering using Generative AI: Prompts and Prompting Patterns,”
arXiv:2311.03832, 2023.

[2] M. Borg, K. Wnuk, and A. Ferrari,
“Requirements Satisfiability with In-Context Learning,” arXiv:2404.12576, 2024.

[3] A. M. Author et al.,
“An Automated Model of Software Requirement Engineering Using GPT-3.5,” 2023.
