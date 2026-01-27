# Week 4 Evaluation: Requirements

**Authors:** [Gavin Deane, Artemiy Vishnyakov, Savira Umar]

## 1. Evaluation Criteria

This section defines how students can determine whether they solved the example problems correctly.

Criteria vary depending on the specific problem. Each problem's evaluation criteria are detailed in Section 2.

---

## 2. Evaluation specifically for Example Problems

### Problem A_1: Stakeholder Interviews Summary

#### Example Good Solution"

1. **Customer Support Representative**
    - **Concern**: The chatbot is forgetting context from earlier in the chat.
    - **Request**: Improve context retention and response generation speed.
    - **Implication**: Enhancing user experience and satisfaction is critical for customer retention.

2. **Financial Stakeholder**
    - **Concern**: High costs associated with the OpenAI API tokens.
    - **Request**: Transition to a more economical solution, potentially using a cheaper model.
    - **Implication**: Budget constraints must be considered, impacting the overall project feasibility.

3. **Software Engineer**
    - **Concern**: Preference for the Claude API due to its perceived technical advantages.
    - **Request**: Advocate for the adoption of the Claude API over other models.
    - **Implication**: Technical feasibility and future-proofing the solution are essential for long-term success.

#### Example Bad Solution

1. **Customer Support** (Lack of details)
    - **Concern**: Customers are unsatisfied with the current chatbot
    - **Request**: Improve chatbot
    - **Implication**: A better chatbot will make customers happy

2. **Financial Stakeholder** (Excessive details prevent broad implications from being drawn)
    - **Concern**: API/token spend is material; target ~40% cost reduction in 3–6 months; migration cap ~$60k if
      justified.
    - **Request**: Demonstrable cost reductions, phased progress, and ROI for any migration spend.
    - **Implication**: (Irrelevant information here)

3. **Software Engineer** (Excessive technical jargon & creation of a solution when only analysis is requestedx)
    - **Concern**: High session context volatility — the agent exhibits poor stateful retention and low contextual
      coherence across turns, causing frequent conversational resets and generic, low-utility outputs; also perceptible
      latency spikes affecting UX.
    - **Request**: Implement robust session-state management (e.g., turn-level embeddings, incremental summarization, or
      context-window orchestration), optimize inference latency (caching, batching, and model selection), and add
      telemetry for turn-wise relevance and intent drift.
    - **Implication**: Requires a stateful session store or vector DB, summarization pipeline and context-truncation
      strategy, additional engineering for caching/throughput and instrumentation, and trade-offs against token budget
      and API spend that must be managed to avoid increased support ticket volume.

**Evaluation**

- **Good**: Demonstrates a deep understanding of the conflicting needs of all stakeholders. Clearly articulates how
  these needs impact the requirements.
- **Satisfactory**: Provides a basic understanding of stakeholder needs but lacks depth or clarity in analysis.
- **Bad**: Fails to adequately identify or analyze stakeholder needs.

---

### Problem A_2: Real-World Constraints (outside of interviews)

#### Example Good Solution:

**Budget**: target 40% recurring cost reduction with one‑time migration budget of $60k limits scope and
tools/consultants.

**Procurement & legal**: vendor contracts, data‑privacy reviews, and approvals can add weeks or months of delay cutting
into the 6-month timeframe.

**Technical integration**: API differences, SDK maturity, context‑window limits, and infra changes may require
non‑trivial refactor.

**Performance**: latency and throughput impacts from new provider prompt approaches must be benchmarked.

**Team/time**: limited engineering capacity and competing priorities lengthen delivery. There is a need staged work and
clear milestones.

**Operations**: monitoring, cost telemetry, rate limits, and fallback strategies required to avoid UX regressions.

#### Example Bad Solution (Nonsensical, confabulated requirements, excessive technical details)

- Require on-prem GPU cluster with 512 GB GPU memory per node to run the model locally; no cloud allowed.
- Mandate support for legacy browsers including Internet Explorer 8 and custom internal kiosks with obsolete TLS stacks.
- Target 10 million concurrent active users at launch with single-region deployment and no autoscaling plan.
- Preserve full raw conversation logs indefinitely (permanent storage), with expected storage growth of multiple
  petabytes per year.
