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
>
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

> Note: These requirements were created using GitHub Copilot (GPT-5-Mini)

##### Context Prompt (No Guidelines)

Please give 10-15 structured requirements based on this problem:

###### 1. Problem description

Given the description of the problem domain and the following questionnaire, use your LLM (GPT-5 mini) to elicit a set
of 10-15 structured requirements.

You would want to feel comfortable:

- 1: Showing these requirements to your boss.
- 2: presenting this list of requirements to a group of stakeholders in order to elicit preferences.
- 3: Agreeing to implement this set of requirements in a contract if the client agreed to them.

_There is no particular submission template for this question. You may structure your requirements as you wish, so long
as it is clear and easy to parse._

This problem takes heavy inspiration from the study conducted by Ronaki et al. (2023) [1].

###### 2. Problem domain

A client wants to build a system that connects an AI personal assistant to an end user's calendar.

Not only should this AI system know what events are when, but the AI should also have awareness of the location of each
event so that the AI can point out when travel times may be tight or unfeasible.

Quote from (fictional) client: "That way, whenever the end user needs to book a meeting, they can simply ask their
assistant whether this works well with my schedule."

In addition, this personal assistant should get better over time as it gets to know what kind of time you prefer not to
be booked or what travel modes you use!

The client considers that privacy of user data could be a potential concern in this case. "I don't want everything about
a user's life to end up exposed on the internet because of our app."

###### 3. Questionnaire

Here are some (not-exhaustive) questions to aid in requirements elicitation:

**Q1**: What kind of correctness and reliability guarantees must the system provide? That is, how often is it acceptable
for the system to make a mistake about whether an event fits or travel time.

**Q2**: Are there any categories of data the system should not learn from? (shared calendars, unusually busy weeks).

**Q3**: How explainable should the system be? Should it give a reasoning for what criteria it used to make its decision?
How in depth should this reasoning be?

**Q4**: What places in the world would you want this system to be deployed? Different countries have different privacy
laws (e.g. the right to be forgotten under the GDPR in the EU).

**Q5**: Should this system to be a piece of hardware or an application?

##### GitHub Copilot Output:

Requirements (12 total)

- Req-01 — Function (Must)
  - Statement: The system shall authenticate and authorize users using OAuth 2.0 (or equivalent) for each calendar provider before reading or writing calendar data.
  - Rationale: Secure, least-privilege access to user calendars and clear consent flow required by providers and regulators.
  - Acceptance criteria: OAuth flow works for Google Calendar and Microsoft Outlook in tests; unauthorized calls return 401; consent screen shows requested scopes.
  - Inputs / Outputs: Input: user-initiated connect request; Output: access token + refresh token (stored per privacy policy).
  - Error modes: Missing/expired tokens produce a clear UI error and re-authentication prompt.
- Req-02 — Function (Must)
  - Statement: The system shall read calendar events (start, end, title, location, attendees, timezone) and maintain a local, minimal event index for scheduling decisions.
  - Rationale: Accurate scheduling decisions require event metadata and time zone awareness.
  - Acceptance criteria: For a linked calendar, 99% of events fetched include a parsable start/end/timezone and location if present; indexing completes within a reasonable time for 1 year of events (e.g., <30s for 10k events).
  - Inputs / Outputs: Input: calendar API responses; Output: normalized events in local index.
  - Error modes: Unparseable events flagged and surfaced to user for fix.
- Req-03 — Function (Must)
  - Statement: The system shall consider event location and compute travel-time estimates between locations and the user's current (or home/office) location using a configurable travel-time provider (e.g., map API) and user-selected transport modes.
  - Rationale: Travel-aware scheduling needs reliable travel-time estimates to detect tight or infeasible bookings.
  - Acceptance criteria: For 95% of test routes, predicted travel time is within ±15% of the provider’s baseline estimate or within ±10 minutes, whichever is larger; travel-time provider failures fall back to conservative default heuristics.
  - Inputs / Outputs: Input: event locations, user transport mode, departure time; Output: travel time estimate, route confidence score.
  - Error modes: If location missing or provider fails, system marks route as "unknown" and asks user for confirmation.
- Req-04 — Function (Must)
  - Statement: The assistant shall, on user request (e.g., "Can I book at 3pm?"), determine whether a proposed event fits the calendar and provide a clear recommendation: Fit / Tight / Does not fit.
  - Rationale: Primary user need is to get a simple, actionable answer about whether a meeting can be scheduled.
  - Acceptance criteria: Recommendation produced for 100% of queries within SLA (see Req-09). Labeling is consistent with configured thresholds and accompanied by confidence.
  - Inputs / Outputs: Input: proposed event time, duration, location; Output: recommendation with reasoning summary and confidence score.
  - Error modes: Low-confidence results produce an explicit “uncertain” outcome and suggested follow-up questions.
- Req-05 — Function (Should)
  - Statement: The system shall present a short, human-readable explanation for each decision that includes (a) key criteria used (conflicting events, travel time, user preferences), (b) estimated travel time and margin, and (c) a numeric confidence score.
  - Rationale: Stakeholders need explainability to trust the assistant and to adjudicate edge cases.
  - Acceptance criteria: Explanations are generated for 100% of decisions; user testing shows ≥80% of users find explanations "sufficient to act" in a usability sample.
  - Inputs / Outputs: Input: decision context; Output: 1–3 sentence explanation + confidence score + link to "details".
  - Error modes: If the model cannot explain, show a fallback structured rationale (e.g., checklist of failed/passing checks).
