# Week 4 Evaluation: Requirements

**Authors:** [Gavin Deane, Artemiy Vishnyakov, Savira Umar]

## 1. Evaluation Criteria

This section defines how students can determine whether they solved the example problems correctly.

Criteria vary depending on the specific problem. Each problem's evaluation criteria are detailed in Section 2.

---

## 2. Evaluation specifically for Example Problems

### Problem A_1: Stakeholder Interviews Summary

### 1. Stakeholder Interviews Summary
## Example Good Solution"
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

## Example Bad Solution
1. **Customer Support** (Lack of details)
    - **Concern**: Customers are unsatisfied with the current chatbot
    - **Request**: Improve chatbot
    - **Implication**: A better chatbot will make customers happy

2. **Financial Stakeholder** (Excessive details prevent broad implications from being drawn)
    - **Concern**: API/token spend is material; target ~40% cost reduction in 3–6 months; migration cap ~$60k if justified.
    - **Request**: Demonstrable cost reductions, phased progress, and ROI for any migration spend.
    - **Implication**: (Irrelevant information here)

3. **Software Engineer** (Excessive technical jargon & creation of a solution when only analysis is requestedx)
    - **Concern**: High session context volatility — the agent exhibits poor stateful retention and low contextual coherence across turns, causing frequent conversational resets and generic, low-utility outputs; also perceptible latency spikes affecting UX.
    - **Request**: Implement robust session-state management (e.g., turn-level embeddings, incremental summarization, or context-window orchestration), optimize inference latency (caching, batching, and model selection), and add telemetry for turn-wise relevance and intent drift.
    - **Implication**: Requires a stateful session store or vector DB, summarization pipeline and context-truncation strategy, additional engineering for caching/throughput and instrumentation, and trade-offs against token budget and API spend that must be managed to avoid increased support ticket volume.

**Evaluation**
- **Good**: Demonstrates a deep understanding of the conflicting needs of all stakeholders. Clearly articulates how these needs impact the requirements.
- **Satisfactory**: Provides a basic understanding of stakeholder needs but lacks depth or clarity in analysis.
- **Bad**: Fails to adequately identify or analyze stakeholder needs.
---

### Problem A_2: Real-World Constraints (outside of interviews)

## Example Good Solution:
**Budget**: target 40% recurring cost reduction with one‑time migration budget of $60k limits scope and tools/consultants.

**Procurement & legal**: vendor contracts, data‑privacy reviews, and approvals can add weeks or months of delay cutting into the 6-month timeframe.

**Technical integration**: API differences, SDK maturity, context‑window limits, and infra changes may require non‑trivial refactor.

**Performance**: latency and throughput impacts from new provider prompt approaches must be benchmarked.

**Team/time**: limited engineering capacity and competing priorities lengthen delivery. There is a need staged work and clear milestones.

**Operations**: monitoring, cost telemetry, rate limits, and fallback strategies required to avoid UX regressions.

## Example Bad Solution (Nonsensical, confabulated requirements, excessive technical details)
- Require on-prem GPU cluster with 512 GB GPU memory per node to run the model locally; no cloud allowed.
- Mandate support for legacy browsers including Internet Explorer 8 and custom internal kiosks with obsolete TLS stacks.
- Target 10 million concurrent active users at launch with single-region deployment and no autoscaling plan.
- Preserve full raw conversation logs indefinitely (permanent storage), with expected storage growth of multiple petabytes per year.
- Require human moderation for every message in real time before any chatbot reply reaches users.
- Enforce strict on-prem data residency in a non-existent “EU-Mars” jurisdiction and quarterly notarized paper audits.
- Assume vendor pricing is fixed and non-negotiable at $1M/month for model access — budget accordingly with no procurement process.
- Plan for zero downtime with a single server design and no redundancy or failover testing.
- Require cryptographic hardware tokens for every user session, replacing existing passwordless flows.
- Expect the engineering team to deliver full integration, QA, and rollout in a single two-week sprint with no additional headcount.

**Evaluation: with part 3**

---

### Problem A_3: Analysis of Conflicting Requirements

### 3. Analysis of Conflicting Requirements
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
- Vendor contracts and data/privacy approvals can delay rollout and if work is started before contracts are made then it may be wasted if contracts fall through.

**Evaluation**
- **Good**: Thorough analysis of the conflicting requirements, insightful comparisons and potential resolutions.
- **Satisfactory**: Provides a basic analysis of conflicting requirements but lacks depth or clarity.
- **Needs Improvement**: Fails to adequately analyze conflicting requirements.

### Problem A_4: Proposed Solutions

### 4. Proposed Solutions (non-exhaustive list of examples)

1. **Balancing Context Retention and Cost**
	- Implement a hybrid approach where the chatbot uses a cheaper model for general inquiries but switches to a more advanced model (like Claude) for complex interactions requiring context retention.
	- This solution addresses the financial stakeholder's concerns while still meeting the customer support representative's need for improved context handling.

2. **Optimizing API Usage**
	- Introduce caching mechanisms to store frequently accessed data, reducing the number of API calls and thus lowering costs.
	- Rolling summaries stored as short embeddings to reduce token costs while keeping long context.
	- Caching common Q&A and retrieval augmented generation (RAG) to reduce token usage.
	- Using token conservation techniques such as prompt engineering, context pruning, compression/summarization between the user prompt and what is sent to the chatbot server.
	- This approach can help mitigate the financial stakeholder's concerns while enhancing the chatbot's performance.

3. **Phased Implementation**
	- Propose a phased rollout of the chatbot enhancements, starting with cost-effective solutions and gradually integrating more advanced features as budget allows.
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