- Require human moderation for every message in real time before any chatbot reply reaches users.
- Enforce strict on-prem data residency in a non-existent “EU-Mars” jurisdiction and quarterly notarized paper audits.
- Assume vendor pricing is fixed and non-negotiable at $1M/month for model access — budget accordingly with no
  procurement process.
- Plan for zero downtime with a single server design and no redundancy or failover testing.
- Require cryptographic hardware tokens for every user session, replacing existing passwordless flows.
- Expect the engineering team to deliver full integration, QA, and rollout in a single two-week sprint with no
  additional headcount.

**Evaluation: combined with part 3**

---

### Problem A_3: Analysis of Conflicting Requirements

**List of requirements**:
Functional

- Improved context retention within a user session (Customer Support, Engineering).
- Faster response times / lower latency (Customer Support, Engineering).
- More personalized, less generic responses (Customer Support).
- Support for a new LLM provider (Claude/Anthropic) as a candidate for migration (Engineering).

Non‑functional

- Reduce OpenAI API/token spend by ~40% within 3–6 months; demonstrate phased progress (Finance).
- One‑time migration budget up to ~$60k if payback within ~3–6 months (Finance).
- No lasting increase in live support headcount; temporary UX regressions acceptable with remediation plan (Finance).
- Ensure integration effort fits team capacity and existing infrastructure (Engineering).

**Conflicts**

1. Cost reduction (~40% recurring) vs richer context retention

- Longer contexts and higher‑quality models increase token spend.

2. One‑time migration budget (~$60k) vs full migration to preferred provider (Claude)

- Full migration or heavy rewrites may exceed budget/approval.

3. No lasting increase in live support headcount vs acceptable temporary regressions

- Any rollout that raises support volume risks violating Finance constraint.

4. Legal and Engineering capacity & timelines vs aggressive 3–6 month savings target

- Limited developer time may prevent meeting targets.
- Vendor contracts and data/privacy approvals can delay rollout and if work is started before contracts are made then it
  may be wasted if contracts fall through.

**Evaluation**

- **Good**: Thorough analysis of the conflicting requirements, insightful comparisons and potential resolutions.
- **Satisfactory**: Provides a basic analysis of conflicting requirements but lacks depth or clarity.
- **Needs Improvement**: Fails to adequately analyze conflicting requirements.

### Problem A_4: Proposed Solutions (non-exhaustive list of examples)

1. **Balancing Context Retention and Cost**
    - Implement a hybrid approach where the chatbot uses a cheaper model for general inquiries but switches to a more
      advanced model (like Claude) for complex interactions requiring context retention.
    - This solution addresses the financial stakeholder's concerns while still meeting the customer support
      representative's need for improved context handling.

2. **Optimizing API Usage**
    - Introduce caching mechanisms to store frequently accessed data, reducing the number of API calls and thus lowering
      costs.
    - Rolling summaries stored as short embeddings to reduce token costs while keeping long context.
    - Caching common Q&A and retrieval augmented generation (RAG) to reduce token usage.
    - Using token conservation techniques such as prompt engineering, context pruning, compression/summarization between
      the user prompt and what is sent to the chatbot server.
    - This approach can help mitigate the financial stakeholder's concerns while enhancing the chatbot's performance.

3. **Phased Implementation**
    - Propose a phased rollout of the chatbot enhancements, starting with cost-effective solutions and gradually
      integrating more advanced features as budget allows.
    - This strategy allows for immediate improvements in user experience while keeping financial constraints in check.

**Evaluation**

- **Good**: Innovative and feasible solutions that address the conflicting requirements effectively.
- **Satisfactory**: Provides basic solutions that may not fully address the conflicts or are not feasible.
- **Bad**: Solutions not viable or nonsensical.

---

### Problem B: Elicitation of Requirements from Problem Domain

> A note on GenAI contribution: Problem B evaluation was written by me (Gavin), with
> contribution from GPT-5.2 as follows:
> - Good and bad examples were written by GPT-5.2 for evaluation criteria, with edits when the context didn't make sense

