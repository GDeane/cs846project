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

Req-01 — Function (Must)

Statement: The system shall authenticate and authorize users using OAuth 2.0 (or equivalent) for each calendar provider
before reading or writing calendar data.

Rationale: Secure, least-privilege access to user calendars and clear consent flow required by providers and regulators.

Acceptance criteria: OAuth flow works for Google Calendar and Microsoft Outlook in tests; unauthorized calls return 401;
consent screen shows requested scopes.

Inputs / Outputs: Input: user-initiated connect request; Output: access token + refresh token (stored per privacy
policy).

Error modes: Missing/expired tokens produce a clear UI error and re-authentication prompt.

Req-02 — Function (Must)

Statement: The system shall read calendar events (start, end, title, location, attendees, timezone) and maintain a
local, minimal event index for scheduling decisions.

Rationale: Accurate scheduling decisions require event metadata and time zone awareness.

Acceptance criteria: For a linked calendar, 99% of events fetched include a parsable start/end/timezone and location if
present; indexing completes within a reasonable time for 1 year of events (e.g., <30s for 10k events).

Inputs / Outputs: Input: calendar API responses; Output: normalized events in local index.

Error modes: Unparseable events flagged and surfaced to user for fix.

Req-03 — Function (Must)
Statement: The system shall consider event location and compute travel-time estimates between locations and the user's
current (or home/office) location using a configurable travel-time provider (e.g., map API) and user-selected transport
modes.
Rationale: Travel-aware scheduling needs reliable travel-time estimates to detect tight or infeasible bookings.
Acceptance criteria: For 95% of test routes, predicted travel time is within ±15% of the provider’s baseline estimate or
within ±10 minutes, whichever is larger; travel-time provider failures fall back to conservative default heuristics.
Inputs / Outputs: Input: event locations, user transport mode, departure time; Output: travel time estimate, route
confidence score.
Error modes: If location missing or provider fails, system marks route as "unknown" and asks user for confirmation.
Req-04 — Function (Must)
Statement: The assistant shall, on user request (e.g., "Can I book at 3pm?"), determine whether a proposed event fits
the calendar and provide a clear recommendation: Fit / Tight / Does not fit.
Rationale: Primary user need is to get a simple, actionable answer about whether a meeting can be scheduled.
Acceptance criteria: Recommendation produced for 100% of queries within SLA (see Req-09). Labeling is consistent with
configured thresholds and accompanied by confidence.
Inputs / Outputs: Input: proposed event time, duration, location; Output: recommendation with reasoning summary and
confidence score.
Error modes: Low-confidence results produce an explicit “uncertain” outcome and suggested follow-up questions.
Req-05 — Function (Should)
Statement: The system shall present a short, human-readable explanation for each decision that includes (a) key criteria
used (conflicting events, travel time, user preferences), (b) estimated travel time and margin, and (c) a numeric
confidence score.
Rationale: Stakeholders need explainability to trust the assistant and to adjudicate edge cases.
Acceptance criteria: Explanations are generated for 100% of decisions; user testing shows ≥80% of users find
explanations "sufficient to act" in a usability sample.
Inputs / Outputs: Input: decision context; Output: 1–3 sentence explanation + confidence score + link to "details".
Error modes: If the model cannot explain, show a fallback structured rationale (e.g., checklist of failed/passing
checks).
Req-06 — Nonfunctional – Accuracy / Reliability (Must)
Statement: For scheduling decisions, the system shall achieve a decision accuracy (match to ground-truth acceptability
in evaluation dataset) of at least 95% under normal conditions; travel-time predictions should meet Req-03.
Rationale: Stakeholders require strong correctness guarantees before relying on automated scheduling advice.
Acceptance criteria: Test suite evaluation demonstrates ≥95% decision accuracy on representative dataset; continuous
monitoring alerts if rolling 7-day accuracy drops below 92%.
Inputs / Outputs: Input: evaluation dataset; Output: metrics and alerts.
Error modes: Degradation triggers restricted-mode recommendations (e.g., require manual confirmation).
Req-07 — Nonfunctional – Latency (Should)
Statement: The system shall provide an initial response to user scheduling queries within 3 seconds 90% of the time and
within 5 seconds 99% of the time when no heavy external API (e.g., route calculation) is required.
Rationale: Fast responses improve usability and adoption.
Acceptance criteria: Load testing shows the latency targets met at expected per-user load (specify in SLO).
Inputs / Outputs: N/A (performance metric).
Error modes: If external API calls prolong response, show progress indicator and allow "get best-effort recommendation
later".
Req-08 — Nonfunctional – Privacy & Data Minimization (Must)
Statement: The system shall only store the minimal data needed for operation (event metadata, user preferences, model
personalization vectors) and shall provide user controls to opt-out of personalization and to delete stored data;
sensitive event content (notes) must be redacted by default unless explicitly permitted by user.
Rationale: Minimize privacy risk and comply with regulatory concerns.
Acceptance criteria: UI provides explicit toggle for personalization and a "delete all data" button; deletion completes
and an audit log confirms removal within 24 hours.
Inputs / Outputs: Input: user toggles, delete requests; Output: confirmation + audit record.
Error modes: Failed deletion produces retry and admin flagging.
Req-09 — Nonfunctional – Regional Data Compliance & Residency (Must)
Statement: The system shall support region-specific data handling: configurable data residency targets and compliance
measures for GDPR, CCPA, and other applicable laws; users shall be able to request data export or erasure per region
rules.
Rationale: Different jurisdictions require different controls (e.g., right to be forgotten).
Acceptance criteria: Export and deletion workflows comply with regional timelines (e.g., GDPR: deletion within 30 days),
and region flags are enforced for storage and processing.
Inputs / Outputs: Input: user region; Output: data stored/processed in region-specific stores or pseudonymized
pipelines.
Error modes: Cross-border transfer attempts are blocked or logged until consent obtained.
Req-10 — Function – Learning & Personalization (Should)
Statement: The system shall learn user scheduling preferences over time (e.g., preferred buffer times before/after
meetings, no-booking windows) using on-device or privacy-preserving federated learning; the user must be able to review
and opt-out.
Rationale: Personalization improves recommendation relevance while addressing privacy concerns.
Acceptance criteria: After 30 days of opt-in usage, personalized recommendations increase acceptance rate by measurable
amount (e.g., +10% relative to baseline) in pilot; opt-out immediately freezes personalization updates.
Inputs / Outputs: Input: user confirmations, historical event patterns; Output: preference model and effect on
recommendations.
Error modes: If model updates degrade performance, rollback to previous model.
Req-11 — Privacy Safeguard — Training Data Exclusions (Must)
Statement: The system shall not use specified categories of data for training/personalization unless explicitly
permitted by the user (e.g., shared calendars flagged as "business-shared", unusually busy weeks flagged by user).
Rationale: Users may not want shared or anomalous periods influencing personalization.
Acceptance criteria: UI and API allow users to tag calendars or date ranges as excluded; training pipeline respects
exclusion flags and includes tests to verify.
Inputs / Outputs: Input: exclusion flags; Output: filtered training examples.
Error modes: If exclusions are ignored, produce audit failure alarm.
Req-12 — Security — Data Protection (Must)
Statement: The system shall encrypt all user data at rest (AES-256 or equivalent) and in transit (TLS 1.2+/HTTPS).
Access to production secrets must be role-based and logged.
Rationale: Protect user data and meet enterprise security expectations.
Acceptance criteria: Penetration test finds no plaintext storage of private calendar content; all endpoints use TLS;
audit logs show role-based access records.
Inputs / Outputs: N/A (security controls).
Error modes: Key rollover or encryption failure triggers fail-closed (no data exposure).
Req-13 — Function – Integration & Write Safety (Should)
Statement: When the assistant writes changes (creates/updates events), it shall require explicit user confirmation and
show the exact calendar and scope being modified; an "undo" action for 10 minutes shall be available.
Rationale: Prevent accidental or incorrect modifications to user calendars.
Acceptance criteria: Write actions present a confirmation UI; undo restores prior state consistently in tests.
Inputs / Outputs: Input: user confirmation; Output: calendar API write + undo token.
Error modes: Failed undo logs the issue and alerts support.
Req-14 — Nonfunctional – Deployment Form Factor (Should)
Statement: The system shall be delivered as a software application with web and mobile clients and an API for enterprise
integration; optional edge/hardware integration (e.g., device with local assistant) may be supported via a separate
deployment profile but is out-of-scope for initial release.
Rationale: Applications maximize reach and meet typical user expectations; hardware adds complexity and regulatory
concerns.
Acceptance criteria: Web and mobile clients available, documented API; hardware integration documented as "future work".
Inputs / Outputs: N/A.
Error modes: N/A.
Req-15 — Nonfunctional – Auditing & Transparency (Should)
Statement: The system shall keep an auditable log of scheduling decisions (what inputs produced a decision, timestamp,
model version, and whether personalization was applied) accessible to the user and to authorized admins for debugging
and compliance.
Rationale: Auditing supports explainability, debugging, and compliance investigations.
Acceptance criteria: Logs are available in user settings (last 90 days) and admin interface; exportable JSON for
compliance requests.
Inputs / Outputs: Input: decision events; Output: tamper-evident logs with metadata.
Error modes: Log retention and tamper controls must be enforced; loss triggers alert.

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
Functional requirements
Req-01 — Authentication & Authorization (Functional, Must)
Statement: The system SHALL authenticate and authorize a user before reading or writing that user's calendar data.
Acceptance criteria: Any request to read or write calendar data without a valid authenticated session is rejected with
an HTTP 401/403-equivalent error; login flow completes successfully for supported providers.
Verification method: Automated integration tests that attempt calendar access with and without valid credentials;
penetration test to confirm unauthorized access is denied.
Req-02 — Calendar Fetch & Normalization (Functional, Must)
Statement: The system SHALL fetch a user's calendar events (start time, end time, title, attendees, timezone, and
location if present) and normalize them into a local minimal index for scheduling decisions.
Acceptance criteria: For a representative test calendar set (1 year, up to 10k events), normalization succeeds within a
defined processing window (e.g., initial sync ≤ 30s for 10k events) and at least 99% of events include parsable
start/end/timezone fields.
Verification method: End-to-end integration tests using synthetic provider data and a perf test to measure sync time and
parsing success rate.
Req-03 — Travel-Time Estimation (Functional, Must)
Statement: The system SHALL compute an estimated travel time between two event locations (or between a user location and
an event) given a user-selected transport mode and scheduled departure time.
Acceptance criteria: For 95% of test routes in the evaluation set, estimated travel time is within ±15% of the baseline
route-provider estimate or within ±10 minutes (whichever is larger); when location is missing, result is flagged as "
unknown."
Verification method: Automated route test harness comparing system estimates to a ground-truth route provider across
representative city/route samples.
Req-04 — Fit/Tight/Does-not-fit Recommendation (Functional, Must)
Statement: On user request with a proposed event (time, duration, optional location), the system SHALL return one of
three recommendations: "Fits", "Tight", or "Does not fit", and include a confidence score.
Acceptance criteria: Recommendation produced for 100% of valid queries within SLA; labels follow configured thresholds
and confidence ∈ [0,1] is returned.
Verification method: Functional tests with representative scenarios verifying expected label output and confidence
presence; unit tests for threshold logic.
Req-05 — Short Human-Readable Explanation (Functional, Should)
Statement: For each scheduling recommendation, the system SHALL provide a concise (1–3 sentence) human-readable
explanation listing the primary factors that led to the recommendation (conflicting events, travel time, user
preferences).
Acceptance criteria: Explanations are returned for 100% of recommendations and include at least the top two contributing
factors; user study (pilot sample) shows ≥80% of users find explanation sufficient to act.
Verification method: Automated checks ensure explanation field is non-empty and contains expected keys; small user trial
for subjective acceptance.
Req-06 — Write Safety for Calendar Changes (Functional, Should)
Statement: When the system writes (creates/updates/deletes) calendar events, the system SHALL require explicit user
confirmation and present the exact calendar and change details before performing the write; an undo action SHALL be
available for at least 10 minutes.
Acceptance criteria: Any write request without prior explicit confirmation is rejected; undo restore succeeds in tests
for standard cases within 10 minutes.
Verification method: Integration tests validating confirmation flow and undo behavior; instrumentation logs verifying UI
prompts.
Non‑functional requirements
Req-07 — Decision Accuracy (Non‑functional, Must)
Statement: The system SHALL achieve at least 95% decision accuracy against a specified evaluation dataset for
determining whether a proposed event "fits" under normal conditions.
Acceptance criteria: Continuous evaluation shows ≥95% accuracy on the approved evaluation dataset; rolling 7‑day
accuracy does not fall below 92% without triggering alerts.
Verification method: Offline evaluation pipeline that scores decisions against labeled dataset and a monitoring alert if
rolling accuracy drops below threshold.
Req-08 — Latency (Non‑functional, Should)
Statement: The system SHALL respond to scheduling queries (excluding heavy external route calculations) within 3 seconds
for 90% of requests and within 5 seconds for 99% of requests under expected load.
Acceptance criteria: Load testing demonstrates the stated latency percentiles for the projected per-user load.
Verification method: Performance tests (load/perf harness) and production telemetry measuring p90 and p99 latencies.
Req-09 — Privacy & Data Minimization (Non‑functional, Must)
Statement: The system SHALL store only the minimal data required for operation (event metadata, preferences, and any
opt‑in personalization vectors), provide user controls to opt out of personalization, and redact sensitive event
content (notes) by default unless explicitly permitted by the user.
Acceptance criteria: UI provides explicit opt-out toggle and delete/export options; storage audits verify no plaintext
retention of redacted fields; data deletion completes within 24 hours for user-initiated delete requests.
Verification method: Security audit, periodic storage scans, and functional tests for opt-out and deletion flows.
Req-10 — Training & Personalization Opt‑In/Exclusion Controls (Non‑functional, Must)
Statement: The system SHALL allow the user to opt‑in to personalization and to mark calendars or date ranges as excluded
from personalization/training; excluded data SHALL not be used for model training or personalization.
Acceptance criteria: Exclusion flags are persisted and honored by training/personalization pipelines verified by unit
tests and a training-data audit.
Verification method: Test pipeline filters that assert excluded samples are not present in training batches; audit log
demonstrating filter enforcement.
Req-11 — Data Residency and Compliance (Non‑functional, Must)
Statement: The system SHALL support region-specific data handling including export and erasure workflows that meet
applicable regulations (e.g., GDPR, CCPA) for the regions the customer requests support for.
Acceptance criteria: Export/erasure workflows complete within policy timelines (e.g., GDPR export/erasure within 30 days
where applicable); region flags are enforced for storage and processing.
Verification method: Legal/compliance testing and automated verification of storage location metadata for sample
accounts.
Req-12 — Security — Encryption & Access Control (Non‑functional, Must)
Statement: The system SHALL encrypt user data at rest and in transit and SHALL enforce role-based access controls for
production secrets and sensitive operations.
Acceptance criteria: All storage endpoints use encryption; TLS enforced for network traffic; access logs show role-based
access enforcement.
Verification method: Security scans, config checks, and privileged-access audit logs.
Req-13 — Auditing & Explainability Metadata (Non‑functional, Should)
Statement: The system SHALL record an auditable log for each scheduling decision including inputs, timestamp,
model/pipeline version, and whether personalization was applied; the user SHALL be able to view their recent decision
log (last 90 days).
Acceptance criteria: Decision logs exist for 100% of decisions and user UI exposes last 90 days; exportable JSON is
available.
Verification method: Integration tests for log creation and UI retrieval; spot audits of log completeness.
Req-14 — Availability & Degraded Mode (Non‑functional, Should)
Statement: The system SHALL provide a best-effort degraded recommendation when external dependencies (e.g., routing
provider) are unavailable and SHALL present the user with a clear indication of reduced confidence.
Acceptance criteria: When an external dependency fails in test, system returns a best-effort recommendation or
explicit "unknown/uncertain" and provides degraded-confidence indicator.
Verification method: Chaos/failure tests that simulate dependency outages and validate outputs and UI indicators.

##### Result:

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

