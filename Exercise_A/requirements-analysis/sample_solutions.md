# Sample Solutions for Requirements Analysis Exercise

### 1. Stakeholder Interviews Summary

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


**Evaluation**
- **Good**: Demonstrates a deep understanding of the conflicting needs of all stakeholders. Clearly articulates how these needs impact the requirements.
- **Satisfactory**: Provides a basic understanding of stakeholder needs but lacks depth or clarity in analysis.
- **Bad**: Fails to adequately identify or analyze stakeholder needs.

### 2. Real-World Constraints (outside of interviews)
**Budget**: target 40% recurring cost reduction with one‑time migration budget of $60k limits scope and tools/consultants.

**Procurement & legal**: vendor contracts, data‑privacy reviews, and approvals can add weeks or months of delay cutting into the 6-month timeframe.

**Technical integration**: API differences, SDK maturity, context‑window limits, and infra changes may require non‑trivial refactor.

**Performance**: latency and throughput impacts from new provider prompt approaches must be benchmarked.

**Team/time**: limited engineering capacity and competing priorities lengthen delivery. There is a need staged work and clear milestones.

**Operations**: monitoring, cost telemetry, rate limits, and fallback strategies required to avoid UX regressions.

**Evaluation: with part 3**

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