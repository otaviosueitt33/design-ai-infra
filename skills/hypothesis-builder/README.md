# hypothesis-builder

Turns a loose idea into a product or growth hypothesis that is **testable, falsifiable and ready to prioritize**, in 9 blocks: context and problem, evidence, opportunity, hypothesis statement, prediction and primary metric, assumptions, experiment design, decision table and results. It guides you one short round at a time, answers in the language you write in, never invents data, and ends with a list of the gaps you still need to close.

**Output:** `hypothesis.md`. **Next step:** [experiment-plan](../experiment-plan/).

## Use it

- **Any chat LLM (ChatGPT, Gemini, Claude, Copilot…):** download [hypothesis-builder.prompt.md](https://github.com/otaviosueitt33/design-ai-infra/releases/latest/download/hypothesis-builder.prompt.md), paste it as instructions or attach it, and describe your idea.
- **Claude Code, Claude apps and other agents:** see [How to use](../../README.md#how-to-use).

Try a first message like *"I have a test idea: if we show shipping costs on the product page, more people will finish checkout."*

## Files

- [`SKILL.md`](SKILL.md): the instructions the model follows
- [`assets/hypothesis-template.md`](assets/hypothesis-template.md): the 9-block template
- [`references/canonical-structure.md`](references/canonical-structure.md): principles, glossary, sample-size formula and two worked examples

## Contribute

Ideas, fixes and translations are welcome. [Open an issue](https://github.com/otaviosueitt33/design-ai-infra/issues) or send a pull request, then run `python3 scripts/build.py` to regenerate `dist/`.
