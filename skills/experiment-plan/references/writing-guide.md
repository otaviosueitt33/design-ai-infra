# Experiment Plan: writing guide, section by section

This is a reference for writing each section well. The template in `../assets/experiment-plan-template.md` gives the skeleton. This guide explains *how* to write each part. Section numbers match the template.

## General tone

- **First person plural:** "We believe that…", "we identified…", "we expect…".
- **Direct and analytical**, with no unnecessary jargon.
- **Always put numbers in context:** "135k users/month" rather than "135,576". Use absolute values when you have them, not just percentages.
- Wherever the user doesn't know something yet, leave an editable placeholder (`[TBD]`). Never invent data.
- Spell out every acronym the first time it appears.

## TL;DR and Identification

The TL;DR is two sentences: what changes, for whom, and which metric decides. Identification is a lookup table. Fill in what exists and leave `[TBD]` for the rest. Don't add rows the team doesn't use.

## 1. Problem summary

An analytical narrative in three parts:
1. **What we observed:** quantitative data, absolute numbers.
2. **Why it matters now:** impact on the goal or OKR (if the team uses them) and the volume of users affected.
3. **How it will run:** a one-line overview of the experiment.

## 2. Hypothesis

Always use the canonical format, with the four non-negotiable elements (change, segment, result + direction, reason):

> **We believe that** [change] **for** [segment] **will** [measurable result] **because** [reason].

The rationale follows right below and cites historical data, qualitative research or a benchmark. If the hypothesis came from the hypothesis-builder skill, reuse its statement and evidence rather than rewriting them.

For multiple hypotheses, number them (H1, H2, H3). When variants have different copy or design, add a comparison table (Control | Variant A | Variant B). Note the **psychological lever** each variant uses where it helps (social proof, scarcity, anchoring, etc.).

## 3. Target audience

Segment, inclusion and exclusion criteria, and estimated eligible volume per week. The volume number feeds the Sample size section directly, so give a source for it if you can.

## 4. Experiment design

- Describe the **target population** and any **segmentation** in prose before the configuration table.
- **Randomization unit:** a logged-in user ID for authenticated flows and an anonymous/device ID for logged-out ones. This guarantees *sticky assignment*: the user stays in the same variant for the whole test. Avoid session-level randomization for anything the user can see more than once.
- **Mutual exclusion:** if other experiments run on the same surface, name the layer or namespace that keeps them from overlapping.
- **Platform setup:** fill in the callout with whatever platform the team uses. If there's no platform yet, say how assignment will be done (e.g. a hash of the user ID) and log it as a gap.
- **Expected volume:** if there are projections, add a table by scenario (% of traffic × days × sample size). It connects directly to section 6.

## 5. Metrics

Four categories, in this order:
1. **Success:** the *single* metric that answers the hypothesis. It's the hypothesis's *Primary metric (OEC)*, renamed here.
2. **Primary:** the main KPIs of the affected funnel around it. This row isn't the OEC.
3. **Secondary:** exploratory or behavioral metrics that help explain *why*.
4. **Guardrail:** metrics that must not regress (revenue, churn, latency, cost, quality). They protect you from gains that hide losses.

Always give the expected effect **with a sign and a unit**: "+5% relative", "+2.3 percentage points", "no drop greater than 1 percentage point".

## 6. Sample size

Point to [Evan Miller's sample size calculator](https://www.evanmiller.org/ab-testing/sample-size.html). Fill in baseline, MDE, power (default 80%), significance (default 95%), sample size per arm and weeks to significance.

**Offline approximation** (no calculator available), for two proportions at 80% power and 95% significance (two-sided):

> n per arm ≈ 16 × p̄ × (1 − p̄) / δ², where p₁ = baseline, p₂ = baseline + MDE, p̄ = (p₁ + p₂) / 2 and δ = p₂ − p₁.
>
> Example: baseline 10%, MDE +2 percentage points → n ≈ 16 × 0.11 × 0.89 / 0.02² ≈ 3,916 per arm.

Then convert to time: weeks ≈ n per arm ÷ (eligible users per week × share of traffic in each arm). Round **up to whole weeks**, so the test covers full weekly cycles.

The document must include this reminder: *"If the required sample is larger than the traffic expected during the planned period, the duration or scope of the experiment must be adjusted."*

For several MDEs, add a helper table: MDE × weeks needed × absolute impact. For continuous metrics (revenue per user, time on task) the formula above doesn't apply. Use the calculator or a t-test power calculation with the metric's variance, and log the variance as a gap if it's unknown.

## 7. Rollout & stop criteria

There are three parts:
- **Stop criteria:** a threshold plus a window, e.g. "success metric drops > 10% for 24h", plus SRM.
- **Rollback plan:** ideally switch off through the feature flag, with no deploy.
- **Channels and owners:** where alerts go and who is on call.

Ask the team for these values. Don't assume them. A gradual ramp isn't needed for email or other controlled-channel experiments.

## 8. Risks & ethical considerations

Cover technical, user and (when relevant) financial risks, each with its mitigation. **Always** include the question: *"Could the impact fall unevenly on vulnerable groups?"*

## 9. Decision rules

Copy the decision table from the hypothesis if there is one. If not, write it now, **before launch**. Each row names the observable condition and the action. "We'll look at the data and decide" isn't a decision rule.

## 10. Pre-launch checklist

The standard items are: tracking implemented, metrics reviewed, sample size documented, stop criteria and rollback agreed, dashboards set up, stakeholders informed. The team assigns an owner to each item at runtime.

## 11. Results & learnings

Fill this in after the test closes. Compare the result with the prediction (under / met / over). Apply the decision rules from section 9 as written. If the team deviates from them, say why. Record the learning even when the test lost, because it feeds the next hypothesis.

## "Review questions" blocks

The template has `> ❓` blocks at the end of the Problem summary, Design, Metrics, Sample size and Checklist sections. They guide the review and help whoever reviews the plan push on the right points. Keep the default questions and add more for this experiment.
