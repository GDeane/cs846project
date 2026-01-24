# Problem specification for Requirements Exercise B

---

### 1. Problem description

Given the description of the problem domain and the following questionnaire, use your LLM (GPT-5 mini) to elicit a set
of 10-15 structured requirements.

You would want to feel comfortable:

- 1: Showing these requirements to your boss.
- 2: presenting this list of requirements to a group of stakeholders in order to elicit preferences.
- 3: Agreeing to implement this set of requirements in a contract if the client agreed to them.

This problem takes heavy inspiration from the study conducted by Ronaki et al. (2023) [1].

### 2. Problem domain

A client wants to build a system that connects an AI personal assistant to an end user's calendar.

Not only should this AI system know what events are when, but the AI should also have awareness of the location of each
event so that the AI can point out when travel times may be tight or unfeasible.

Quote from (fictional) client: "That way, whenever the end user needs to book a meeting, they can simply ask their
assistant whether this works well with my schedule."

In addition, this personal assistant should get better over time as it gets to know what kind of time you prefer not to
be booked or what travel modes you use!

The client considers that privacy of user data could be a potential concern in this case. "I don't want everything about
a user's life to end up exposed on the internet because of our app."

### 3. Questionnaire

Here are some (not-exhaustive) questions to aid in requirements elicitation:

**Q1**: What kind of correctness and reliability guarantees must the system provide? That is, how often is it acceptable
for the system to make a mistake about whether an event fits or travel time.

**Q2**: Are there any categories of data the system should not learn from? (shared calendars, unusually busy weeks).

**Q3**: How explainable should the system be? Should it give a reasoning for what criteria it used to make its decision?
How in depth should this reasoning be?

**Q4**: What places in the world would you want this system to be deployed? Different countries have different privacy
laws (e.g. the right to be forgotten under the GDPR in the EU).

**Q5**: Should this system to be a piece of hardware or an application?

### 4. References

[1] K. Ronanki, C. Berger, and J. Horkoff, “Investigating ChatGPT’s Potential to Assist in Requirements Elicitation
Processes,” Jul. 14, 2023, arXiv: arXiv:2307.07381. doi: 10.48550/arXiv.2307.07381.


