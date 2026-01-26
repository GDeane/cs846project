# Week 4 Evaluation: Requirements

**Authors:** [Gavin Deane, Artemiy Vishnyakov, Savira Umar]

## 1. Evaluation Criteria

This section defines how students can determine whether they solved the example problems correctly.

Criteria vary depending on the specific problem. Each problem's evaluation criteria are detailed in Section 2.

---

## 2. Evaluation specifically for Example Problems

### Problem A_1: Stakeholder Interviews Summary

**Evaluation Description:**  
The evaluation for this task is described in Exercise_A/requirements-analysis/sample-solutions.md.

**Code:**  
N/A

---

### Problem A_2: Real-World Constraints (outside of interviews)

**Evaluation Description:**  
The evaluation for this task is described in Exercise_A/requirements-analysis/sample-solutions.md.

**Code:**  
N/A

---

### Problem A_3: Analysis of Conflicting Requirements

**Evaluation Description:**  
The evaluation for this task is described in Exercise_A/requirements-analysis/sample-solutions.md.

**Code:**  
N/A

---

### Problem A_4: Proposed Solutions

**Evaluation Description:**  
The evaluation for this task is described in Exercise_A/requirements-analysis/sample-solutions.md.

**Code:**  
N/A

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

- REQ\-F\-01 The system SHALL determine for a proposed meeting whether the meeting "fits" the user’s schedule and SHALL return a binary decision (fits / does not fit), a confidence score in the range 0.0–1.0, and a concise rationale summary explaining the top 3 factors that affected the decision.
    - Acceptance criteria: For 1,000 labeled queries from pilot users, the response payload contains decision, confidence, and a rationale field for 100% of queries.
    - Verification method: Integration test against API contract + automated payload validation.

- REQ\-F\-02 The system SHALL estimate end\-to\-end travel time between event locations for supported travel modes and return a travel time (minutes) and uncertainty interval.
    - Acceptance criteria: Travel time value and interval present for 100% of queries where event locations are specified.
    - Verification method: Integration tests using synthetic location pairs; field verification against logged real trips during pilot.

- REQ\-F\-03 The system SHALL report a meeting as "unfeasible" when the estimated travel time plus a configurable buffer causes overlap with another confirmed event.
    - Acceptance criteria: For test cases where travel+buffer causes overlap, system reports "unfeasible" in 100% of cases.
    - Verification method: Deterministic unit/integration tests using synthetic calendars.

- REQ\-F\-04 The system SHALL allow the user to configure personal scheduling preferences (preferred travel modes, protected time windows, scheduling aggressiveness) and SHALL use those preferences in every decision.
    - Acceptance criteria: Preference change reflected in subsequent decisions within one session for 100% of changes.
    - Verification method: End\-to\-end functional test altering preferences and validating decision outputs.

- REQ\-F\-05 The system SHALL provide a user control to opt\-out of model personalization and SHALL not use opt\-out accounts for personalization updates.
    - Acceptance criteria: For accounts that opt out, no personalization artifacts for that account appear in model update datasets.
    - Verification method: Data pipeline audit and sampling of training inputs; pipeline unit tests.

- REQ\-F\-06 The system SHALL allow users to explicitly exclude specific calendars or named date ranges (e.g., vacations, anomalous weeks) from personalization and SHALL not use excluded items for model updates.
    - Acceptance criteria: Excluded calendars/date ranges not present in any personalization input snapshots for 100% of exclusions.
    - Verification method: Data export + automated verification of training dataset membership.

- REQ\-F\-07 The system SHALL support at launch the travel modes: walking, driving, public transit, and biking.
    - Acceptance criteria: For each supported mode, travel time estimate returned for at least 95% of valid location pairs in synthetic tests.
    - Verification method: Mode coverage integration tests.

- REQ\-F\-08 The system SHALL provide alternatives (proposed meeting time suggestions) when confidence is below a configurable threshold and SHALL not auto\-schedule without explicit user consent.
    - Acceptance criteria: When confidence < threshold, alternatives returned 100% of time and no auto\-scheduling executed.
    - Verification method: Workflow tests simulating low confidence scenarios.

