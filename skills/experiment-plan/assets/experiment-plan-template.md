# Experiment: [experiment title]

> **Team / Area:** [TBD] · **Status:** Draft · **Owner:** [TBD] · **Created on:** [date]

**TL;DR:** [two sentences: what we're changing, for whom, and which metric decides it]

---

## Identification

| Field | Value |
|---|---|
| **Experiment name** | [descriptive name] |
| **Tracking key** | [key in the experimentation platform, e.g. `signup_form_fields`] |
| **Start / estimated end** | [start date] · [estimated end date] |
| **Owner** | [name] |
| **Stakeholders** | [names] |
| **Status** | Draft · In design · Running · Closed |
| **Ticket / task** | [link] |
| **Design** | [link] |
| **Experiment config** | [link to the experiment in the platform] |
| **Results dashboard** | [link] |
| **Source hypothesis** | [link to the hypothesis document, if any] |

---

## 1. Problem summary

**What we observed:** [narrative paragraph with quantitative data in context: absolute numbers, not just percentages.]

**Why test it now:** [urgency, goal or OKR (if the team uses them), strategic timing.]

**How it will run:** [one line: test type, groups, split.]

> ❓ **Review questions:** Why are we testing this now? How does it connect to a real pain shown by data or research? What changes for the user if it works? Are we isolating one variable?

---

## 2. Hypothesis

> **We believe that** [change] **for** [user segment] **will** [measurable result + direction] **because** [evidence-based reason].
>
> **And therefore** [expected business impact].

**Rationale:**
- [historical data, qualitative research or benchmark that supports the "because"]

---

## 3. Target audience

- **Segment:** [who enters the experiment]
- **Inclusion criteria:** [eligibility rules, e.g. logged-in user, plan X, country Y]
- **Exclusion criteria:** [who is left out]
- **Estimated volume:** [eligible users per week or per month]

---

## 4. Experiment design

### Configuration

| Field | Value |
|---|---|
| **Type** | [A/B · A/B/C · Multivariate · Holdout] |
| **Traffic split** | [e.g. 50% control / 50% variant · 34% / 33% / 33%] |
| **Randomization unit** | [Logged-in user ID · Anonymous/device ID] |
| **Mutual exclusion** | [layer/namespace that keeps this test from overlapping with others] |
| **Minimum estimated duration** | [TBD: see Sample size] |

### Variants

**Control**: [description of the current state, unchanged]
> Design: [link]

**Variant A**: [description of the change]
> Design: [link]

**Variant B** *(if any)*: [description]
> Design: [link]

### Experimentation platform setup

> **Platform:** [GrowthBook · Optimizely · Statsig · LaunchDarkly · in-house · TBD]
> **Project / group:** [e.g. `signup`, `checkout`]
> **Experiment name / key:** [TBD]
> **Feature flag:** [flag name, e.g. `signup_form_fields`]
> **Variations:**
> - `control` → unchanged
> - `variant_a` → [short description]
> - `variant_b` → [short description, if any]
>
> **Traffic split:** [e.g. 50% / 50%]

> ❓ **Review questions:** Does each variant change one variable? Are there too many variants for the traffic and time available? Does the segmentation produce clean, comparable groups?

---

## 5. Metrics

| Category | Metric | Definition | Baseline | Expected effect |
|---|---|---|---|---|
| **Success metric** *(OEC: the single metric that answers the hypothesis)* | [name] | [how it's calculated] | [pull right before launch] | [e.g. +5% relative] |
| **Primary metric** *(main funnel KPIs around the success metric)* | [name] | | | |
| **Secondary metric** | [name] | | | [exploratory] |
| **Guardrail metric** *(must not regress)* | [name] | | | [e.g. no drop greater than 1 percentage point] |

> ⚠️ **Baseline:** pull reference values right before launch, not when you write the design. Seasonal swings can distort the comparison.

> ❓ **Review questions:** Does the success metric answer the hypothesis directly? Is the expected effect consistent with the size of the change, and is there historical support for it? Is any business metric at risk, and is it covered by a guardrail?

---

## 6. Sample size *(power analysis)*

| Success metric | Baseline | MDE (smallest change worth detecting) | Power | Significance | Eligible traffic | Required sample per arm | Estimated weeks |
|---|---|---|---|---|---|---|---|
| [metric] | | | 80% | 95% | | | |

**Math:** [show the calculation: n per arm ≈ 16 × p̄ × (1 − p̄) / δ², then weeks ≈ n ÷ weekly traffic per arm]

> If the required sample is larger than the traffic available in the planned period, adjust the duration or the scope of the experiment before launching.

> ❓ **Review questions:** Is the sample feasible with current traffic? Do the duration and sample size line up? Do stakeholders understand the risk of stopping the test too early?

---

## 7. Rollout & stop criteria *(gradual rollout optional: recommended for high-traffic or high-risk flows)*

| Step | Coverage | Observation time | Criterion to advance |
|---|---|---|---|
| 1 | 10% | 24–48 h | System health check · Sample Ratio Mismatch (SRM) within expected range |
| 2 | 25% | 24–48 h | Guardrail metrics stable |
| 3 | 50% | 48 h | No clear drop in the success metric vs. control |
| 4 | 100% | n/a | Until the required sample is reached |

**Early stop criteria**
- A guardrail drops past the agreed limit with statistical significance → pause
- Sample Ratio Mismatch (SRM) detected → pause and investigate before any further step
- In an A/B/C test: you can pause only the problematic variant and keep control vs. the healthy variant

**Rollback plan:** [ideally switch the variant off through the feature flag, with no deploy]

**Channels and owners:** [where alerts go + who is on call for the test]

---

## 8. Risks & ethical considerations

**Technical risks**
- [e.g. page performance degrades with extra content]
- [e.g. feature flag not active in production before launch]

**User risks**
- [e.g. a worse variant exposes part of the traffic to a poorer experience; mitigated by the gradual rollout]
- [e.g. cannibalization: a user who would have stayed on the current plan moves to a cheaper one]

**Financial risks** *(if relevant)*
- [TBD]

**Could the impact fall unevenly on vulnerable groups?** [answer explicitly]

---

## 9. Decision rules *(defined BEFORE launch)*

| Result | Decision |
|---|---|
| **Win**: success metric rises above the MDE, guardrails OK | [e.g. roll out to 100% + document] |
| **Lose**: success metric flat or down, or a guardrail breaks | [e.g. don't roll out, record the learning] |
| **Inconclusive**: no significance | [e.g. extend / increase sample / redesign] |

---

## 10. Pre-launch checklist

| Item | Status | Owner |
|---|---|---|
| Tracking implemented and reviewed | ☐ | [TBD] |
| Metrics and baselines reviewed | ☐ | [TBD] |
| Sample size documented | ☐ | [TBD] |
| Stop criteria and rollback agreed | ☐ | [TBD] |
| Dashboards set up | ☐ | [TBD] |
| Stakeholders informed | ☐ | [TBD] |

> ❓ **Review questions:** Is there a communication plan for the impacted teams? Who owns the final Go/No-Go?

---

## 11. Results & learnings *(fill in after closing)*

**Observed data**

| Variant | Success metric | Primary metrics | Guardrail metrics | Statistical significance |
|---|---|---|---|---|
| Control | | | | |
| Variant A | | | | |

**Conclusion**

- **Result:** [Won · Lost · Inconclusive]
- **Decision:** [Ship · Iterate · Discard]
- **Reasoning:** [why this decision, based on the data and the rules in section 9]
- **Learning:** [what this taught us about the user or product, regardless of the outcome]
- **Next steps:** [TBD]

---

## ⚠️ Gaps: what's missing for the Go/No-Go

> The items below must be resolved before launch.

- [ ] [gap 1]
- [ ] [gap 2]
