# Filled-in example: signup form fields (B2B SaaS)

> **Entirely illustrative.** The company, numbers and outcome are made up. It's built from Example A in the
> hypothesis-builder skill (signup form, 5 → 3 fields) to show tone, the level of detail per section, and the
> **sample-size math worked out step by step**. Section numbers match `../assets/experiment-plan-template.md`.

---

# Experiment: remove two fields from the signup form

> **Team / Area:** Growth · Acquisition · **Status:** Closed · **Owner:** [TBD] · **Created on:** [date]
> **Source hypothesis:** `signup-form-fields/hypothesis.md`

**TL;DR:** We're testing a 3-field signup form against the current 5-field one for new visitors. The
success metric is form completion rate, with 7-day activation as the guardrail so we don't trade lead
quality for volume.

## Identification

| Field | Value |
|---|---|
| **Experiment name** | Signup form: 5 → 3 fields |
| **Tracking key** | `signup_form_fields` |
| **Start / estimated end** | [date] · [date + 2 weeks] |
| **Owner** | [TBD] |
| **Stakeholders** | [Growth PM, Sales Ops lead, Frontend engineer] |
| **Status** | Closed |
| **Source hypothesis** | `signup-form-fields/hypothesis.md` |

## 1. Problem summary

**What we observed:** the signup form gets ~12,000 views a week from ~9,000 unique visitors, and only
32% of the people who open it submit it. Field-level analytics show most abandonment right after
"Company size" and "Phone". In 6 of 10 usability sessions, participants hesitated at "Phone" and said
they didn't want a sales call yet.

**Why test it now:** the quarterly acquisition goal is to raise signup completion from 32% to 38%, and
the form is the largest single drop in the funnel.

**How it will run:** a 50/50 A/B test on all new visitors, control (5 fields) vs. variant (3 fields).

> ❓ **Review questions:** Why now? Covered by the quarterly goal. Are we isolating one variable? Yes:
> the only change is which fields are present. Copy and layout are unchanged.

## 2. Hypothesis

> **We believe that** removing the "Company size" and "Phone" fields (5 → 3 fields) **for** new visitors
> on the signup form **will** increase the form completion rate **because** those fields ask for
> commitment before the user has seen any value.
>
> **And therefore** more trial accounts will start each week.

**Rationale:**
- 68% abandonment at the form, concentrated after the two fields being removed.
- Usability sessions (n = 10): 6 participants hesitated at "Phone" for fear of a sales call.

## 3. Target audience

