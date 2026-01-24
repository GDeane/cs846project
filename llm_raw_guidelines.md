# Week X Raw Guidelines: [Topic Title]

**Authors:** [Student Name 1, Student Name 2, Savira Umar]  
**Readings:**

- [Additional sources explored beyond assigned readings]

## 1. Guidelines from Readings

> **Note:** Guidelines should be actionable, specific, and usable during real coding tasks.

### Guideline 1: [Short, Actionable Title]

**Description:**  
State the guideline clearly and concretely.

**Reasoning:**  
Explain _why_ this guideline is important, referencing readings and external sources where relevant.

**Example:**  
Provide a brief illustrative example (code or pseudo-code if helpful).

---

### Guideline 2: [Short, Actionable Title]

(Repeat the same structure for each guideline.)

---

### Guideline N: [Short, Actionable Title]

(Repeat the same structure for each guideline.)

---

## 2. Guidelines from from any related research/grey literature like practitioner or developer tool blogs

> **Note:** Guidelines should be actionable, specific, and usable during real coding tasks.

### Guideline 1: [Short, Actionable Title]

**Description:**  
State the guideline clearly and concretely.

**Reasoning:**  
Explain _why_ this guideline is important, referencing readings and external sources where relevant.

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

#### Guideline 1: Start with Role + Standards Frame

#### Description:

Tell the LLM what expert role to take and what standards to follow (e.g., ISO 29148, IEEE 29148, ISO/IEC 25010).

#### Reasoning:

Role + standards anchors vocabulary, rigor, and requirement quality expectations so outputs are more consistent and professional.

#### Example:

“Act as a senior requirements engineer. Follow ISO/IEC/IEEE 29148. Use testable SHALL statements.”

#### Suggested by:

Savira (GPT), Gavin (Gemini), Savira (Gemini)

#### Guideline 2: Provide Project Ecosystem Context First

#### Description:

Before asking for requirements, provide scope, stakeholders, goals, constraints, and any risks.

#### Reasoning:

Missing context causes generic requirements and wrong assumptions. Context helps the model tailor requirements to the real situation.

#### Example:

“Goal: reduce customer support calls 40%. Users: customers + agents. Constraints: must integrate with CRM; PII data; budget limit.”

#### Suggested by:

Artemiy (Copilot), Savira (Claude), Savira (DeepSeek)

#### Guideline 3: Separate Problem Space from Solution Space

#### Description:

First elicit goals/needs; only later discuss design/implementation.

#### Reasoning:

LLMs tend to jump to solutions; separating spaces prevents premature design decisions and keeps requirements focused on needs.

#### Example:

“Phase 1: ask clarifying questions only. Do NOT propose architecture or tools yet.”

#### Suggested by:

Savira (GPT)

#### Guideline 4: Use a Structured Prompt Format (Role–Goal–Context–Output–Constraints–Examples)

#### Description:

Write prompts in a consistent structure: Role, Goal, Context, Output format, Constraints, Examples.

#### Reasoning:

Structure reduces ambiguity, improves repeatability, and makes outputs easier to evaluate and compare.

#### Example:

    •	Role: “Product Manager”
    •	Goal: “Elicit NFRs for privacy”
    •	Output: “Table with ID, SHALL, Rationale, Acceptance Criteria”

#### Suggested by:

Artemiy (Copilot)

#### Guideline 5: Use Explicit Requirement Templates

#### Description:

Require outputs to follow a fixed template: ID, Type, SHALL statement, Rationale, Acceptance Criteria, Priority (and optional Verification Method).

#### Reasoning:

Templates force completeness and produce requirements that are easier to test, trace, and review.

#### Example (template row):

ID: NFR-01 | Type: Security | SHALL: “The system SHALL encrypt PII at rest using AES-256.” | AC: “Verify encryption enabled in DB config.”

#### Suggested by:

Savira (GPT), Gavin (Gemini), Savira (Gemini)

#### Guideline 6: Ban Vague Words Unless Quantified

#### Description:

Forbid terms like “fast,” “robust,” “user-friendly,” “secure” unless measurable.

#### Reasoning:

Vague language cannot be verified, causing weak requirements and disputes later.

#### Example:

Bad: “System shall be fast.”
Good: “System SHALL respond within 2 seconds for 95% of requests.”

#### Suggested by:

Savira (GPT), Savira (Claude)

#### Guideline 7: Enforce RFC-2119 Modal Verbs (SHALL/SHOULD/MAY)

#### Description:

Require SHALL for mandatory requirements; SHOULD for recommended; MAY for optional—and flag anything that can’t be stated clearly.

#### Reasoning:

Standard modality reduces ambiguity and helps prioritize and test requirements.

#### Example:

“If a requirement cannot be written as SHALL, rewrite it or mark it ambiguous.”

#### Suggested by:

Savira (GPT)

#### Guideline 8: Decompose Complex Requirements into Atomic Ones

#### Description:

Split “and/or” and multi-part requirements into single, testable statements.

#### Reasoning:

Atomic requirements improve traceability, testing, and reduce hidden scope.

#### Example:

Bad: “The system shall store and share user data securely.”
Good: (1) store data with encryption; (2) share data only with user consent.

#### Suggested by:

Savira (Claude), Gavin (Gemini), Savira (Gemini)

#### Guideline 9: Work in RE-Aligned Phases (Elicit → Analyze → Validate → Manage Change)

#### Description:

