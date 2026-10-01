# experiment-plan

Turns a hypothesis into an **executable experiment plan**: target audience, variants, randomization unit, platform setup, metrics (success, primary, secondary, guardrail), sample size with the math shown, rollout and stop criteria, risks, decision rules set before launch, a pre-launch checklist and a results section. Comes in a **full** format for formal review and a **lean** one-pager for quick alignment. It asks for your team, owner and tooling instead of assuming them, and never invents data.

**Output:** `experiment-plan.md`. **Works best after:** [hypothesis-builder](../hypothesis-builder/).

## Use it

- **Any chat LLM (ChatGPT, Gemini, Claude, Copilot…):** download [experiment-plan.prompt.md](https://github.com/otaviosueitt33/design-ai-infra/releases/latest/download/experiment-plan.prompt.md), paste it as instructions or attach it, then paste your hypothesis.
- **Claude Code, Claude apps and other agents:** see [How to use](../../README.md#how-to-use).

Try a first message like *"Turn this hypothesis into an experiment plan"*, followed by your `hypothesis.md`.

## Files

- [`SKILL.md`](SKILL.md): the instructions the model follows
- [`assets/experiment-plan-template.md`](assets/experiment-plan-template.md) and [`assets/experiment-plan-lean-template.md`](assets/experiment-plan-lean-template.md): full and lean templates
- [`references/writing-guide.md`](references/writing-guide.md): how to write each section
- [`references/example.md`](references/example.md): a filled-in example with the sample-size math worked out

## Contribute

Ideas, fixes and translations are welcome. [Open an issue](https://github.com/otaviosueitt33/design-ai-infra/issues) or send a pull request, then run `python3 scripts/build.py` to regenerate `dist/`.
