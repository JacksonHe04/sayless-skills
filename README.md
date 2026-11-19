# sayless-skills

Public agent skills by [@JacksonHe04](https://github.com/JacksonHe04), published in the
[Agent Skills](https://agentskills.io) open format. One skill is one directory with a `SKILL.md`:
no build step, no package registry, nothing to compile.

The point is restraint. Everything here was first a private workflow that actually ran on my own
machine, then got stripped of anything that belongs to me or my employer, then shipped. If a skill
is here, it earned its place by being useful more than once.

## Install

```bash
npx skills add JacksonHe04/sayless-skills                  # into the current project
npx skills add JacksonHe04/sayless-skills --list           # just show what exists
npx skills add JacksonHe04/sayless-skills --skill <name> -g  # one skill, globally
```

`npx skills` is Vercel Labs' installer for the Agent Skills ecosystem — it runs from npm, but the
skills themselves come from this Git repository. It symlinks them into each host's directory
(`~/.claude/skills/`, `~/.agents/skills/`, `~/.codex/skills/`, …), so one update reaches every
agent you use.

Prefer GitHub's own tooling?

```bash
gh skill install JacksonHe04/sayless-skills <name> --pin v0.2.0
```

## What's inside

Currently: the collection's own skill (`SKILL.md`), which doubles as the index and the publishing
guide. Public skills go under `skills/<name>/` — nothing there yet, because publishing is a
careful act, not a dump.

```
SKILL.md        # the collection's own skill: index, add-a-skill flow, pre-publish checklist
README.md       # you are here
LICENSE         # MIT
skills/         # individual public skills, one directory each
```

When skills land, they get listed in `SKILL.md` with a one-line "what it does" — that table is the
canonical index; this README will not maintain a second copy of it.

## Why so few

A leaked API key, a real customer name or an internal hostname inside a skill is a bad trade for a
star. Every skill added here passes the checklist in `SKILL.md`: credentials, real data, internal
paths and personal traces removed, then grepped for again. That is why the collection grows slowly.

## Contributing

Issues and ideas are welcome. If you want to add a skill, read `SKILL.md` first — it defines the
frontmatter fields, the naming rules and the checklist a pull request has to pass.

## 中文

这是我公开的 Agent Skills 集合，遵循 [Agent Skills](https://agentskills.io) 标准。技能都来自我自己真实在跑的私有工作流，脱敏后才放进来。

```bash
npx skills add JacksonHe04/sayless-skills
```

加技能前请先读 `SKILL.md` 里的规范与脱敏清单。

## License

MIT — see [LICENSE](LICENSE).