Ask the LLM to follow phases instead of producing everything at once.

#### Reasoning:

Phased workflows reduce hallucination, improve focus, and mirror real RE processes.

#### Example:

“Step 1: Extract atomic requirements. Step 2: classify FR/NFR. Step 3: add verification method.”

#### Suggested by:

Savira (DeepSeek), Gavin (Gemini), Savira (Gemini)

#### Guideline 10: Use Hierarchical Decomposition Instead of “Write Full SRS”

#### Description:

Break big tasks into smaller subtasks: overview → extraction → classification → refinement.

#### Reasoning:

Asking for a full SRS often produces generic fluff; decomposition improves quality and reduces errors.

#### Example:

“First list stakeholders and goals. Then extract 15 atomic requirements. Then label FR/NFR/constraints.”

#### Suggested by:

Gavin (Gemini), Savira (Gemini)

#### Guideline 11: Use Recursive Refinement (Generate → Critique → Refine)

##### Description:

Make the model critique its own output, then rewrite.

##### Reasoning:

First drafts are rarely good; critique/refine improves clarity, resolves conflicts, and increases testability.

##### Example:

Prompt 1: “Generate 10 requirements.”
Prompt 2: “Find 3 ambiguities + 2 conflicts.”
Prompt 3: “Rewrite requirements + add verification method.”

##### Suggested by:

Gavin (Gemini), Savira (Gemini)

#### Guideline 12: Ask for Assumptions Explicitly

### Description:

Require the LLM to list assumptions it made and identify missing info.

#### Reasoning:

Hidden assumptions cause requirement defects; surfacing them early improves correctness.

#### Example:

“List assumptions about users, data volume, and compliance rules.”

#### Suggested by:

Artemiy (Copilot), Savira (DeepSeek)

#### Guideline 13: Generate Concrete Examples + Negative Scenarios

#### Description:

Ask for realistic examples and edge cases (failure/abuse cases).

#### Reasoning:

Examples ground the requirement and expose gaps; negative scenarios reveal missing constraints and NFRs.

#### Example:

“Give 2 misuse cases (e.g., brute-force login attempts) and the missing security requirements.”

#### Suggested by:

Artemiy (Copilot), Gavin (Gemini), Savira (Gemini)

#### Guideline 14: Use Pre-Mortem Prompting for Risk-Driven Requirements

#### Description:

Ask the LLM to assume the system failed, then work backward to identify missing requirements.

#### Reasoning:

Pre-mortems create realistic, safety/security-focused requirements tied to real failure modes.

#### Example:

“Assume a data breach occurred. What privacy/security requirement was missing?”

#### Suggested by:

Gavin (Gemini), Savira (Gemini)

#### Guideline 15: Elicit Non-Functional Requirements Separately

#### Description:

Prompt explicitly for NFR categories (performance, security, privacy, usability, reliability, scalability).

#### Reasoning:

NFRs are commonly missed unless asked directly; separating them ensures coverage.

#### Example:

“List security NFRs for handling PII. Output as SHALL statements with acceptance criteria.”

#### Suggested by:

Savira (Claude)

#### Guideline 16: Require Testability Checks + Verification Method

#### Description:

For each requirement, require a testability judgment and a verification method (Test/Demo/Analysis/Inspection).

#### Reasoning:

Forces requirements to be verifiable and reduces vague statements.

#### Example:

“Add column: Verification Method = Test; AC = ‘95% requests < 2s’ measured in load test.”

#### Suggested by:

Savira (GPT), Gavin (Gemini), Artemiy (Copilot)

#### Guideline 17: Produce Traceability Links (Requirement ↔️ Tests ↔️ Stakeholders)

#### Description:

Ask the LLM to link each requirement to stakeholders, rationale, and test cases.

#### Reasoning:

Traceability improves change impact analysis and helps ensure each requirement has a purpose and verification.

#### Example:

REQ-05 → Stakeholder: Patient → Test: TC-05 “Appointment booking happy path” → Rationale: reduce phone calls.

#### Suggested by:

Artemiy (Copilot)

#### Guideline 18: Keep Outputs Small and Iterate

#### Description:

Ask for a small batch (5–10 requirements/questions), review, then expand.

#### Reasoning:

Iteration reduces errors, improves alignment, and avoids large hallucinated requirement lists.

#### Example:

“Start with 5 key requirements. Ask 5 clarifying questions. Then produce the next 10.”

#### Suggested by:

Artemiy (Copilot)

#### Guideline 19: Use “Ask Clarifying Questions First” Mode

#### Description:

Instruct the model to ask clarifying questions before generating requirements.

#### Reasoning:

Better input quality leads to better output; clarifying questions reduce ambiguity early.

#### Example:

“Before drafting, ask 5 questions about stakeholders, latency, data sensitivity, and integrations.”

#### Suggested by:

Gavin (Gemini), Savira (GPT)

#### Guideline 20: Keep Humans in the Loop (LLM as Facilitator, Not Final Authority)

#### Description:

Use the LLM to assist (brainstorm, critique, structure), but keep final decisions with human stakeholders/engineers.

#### Reasoning:

LLMs lack true domain accountability and can hallucinate; human validation is required for correctness and ethics.

#### Example:

Human drafts requirements → LLM flags ambiguity → human revises → stakeholders approve.

#### Suggested by:

Savira (DeepSeek), Artemiy (Copilot), Savira (GPT/Claude)

## 4. References

[1]  
[2]

---