There are many possible criteria for evaluating requirements as good or bad.

In this problem, we will evaluate individual requirements based on the 7 requirement quality attributes previously
presented by Denger et al. [2] and Genova et al. [3], and applied in the study by Ronaki et al. (2023) [1]. These
quality attributes include:

- Abstraction
- Atomicity
- Consistency
- Correctness
- Unambiguity
- Understandability
- Feasibility

For each quality attribute, a brief description, good example, and bad example are given.

#### 1. Evaluation Criteria

1. Abstraction

**Description:**  
"The requirements tell what the application must do without telling how it must
do it, i.e. excess of technical detail about the implementation must be avoided in the
specification of the requirements" [3].

**Good Example:**
"The system shall allow the user to ask whether a proposed meeting time fits their schedule, considering existing events
and expected travel time."

**Bad Example:**
"The system shall call the Google Calendar API every 60 seconds, store events in a PostgreSQL table called events,
compute travel time using OSRM with the car.lua profile, and cache results in Redis."

---

2. Atomicity

**Description:**  
"Each requirement is clearly determined and identified, without mixing it with
other requirements" [3]. No usage of "and".

**Good Example:**
"The system shall state in its reasoning the estimated travel time between two consecutive events."

**Bad Example:**
"The system shall display the estimated travel time between two consecutive events and automatically suggest a new
meeting time and notify all attendees."

---

3. Consistency

**Description:**  
"There are no contradictions among requirements" [3]. That is, you must not have two mutually exclusive requirements.

**Good Example:**
"The system shall store the user’s calendar data only on the user’s device."

"The system shall perform travel-time calculations locally on the user’s device."

**Bad Example:**
"The system shall store the user’s full calendar history indefinitely to improve recommendations over time."

"The system shall delete all user calendar data immediately after each query."
(Contradiction here)

---

4. Correctness

**Description:**  
"The requirements that are implemented have to reflect the expected (intended) behavior of the users and customers.
That is, everything stated as a requirement is something that shall be met by the final system to fulfill a certain
purpose (suitability). " [2].

**Good Example:**
"The system shall warn the user when the estimated travel time between two events makes it impossible to arrive by the
start time of the later event."

**Bad Example:**
"The system shall display the current stock price of Apple on the calendar screen."
(Doesn't reflect the user's intended purposes of scheduling + travel feasibility + privacy)

---

5. Unambiguity

**Description:**  
"The requirements should only have one possible interpretation. Note that one requirement might be unambiguous to a
certain group of stakeholder but has a different meaning in another. It is important to involve all stakeholders in the
requirements engineering process to gain a common understanding" [2].

"There exists only one interpretation for each requirement" [3].

**Good Example:**
"When the user asks whether a proposed meeting fits, the system shall respond with one of: 'Fits', 'Does not fit', or
'Fits only if the previous meeting ends by [time]', and shall include the computed travel time in minutes."

**Bad Example:**
"The system should usually try to avoid booking meetings when travel would be tight."
(The words "Usually", "try", and "tight" are all open to interpretation.)

---

6. Understandability

**Description:**  
"The requirements are correctly understood without difficulty" [3].

**Good Example:**
"The system shall allow the user to mark a time block as 'Do not schedule meetings'."

**Bad Example:**
"The system shall implement adaptive temporal preference inference with multi-factor context fusion to minimize schedule
intrusion."
(jargon-heavy. Ineffective for communication with stakeholders.)

---

7. Feasibility

**Description:**  
"All requirements can be implemented with the available technology, human resources and budget. Moreover, all
requirements contribute to the monetary success of the system, that is, they are worth to include in the system" [2].

**Good Example:**
"The system shall support travel-time estimates for the user’s selected mode(s) of transportation: walking, driving, and
public transit."

**Bad Example:**
"The system shall predict real-world travel time with 100% accuracy for all cities worldwide, including unexpected
events such as accidents, protests, and weather changes."
(As written, requires fantasy-levels of technology)

---

#### 3. Example Solution Set

> Note: These requirements were created using GitHub Copilot (GPT-5-Mini) using the suggested guidelines.

