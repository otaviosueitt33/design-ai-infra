# design-ai-infra

Open AI skills for product and growth experimentation, by [Otávio Sueitt](https://www.linkedin.com/in/otaviosueitt/).

They come from my work leading Growth Design: a hypothesis is only useful if it is testable, falsifiable and decided before the test runs. These skills guide anyone, one short round at a time, from a loose idea to an experiment a team can actually ship and read. They work with any LLM and answer in the language you write in.

```
 loose idea ──► hypothesis-builder ──► hypothesis.md ──► experiment-plan ──► experiment-plan.md
```

| Skill | What it does | Output |
|---|---|---|
| [**hypothesis-builder**](skills/hypothesis-builder/SKILL.md) | Turns an idea into a testable, falsifiable hypothesis in 9 blocks (problem, evidence, opportunity, statement, prediction and primary metric, assumptions, design, decision table, results) and names every gap that blocks prioritization. | `hypothesis.md` |
| [**experiment-plan**](skills/experiment-plan/SKILL.md) | Turns the hypothesis into an executable plan: audience, variants, randomization, metrics, sample size with the math shown, rollout and stop criteria, risks, pre-registered decision rules and a pre-launch checklist. Full or one-page lean format. | `experiment-plan.md` |

What they won't do: invent data. Anything you don't know becomes a `[TBD]` placeholder and a listed gap.

## Download

| File | For |
|---|---|
| [design-ai-infra.zip](https://github.com/otaviosueitt33/design-ai-infra/releases/latest/download/design-ai-infra.zip) | Everything: both skills, single-file prompts and docs |
| [hypothesis-builder.prompt.md](https://github.com/otaviosueitt33/design-ai-infra/releases/latest/download/hypothesis-builder.prompt.md) · [experiment-plan.prompt.md](https://github.com/otaviosueitt33/design-ai-infra/releases/latest/download/experiment-plan.prompt.md) | Any chat LLM (one file each, everything inlined) |
| [hypothesis-builder.zip](https://github.com/otaviosueitt33/design-ai-infra/releases/latest/download/hypothesis-builder.zip) · [experiment-plan.zip](https://github.com/otaviosueitt33/design-ai-infra/releases/latest/download/experiment-plan.zip) | Tools that import a skill as a zip (Claude apps) |

## How to use

### Any LLM (ChatGPT, Gemini, Claude, Copilot, Mistral, Llama, an API…)

Use the single-file prompts in [`dist/`](dist/). Each one bundles the skill and every template and reference it needs.

1. Download `hypothesis-builder.prompt.md` (or `experiment-plan.prompt.md`).
2. Either paste it as the system prompt or custom instructions (a ChatGPT custom GPT or Project, a Gemini Gem, a Claude Project, an API system prompt), or attach it to a chat and write *"Follow the instructions in this file."*
3. Describe your idea. The model will guide you and hand back the Markdown document.

### Claude Code

```bash
claude plugin marketplace add otaviosueitt33/design-ai-infra
claude plugin install design-ai-infra@design-ai-infra
```

Or copy the folders in `skills/` to `~/.claude/skills/`. Claude picks the right skill from what you ask, for example *"I have a test idea: …"* or *"turn this hypothesis into an experiment plan"*.

### Claude apps (claude.ai and desktop)

Download `hypothesis-builder.zip` and `experiment-plan.zip` and upload each one as a skill in the app's skill settings.

### Other agents that support skills

The folders in `skills/` follow the open Agent Skills format (a `SKILL.md` with `name` and `description` frontmatter, plus `assets/` and `references/`). If your agent supports it, copy them to the skills directory described in its docs. Coding agents that read `AGENTS.md` will find the skills from this repository's [`AGENTS.md`](AGENTS.md).

## Repository layout

```
skills/
  hypothesis-builder/   SKILL.md · assets/hypothesis-template.md · references/canonical-structure.md
  experiment-plan/      SKILL.md · assets/ (full and lean templates) · references/ (writing guide, worked example)
dist/                   single-file prompts, generated from skills/
.claude-plugin/         Claude Code plugin and marketplace manifests
scripts/build.py        regenerates dist/ and the zips
AGENTS.md               instructions for coding agents
```

## Contributing

Edit the files in `skills/`, then run `python3 scripts/build.py` to regenerate `dist/`. Issues and pull requests are welcome.

## Credits

The structure draws on Reforge, Teresa Torres (Continuous Discovery), Lean UX and Lean Startup, and Kohavi, Tang and Xu's *Trustworthy Online Controlled Experiments*. Full sources are in [`canonical-structure.md`](skills/hypothesis-builder/references/canonical-structure.md). All examples are illustrative, with made-up numbers.

## License

[MIT](LICENSE). Use, adapt and share freely.

---

### Em português

Skills abertas de IA para experimentação em produto e growth. A **hypothesis-builder** transforma uma ideia solta numa hipótese testável e falseável, e a **experiment-plan** transforma a hipótese num plano de experimento executável. Funcionam com qualquer LLM e respondem no idioma em que você escrever. Para usar no ChatGPT, Gemini ou outro chat, baixe o arquivo `.prompt.md` da skill e cole como instrução ou anexe na conversa. As instruções para Claude e outros agentes estão acima.
