# The Canonical Structure of a Product Hypothesis

> **What this document is for:** it defines what a hypothesis needs before it can leave someone's head
> and become something you can test, decide on and learn from.
>
> **How it was built:** from widely used product and experimentation frameworks (Reforge, Teresa Torres,
> Lean UX, Lean Startup, and the online-experimentation literature from Kohavi et al.). Sources are at the end.

## Contents

- [1. Principles: what makes a hypothesis "good"](#1-principles-what-makes-a-hypothesis-good)
- [2. The canonical structure](#2-the-canonical-structure) (Blocks 0 to 9)
- [3. Quality checklist (use before prioritizing)](#3-quality-checklist-use-before-prioritizing)
- [4. Prioritization (after writing, decide what to test first)](#4-prioritization-after-writing-decide-what-to-test-first)
- [5. Quick sample-size estimate](#5-quick-sample-size-estimate)
- [6. Filled-in examples](#6-filled-in-examples): SaaS signup form and e-commerce shipping costs
- [7. Reference frameworks (where the blocks come from)](#7-reference-frameworks-where-the-blocks-come-from)
- [8. Quick glossary](#8-quick-glossary)
- [Sources](#sources)

---

## 1. Principles: what makes a hypothesis "good"

Every hypothesis needs to meet these criteria. Check it against them before using the template.

**Testable.** You can design an experiment that confirms or refutes it. If you can't, it isn't a hypothesis. It's an opinion.

**Falsifiable.** Some possible result proves it *wrong*. "Improving the UI makes users happier" isn't falsifiable, so it's useless. "Cutting the signup form from 5 to 3 fields increases the completion rate" is.

**Specific.** It names the exact change (not "improve search" but "add filters by date, category and status"), the segment, the metric and the expected direction of the effect.

**Grounded in evidence.** It comes from data, research or observed behavior, not a hunch. The "because" in the hypothesis has to point to that evidence.

**One change per hypothesis.** Three ideas are three hypotheses. Testing them together gives you dirty data that nobody can interpret.

**Honest about uncertainty.** The hypothesis says which assumption is the riskiest (the *leap of faith*). At Microsoft, about a third of tested ideas improve the key metric, a third are neutral and a third make it worse (Kohavi et al.). A rigorous design is what turns a test into a reliable decision instead of a guess with a number attached.

---

## 2. The canonical structure

An ideal hypothesis has **9 blocks**. Blocks 1–8 are filled in *before* the experiment and Block 9 *after*. Not every hypothesis needs every field at the same depth, but every field should be considered on purpose.

| # | Block | Question it answers | When to fill in |
|---|-------|---------------------|-----------------|
| 0 | Metadata | Who, when, which product, what status | Start |
| 1 | Context & Problem | Who suffers from what, and how badly | Start |
| 2 | Evidence | Why we believe the problem exists | Start |
| 3 | Opportunity & Alignment | Is it worth it? Which goal does it connect to? | Start |
| 4 | Hypothesis (core) | What we believe and why | Start |
| 5 | Prediction & Success criteria | How we'll know we were right | Start |
| 6 | Assumptions & Risks | What has to be true; what could go wrong | Start |
| 7 | Experiment design | How we'll test it | Start |
| 8 | Decision | What we'll do with each possible result | Start |
| 9 | Results & Learnings | What actually happened and what we learned | After |

---

### Block 0: Metadata

Short header fields:

- **Experiment name:** the slug used in your experimentation platform and dashboards (e.g. `signup-form-fields`).
- **Author / Team / Product.**
- **Creation date** and **planned start/end dates**.
- **Status:** `Problem/Idea` → `In design` → `Running` → `Done` → `Rolled out` / `Deprioritized`.
- **Parent hypothesis:** any hypothesis can break down into sub-hypotheses. Recording the hierarchy links a small test to a bigger strategic bet.
- **Links:** results dashboard, feature flag or experiment config, PR, design file.

---

### Block 1: Context & Problem

A hypothesis only makes sense when it's tied to a real problem of a real user.

- **User profile / product behaviors:** who they are and what they do in the product.
- **Problem:** a clear description of the pain.
- **Severity:** how serious or frequent it is (high/medium/low, with a reason).
- **Current alternatives:** what people do today to get around it (workaround, competitor, give up).
- **User goals:**
  - *Qualitative:* what we hope to improve in the experience.
  - *Quantitative:* which metrics we hope to move.
  - *Non-goals:* what we are explicitly **not** trying to solve now.

---

### Block 2: Evidence

Separate signal from guesswork. Without evidence, the hypothesis is just a bet.

- **Qualitative evidence:** interviews, support tickets, feedback, session recordings, NPS comments.
- **Quantitative evidence:** funnel numbers, usage data, analytics queries, benchmarks.

> Rule of thumb: if the evidence field is empty, this is still an *idea*, not a hypothesis ready to prioritize.

---

### Block 3: Opportunity & Alignment

This block answers "is it worth the effort?" and connects the test to strategy.

- **Size of the opportunity:** how many users or how much value is affected. Quantify whenever you can (e.g. *"68% of visitors who open the signup form abandon it; that's ~8,000 people a week"*).
- **Strategic alignment:** which company goal it connects to (or OKR, if the team uses them).
- **Key result / numeric target:** the outcome we hope to move (e.g. *"raise signup completion from 32% to 38%"*).
- **Value to the customer:** what concretely improves for the person.

---

### Block 4: Hypothesis (the core)

This is the heart of the document. Use a format that includes the segment and the reason:

> **We believe that** [specific change] **for** [user segment] **will** [expected impact on a metric + direction] **because** [reason/insight grounded in evidence].
>
> **And therefore** [expected business consequence].

Equivalent formats, if one communicates better:

- **If/Then/Because:** *"If [change], then [metric] will [direction] by [expected magnitude], because [reason]."*
- **Lean UX:** *"We believe that [building X] for [persona] will result in [outcome]. We'll know it's true when we see [signal/metric]."*

The statement must **always** include the **change**, the **segment**, the **metric/direction** and the **reason**.

---

### Block 5: Prediction & Success criteria

This block turns the belief into a test with a clear decision:

> **To verify this, we will** [action/experiment].
> **We will measure** [metric].
> **We'll know we're right if** [measurable success condition].

Describe the metrics in three layers, the standard in mature experimentation programs:

- **Primary metric (OEC, Overall Evaluation Criterion):** the *one* metric that decides the experiment. Defining the OEC before running is the most important question in any test.
- **Secondary metrics:** supporting indicators that help explain *why*.
- **Guardrail metrics:** what must not get worse (e.g. cost, latency, churn, revenue, lead quality). They protect you from gains that hide losses.
- **Statistical criterion:** minimum detectable effect (MDE), confidence level and the required duration or sample. A winner is a statistically significant gain on the primary metric **with** guardrails neutral or positive.

---

### Block 6: Assumptions & Risks

- **Riskiest assumption (leap of faith):** the thing that *has to be true* for the hypothesis to work and that we're least sure of. Map assumptions on two axes, importance × uncertainty, and test the "high importance + high uncertainty" one first.
- **Assumption types to check** (Teresa Torres): desirability, viability (business), feasibility (technical), usability and ethics.
- **Risks and side effects:** what could go wrong, including the null-effect scenario (more isn't always better).

---

### Block 7: Experiment design

How the test runs in practice:

- **Test type:** A/B, A/B/C, holdout, before/after, qualitative panel, etc.
- **Groups and traffic allocation:** control vs. variant(s) and the % of each (e.g. 20%/20% with 60% excluded).
- **Randomization unit:** the attribute that assigns a user to a group. Use a logged-in user ID for authenticated flows and an anonymous/device ID for logged-out ones. This guarantees *sticky assignment*.
- **Tool & infrastructure:** feature flag or experiment in your experimentation platform (e.g. GrowthBook, Optimizely, Statsig, LaunchDarkly, or in-house), a mutual-exclusion layer so concurrent experiments don't hit the same user, and the analytics source for the metrics.
- **Sample size & duration:** estimated from the MDE and traffic volume (see section 5).
- **Acceptance criteria / QA plan:** which business rules are covered and how they'll be tested end to end before launch.

---

### Block 8: Decision (defined BEFORE running)

A decision table prevents rationalizing after the result comes in:

| Result | Decision |
|--------|----------|
| **Win**: primary metric rises above the MDE, guardrails OK | Roll out to 100% + document the learning |
| **Lose**: primary metric flat or down, or a guardrail breaks | Don't roll out; record the learning and generate the next hypothesis |
| **Inconclusive**: no significance | Extend, increase the sample or redesign |

---

### Block 9: Results & Learnings (after the experiment)

- **Result vs. prediction:** did the experiment *under*-perform, *meet* or *over*-perform the hypothesis?
- **Final numbers:** primary, secondary and guardrail values + dashboard link.
- **Decision taken:** roll out / iterate / kill / deprioritize.
- **Learning:** what this taught you about the user or product, whether or not it "won". What you learn from a losing experiment feeds the next hypothesis.
- **Next steps.**

---

## 3. Quality checklist (use before prioritizing)

- [ ] Is the change **specific** (could someone else implement it without asking)?
- [ ] Is it **falsifiable** (could some result prove it wrong)?
- [ ] Is there **only one** change?
- [ ] Is there **evidence** (qualitative and/or quantitative) in Block 2?
- [ ] Is a **single primary metric (OEC)** defined?
- [ ] Is there a **guardrail metric**?
- [ ] Is the **size of the opportunity** quantified?
- [ ] Is the **riskiest assumption** named?
- [ ] Was the **decision table** defined before running?
- [ ] Does it connect to a **goal** (or OKR, if the team uses them)?

---

## 4. Prioritization (after writing, decide what to test first)

**ICE**, the Reforge-style default: score each factor from 1 to 10 and multiply.

- **Impact:** if it works, how much does it move the target metric?
- **Confidence:** how strong is the evidence that it will work? (10 = strong prior data; 1 = a hunch)
- **Ease:** how easy or fast is it to run?

`Score = Impact × Confidence × Ease`. The alternative is **RICE** (Reach × Impact × Confidence ÷ Effort), for when reach varies a lot between ideas.

---

## 5. Quick sample-size estimate

Use it when the user has a baseline conversion rate and wants to know whether an A/B test is feasible. The full calculation belongs in the experiment plan. This is a sanity check.

For two proportions at 95% significance (two-sided) and 80% power:

> **n per arm ≈ 16 × p̄ × (1 − p̄) / δ²**, where p₁ = baseline, p₂ = baseline + MDE, p̄ = (p₁ + p₂) / 2 and δ = p₂ − p₁.
>
> Example: baseline 10%, MDE +2 percentage points → n ≈ 16 × 0.11 × 0.89 / 0.02² ≈ **3,916 per arm**.

For an exact number, use [Evan Miller's sample size calculator](https://www.evanmiller.org/ab-testing/sample-size.html). If the required sample is larger than the traffic available in the planned window, the test needs a longer duration, a bigger MDE or a different design. Log this as a gap.

---

## 6. Filled-in examples

Both examples are **illustrative**. The numbers are made up to show the level of detail, not taken from a real company.

### Example A: B2B SaaS signup form

- **Metadata:** `signup-form-fields` · Growth team · A/B · In design.
- **Problem:** visitors who start signup abandon it at the form. Severity high: it's the biggest drop in the acquisition funnel.
- **Evidence (quant.):** 68% of people who open the form never submit it (completion is 32%). Field-level analytics show most abandonment after the "Company size" and "Phone" fields.
- **Evidence (qual.):** in 6 of 10 usability sessions, participants hesitated at "Phone" and said they didn't want a sales call yet.
- **Opportunity:** ~12,000 form views a week. Goal: raise signup completion from 32% to 38%.
- **Hypothesis:** *We believe that removing the "Company size" and "Phone" fields (5 → 3 fields) for new visitors on the signup form will increase the completion rate, because those fields ask for commitment before the user has seen any value. And therefore more trial accounts will start each week.*
- **Prediction:** we'll run a 50/50 A/B test and measure form completion rate. We'll know we're right if completion rises by at least 2 percentage points with significance, with no drop in 7-day activation (guardrail: fewer fields could mean lower-intent signups).
- **Riskiest assumption:** that the sales team can qualify leads without company size at signup.
- **Design:** control = 5 fields (50%), variant = 3 fields (50%), randomized by anonymous ID.
- **Decision:** win → roll out and move the two fields into onboarding; lose → keep the fields, test explanatory microcopy instead; inconclusive → extend one more week.

### Example B: E-commerce shipping cost on the product page

- **Problem:** shoppers abandon carts when shipping costs appear for the first time at checkout.
- **Evidence:** the funnel shows the biggest drop at the step where shipping is calculated. Exit-survey answers mention "unexpected costs" more than any other reason.
- **Opportunity:** every shopper who reaches checkout. Goal: increase checkout conversion.
- **Hypothesis:** *We believe that showing an estimated shipping cost on the product page, for shoppers with a known postal code, will increase checkout conversion, because it removes the surprise that causes abandonment.*
- **Prediction:** A/B on the product page. Primary metric = checkout conversion. Secondary = add-to-cart rate. Guardrail = average order value. We're right if the variant converts more with significance and without lowering average order value.
- **Decision:** win → roll out; lose → test a free-shipping threshold message instead; inconclusive → extend the sample.

---

## 7. Reference frameworks (where the blocks come from)

- **Reforge / Brian Balfour:** the Business Hypothesis Canvas (structure the bet and communicate it) and the Growth Experiment Management System (ICE; record the result vs. the hypothesis as under/met/over). Basis for Blocks 4, 8, 9 and section 4.
- **Teresa Torres (Continuous Discovery):** the Opportunity Solution Tree (outcome → opportunities → solutions → assumption tests) and the five assumption types. Basis for Block 6.
- **Lean UX / Lean Startup:** the "We believe… we'll know when we see…" format and *leap-of-faith assumptions*. Basis for Blocks 4 and 6.
- **Kohavi, Tang & Xu, *Trustworthy Online Controlled Experiments*:** the OEC, guardrail metrics, sticky assignment, sample ratio mismatch, and the base rate of ideas that don't work. Basis for Blocks 5 and 7.
- **Common experiment cards** (problem → evidence → hypothesis → prediction → acceptance criteria). Basis for Blocks 1, 2, 4, 5 and 7.

---

## 8. Quick glossary

- **OEC (Overall Evaluation Criterion):** the single metric that decides the experiment.
- **Guardrail:** a metric that must not get worse, even if the primary metric improves.
- **MDE (Minimum Detectable Effect):** the smallest effect the test can reliably detect. It determines sample size and duration.
- **Leap-of-faith assumption:** the hypothesis's most uncertain and most critical assumption.
- **Sticky assignment:** the guarantee that a user stays in the same variant for the whole test.
- **Mutual exclusion (namespace / layer):** a mechanism that stops concurrent experiments from hitting the same user at the same time.

---

## Sources

- [Reforge: Business Hypothesis Canvas](https://www.reforge.com/artifacts/business-hypothesis-canvas-at-reforge)
- [Brian Balfour: The Hypotheses Behind Reforge's Journey](https://brianbalfour.com/essays/business-hypothesis-canvas-reforge)
- [Reforge: Growth Experiment Management System](https://www.reforge.com/blog/growth-experiment-management-system)
- [Reforge: Hypotheses and experiment mapping for 0-1 product](https://www.reforge.com/artifacts/hypotheses-and-experiment-mapping-for-0-1-product-at-reforge)
- [Teresa Torres: Opportunity Solution Trees (Product Talk)](https://www.producttalk.org/opportunity-solution-trees/)
- Ron Kohavi, Diane Tang, Ya Xu: *Trustworthy Online Controlled Experiments* (Cambridge University Press, 2020)
- [Centercode: Product Hypothesis: Write and Test Assumptions](https://www.centercode.com/blog/product-hypothesis)
- [Aakash Gupta: What Makes a Good Hypothesis](https://www.aakashg.com/what-makes-a-good-hypothesis/)
- [Mind the Product: Hypothesis-driven product management](https://www.mindtheproduct.com/hypothesis-driven-product-management/)
- [Evan Miller: Sample Size Calculator](https://www.evanmiller.org/ab-testing/sample-size.html)