Functional requirements (atomic, testable; RFC\-2119)

- REQ\-F\-01 The system SHALL determine for a proposed meeting whether the meeting "fits" the user’s schedule and SHALL
  return a binary decision (fits / does not fit), a confidence score in the range 0.0–1.0, and a concise rationale
  summary explaining the top 3 factors that affected the decision.
    - Acceptance criteria: For 1,000 labeled queries from pilot users, the response payload contains decision,
      confidence, and a rationale field for 100% of queries.
    - Verification method: Integration test against API contract + automated payload validation.

- REQ\-F\-02 The system SHALL estimate end\-to\-end travel time between event locations for supported travel modes and
  return a travel time (minutes) and uncertainty interval.
    - Acceptance criteria: Travel time value and interval present for 100% of queries where event locations are
      specified.
    - Verification method: Integration tests using synthetic location pairs; field verification against logged real
      trips during pilot.

- REQ\-F\-03 The system SHALL report a meeting as "unfeasible" when the estimated travel time plus a configurable buffer
  causes overlap with another confirmed event.
    - Acceptance criteria: For test cases where travel+buffer causes overlap, system reports "unfeasible" in 100% of
      cases.
    - Verification method: Deterministic unit/integration tests using synthetic calendars.

- REQ\-F\-04 The system SHALL allow the user to configure personal scheduling preferences (preferred travel modes,
  protected time windows, scheduling aggressiveness) and SHALL use those preferences in every decision.
    - Acceptance criteria: Preference change reflected in subsequent decisions within one session for 100% of changes.
    - Verification method: End\-to\-end functional test altering preferences and validating decision outputs.

- REQ\-F\-05 The system SHALL provide a user control to opt\-out of model personalization and SHALL not use opt\-out
  accounts for personalization updates.
    - Acceptance criteria: For accounts that opt out, no personalization artifacts for that account appear in model
      update datasets.
    - Verification method: Data pipeline audit and sampling of training inputs; pipeline unit tests.

- REQ\-F\-06 The system SHALL allow users to explicitly exclude specific calendars or named date ranges (e.g.,
  vacations, anomalous weeks) from personalization and SHALL not use excluded items for model updates.
    - Acceptance criteria: Excluded calendars/date ranges not present in any personalization input snapshots for 100% of
      exclusions.
    - Verification method: Data export + automated verification of training dataset membership.

- REQ\-F\-07 The system SHALL support at launch the travel modes: walking, driving, public transit, and biking.
    - Acceptance criteria: For each supported mode, travel time estimate returned for at least 95% of valid location
      pairs in synthetic tests.
    - Verification method: Mode coverage integration tests.

- REQ\-F\-08 The system SHALL provide alternatives (proposed meeting time suggestions) when confidence is below a
  configurable threshold and SHALL not auto\-schedule without explicit user consent.
    - Acceptance criteria: When confidence < threshold, alternatives returned 100% of time and no auto\-scheduling
      executed.
    - Verification method: Workflow tests simulating low confidence scenarios.

- REQ\-F\-09 The system SHALL expose per\-account controls to export, rectify, and request deletion of account data and
  SHALL complete deletion within 30 days of a validated request for accounts under jurisdictions that require it.
    - Acceptance criteria: Export, rectification, and deletion operations complete and logged; deletion completed within
      30 days where applicable.
    - Verification method: Manual/automated verification of CRUD operations; audit log inspection.

Non\-functional requirements

- REQ\-N\-01 The system SHALL respond to an interactive scheduling query (decision + rationale) within 2 seconds at the
  99th percentile for the configured production workload.
    - Acceptance criteria: Measured latency ≤ 2s at 99th percentile over a 7\-day rolling production load test.
    - Verification method: Synthetic load tests and production telemetry.

- REQ\-N\-02 The system SHALL achieve at least 95% accuracy on labeled test datasets for the binary "fits/does not fit"
  decision prior to GA.
    - Acceptance criteria: Validation run against representative dataset of at least 10,000 labeled events yields ≥95%
      accuracy.
    - Verification method: Offline model evaluation with documented dataset and test harness.

