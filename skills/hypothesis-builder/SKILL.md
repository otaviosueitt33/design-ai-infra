---
name: hypothesis-builder
description: Guides the user, one short round at a time, from a loose idea to a product or growth hypothesis that is testable, falsifiable and ready to prioritize, and names what is still missing. Delivers a Markdown document with a metadata header and 9 blocks (context and problem, evidence, opportunity, hypothesis statement, prediction and primary metric, assumptions, experiment design, decision table, results) plus a Gaps section. Use when someone wants to write, structure or review a hypothesis, experiment or A/B test. Typical prompts are "I have a test idea", "I think if we change X, Y improves", "help me frame this hypothesis" and "is this a good hypothesis?". Also use when someone pastes a rough idea and asks to make it testable. If the hypothesis is already written and the user wants the operational plan (sample size, rollout, stop criteria, pre-launch checklist), use the experiment-plan skill instead.
---

# Hypothesis Builder

This skill turns a loose idea into a **product hypothesis that is testable, falsifiable and decidable**. It works as a **guided conversation**. It asks questions, fills in what it can from the answers, and **says explicitly what is still missing**. A hypothesis with no evidence and no decision rule is still a guess.

The output is always a **Markdown file** with the 9-block structure in `assets/hypothesis-template.md`, plus a **Gaps** section listing what must be resolved before prioritizing.

## Language

This skill is written in English, but **talk to the user in the language they write in, and write the document in that language too**. Translate everything in the template into that language, keeping the meaning: headings, fixed phrases ("We believe that…", "To verify this, we will…"), status values and table cells. Keep widely used acronyms (OEC, MDE, A/B) and explain each one the first time it appears.

## Principles (your quality filter)

The user does not need to memorize these, but you should check every answer against them. A good hypothesis is:

- **Testable**: you can design an experiment that confirms or refutes it. If you can't, it is an opinion.
- **Falsifiable**: some outcome would prove it *wrong*. "Improving the UI makes users happier" is not falsifiable. "Cutting the signup form from 5 to 3 fields increases completion" is.
- **Specific**: it names the exact change, the segment, the metric and the direction of the effect.
- **Grounded in evidence**: it comes from data, research or observed behavior, not a hunch.
- **One change per hypothesis**: three ideas are three hypotheses. Testing them together produces data nobody can interpret.
- **Honest about uncertainty**: it names the riskiest assumption (the *leap of faith*). In large-scale programs such as Microsoft's, roughly a third of tested ideas improve the target metric, a third are neutral and a third make it worse. That is why a rigorous design matters.

When something the user says breaks one of these principles (two changes bundled together, a vague metric, no evidence), **say so kindly and explain why**. Don't just record it. When the user bundles several changes, pick one with them for this document. Log each of the others as a separate hypothesis in the Gaps section, and offer to write it next.

## How to run the conversation

Don't dump all 9 blocks at once or ask for everything in one giant form, because that stalls people. Work in **short, themed rounds**, and play back what you understood before moving on.

**Step 1: Find the starting point.** Ask what the user already has: an observed pain, a data point that caught their eye, or a solution idea. That decides where to begin. If they arrive with a ready-made solution ("I want to test a new button"), steer back to the problem before accepting it. Good hypotheses start from the problem, not the feature.

**Step 2: Core first.** Help write the problem (Block 1) and the hypothesis statement (Block 4), since they anchor everything else. Use this format:
> **We believe that** [specific change] **for** [segment] **will** [impact + direction on a metric] **because** [evidence-based reason]. **And therefore** [business consequence].

Make sure the statement has the four non-negotiable elements: **change, segment, metric/direction and reason**. If one is missing, ask for it.

**Step 3: Evidence (Block 2).** Ask what the belief rests on, both qualitative (interviews, support tickets, NPS comments, session recordings) and quantitative (funnel data, usage analytics, benchmarks). **This skill does not fetch data.** It works with what the user provides. If the evidence is empty or weak, log it as a high-priority gap and say so plainly: *"without evidence this is still an idea, not a hypothesis ready to prioritize. It's worth gathering [X] first."* Suggest **what evidence you would look for** (for example "check the completion rate at this funnel step" or "pull 5 support tickets about this"), but never invent it.

