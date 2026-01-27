# Week 4 Example Problems: Requirements

**Authors:** [Gavin Deane, Artemiy Vishnyakov, Savira Umar]

Additional Materials in Repository: https://github.com/GDeane/cs846project

## 1. Example Problems

For consistency and comparison use the Copilot GPT-5 mini model for all parts of exercise A.

### Problem A_1: Stakeholder Interviews Summary

**Task Description:**  
Summarize the key points from each stakeholder interview. Include their main concerns, requirements, and any conflicting
interests.

Find the related files in the Exercise_A/docs/transcripts folder.

**Starter Code:**

1. **Customer Support**
    - **Concern**:
    - **Request**:
    - **Implication**:

2. **Financial Stakeholder**
    - **Concern**:
    - **Request**:
    - **Implication**:

3. **Software Engineer**
    - **Concern**:
    - **Request**:
    - **Implication**:

---

### Problem A_2: Real-World Constraints (outside of interviews)

**Task Description:**  
List and describe the real-world constraints that may impact the project, including budget, technical feasibility, and
time limitations outside of what was stated in the interviews.

**Starter Code:**  
There is no starter code for this task. Related files are in the Exercise_A/docs/transcripts
folder.

---

### Problem A_3: Analysis of Conflicting Requirements

**Task Description:**  
Analyze the conflicting requirements from the stakeholders and any conflicts that arise with real-world constraints.
Discuss the implications of these conflicts and potential ways to address them.

**Starter Code:**  
There is no starter code for this task. Related files are in the Exercise_A/docs/transcripts
folder.

---

### Problem A_4: Proposed Solutions

**Task Description:**  
Outline your proposed solutions to reconcile the conflicting requirements. Include any recommendations, patterns,
strategies based on stakeholder needs.

**Starter Code:**  
There is no starter code for this task. Related files are in the Exercise_A/docs/transcripts
folder.

---

### Problem B: Elicitation of Requirements from Problem Domain

> A note on GenAI contribution: Problem B was written by me (Gavin), with
> contribution from GPT-5.2 as follows:
> - Correctness and reliability guarantees question for example problem questionnaire

For consistency and comparison use the Copilot GPT-5 mini model for all parts of exercise B.

#### 1. Problem description

Given the description of the problem domain and the following questionnaire, use your LLM (GPT-5 mini) to elicit a set
of 10-15 structured requirements.

You would want to feel comfortable:

- 1: Showing these requirements to your boss.
- 2: presenting this list of requirements to a group of stakeholders in order to elicit preferences.
- 3: Agreeing to implement this set of requirements in a contract if the client agreed to them.

_There is no particular submission template for this question. You may structure your requirements as you wish, so long
as it is clear and easy to parse._

This problem takes heavy inspiration from the study conducted by Ronaki et al. (2023) [1].

#### 2. Problem domain

A client wants to build a system that connects an AI personal assistant to an end user's calendar.

Not only should this AI system know what events are when, but the AI should also have awareness of the location of each
event so that the AI can point out when travel times may be tight or unfeasible.

Quote from (fictional) client: "That way, whenever the end user needs to book a meeting, they can simply ask their
assistant whether this works well with my schedule."

In addition, this personal assistant should get better over time as it gets to know what kind of time you prefer not to
be booked or what travel modes you use!

The client considers that privacy of user data could be a potential concern in this case. "I don't want everything about
a user's life to end up exposed on the internet because of our app."

#### 3. Questionnaire

Here are some (not-exhaustive) questions to aid in requirements elicitation:

**Q1**: What kind of correctness and reliability guarantees must the system provide? That is, how often is it acceptable
for the system to make a mistake about whether an event fits or travel time.

**Q2**: Are there any categories of data the system should not learn from? (shared calendars, unusually busy weeks).

**Q3**: How explainable should the system be? Should it give a reasoning for what criteria it used to make its decision?
How in depth should this reasoning be?

**Q4**: What places in the world would you want this system to be deployed? Different countries have different privacy
laws (e.g. the right to be forgotten under the GDPR in the EU).

**Q5**: Should this system to be a piece of hardware or an application?

---