- Req-06 — Nonfunctional – Accuracy / Reliability (Must)
  - Statement: For scheduling decisions, the system shall achieve a decision accuracy (match to ground-truth acceptability in evaluation dataset) of at least 95% under normal conditions; travel-time predictions should meet Req-03.
  - Rationale: Stakeholders require strong correctness guarantees before relying on automated scheduling advice.
  - Acceptance criteria: Test suite evaluation demonstrates ≥95% decision accuracy on representative dataset; continuous monitoring alerts if rolling 7-day accuracy drops below 92%.
  - Inputs / Outputs: Input: evaluation dataset; Output: metrics and alerts.
  - Error modes: Degradation triggers restricted-mode recommendations (e.g., require manual confirmation).
- Req-07 — Nonfunctional – Latency (Should)
  - Statement: The system shall provide an initial response to user scheduling queries within 3 seconds 90% of the time and within 5 seconds 99% of the time when no heavy external API (e.g., route calculation) is required.
  - Rationale: Fast responses improve usability and adoption.
  - Acceptance criteria: Load testing shows the latency targets met at expected per-user load (specify in SLO).
  - Inputs / Outputs: N/A (performance metric).
  - Error modes: If external API calls prolong response, show progress indicator and allow "get best-effort recommendation later".
- Req-08 — Nonfunctional – Privacy & Data Minimization (Must)
  - Statement: The system shall only store the minimal data needed for operation (event metadata, user preferences, model personalization vectors) and shall provide user controls to opt-out of personalization and to delete stored data; sensitive event content (notes) must be redacted by default unless explicitly permitted by user.
  - Rationale: Minimize privacy risk and comply with regulatory concerns.
  - Acceptance criteria: UI provides explicit toggle for personalization and a "delete all data" button; deletion completes and an audit log confirms removal within 24 hours.
  - Inputs / Outputs: Input: user toggles, delete requests; Output: confirmation + audit record.
  - Error modes: Failed deletion produces retry and admin flagging.
- Req-09 — Nonfunctional – Regional Data Compliance & Residency (Must)
  - Statement: The system shall support region-specific data handling: configurable data residency targets and compliance measures for GDPR, CCPA, and other applicable laws; users shall be able to request data export or erasure per region rules.
  - Rationale: Different jurisdictions require different controls (e.g., right to be forgotten).
  - Acceptance criteria: Export and deletion workflows comply with regional timelines (e.g., GDPR: deletion within 30 days), and region flags are enforced for storage and processing.
  - Inputs / Outputs: Input: user region; Output: data stored/processed in region-specific stores or pseudonymized pipelines.
  - Error modes: Cross-border transfer attempts are blocked or logged until consent obtained.
- Req-10 — Function – Learning & Personalization (Should)
  - Statement: The system shall learn user scheduling preferences over time (e.g., preferred buffer times before/after meetings, no-booking windows) using on-device or privacy-preserving federated learning; the user must be able to review and opt-out.
  - Rationale: Personalization improves recommendation relevance while addressing privacy concerns.
  - Acceptance criteria: After 30 days of opt-in usage, personalized recommendations increase acceptance rate by measurable amount (e.g., +10% relative to baseline) in pilot; opt-out immediately freezes personalization updates.
  - Inputs / Outputs: Input: user confirmations, historical event patterns; Output: preference model and effect on recommendations.
  - Error modes: If model updates degrade performance, rollback to previous model.
- Req-11 — Privacy Safeguard — Training Data Exclusions (Must)
  - Statement: The system shall not use specified categories of data for training/personalization unless explicitly permitted by the user (e.g., shared calendars flagged as "business-shared", unusually busy weeks flagged by user).
  - Rationale: Users may not want shared or anomalous periods influencing personalization.
  - Acceptance criteria: UI and API allow users to tag calendars or date ranges as excluded; training pipeline respects exclusion flags and includes tests to verify.
  - Inputs / Outputs: Input: exclusion flags; Output: filtered training examples.
  - Error modes: If exclusions are ignored, produce audit failure alarm.
- Req-12 — Security — Data Protection (Must)
  - Statement: The system shall encrypt all user data at rest (AES-256 or equivalent) and in transit (TLS 1.2+/HTTPS). Access to production secrets must be role-based and logged.
  - Rationale: Protect user data and meet enterprise security expectations.
  - Acceptance criteria: Penetration test finds no plaintext storage of private calendar content; all endpoints use TLS; audit logs show role-based access records.
  - Inputs / Outputs: N/A (security controls).
  - Error modes: Key rollover or encryption failure triggers fail-closed (no data exposure).
- Req-13 — Function – Integration & Write Safety (Should)
  - Statement: When the assistant writes changes (creates/updates events), it shall require explicit user confirmation and show the exact calendar and scope being modified; an "undo" action for 10 minutes shall be available.
  - Rationale: Prevent accidental or incorrect modifications to user calendars.
  - Acceptance criteria: Write actions present a confirmation UI; undo restores prior state consistently in tests.
  - Inputs / Outputs: Input: user confirmation; Output: calendar API write + undo token.
  - Error modes: Failed undo logs the issue and alerts support.
- Req-14 — Nonfunctional – Deployment Form Factor (Should)
  - Statement: The system shall be delivered as a software application with web and mobile clients and an API for enterprise integration; optional edge/hardware integration (e.g., device with local assistant) may be supported via a separate deployment profile but is out-of-scope for initial release.
  - Rationale: Applications maximize reach and meet typical user expectations; hardware adds complexity and regulatory concerns.
  - Acceptance criteria: Web and mobile clients available, documented API; hardware integration documented as "future work".
  - Inputs / Outputs: N/A.
  - Error modes: N/A.
