# Agent instructions

This repository contains AI skills for product and growth experimentation. Each skill is a folder in `skills/` with a `SKILL.md` (instructions, with a `name` and `description` in the frontmatter) plus the `assets/` and `references/` files it uses.

| Skill | Use it when the user wants to |
|---|---|
| `skills/hypothesis-builder` | write, structure or review a product/growth hypothesis, or make a rough idea testable |
| `skills/experiment-plan` | turn a hypothesis into an executable experiment plan (A/B test plan, test spec, XP Plan) |

When a request matches a skill, read its `SKILL.md` and follow it. Open the files it references only when you need them. The skills chain: a hypothesis from `hypothesis-builder` is the input for `experiment-plan`.

If you can't read the folders, use the single-file versions in `dist/`, which inline every referenced file.

Maintenance: after changing anything in `skills/`, run `python3 scripts/build.py` to regenerate `dist/`.