- REQ\-F\-09 The system SHALL expose per\-account controls to export, rectify, and request deletion of account data and SHALL complete deletion within 30 days of a validated request for accounts under jurisdictions that require it.
    - Acceptance criteria: Export, rectification, and deletion operations complete and logged; deletion completed within 30 days where applicable.
    - Verification method: Manual/automated verification of CRUD operations; audit log inspection.

Non\-functional requirements

- REQ\-N\-01 The system SHALL respond to an interactive scheduling query (decision + rationale) within 2 seconds at the 99th percentile for the configured production workload.
    - Acceptance criteria: Measured latency ≤ 2s at 99th percentile over a 7\-day rolling production load test.
    - Verification method: Synthetic load tests and production telemetry.

- REQ\-N\-02 The system SHALL achieve at least 95% accuracy on labeled test datasets for the binary "fits/does not fit" decision prior to GA.
    - Acceptance criteria: Validation run against representative dataset of at least 10,000 labeled events yields ≥95% accuracy.
    - Verification method: Offline model evaluation with documented dataset and test harness.

- REQ\-N\-03 The system SHALL achieve travel time estimates within ±10 minutes for journeys under 90 minutes in at least 90% of evaluated cases on a validated test set.
    - Acceptance criteria: Evaluation on at least 2,000 real or high‑fidelity synthetic journeys meets threshold.
    - Verification method: Offline evaluation; field verification in pilot.

- REQ\-N\-04 The system SHALL maintain immutable audit records for automated scheduling decisions and user overrides including timestamp, inputs summary, decision, confidence, and user action for at least the retention period configured per region.
    - Acceptance criteria: Audit records available and queryable for 100% of automated decisions in test period.
    - Verification method: Audit log queries + spot checks.

- REQ\-N\-05 The system SHALL support per\-region configurable data retention and data residency policies and SHALL enforce account\-level residency settings.
    - Acceptance criteria: Data residency/retention rules applied to test accounts and verified by data locality checks.
    - Verification method: Deployment validation and automated checks.

Privacy and security requirements

- REQ\-P\-01 The system SHALL only use data sources for personalization that the user has explicitly consented to and SHALL provide an explicit UI listing currently used sources.
    - Acceptance criteria: Consent records present for all personalization inputs; UI shows sources for 100% of accounts.
    - Verification method: Consent record audit + UI inspection.

- REQ\-P\-02 The system SHALL minimize stored personal event details by default and SHALL retain raw event content only with explicit user consent.
    - Acceptance criteria: By default, raw event content absent from stored datasets for 100% of accounts without consent.
    - Verification method: Data inspections and exports.

Assumptions and potential conflicts

- Assumption: Representative labeled datasets for accuracy and travel evaluation will be available prior to GA (size and distribution agreed with Product Owner).
- Assumption: External map/traffic providers yield sufficient coverage and latency to meet latency and accuracy targets.
- Conflict: The 2s 99th percentile latency target (REQ\-N\-01) may conflict with REQ\-N\-03 travel accuracy if travel estimation requires slow external lookups.
- Conflict: Personalization (REQ\-F\-05/REQ\-F\-06) and data retention/residency (REQ\-N\-05) may conflict—model updates that improve quality could be limited for accounts with strict residency or opt\-out settings.
- Assumption: Product Owner will set the confidence threshold used in REQ\-F\-08 prior to verification.

Out\-of\-scope (initial release)

- On\-premise or hardware appliance deployments.
- Passive continual location tracking beyond event location/time data.
- Native voice assistant features or speech recognition integration.
- Support for every global calendar provider at launch (scope limited to prioritized platforms).
- Automated cross\-organisational meeting negotiation (beyond suggesting alternatives to the end user).

Traceability matrix (requirement → stakeholders / goals / priority)

