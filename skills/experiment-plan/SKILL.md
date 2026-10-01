---
name: experiment-plan
description: Turns a product or growth hypothesis into an executable experiment plan (an "XP Plan"). The plan is a Markdown document covering identification, the hypothesis with context, target audience, experiment design (variants, split, randomization unit, platform setup), metrics with a sample-size calculation, rollout and stop criteria, risks, pre-registered decision rules, a pre-launch checklist and results. Comes in two formats. The full format (default) covers the whole cycle from planning through launch to decision. The lean format is a one-pager (Context / Problem / Hypothesis / Scope / Metrics) for sharing and aligning quickly. Asks for team, owner and tooling instead of assuming them. Use when someone asks to create or fill in an experiment plan, A/B test plan, test spec or XP Plan, or to "turn this hypothesis into an experiment". Also use when a conversation brings hypothesis, metrics, variants and a control group together. If there is no hypothesis yet, start with the hypothesis-builder skill.
---

# Experiment Plan

This skill turns a **hypothesis** into an **experiment document that can be executed and reviewed**. The document covers the full cycle: planning, then launch, then decision. It assumes no particular company, team or tool. Anything team-specific (owner, stakeholders, the goal or OKR it connects to, the experimentation platform, the analytics source) is **asked for at runtime**.

The output is a **Markdown file** in one of **two formats**. Ask which one at the start (see Step 0).

- **Full** (default): follows `assets/experiment-plan-template.md` and ends with a **Gaps** section listing what's missing for the Go/No-Go.
- **Lean**: a one-pager that follows `assets/experiment-plan-lean-template.md`, with five blocks: **Context / Problem / Hypothesis / Scope / Metrics**. It's built for sharing (a wiki, a doc, a chat thread) and quick alignment. It doesn't replace the full plan when the experiment needs formal review.

## Language

This skill is written in English, but **talk to the user in the language they write in, and write the document in that language too**. Translate everything in the template into that language, keeping the meaning: headings, fixed phrases ("We believe that…", "We observed that…"), status values and table cells. Keep widely used acronyms (OEC, MDE, SRM, A/B) and spell each one out the first time it appears.

## Starting point: the hypothesis

An experiment plan starts from a hypothesis. Before anything else, find out where it comes from.

- **If the user has a hypothesis document** (for example the output of the **hypothesis-builder** skill) or pastes the text, read it and **reuse what is already defined**: problem context, evidence, hypothesis statement, primary metric and the decision table. The hypothesis's *Primary metric (OEC)* becomes this plan's **Success metric**. The plan's own *Primary* row holds the main funnel KPIs around it, not the OEC. Carry the hypothesis's open gaps forward too. Don't ask again for what the hypothesis already answers.
- **If the user has no hypothesis yet**, recommend running **hypothesis-builder** first. If it isn't installed, or the user wants to go ahead anyway, help them write the minimal statement before designing the experiment: change, segment, metric/direction and reason.

The experiment plan **expands** the hypothesis into the operational plan. It details the design, sizes the sample and documents risks. It doesn't replace the hypothesis. It builds on it.

## How to run it

Work in short rounds and play back what you understood before moving on. Don't dump all the questions at once.

**Step 0: Ask for the format.** Before anything else, ask whether the user wants the **full** or the **lean** version.

- **Full** (default): the whole operational document. Follow Steps 1–5.
- **Lean**: the alignment one-pager. Follow the "Lean flow" section. Step 1 still applies, and so do the Step 3 questions the one-pager needs (platform, rollout). Skip Steps 2, 4 and 5. The lean format has no sample-size or results table. It has a short **Open items** list in place of the Gaps section.

If the user doesn't answer, or just asks for "the experiment plan", assume **full**.

**Step 1: Take in the hypothesis.** Identify the **team / product area** and the **title** of the experiment.

**Step 2: Collect the essentials.** If something is missing and the user doesn't know it, leave an editable placeholder (`[TBD]`). **Never invent it.** The minimum needed to generate the document:
1. Experiment title and team / product area
2. Product, feature or flow being tested
3. Problem context (from the hypothesis if there is one)
4. Why test now (urgency, goal, timing)
5. Main hypothesis (from the hypothesis if there is one)
6. Test type (A/B · A/B/C · multivariate · holdout)
7. Variants (control + variant(s), with a description and a link to the design if there is one)
8. Traffic split (e.g. 50/50, 95/5)
9. Metrics: at least the **Success** metric and one **Guardrail**
10. Owner and stakeholders. **Ask; don't assume names.**

Useful but optional: experimentation-platform setup (experiment key, feature flag, mutual-exclusion layer), metric baselines, an MDE already calculated, a gradual rollout strategy.

**Step 3: Team context, at runtime.** Ask, and don't assume:
- which goal (or OKR, if the team uses them) the experiment connects to
- which **experimentation platform** runs it (GrowthBook, Optimizely, Statsig, LaunchDarkly, an in-house system, or none yet)
- where the metrics come from (analytics tool, warehouse, dashboard)
- whether a gradual rollout is needed (high-traffic or high-risk flows)