- Req-15 — Nonfunctional – Auditing & Transparency (Should)
  - Statement: The system shall keep an auditable log of scheduling decisions (what inputs produced a decision, timestamp, model version, and whether personalization was applied) accessible to the user and to authorized admins for debugging and compliance.
  - Rationale: Auditing supports explainability, debugging, and compliance investigations.
  - Acceptance criteria: Logs are available in user settings (last 90 days) and admin interface; exportable JSON for compliance requests.
  - Inputs / Outputs: Input: decision events; Output: tamper-evident logs with metadata.
  - Error modes: Log retention and tamper controls must be enforced; loss triggers alert.

##### Context Prompt (With Guidelines)

You are a senior systems engineer following IEEE 29148.

For the problem I am giving you, I want you to do the following

- Produce functional and non-functional requirements using "The system SHALL..."
- Each requirement must be atomic, testable, and free of design decisions
- Include acceptance criteria and verification method
- List assumptions and potential conflicts
- Identify out-of-scope items
- Provide a traceability matrix

Finally, critique the requirements for ambiguity and testability and revise as needed.

Here is the problem description:

###### 1. Problem description

Given the description of the problem domain and the following questionnaire, use your LLM (GPT-5 mini) to elicit a set
of 10-15 structured requirements.

You would want to feel comfortable:

- 1: Showing these requirements to your boss.
- 2: presenting this list of requirements to a group of stakeholders in order to elicit preferences.
- 3: Agreeing to implement this set of requirements in a contract if the client agreed to them.

_There is no particular submission template for this question. You may structure your requirements as you wish, so long
as it is clear and easy to parse._

This problem takes heavy inspiration from the study conducted by Ronaki et al. (2023) [1].

###### 2. Problem domain

A client wants to build a system that connects an AI personal assistant to an end user's calendar.

Not only should this AI system know what events are when, but the AI should also have awareness of the location of each
event so that the AI can point out when travel times may be tight or unfeasible.

Quote from (fictional) client: "That way, whenever the end user needs to book a meeting, they can simply ask their
assistant whether this works well with my schedule."

In addition, this personal assistant should get better over time as it gets to know what kind of time you prefer not to
be booked or what travel modes you use!

The client considers that privacy of user data could be a potential concern in this case. "I don't want everything about
a user's life to end up exposed on the internet because of our app."

###### 3. Questionnaire

Here are some (not-exhaustive) questions to aid in requirements elicitation:

**Q1**: What kind of correctness and reliability guarantees must the system provide? That is, how often is it acceptable
for the system to make a mistake about whether an event fits or travel time.

**Q2**: Are there any categories of data the system should not learn from? (shared calendars, unusually busy weeks).

**Q3**: How explainable should the system be? Should it give a reasoning for what criteria it used to make its decision?
How in depth should this reasoning be?

**Q4**: What places in the world would you want this system to be deployed? Different countries have different privacy
laws (e.g. the right to be forgotten under the GDPR in the EU).

**Q5**: Should this system to be a piece of hardware or an application?

##### GitHub Copilot Output:

Requirements (IDs Req-01 .. Req-14)

- Functional requirements
  - Req-01 — Authentication & Authorization (Functional, Must)
    - Statement: The system SHALL authenticate and authorize a user before reading or writing that user's calendar data.
    - Acceptance criteria: Any request to read or write calendar data without a valid authenticated session is rejected with an HTTP 401/403-equivalent error; login flow completes successfully for supported providers.
    - Verification method: Automated integration tests that attempt calendar access with and without valid credentials; penetration test to confirm unauthorized access is denied.
  - Req-02 — Calendar Fetch & Normalization (Functional, Must)
    - Statement: The system SHALL fetch a user's calendar events (start time, end time, title, attendees, timezone, and location if present) and normalize them into a local minimal index for scheduling decisions.
    - Acceptance criteria: For a representative test calendar set (1 year, up to 10k events), normalization succeeds within a defined processing window (e.g., initial sync ≤ 30s for 10k events) and at least 99% of events include parsable start/end/timezone fields.
    - Verification method: End-to-end integration tests using synthetic provider data and a perf test to measure sync time and parsing success rate.
  - Req-03 — Travel-Time Estimation (Functional, Must)
    - Statement: The system SHALL compute an estimated travel time between two event locations (or between a user location and an event) given a user-selected transport mode and scheduled departure time.
    - Acceptance criteria: For 95% of test routes in the evaluation set, estimated travel time is within ±15% of the baseline route-provider estimate or within ±10 minutes (whichever is larger); when location is missing, result is flagged as "unknown."
    - Verification method: Automated route test harness comparing system estimates to a ground-truth route provider across representative city/route samples.
  - Req-04 — Fit/Tight/Does-not-fit Recommendation (Functional, Must)
    - Statement: On user request with a proposed event (time, duration, optional location), the system SHALL return one of three recommendations: "Fits", "Tight", or "Does not fit", and include a confidence score.
    - Acceptance criteria: Recommendation produced for 100% of valid queries within SLA; labels follow configured thresholds and confidence ∈ [0,1] is returned.
    - Verification method: Functional tests with representative scenarios verifying expected label output and confidence presence; unit tests for threshold logic.
  - Req-05 — Short Human-Readable Explanation (Functional, Should)
    - Statement: For each scheduling recommendation, the system SHALL provide a concise (1–3 sentence) human-readable explanation listing the primary factors that led to the recommendation (conflicting events, travel time, user preferences).
    - Acceptance criteria: Explanations are returned for 100% of recommendations and include at least the top two contributing factors; user study (pilot sample) shows ≥80% of users find explanation sufficient to act.
    - Verification method: Automated checks ensure explanation field is non-empty and contains expected keys; small user trial for subjective acceptance.
  - Req-06 — Write Safety for Calendar Changes (Functional, Should)
    - Statement: When the system writes (creates/updates/deletes) calendar events, the system SHALL require explicit user confirmation and present the exact calendar and change details before performing the write; an undo action SHALL be available for at least 10 minutes.
    - Acceptance criteria: Any write request without prior explicit confirmation is rejected; undo restore succeeds in tests for standard cases within 10 minutes.
    - Verification method: Integration tests validating confirmation flow and undo behavior; instrumentation logs verifying UI prompts.
