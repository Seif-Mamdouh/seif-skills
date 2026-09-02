# seif-skills

A collection of Claude Code skills. Each skill lives in `skills/<name>/` with a `SKILL.md` entry point.

| Skill | What it does |
|---|---|
| `debugger` | Hypothesis-driven debugging workflow using read-only investigation scripts. |
| `grill-me` | Grilling session that stress-tests a plan against your project's domain model and updates CONTEXT.md / ADRs inline. |
| `microworld` | Builds an interactive "micro world" so you can understand a diff, feature, or plan by playing with it instead of reading it. |
| `explain-diff` | Produces a rich, interactive HTML explanation of a code change, diff, branch, or PR. |
| `plan` | Controlled technical writing (CTE, ASD-STE100, Google style, Diátaxis) for precise, translatable docs. |

## Install

Copy any skill folder into your user-level skills directory:

```sh
cp -R skills/<name> ~/.claude/skills/
```

or into a project's `.claude/skills/` to scope it to that repo.