**Step 4: Prediction and metrics (Block 5).** This is where the belief becomes a decidable test:
> **To verify this, we will** [experiment]. **We will measure** [metric]. **We'll know we're right if** [measurable condition].

Insist on **one primary metric (OEC)** and at least one **guardrail**, meaning something that must not get worse, such as cost, latency, churn or revenue. A gain that hides a loss is the most common mistake.

**Step 5: Assumptions, design and decision (Blocks 6–8).** Name the **riskiest assumption**. Sketch the **design**: test type, groups, allocation and the tool that will run it. Then fill in the **decision table BEFORE the test runs**: what you will do on a win, a loss and an inconclusive result. Deciding in advance prevents rationalizing the result afterwards. If the user has no rules yet, you may propose the defaults from the template, marked *(proposed, to confirm)*. The gap stays open until the team confirms them.

**Step 6: Opportunity and alignment (Block 3).** Size the opportunity whenever possible. Ask which goal the hypothesis serves. If the team uses OKRs, connect it to a key result. A team without OKRs is fine and isn't a gap. Having no goal at all is a low-priority gap. You can cover this alongside the core if the user already has the numbers.

Block 9 (Results & Learnings) is filled in **after** the experiment runs. Keep it in the template, but don't push for it now.

Match the depth to where the user is. An idea-stage hypothesis can have shallow blocks as long as its gaps are named. Don't stall the conversation by demanding perfection in every field.

## Calling out gaps (the heart of this skill)

As the conversation goes on, **keep track of what is still open** and consolidate it at the end in the "⚠️ Gaps" section. For each gap, state *what is missing* and *how the user could fill it*. Base what you ask for on this quality checklist:

- [ ] Is the change specific (could someone else implement it without asking)?
- [ ] Is it falsifiable (could some result prove it wrong)?
- [ ] Is there only one change?
- [ ] Is there evidence (qualitative and/or quantitative)?
- [ ] Is a single primary metric (OEC) defined?
- [ ] Is there a guardrail metric?
- [ ] Is the size of the opportunity quantified?
- [ ] Is the riskiest assumption named?
- [ ] Was the decision table defined before running?
- [ ] Does it connect to a goal? (OKR only if the team uses them; no goal at all is a low-priority gap.)

Treat missing evidence, a missing OEC and a missing decision table as **high-priority** gaps. Without them the hypothesis should not be prioritized.

## Delivery

Generate a Markdown file from `assets/hypothesis-template.md`. Fill the blocks with what you collected, put `[TBD]` in empty fields, and replace the sample items in the Gaps section with the real open items. **Never invent data.** A placeholder is always better than a plausible-looking number.

Name the file `hypothesis.md` inside a folder named after a short kebab-case slug, for example `signup-form-fields/hypothesis.md`. If the user has a place where experiment docs live (a repo folder, a wiki, a doc tool), ask and follow it. If you can't write files where you're running, give the document as a downloadable file or a single copyable Markdown block. Show the result and ask whether they want to adjust any block before closing.

If the hypothesis is going to become an A/B test, the next step is the **experiment-plan** skill. It reuses Blocks 1–8 to build the operational plan (audience, sample size, rollout, stop criteria, checklist). If that skill isn't installed, tell the user it is the natural next step and offer to sketch the sample size with the formula in `references/canonical-structure.md`.

## Prioritization (optional, when asked)

Once hypotheses are written, if the user wants to decide what to test first, use **ICE**, scoring each factor from 1 to 10: `Score = Impact × Confidence × Ease`. Confidence reflects how strong the evidence is (10 = strong prior data, 1 = a hunch). Use **RICE** (Reach × Impact × Confidence ÷ Effort) when reach varies a lot between ideas.

## Reference

`references/canonical-structure.md` has the full canonical structure:

- a detailed description of each of the 9 blocks
- a glossary (OEC, MDE, guardrail, sticky assignment, mutual exclusion)
- the frameworks each block comes from
- two filled-in examples: a SaaS signup form and e-commerce shipping costs

Open it when you need the detail of a specific block or the glossary, or want to show the user what a well-filled block looks like.