- Non‑functional requirements
  - Req-07 — Decision Accuracy (Non‑functional, Must)
    - Statement: The system SHALL achieve at least 95% decision accuracy against a specified evaluation dataset for determining whether a proposed event "fits" under normal conditions.
    - Acceptance criteria: Continuous evaluation shows ≥95% accuracy on the approved evaluation dataset; rolling 7‑day accuracy does not fall below 92% without triggering alerts.
    - Verification method: Offline evaluation pipeline that scores decisions against labeled dataset and a monitoring alert if rolling accuracy drops below threshold.
  - Req-08 — Latency (Non‑functional, Should)
    - Statement: The system SHALL respond to scheduling queries (excluding heavy external route calculations) within 3 seconds for 90% of requests and within 5 seconds for 99% of requests under expected load.
    - Acceptance criteria: Load testing demonstrates the stated latency percentiles for the projected per-user load.
    - Verification method: Performance tests (load/perf harness) and production telemetry measuring p90 and p99 latencies.
  - Req-09 — Privacy & Data Minimization (Non‑functional, Must)
    - Statement: The system SHALL store only the minimal data required for operation (event metadata, preferences, and any opt‑in personalization vectors), provide user controls to opt out of personalization, and redact sensitive event content (notes) by default unless explicitly permitted by the user.
    - Acceptance criteria: UI provides explicit opt-out toggle and delete/export options; storage audits verify no plaintext retention of redacted fields; data deletion completes within 24 hours for user-initiated delete requests.
    - Verification method: Security audit, periodic storage scans, and functional tests for opt-out and deletion flows.
  - Req-10 — Training & Personalization Opt‑In/Exclusion Controls (Non‑functional, Must)
    - Statement: The system SHALL allow the user to opt‑in to personalization and to mark calendars or date ranges as excluded from personalization/training; excluded data SHALL not be used for model training or personalization.
    - Acceptance criteria: Exclusion flags are persisted and honored by training/personalization pipelines verified by unit tests and a training-data audit.
    - Verification method: Test pipeline filters that assert excluded samples are not present in training batches; audit log demonstrating filter enforcement.
  - Req-11 — Data Residency and Compliance (Non‑functional, Must)
    - Statement: The system SHALL support region-specific data handling including export and erasure workflows that meet applicable regulations (e.g., GDPR, CCPA) for the regions the customer requests support for.
    - Acceptance criteria: Export/erasure workflows complete within policy timelines (e.g., GDPR export/erasure within 30 days where applicable); region flags are enforced for storage and processing.
    - Verification method: Legal/compliance testing and automated verification of storage location metadata for sample accounts.
  - Req-12 — Security — Encryption & Access Control (Non‑functional, Must)
    - Statement: The system SHALL encrypt user data at rest and in transit and SHALL enforce role-based access controls for production secrets and sensitive operations.
    - Acceptance criteria: All storage endpoints use encryption; TLS enforced for network traffic; access logs show role-based access enforcement.
    - Verification method: Security scans, config checks, and privileged-access audit logs.
  - Req-13 — Auditing & Explainability Metadata (Non‑functional, Should)
    - Statement: The system SHALL record an auditable log for each scheduling decision including inputs, timestamp, model/pipeline version, and whether personalization was applied; the user SHALL be able to view their recent decision log (last 90 days).
    - Acceptance criteria: Decision logs exist for 100% of decisions and user UI exposes last 90 days; exportable JSON is available.
    - Verification method: Integration tests for log creation and UI retrieval; spot audits of log completeness.
  - Req-14 — Availability & Degraded Mode (Non‑functional, Should)
    - Statement: The system SHALL provide a best-effort degraded recommendation when external dependencies (e.g., routing provider) are unavailable and SHALL present the user with a clear indication of reduced confidence.
    - Acceptance criteria: When an external dependency fails in test, system returns a best-effort recommendation or explicit "unknown/uncertain" and provides degraded-confidence indicator.
    - Verification method: Chaos/failure tests that simulate dependency outages and validate outputs and UI indicators.

##### Result:

1. Abstraction: Set 2 wins