- REQ\-N\-03 The system SHALL achieve travel time estimates within ±10 minutes for journeys under 90 minutes in at least
  90% of evaluated cases on a validated test set.
    - Acceptance criteria: Evaluation on at least 2,000 real or high‑fidelity synthetic journeys meets threshold.
    - Verification method: Offline evaluation; field verification in pilot.

- REQ\-N\-04 The system SHALL maintain immutable audit records for automated scheduling decisions and user overrides
  including timestamp, inputs summary, decision, confidence, and user action for at least the retention period
  configured per region.
    - Acceptance criteria: Audit records available and queryable for 100% of automated decisions in test period.
    - Verification method: Audit log queries + spot checks.

- REQ\-N\-05 The system SHALL support per\-region configurable data retention and data residency policies and SHALL
  enforce account\-level residency settings.
    - Acceptance criteria: Data residency/retention rules applied to test accounts and verified by data locality checks.
    - Verification method: Deployment validation and automated checks.

Privacy and security requirements

- REQ\-P\-01 The system SHALL only use data sources for personalization that the user has explicitly consented to and
  SHALL provide an explicit UI listing currently used sources.
    - Acceptance criteria: Consent records present for all personalization inputs; UI shows sources for 100% of
      accounts.
    - Verification method: Consent record audit + UI inspection.

- REQ\-P\-02 The system SHALL minimize stored personal event details by default and SHALL retain raw event content only
  with explicit user consent.
    - Acceptance criteria: By default, raw event content absent from stored datasets for 100% of accounts without
      consent.
    - Verification method: Data inspections and exports.

Assumptions and potential conflicts

- Assumption: Representative labeled datasets for accuracy and travel evaluation will be available prior to GA (size and
  distribution agreed with Product Owner).
- Assumption: External map/traffic providers yield sufficient coverage and latency to meet latency and accuracy targets.
- Conflict: The 2s 99th percentile latency target (REQ\-N\-01) may conflict with REQ\-N\-03 travel accuracy if travel
  estimation requires slow external lookups.
- Conflict: Personalization (REQ\-F\-05/REQ\-F\-06) and data retention/residency (REQ\-N\-05) may conflict—model updates
  that improve quality could be limited for accounts with strict residency or opt\-out settings.
- Assumption: Product Owner will set the confidence threshold used in REQ\-F\-08 prior to verification.

Out\-of\-scope (initial release)

- On\-premise or hardware appliance deployments.
- Passive continual location tracking beyond event location/time data.
- Native voice assistant features or speech recognition integration.
- Support for every global calendar provider at launch (scope limited to prioritized platforms).
- Automated cross\-organisational meeting negotiation (beyond suggesting alternatives to the end user).

Traceability matrix (requirement → stakeholders / goals / priority)

| Req ID     |                 Short description | Stakeholders              | Mapped goals                         | Priority |
|------------|----------------------------------:|---------------------------|--------------------------------------|---------:|
| REQ\-F\-01 | Decision + confidence + rationale | End User, Product Owner   | User outcomes, day\-one scope        |     High |
| REQ\-F\-02 |             Travel time estimates | End User, Ops             | Location integration, day\-one scope |     High |
| REQ\-F\-03 |    Unfeasible detection w/ buffer | End User                  | Accuracy of scheduling               |     High |
| REQ\-F\-04 |                  User preferences | End User, Business        | Personalization, retention           |     High |
| REQ\-F\-05 |          Opt\-out personalization | Privacy Officer, End User | Privacy controls                     |     High |
| REQ\-F\-06 |     Exclude calendars/date ranges | End User                  | Privacy & model correctness          |     High |
| REQ\-F\-07 |            Supported travel modes | Product Owner             | Day\-one functionality               |     High |
| REQ\-F\-08 |  Alternatives when low confidence | End User                  | UX, safety                           |   Medium |
| REQ\-F\-09 |             Export/rectify/delete | Privacy Officer, Legal    | Compliance                           |     High |
| REQ\-N\-01 |       2s @99th percentile latency | End User, Business        | User outcomes                        |     High |
| REQ\-N\-02 |             95% decision accuracy | Product Owner             | Reliability guarantees               |     High |
| REQ\-N\-03 |               Travel time ±10 min | Product Owner             | Travel accuracy                      |   Medium |
| REQ\-N\-04 |              Immutable audit logs | Ops, Legal                | Auditability                         |     High |
| REQ\-N\-05 |          Data residency/retention | Legal, IT                 | Compliance                           |     High |
| REQ\-P\-01 |       Consent for personalization | Privacy Officer           | Privacy controls                     |     High |
| REQ\-P\-02 |        Minimize stored raw events | Privacy Officer           | Privacy by default                   |     High |