If the user doesn't know, leave a placeholder and log it as a gap.

**Step 4: Generate the document** from `assets/experiment-plan-template.md`, following the writing guide in `references/writing-guide.md`. A filled-in example is in `references/example.md`. Use it to calibrate tone, level of detail and how to show the sample-size math.

**Step 5: Call out gaps.** Consolidate what's still open in the "⚠️ Gaps" section. High priority:
- the success metric isn't defined
- the sample size is missing, so there's no way to know whether traffic can support the test
- the estimated sample is larger than the available traffic
- the decision rules aren't defined before launch

## Lean flow

The lean format is the **executive summary of the experiment** in five blocks, following `assets/experiment-plan-lean-template.md`. It has three starting points:

- **A hypothesis document exists but no plan yet** (the most common case): take the context, problem, statement, metrics and gaps from it, and ask only for what the one-pager still needs (variants, split, audience rules, owner).
- **A full plan already exists** (the user points to it): condense or expand **in the same file** without asking again for what it already answers. Lean and full are the same document, so changing format means editing the file, not creating a sibling.
- **Starting from scratch**: collect only the lean minimum. That is the hypothesis (or the hypothesis-builder output), team, context data, variants + traffic split, success metric and guardrails, and owner. Anything missing becomes a placeholder (`[TBD]`), never an invention.

How to fill each block:

- **Context**: a short paragraph on the product or flow, then bullets with the data that supports the problem (numbers in context) and a link to the source discovery or hypothesis. If the data has a limitation that only the experiment can resolve, say so here.
- **Problem**: three linked sentences, in exactly this skeleton: **"We observed that:** [current state, with the data that sizes it], **which causes:** [affected persona/cohort] **to suffer from:** [why the current state isn't ideal: the pain, or the value left on the table]".
- **Hypothesis**: **"We believe that:** [proposed solution] **for:** [cohort] **will result in:** [success metric + direction] **because:** [evidence-based reason]". If the experiment decides a trade-off (e.g. volume × conversion), close the block with it.
- **Scope**: test type + traffic split + randomization unit; bullets for the variants (control first); a design link if there is one; and a "Business rules" sub-block in bullets covering audience, exclusions, variant rules, ramp if any, and platform setup (flag, mutual exclusion).
- **Metrics**: **"Measured by:"** (the success metric first, with baseline when known, then any supporting funnel metrics) and **"Guarded by:"** (guardrails, with the acceptable limit when defined).
- **Open items**: anything unknown or unconfirmed, including the gaps carried over from the hypothesis, one line each, high-priority ones first. Omit the block if nothing is open.

Rules for the lean format: no identification table, sample-size table, risks or results. Anyone who needs those uses the full format. When delivering, also offer the Markdown in a single code block, ready to paste into a doc or wiki.

## Essential standards

- **Hypothesis:** "We believe that [change] for [segment] will [result] because [reason]." Reuse it from hypothesis-builder when it comes from there.
- **Metrics:** Success (one only: the Overall Evaluation Criterion, the hypothesis's primary metric), Primary (the main funnel KPIs around it), Secondary, Guardrail. Always give the expected effect with a sign and a unit ("+5% relative", "no drop greater than 1 percentage point").
- **Sample size:** fill in the table in the Sample size section with baseline, MDE and estimated weeks, and show the math. If the required sample exceeds the available traffic, log it as a high-priority gap.
- **Randomization unit:** a logged-in user ID for authenticated flows and an anonymous/device ID for logged-out flows. This keeps assignment stable across sessions (sticky assignment). Avoid session-level randomization for anything a user can see twice.
- **Platform setup:** fill in the platform setup callout (experiment key, feature flag, variants, split, mutual exclusion) whenever engineering is involved. It's the field that saves the most questions during implementation.
- **Gradual rollout:** recommend a ramp (10% → 25% → 50% → 100%) for high-traffic or high-risk flows. It isn't needed for email or other controlled-channel experiments.
- **Decide before launch:** the decision rules (win / lose / inconclusive) are written before the test starts, not after. You may propose defaults marked *(proposed, to confirm)*, and they stay a gap until the team confirms them.
- **Tone:** first person plural ("we observed…", "we expect…"), analytical, numbers in context (absolute and relative).

## Delivery

Name the file `experiment-plan.md` inside a folder named after a short kebab-case slug, next to the hypothesis if there is one, for example `signup-form-fields/experiment-plan.md`. If the user has a place where experiment docs live (a repo folder, a wiki, a doc tool), ask and follow it. If you can't write files where you're running, give the document as a downloadable file or a single copyable Markdown block. Show the result and ask whether they want to adjust any section before closing.

> This skill **doesn't write directly into project-management or doc tools and doesn't run queries**. It produces a versionable Markdown document. If the user has existing metric definitions or queries, reference them rather than inventing new logic.