| Req ID | Short description | Stakeholders | Mapped goals | Priority |
|---|---:|---|---|---:|
| REQ\-F\-01 | Decision + confidence + rationale | End User, Product Owner | User outcomes, day\-one scope | High |
| REQ\-F\-02 | Travel time estimates | End User, Ops | Location integration, day\-one scope | High |
| REQ\-F\-03 | Unfeasible detection w/ buffer | End User | Accuracy of scheduling | High |
| REQ\-F\-04 | User preferences | End User, Business | Personalization, retention | High |
| REQ\-F\-05 | Opt\-out personalization | Privacy Officer, End User | Privacy controls | High |
| REQ\-F\-06 | Exclude calendars/date ranges | End User | Privacy & model correctness | High |
| REQ\-F\-07 | Supported travel modes | Product Owner | Day\-one functionality | High |
| REQ\-F\-08 | Alternatives when low confidence | End User | UX, safety | Medium |
| REQ\-F\-09 | Export/rectify/delete | Privacy Officer, Legal | Compliance | High |
| REQ\-N\-01 | 2s @99th percentile latency | End User, Business | User outcomes | High |
| REQ\-N\-02 | 95% decision accuracy | Product Owner | Reliability guarantees | High |
| REQ\-N\-03 | Travel time ±10 min | Product Owner | Travel accuracy | Medium |
| REQ\-N\-04 | Immutable audit logs | Ops, Legal | Auditability | High |
| REQ\-N\-05 | Data residency/retention | Legal, IT | Compliance | High |
| REQ\-P\-01 | Consent for personalization | Privacy Officer | Privacy controls | High |
| REQ\-P\-02 | Minimize stored raw events | Privacy Officer | Privacy by default | High |

Critique for ambiguity and testability, and revisions

- Ambiguity: "Representative dataset" (REQ\-N\-02, REQ\-N\-03) lacks concrete definition. Revision: replace with "representative dataset defined and approved by Product Owner, containing at least 10,000 labeled decisions and 2,000 journeys with ground truth." (Applied above.)
- Ambiguity: "Concise rationale" (REQ\-F\-01) is subjective. Revision: specify "top 3 factors" which was applied.
- Ambiguity: "Configurable buffer" in REQ\-F\-03 not quantified. Revision: specify buffer is a per\-user numeric setting (minutes) available in preferences. (Applied via REQ\-F\-04 linkage.)
- Testability concern: External dependencies (map/traffic) affect verifiability. Mitigation: require synthetic and field tests; record external provider versions and instrument fallbacks. (Verification methods include both synthetic and field checks.)
- Conflict: Latency vs accuracy—explicitly call out performance verification under production‑like conditions; require Product Owner signoff if tradeoffs needed.

Revisions summary (applied in requirements above)

- Defined dataset sizes and acceptance thresholds for accuracy and travel evaluation.
- Defined "concise rationale" as "top 3 factors."
- Required per\-user numeric buffer in preferences (linked REQ\-F\-03 ← REQ\-F\-04).
- Required both synthetic and field verification methods to account for external provider variability.

---

#### 2. References

[1] K. Ronanki, C. Berger, and J. Horkoff, “Investigating ChatGPT’s Potential to Assist in Requirements Elicitation
Processes,” Jul. 14, 2023, arXiv: arXiv:2307.07381. doi: 10.48550/arXiv.2307.07381.

[2] Denger, Christian and Olsson, Thomas. Quality Assurance in Requirements Engineering. In Engineering and Managing
Software Requirements, pages 163–185. Springer, 2005.

[3] Génova, Gonzalo and Fuentes, José M and Llorens, Juan and Hurtado, Omar and Moreno, Valentín. A framework to
Measure and Improve the Quality of Textual Requirements. Requirements engineering, 18(1):2541, 2013.

---

### Problem C_1: Functional vs Non-Functional Requirement Classification with AI Awareness

**Evaluation Description:**  
The evaluation for this task is described in Exercise_C/evaluation.md.

**Code:**  
N/A

---

### Problem C_2: Requirements Satisfiability Reasoning

**Evaluation Description:**  
The evaluation for this task is described in Exercise_C/evaluation.md.

**Code:**  
N/A

---

### Problem C_3: Requirements Elicitation Question Generation with AI Assistance

**Evaluation Description:**  
The evaluation for this task is described in Exercise_C/evaluation.md.

**Code:**  
N/A

---

## 3. References

> References for the evaluation criteria are provided within the respective Exercise folders.

---