Critique for ambiguity and testability, and revisions

- Ambiguity: "Representative dataset" (REQ\-N\-02, REQ\-N\-03) lacks concrete definition. Revision: replace with "
  representative dataset defined and approved by Product Owner, containing at least 10,000 labeled decisions and 2,000
  journeys with ground truth." (Applied above.)
- Ambiguity: "Concise rationale" (REQ\-F\-01) is subjective. Revision: specify "top 3 factors" which was applied.
- Ambiguity: "Configurable buffer" in REQ\-F\-03 not quantified. Revision: specify buffer is a per\-user numeric
  setting (minutes) available in preferences. (Applied via REQ\-F\-04 linkage.)
- Testability concern: External dependencies (map/traffic) affect verifiability. Mitigation: require synthetic and field
  tests; record external provider versions and instrument fallbacks. (Verification methods include both synthetic and
  field checks.)
- Conflict: Latency vs accuracy—explicitly call out performance verification under production‑like conditions; require
  Product Owner signoff if tradeoffs needed.

Revisions summary (applied in requirements above)

- Defined dataset sizes and acceptance thresholds for accuracy and travel evaluation.
- Defined "concise rationale" as "top 3 factors."
- Required per\-user numeric buffer in preferences (linked REQ\-F\-03 ← REQ\-F\-04).
- Required both synthetic and field verification methods to account for external provider variability.

---

### Problem C_1: Functional vs Non-Functional Requirement Classification with AI Awareness

The following criteria apply to this question:

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

---

### Problem C_2: Requirements Satisfiability Reasoning

The following criteria apply to this question:

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

---

### Problem C_3: Requirements Elicitation Question Generation with AI Assistance

> A note on GenAI contribution:
> - Example solutions were written by GPT-5.2, with edits when the context didn't make sense

The following criteria apply to requirements elicitation problems in this question:

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

---

## 3. References

[1] K. Ronanki, C. Berger, and J. Horkoff, “Investigating ChatGPT’s Potential to Assist in Requirements Elicitation
Processes,” Jul. 14, 2023, arXiv: arXiv:2307.07381. doi: 10.48550/arXiv.2307.07381.

[2] Denger, Christian and Olsson, Thomas. Quality Assurance in Requirements Engineering. In Engineering and Managing
Software Requirements, pages 163–185. Springer, 2005.

[3] Génova, Gonzalo and Fuentes, José M and Llorens, Juan and Hurtado, Omar and Moreno, Valentín. A framework to
Measure and Improve the Quality of Textual Requirements. Requirements engineering, 18(1):2541, 2013.

[4] K. Ronanki, B. Cabrero-Daniel, J. Horkoff, and C. Berger, “Requirements Engineering using Generative AI: Prompts and
Prompting Patterns,” Nov. 07, 2023, arXiv: arXiv:2311.03832. doi: 10.48550/arXiv.2311.03832.

[5] S. Santos, T. Breaux, T. Norton, S. Haghighi, and S. Ghanavati, “Requirements Satisfiability with In-Context
Learning,” Apr. 19, 2024, arXiv: arXiv:2404.12576. doi: 10.48550/arXiv.2404.12576.

[6] J. S. Yeow, M. E. Rana, and N. A. Abdul Majid, “An Automated Model of Software Requirement Engineering Using
GPT-3.5,” in 2024 ASU International Conference in Emerging Technologies for Sustainability and Intelligent Systems (
ICETSIS), Jan. 2024, pp. 1746–1755. doi: 10.1109/ICETSIS61505.2024.10459458.

---