- The first set fails at abstraction by often specifying implementation details (e.g. "OAuth 2.0)
- The second set simply states "authenticate and authorize" without implementation details

2. Atomicity: Neither is perfect, both have several 'ands' in their requirements

3. Consistency: Both sets are highly consistent. No obvious contradictions

4. Correctness: Set 1 wins

- The first set includes rationale, making it easy to verify the requirement reflects user-intended behavior.

5. Unambiguity: Set 2 wins

- Specifying a verification method under each requirement makes it clear what a requirement must fulfill

6. Understandability: written for different audiences

- The rationale section in set 1 makes it easier to understand for stakeholders
- The formality of set 2 makes it easier to understand for engineers and QA testers

7. Feasibility: Both sets are sketchy

- Both sets include 100% requirements, which are dangerous.

Overall, the main difference between these requirements is the audience they are written for.

- Set 1 is better for stakeholder communication
- Set 2 is more useful for engineers and QA testers

---

### Problem C_1: Functional vs Non-Functional Requirement Classification with AI Awareness

---

> A Note on GenAI Contribution, problem_C1 solutions was written by me using GitHub Copilot (GPT-5-Mini) with the following prompt:,
> This evaluation compares baseline prompting versus guideline-based prompting and analyzes their effect on correctness, reasoning quality, and reproducibility.

> This problem takes inspiration from a study conducted by Ronaki et al. (2023).

## 1. Evaluation Criteria

This problem is evaluated on three dimensions:

1. Correct classification of Functional vs Non-Functional requirements
2. Clarity and reasoning of justification
3. Ability to produce stable, structured outputs using improved prompting

Students must demonstrate both conceptual understanding and effective use of prompting strategies.

### Task 1 — Requirement Classification

#### Expected Correct Classification

A correct solution must classify:

**Functional Requirements (FR)**

- Appointment booking
- Appointment reminders

These describe **what the system does**.

**Non-Functional Requirements (NFR)**

- Encryption
- Response time (2 seconds)
- Regulatory compliance
- Usability

These describe how well or under what constraintsthe system operates.

A good solution must clearly distinguish between system behavior and quality constraints.

### Evaluation Levels

**Good Solution**

A good solution:

- Correctly classifies all requirements
- Provides clear one-sentence justifications
- Shows understanding of FR vs NFR distinction
- Uses a consistent structured format
- Produces stable output when evaluated with improved guidelines

**Satisfactory Solution **

A satisfactory solution:

- Classifies most requirements correctly
- Provides partial or unclear reasoning
- Shows basic understanding but lacks precision
- Format may be inconsistent

**Bad Solution**

A bad solution:

- Misclassifies multiple requirements
- Shows no conceptual understanding
- Provides weak or missing justification
- Produces unstable or unstructured output

### Task 2 — Human Oversight Reflection

**Good Solution**

A good solution must explain why AI requires human review, such as:

- AI may misinterpret ambiguous wording
- AI lacks domain or stakeholder context
- AI can produce inconsistent results
- Human judgment is required for accountability

The explanation should connect to real risks in requirements engineering.

**Bad Solution**

A bad solution:

- Claims AI is always correct
- Says human review is unnecessary
- Provides vague or unsupported reasoning

**Reproducibility and Output Stability**

This evaluation also considers whether prompting techniques improve formatting consistency and reproducibility.

## 2. Example Solution Set

**Context Prompt (No Guidelines)**

**Baseline prompt:**

> Classify each requirement as Functional Requirement (FR) or Non-Functional Requirement (NFR) and justify briefly. Then explain why AI-assisted classification requires human review.

**Observed Output Characteristics**

- Correct classification
- Reasonable justifications
- Extra narration and progress messages
- Inconsistent formatting

---

**GitHub Copilot Output**

> Progress: Extracted 6 requirements from C1_problem_test.txt; now classifying them.

- R1: Functional Requirement (FR): Enables a specific system capability—patients booking appointments is a core function.
- R2: Non-Functional Requirement (NFR): Describes a security property (data encryption) that constrains how data is handled, not a user-facing function.
- R3: Functional Requirement (FR): Specifies an action the system must perform (sending reminders) — a concrete service.
- R4: Non-Functional Requirement (NFR): A performance requirement (response time ≤ 2s), which defines quality of service.
- R5: Non-Functional Requirement (NFR): Compliance is a regulatory/constraint requirement governing behavior and processes, not a feature.
- R6: Non-Functional Requirement (NFR): Usability/accessibility requirement (interface quality for elderly users), a quality attribute.

**Human review explanation:**  
I classification can misinterpret stakeholder intent, ambiguous wording, or domain-specific constraints; humans provide context, prioritize trade-offs, and validate legal/regulatory implications. Final decisions often need stakeholder judgment and acceptance criteria that only people can supply.

**Context Prompt (With Guidelines)**

Structured prompt using task-tag isolation:
<task>
Classify R1–R6 as FR or NFR and justify each in one sentence.
Then explain why AI-assisted classification needs human review.
</task>
Observed Output Characteristics

- Correct classification
- Clear, concise justifications
- Strict adherence to required format
- No extraneous narration

**GitHub Copilot Output**

- R1:1: FR — Allows patients to perform a concrete user-facing action (booking appointments), which defines a system capability.
- R2: NFR — Specifies a security/quality constraint (encryption of stored patient data) rather than a user-visible function.
- R3: FR — Requires the system to perform a specific service (sending reminders via email and SMS), which is a functional behavior.
- R4: NFR — Defines a performance/quality target (response time ≤ 2 seconds), describing how the system must behave under conditions.
- R5: NFR — Imposes regulatory/compliance constraints on data handling and processes, not a standalone feature.
- R6: NFR — Describes a usability/accessibility quality (interface suitability for elderly patients), which is a non-functional attribute.

**Human oversight:**  
AI can misinterpret ambiguous wording, stakeholder intent, or domain-specific/legal nuances and may overlook priority or trade-off considerations; human reviewers add contextual judgment, validate acceptance criteria, and resolve ambiguities before requirements are finalized.

## 3. Comparison and Analysis

Both prompts produced correct classifications and similar reasoning quality.

The primary difference lies in formatting stability:

- Baseline prompting introduced variability and conversational text
- Structured prompting produced consistent, reproducible outputs

This improvement is primarily due to Guideline 12 (task-tag structured prompting).

Guideline relevance:

- G12 improves evaluation reproducibility
- G11 is not applicable to classification tasks
- G6 is irrelevant outside transcript analysis

Structured prompting improves evaluation reliability without significantly changing reasoning performance.

## 4. Integration into Updated Guidelines

This experiment supports the adoption of structured task-tag prompting as part of our updated requirements engineering guidelines.

Specifically:

- Task-tag prompting (Guideline 12) should be required for structured classification and evaluation exercises to enforce consistent output format and reduce output drift.
- Prompts should include explicit output templates to improve reproducibility and comparability across runs.
  -Guidelines should clearly document when they are task-specific to prevent inappropriate overuse.

This experiment also clarifies scope boundaries:

- Guideline 11 applies only to measurable requirement writing tasks and is not relevant to classification exercises.
- Guideline 6 applies only to transcript analysis and multi-speaker contexts.

These refinements promote selective and context-aware guideline application while improving evaluation clarity and reproducibility.

## Result Summary

**Correctness:** Tie  
Both baseline and guided outputs classify R1–R6 correctly (FR vs NFR).

**Reasoning Quality:** Tie  
Both provide clear 1-sentence explanations that correctly justify FR (“what the system does”) vs NFR (“constraints/quality”).

**Output Stability / Reproducibility:** **Set 2 wins (Guided Prompt)**  
The baseline output includes extra narration (e.g., “Progress: … extracted requirements…”), which makes comparison harder.
The guided output follows the required template exactly and has no extra text

**Human Oversight Reflection:** Tie  
Both explain why humans must review AI outputs (ambiguity, domain context, legal nuance).

### Overall Conclusion

Set 2 wins mainly because it is more reproducible and easier to grade, not because it is “more correct.”

---

### Problem C_2: Requirements Satisfiability Reasoning

> A Note on GenAI Contribution, problem_C1 solutions was written by me using GitHub Copilot (GPT-5-Mini) with and without structured prompting guidelines.

> This evaluation compares baseline prompting and guideline-based prompting to analyze their impact on reasoning quality, correctness, and reproducibility.

> This problem takes inspiration from a study conducted by Santos et al. (2024) [3].

---

## 1. Evaluation Criteria

This problem evaluates the student’s ability to reason about whether a system design satisfies a stated requirement. The emphasis is on logical reasoning and practical improvement suggestions, not formatting style.

The following criteria apply:

- Correct reasoning about requirements satisfiability
- Clear justification grounded in the provided design
- Ability to propose a practical and relevant design improvement
- Awareness of the role of human judgment in evaluating system designs

This problem is evaluated across three tasks.

### Task 1 — Satisfiability Decision

**Good solution\_**

- Correctly answers No, recognizing that username/password authentication alone is insufficient to guarantee that only authorized users access sensitive patient records.
- Demonstrates understanding that authentication strength directly affects requirement satisfiability.

**Satisfactory solution**

- Provides the correct decision but with limited or partially developed reasoning.

**Bad solution**

- Answers Yes without qualification.
- Assumes basic authentication is sufficient without considering security risks.
- Shows misunderstanding of the requirement or the design.

### Task 2 — Reasoning

**Good solution**

- Clearly explains why the design fails to satisfy the requirement (e.g., weak authentication, lack of additional verification, increased risk of unauthorized access).
- Reasoning is explicitly tied to the requirement and the given design.
- Avoids inventing features not present in the design.

**Satisfactory solution**

- Provides a partially correct explanation but lacks clarity or depth.

**Bad solution**

- Provides vague or generic security statements.
- Does not connect the explanation to the requirement or design details.
- Introduces invented system features not stated in the problem.

### Task 3 — Design Improvement

**_Good solution _**

- Proposes a realistic and relevant improvement, such as:
  - multi-factor authentication
  - role-based access control
  - stronger authentication mechanisms
- Clearly explains how the improvement increases requirement satisfiability.

  **Satisfactory solution**

- Suggests a relevant improvement but provides limited explanation.

  **Bad solution**

- Suggests unrelated or impractical changes.
- Proposes improvements without explanation.
- Provides no actionable design modification.

**_2. Example Solution Set_**

**Context Prompt (No Guidelines)**

**Baseline prompt:**

Read the problem C2 and complete the student tasks.  
Does the design satisfy the requirement? Explain your reasoning. Suggest one improvement.

**Observed output characteristics**

- Correct satisfiability decision
- Clear reasoning
- Appropriate design improvement
- Minor formatting variation
- Extra conversational narration

  **GitHub Copilot output**

**User:** Read the problem C2 and complete the student tasks.  
Does the design satisfy the requirement?  
Explain your reasoning in 2–3 sentences.  
Suggest one design improvement.

**GitHub Copilot:**

**Satisfiability Decision:** No.

**Reasoning:** The design relies solely on username/password authentication, which can be compromised and does not provide sufficient assurance that only authorized users access patient records. It also lacks additional controls (e.g., MFA, RBAC, or auditing) needed to reliably enforce and verify authorization.

**Design improvement:** Require multi-factor authentication (MFA) for all user logins to substantially reduce unauthorized access risk.

### **_Context Prompt (With Guidelines)_**

Structured prompt using task-tag isolation:

```
<task>
1. Decide if the design satisfies the requirement (Yes/No).
2. Explain why in 2–3 sentences using ONLY the given design.
3. Suggest ONE design improvement in 1 sentence.
</task>
```

**Observed output characteristics**

- Correct satisfiability decision
- Comparable reasoning quality
- Identical improvement suggestion
- Strict adherence to format
- No extraneous narration

**GitHub Copilot output**

**Satisfies:** No  
**Reasoning:** The current design only includes username and password for authentication, which makes it susceptible to compromise since it lacks multi-factor authentication (MFA). It is constrained to this design framework, and therefore, it cannot incorporate additional features such as RBAC or auditing, as they are not specified.  
**Improvement:** Implementing multi-factor authentication would enhance security significantly.

**Satisfies:** No  
**Reasoning:** The design relies solely on username and password, making it vulnerable to compromise and unable to ensure that only authorized users can access records. Additionally, it explicitly lacks multi-factor authentication (MFA), which diminishes user authorization assurance. It's important to stick to the given design elements without adding new features.  
**Improvement:** Multi-factor authentication should be required for all logins to enhance security.

**Satisfies:** No  
**Reasoning:** The design relies solely on username and password authentication, which can be compromised and does not guarantee that only authorized users access patient records. It explicitly lacks multi-factor authentication, reducing assurance of user identity.  
**Improvement:** Add multi-factor authentication (MFA) for all user logins.

## 3. Comparison and Analysis

Both prompting approaches produced correct reasoning and appropriate design improvements.

The structured prompt improved format consistency but did not significantly change reasoning quality or correctness.

This experiment shows:

- Structured prompting improves reproducibility
- Reasoning performance remains similar
- Differences are primarily cosmetic and formatting-related

Relevant guideline impact:

- Guideline 12 (task-tag prompting) improves formatting stability
- Guidelines related to measurable requirements or transcript formatting are not applicable to this reasoning task

Structured prompting is therefore useful for grading workflows but does not inherently improve reasoning depth in satisfiability analysis.

## 4. Integration into Updated Guidelines

This experiment reinforces that structured task-tag prompting improves formatting consistency and evaluation reproducibility but does not inherently improve reasoning quality in satisfiability analysis tasks.

Based on these observations:

- Task-tag structured prompting should be recommended primarily for grading and structured evaluation workflows where output consistency is important.
- Our guidelines should explicitly distinguish between formatting-level improvements and reasoning-level improvements.
- Task-specific applicability of guidelines should be documented to encourage selective and appropriate use.

These refinements help future users match prompting strategies to task requirements rather than assuming universal effectiveness.

## Result Summary

**Satisfiability Decision:** Tie  
Both sets correctly answer No (username/password alone does not ensure only authorized users access records).

**Reasoning Quality:** Tie  
Both connect the decision to the design and stay consistent with the requirement.

**Improvement Suggestion:** Tie  
Both suggest MFA as the improvement.

**Output Stability / Reproducibility:** Set 2 wins (Guided Prompt)  
Guided output is easier to compare across runs.

### Overall conclusion

Set 2 wins slightly due to format consistency, but the thinking quality is basically the same in both.

---

### Problem C_3: Requirements Elicitation Question Generation with AI Assistance

> A Note on GenAI Contribution, problem_C1 solutions was written by me using GitHub Copilot (GPT-5-Mini) with the following prompt:,
> This evaluation compares baseline prompting and guideline-based prompting to analyze their effect on elicitation quality, structure, and reproducibility.

> This problem takes inspiration from a study conducted by Yeow et al. (2024) [4].

## 1. Evaluation Criteria

This problem evaluates the student’s ability to:

- Design relevant and well-scoped elicitation questions
- Clearly distinguish between survey and interview questions
- Demonstrate awareness of question quality attributes (clarity, specificity, relevance)
- Critically review and improve AI-assisted outputs
- Recognize the need for human judgment in requirements elicitation

This problem is evaluated across four tasks.

---

### Task 1 — Survey Question Design

**Good Solution**

A good solution provides exactly three survey questions appropriate for general users (drivers). The questions should be concise, easy to answer in a structured format (e.g., Likert scale or multiple choice), and focused on usage behavior, satisfaction, or feature importance. Questions should be understandable to non-technical users and directly relevant to the parking system context.

**Bad Solution**

A bad solution provides fewer than three questions, includes vague or overly technical wording, or asks open-ended interview-style questions unsuitable for surveys. Questions that are irrelevant to drivers’ experience or system usage are also considered poor.

### Task 2 — Interview Question Design

**Good Solution**

A good solution provides exactly three open-ended interview questions suitable for a city transportation administrator. Questions should address organizational goals, system constraints, privacy/security policies, scalability, or operational management. They should encourage detailed discussion rather than yes/no responses.

**Bad Solution**

A bad solution includes generic or user-focused questions, ignores administrative concerns, or uses closed yes/no questions that limit stakeholder insight.

### Task 3 — Question Quality Review

**Good Solution**

A good solution identifies at least one meaningful weakness in the elicitation questions, such as ambiguity, lack of scope, or missing non-functional considerations. The explanation should clearly connect the weakness to established requirement quality attributes (e.g., clarity, completeness, verifiability).

**Bad Solution**

A bad solution identifies a trivial or unrelated issue, fails to explain why it is problematic, or claims that no improvement is necessary.

### Task 4 — Question Improvement

**Good Solution**

A good solution rewrites one question to directly address the identified weakness. The revised question should demonstrate improved clarity, specificity, or scope and should be measurably better than the original.

**Bad Solution**

A bad solution makes only superficial wording changes, fails to address the identified weakness, or produces a less clear question than before.

### Human Oversight Requirement

Even when AI generates plausible elicitation questions, human review is essential. AI systems may overlook stakeholder context, domain-specific priorities, or implicit assumptions. Human judgment is required to validate relevance, resolve ambiguities, and ensure that elicitation questions align with real stakeholder needs and organizational goals.

## 2. Example Solution Set

### Context Prompt (No Guidelines)

**Baseline prompt:**

Read problem C3 and complete the listed elicitation tasks.

#### Observed output characteristics

- Generated relevant survey and interview questions
- Identified a reasonable weakness
- Produced a meaningful improvement
- Included extra planning narration (TODO lists and progress messages)
- Output formatting varied across runs

**Github Copilot Output**

**1. Survey Questions (drivers)**

- **Survey Q1:** How often do you use a mobile app or digital signage to find parking in the city?
- **Survey Q2:** Which factors influence your parking choice most? (select up to 3: price, distance to destination, time to find a spot, safety, EV charging, payment method)
- **Survey Q3:** How willing are you to share real-time location data to receive accurate parking availability? (Very willing / Somewhat willing / Neutral / Somewhat unwilling / Very unwilling)

**2. Interview Questions (city transportation administrator)**

- **Interview Q1:** What are the city's top objectives for a smart parking system (e.g., reduce congestion, increase turnover, raise revenue, improve accessibility)?
- **Interview Q2:** Which specific data sources and vendor systems must the parking system integrate with (e.g., on-street sensors, parking meters, payment gateways, traffic management), and are there existing APIs or formats we must support?
- **Interview Q3:** What legal, privacy, retention, and public-data-sharing constraints must the system comply with (e.g., retention periods, anonymization, data-sharing agreements)?

**3. Weakness**

- **Weakness:** The questions emphasize functional and usability concerns but lack explicit coverage of non-functional requirements (privacy/security, scalability, reliability, maintenance costs, accessibility and equity).

**4. Rewritten / Improved Question**

- **Improved Interview Q2:** Which exact data sources (for example: on-street sensor feeds, parking-meter transaction logs, mobile app telemetry, CCTV-derived occupancy) and vendor systems must we integrate with, what data formats/APIs do they expose, and which integrations are required within the first 12 months?

### Context Prompt (With Guidelines)

Structured prompt using task-tag isolation and formatting constraints:

```
<task>
Generate elicitation questions and improvements only.
</task>
```

#### Observed output characteristics

- Similar question quality to baseline
- Clean and structured output
- No extra narration
- Strict adherence to requested format

**Github Copilot Output**

Satisfies: No  
Reasoning: The provided design only states the high-level intent—to help drivers find available parking and assist city administrators—but includes no concrete functional or non-functional specifications, integration details, or acceptance criteria that would demonstrate the requirement is met. Without those concrete design elements and verifiable success metrics, the requirement cannot be confirmed as satisfied.  
Improvement: Add concrete, verifiable specifications including required data sources and integrations, privacy and retention constraints, performance targets, and acceptance criteria.

---

## 3. Comparison and Analysis

Both prompting approaches produced useful elicitation questions and improvements.

The structured prompt improved:

- formatting consistency
- reproducibility
- evaluation clarity

However, it did not significantly change the substantive quality of the elicitation questions.

This experiment shows:

- Structured prompting stabilizes output format
- Reasoning and creativity remain comparable
- Improvements are primarily organizational rather than conceptual

Relevant guideline impact:

- Guideline 12 (task-tag prompting) improves formatting stability
- Group 2 improvements reduce invented assumptions
- Group 1 improvements enforce structured output templates

## 4. Integration into Updated Guidelines

Based on these findings:

- Task-tag prompting should be recommended for structured elicitation workflows
- Prompts should explicitly forbid invented assumptions
- Output templates should be required for evaluation tasks
- Guidelines should distinguish formatting improvements from reasoning improvements

These updates support more reproducible and testable elicitation processes.

## Result Summary

### Task Matching / Correct Task Type: Set 1 wins (Baseline Prompt)

The baseline prompt directly matches the C3 problem tasks by generating:

- 3 survey questions
- 3 interview questions
- 1 identified weakness
- 1 improved question

This makes the baseline output usable for requirements elicitation evaluation.

The guided prompt initially used a design-satisfiability template, which is structurally clean but mismatched to the C3 elicitation task. Therefore, for task alignment, Set 1 performs better.

### Output Stability / Reproducibility: Set 2 wins (Guided Prompt)

The baseline output contains extra narration such as planning messages and file-reading notes. This introduces variability and makes the output harder to compare across runs.

The guided prompt enforces strict formatting through task-tag isolation, resulting in stable, reproducible output without extraneous text.

### Content Quality: Tie

Both prompts generate relevant and well-scoped elicitation questions. The improvement is not in question correctness but in output control and reproducibility.

## Overall Result

- For task correctness and assignment alignment: Set 1 wins
- For formatting stability and reproducibility: Set 2 wins

Because answering the correct elicitation task is more important than formatting alone, the baseline prompt produces the more usable submission. However, combining the baseline task structure with guided formatting would yield the best overall result.

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