- **Segment:** all new visitors who open the signup form.
- **Inclusion criteria:** no existing account; any country; desktop and mobile.
- **Exclusion criteria:** visitors arriving from sales-led campaigns (they're routed to a different form).
- **Estimated volume:** ~9,000 unique eligible visitors per week (last 8 weeks average).

## 4. Experiment design

| Field | Value |
|---|---|
| **Type** | A/B |
| **Traffic split** | 50% control / 50% variant |
| **Randomization unit** | Anonymous visitor ID (logged-out flow, sticky across sessions) |
| **Mutual exclusion** | `signup` layer, so no other signup-page test runs at the same time |
| **Minimum estimated duration** | 2 weeks (see section 6) |

**Control**: current form with 5 fields: name, work email, password, company size, phone.

**Variant A**: 3 fields: name, work email, password. Company size and phone move to the first
onboarding screen, where they're optional.

> **Platform:** [the team's experimentation platform]
> **Project / group:** `signup`
> **Feature flag:** `signup_form_fields`
> **Variations:** `control` → 5 fields · `variant_a` → 3 fields
> **Traffic split:** 50% / 50%

## 5. Metrics

| Category | Metric | Definition | Baseline | Expected effect |
|---|---|---|---|---|
| **Success** | Form completion rate | submitted forms ÷ unique visitors who opened the form | 32% | +2 percentage points (MDE) |
| **Primary** | Trials started per week | new trial accounts created | ~2,900/week | +6% relative |
| **Secondary** | Time to submit | median seconds from form open to submit | 48 s | exploratory |
| **Guardrail** | 7-day activation | % of new accounts that complete the core setup within 7 days | 41% | no drop greater than 1 percentage point |

## 6. Sample size

Calculator: [Evan Miller: Sample Size](https://www.evanmiller.org/ab-testing/sample-size.html).
Offline approximation for two proportions (95% significance, two-sided; 80% power):

> **n per arm ≈ 16 × p̄ × (1 − p̄) / δ²**

**Math for this experiment** (baseline 32%):

- MDE **+2 percentage points**: p₁ = 0.32 · p₂ = 0.34 · p̄ = 0.33 · δ = 0.02
  → n ≈ 16 × 0.33 × 0.67 / 0.02² = 16 × 0.2211 / 0.0004 ≈ **8,844 per arm**.
- MDE **+1 percentage point**: p₁ = 0.32 · p₂ = 0.33 · p̄ = 0.325 · δ = 0.01
  → n ≈ 16 × 0.325 × 0.675 / 0.01² = 16 × 0.2194 / 0.0001 ≈ **35,100 per arm**.

Traffic: ~9,000 eligible visitors a week → 4,500 per arm per week with the 50/50 split.

| Success metric | Baseline | MDE | Power | Significance | Eligible traffic | Required sample per arm | Estimated weeks |
|---|---|---|---|---|---|---|---|
| Form completion rate | 32% | +2 percentage points | 80% | 95% | ~9,000/week | ~8,844 | ~2.0 → plan 2 full weeks |

Helper scenario (MDE × feasibility): +1 percentage point would need ~35,100 per arm, or **~7.8 weeks**,
which is too long for the quarter. Decision: size for +2 percentage points. A smaller lift wouldn't
justify moving the fields into onboarding.

> ⚠️ If the required sample is larger than the traffic expected during the planned period, the duration
> or scope of the experiment must be adjusted.

## 7. Rollout & stop criteria

No gradual ramp: the change is low-risk and fully reversible through the flag.

- **Stop criteria:** 7-day activation in the variant more than 3 percentage points below control at the
  end of week 1; or SRM detected (split outside 49.5/50.5).
- **Rollback plan:** switch `signup_form_fields` to `control` for everyone. No deploy needed.
- **Channels and owners:** [team alert channel] · [frontend engineer on call].

## 8. Risks & ethical considerations

- **Technical:** onboarding must accept company size and phone as optional, or new accounts break.
  Covered in QA.
- **User:** none expected. Fewer required fields reduce effort.
- **Financial:** Sales loses two qualification fields at signup. Mitigation: they're asked in
  onboarding, and Sales Ops agreed to qualify by email domain in the meantime.
- **Could the impact fall unevenly on vulnerable groups?** Not identified. The change applies to
  everyone in the flow equally.

## 9. Decision rules

| Result | Decision |
|---|---|
| **Win**: completion +2 percentage points or more with significance, activation within −1 percentage point | Roll out to 100%; keep the fields in onboarding |
| **Lose**: completion flat/down, or activation drops more than 1 percentage point | Keep 5 fields; next hypothesis: explanatory microcopy on "Phone" |
| **Inconclusive** | Extend 1 week once; if still inconclusive, keep control |

## 10. Pre-launch checklist

| Item | Status | Owner |
|---|---|---|
| Tracking implemented and reviewed | ☑ | [frontend engineer] |
| Metrics and baselines reviewed | ☑ | [Growth PM] |
| Sample size documented | ☑ | [Growth PM] |
| Stop criteria and rollback agreed | ☑ | [frontend engineer] |
| Dashboards set up | ☑ | [analyst] |
| Stakeholders informed | ☑ | [Growth PM] |

## 11. Results & learnings *(fictional outcome, included to show how to close the section)*

| Variant | Success metric | Primary metrics | Guardrail metrics | Statistical significance |
|---|---|---|---|---|
| Control | 32.1% | 2,880 trials/week | 41.0% | n/a |
| Variant A | 34.7% | 3,120 trials/week | 40.4% | p < 0.01 on completion; activation difference not significant |

- **Result:** Won. +2.6 percentage points on completion; activation within the −1 percentage point limit.
- **Decision:** Ship, following the Win rule in section 9.
- **Reasoning:** the gain exceeded the MDE and the guardrail held.
- **Learning:** the asks that block signup are the ones that signal a sales call, not the length of the
  form itself. Users answered the same questions in onboarding at a 71% rate.
- **Next steps:** test making "Phone" opt-in with a "talk to sales" checkbox in onboarding.