### Problem C_1: Functional vs Non-Functional Requirement Classification with AI Awareness

For consistency and comparison use the Copilot GPT-5 mini model for all parts of exercise C.

This problem takes inspiration from another study conducted by Ronaki et al. (2023) [2].

**Task Description:**  
You are working as a requirements engineer on an Online Healthcare Appointment System.
The system allows patients to book appointments, receive reminders, and manage medical data.

An AI assistant (e.g., GitHub Copilot Chat) is available to assist with requirements engineering tasks;
however, human judgment is still required.

You are given the following requirements:

- R1. The system shall allow patients to book appointments online.
- R2. The system shall encrypt all patient data stored in the database.
- R3. The system shall send appointment reminders via email and SMS.
- R4. The system shall respond to user requests within 2 seconds.
- R5. The system shall comply with healthcare data privacy regulations.
- R6. The system shall provide a user-friendly interface for elderly patients.

**Student Tasks:**

1. Classify each requirement as either Functional Requirement (FR) or Non-Functional Requirement (NFR) and provide a
   brief justification for each classification.
2. Human Oversight Reflection - explain why AI-assisted requirement classification should always include human review

---

### Problem C_2: Requirements Satisfiability Reasoning

This problem takes inspiration from a study conducted by Santos et al. (2024) [3].

**Task Description:**  
You are evaluating whether a system design satisfies a stated security requirement for an Online Healthcare System.

Your task is to determine if the current design meets the requirement and to reason about potential improvements.

An AI assistant may be used to support analysis; however, human judgment is required.

Requirement:
“The system shall ensure that only authorized users can access patient records.”

Design Description:

- Users log in with a username and password.
- No multi-factor authentication is used.

**_Student Tasks:_**

1. Satisfiability Decision - Does the given design satisfy the requirement? Answer Yes or No.

2. Reasoning - Explain your decision in 2–3 sentences.

3. Design Improvement - Suggest one design change that would improve the satisfiability of the requirement.

---

### Problem C_3: Requirements Elicitation Question Generation with AI Assistance

This problem takes inspiration from a study conducted by Yeow et al. (2024) [4].

**Task Description:**
You are supporting early-stage requirements elicitation for a Smart Parking System.

The system is intended to help drivers find available parking spaces and help city administrators manage parking
resources.

An AI assistant (e.g., GitHub Copilot Chat) can be used to help generate requirements elicitation questions.
However, the usefulness of the questions depends on prompt clarity and human review.

**_Student Tasks:_**

1. Survey Question Design - Write three survey questions intended to be answered by general users (drivers) of the smart
   parking system.

2. Interview Question Design - Write three interview questions intended to be answered by a city transportation
   administrator.

3. Question Quality Review - Identify one weakness in the generated questions (e.g., ambiguity, lack of scope, missing
   non-functional aspects).

4. Question Improvement - Rewrite one question to improve its clarity or specificity.

---

## 2. References

[1] K. Ronanki, C. Berger, and J. Horkoff, “Investigating ChatGPT’s Potential to Assist in Requirements Elicitation
Processes,” Jul. 14, 2023, arXiv: arXiv:2307.07381. doi: 10.48550/arXiv.2307.07381.

[2] K. Ronanki, B. Cabrero-Daniel, J. Horkoff, and C. Berger, “Requirements Engineering using Generative AI: Prompts and
Prompting Patterns,” Nov. 07, 2023, arXiv: arXiv:2311.03832. doi: 10.48550/arXiv.2311.03832.

[3] S. Santos, T. Breaux, T. Norton, S. Haghighi, and S. Ghanavati, “Requirements Satisfiability with In-Context
Learning,” Apr. 19, 2024, arXiv: arXiv:2404.12576. doi: 10.48550/arXiv.2404.12576.

[4] J. S. Yeow, M. E. Rana, and N. A. Abdul Majid, “An Automated Model of Software Requirement Engineering Using
GPT-3.5,” in 2024 ASU International Conference in Emerging Technologies for Sustainability and Intelligent Systems (
ICETSIS), Jan. 2024, pp. 1746–1755. doi: 10.1109/ICETSIS61505.2024.10459458.


