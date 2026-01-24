# Week X Example Problems: [Topic Title]

**Authors:** [Student Name 1, Student Name 2, Student Name 3]

## 1. Example Problems

### Problem A_1: Functional vs Non-Functional Requirement Classification with AI Awareness

**Task Description:**  
You are working as a requirements engineer on an Online Healthcare Appointment System.
The system allows patients to book appointments, receive reminders, and manage medical data.

An AI assistant (e.g., GitHub Copilot Chat or ChatGPT) is available to assist with requirements engineering tasks; however, human judgment is still required.

You are given the following requirements:
• R1. The system shall allow patients to book appointments online.
• R2. The system shall encrypt all patient data stored in the database.
• R3. The system shall send appointment reminders via email and SMS.
• R4. The system shall respond to user requests within 2 seconds.
• R5. The system shall comply with healthcare data privacy regulations.
• R6. The system shall provide a user-friendly interface for elderly patients.

**Student Tasks:**

1. Manual Classification
   Classify each requirement as either:
   • Functional Requirement (FR), or
   • Non-Functional Requirement (NFR).

2. Prompt Design Reflection

Consider the following two prompts for using an AI tool:
• Prompt A:
“Classify these requirements.”
• Prompt B:
“Classify each of the following requirements as Functional or Non-Functional and briefly justify your answer.”
Answer the following:
• Which prompt is better designed for this task?
• Provide one reason for your choice. 3. Human Oversight Reflection
explain why AI-assisted requirement classification should always include human review.

**Starter Code:**

```python
requirements = [
    "The system shall allow patients to book appointments online.",
    "The system shall encrypt all patient data stored in the database.",
    "The system shall send appointment reminders via email and SMS.",
    "The system shall respond to user requests within 2 seconds.",
    "The system shall comply with healthcare data privacy regulations.",
    "The system shall provide a user-friendly interface for elderly patients."
]

NFR_KEYWORDS = {
    "encrypt", "security", "privacy", "comply", "compliance",
    "within", "seconds", "performance", "usable", "usability",
    "user-friendly", "reliable", "availability"
}

def classify_requirement(text: str) -> str:
    t = text.lower()
    for kw in NFR_KEYWORDS:
        if kw in t:
            return "NFR"
    return "FR"

for r in requirements:
    print(r, "->", classify_requirement(r))
```

### Problem A_2: Requirements Satisfiability Reasoning

**Task Description:**  
You are evaluating whether a system design satisfies a stated security requirement for an Online Healthcare System.
Your task is to determine if the current design meets the requirement and to reason about potential improvements.
An AI assistant may be used to support analysis; however, human judgment is required.

Requirement:
“The system shall ensure that only authorized users can access patient records.”

Design Description:
• Users log in with a username and password.
• No multi-factor authentication is used.

**_Student Tasks:_** 1. Satisfiability Decision
Does the given design satisfy the requirement? Answer Yes or No. 2. Reasoning
Explain your decision in 2–3 sentences. 3. Design Improvement
Suggest one design change that would improve the satisfiability of the requirement.

**Starter Code:**

```python
design = {
    "username_password_login": True,
    "multi_factor_authentication": False
}

def check_satisfiability(design: dict):
    if design.get("username_password_login") and not design.get("multi_factor_authentication"):
        return (False, "Password-only login is insufficient; add MFA or RBAC.")

    if design.get("username_password_login") and design.get("multi_factor_authentication"):
        return (True, "MFA strengthens authorization.")

    return (False, "No authentication mechanism defined.")

print(check_satisfiability(design))
```

### Problem A_3: Requirements Elicitation Question Generation with AI Assistance

**Task Description:**
You are supporting early-stage requirements elicitation for a Smart Parking System.
The system is intended to help drivers find available parking spaces and help city administrators manage parking resources.
An AI assistant (e.g., GitHub Copilot Chat or ChatGPT) can be used to help generate requirements elicitation questions.
However, the usefulness of the questions depends on prompt clarity and human review.

**_Student Tasks:_** 1. Survey Question Design
Write three survey questions intended for general users (drivers) of the smart parking system. 2. Interview Question Design
Write three interview questions intended for a city transportation administrator. 3. Question Quality Review
Identify one weakness in the generated questions (e.g., ambiguity, lack of scope, missing non-functional aspects). 4. Question Improvement
Rewrite one question to improve its clarity or specificity.

**Starter Code:**

```python
domain = "smart parking system"

survey_templates = [
    "How often do you use a {domain}?",
    "What feature is most important to you in a {domain}?",
    "How satisfied are you with the performance of current {domain}s?"
]

interview_templates = [
    "What are the main challenges you face when managing a {domain}?",
    "What security or privacy concerns exist for a {domain}?",
    "What system constraints must be considered for a {domain}?"
]

def fill(templates, domain):
    return [t.format(domain=domain) for t in templates]

survey_qs = fill(survey_templates, domain)[:3]
interview_qs = fill(interview_templates, domain)[:3]

print("Survey:", survey_qs)
print("Interview:", interview_qs)

weakness = "Some questions are vague and lack measurable criteria."
improved = "How satisfied are you with the time to find parking using the smart parking system (1–5) during peak hours?"

print("Weakness:", weakness)
print("Improved:", improved)
```

```

## 2. References

[1] K. Ronanki, B. Cabrero-Daniel, J. Horkoff, and C. Berger,
“Requirements Engineering using Generative AI: Prompts and Prompting Patterns,”
arXiv:2311.03832, 2023.
[2] M. Borg, K. Wnuk, and A. Ferrari,
“Requirements Satisfiability with In-Context Learning,” arXiv:2404.12576, 2024.
[3] A. M. Author et al.,
“An Automated Model of Software Requirement Engineering Using GPT-3.5,” 2023.
```
