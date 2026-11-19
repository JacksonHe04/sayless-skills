---
name: sayless-skills
description: Index and publish workflow for Sayless's public agent skills collection (github.com/JacksonHe04/sayless-skills). Use when someone asks which skills sayless publishes, how to install them via `npx skills add` or `gh skill install`, or how to add a new public skill here — including the mandatory pre-publish checklist for stripping private data, credentials, internal paths and customer content before anything goes public.
license: MIT
metadata:
  author: JacksonHe04
  repo: "https://github.com/JacksonHe04/sayless-skills"
---

# Sayless Skills

The public side of my agent skills: a small, curated collection published under the
[Agent Skills](https://agentskills.io) open standard. A skill is just a directory with a
`SKILL.md` — no build step, no package registry.

This repository is itself a skill (`sayless-skills`, the file you are reading) and a container
for the public skills under `skills/`.

## Layout

```
sayless-skills/
├── SKILL.md          # this file — the collection's own skill
├── README.md         # human-facing guide
├── LICENSE
└── skills/
    └── <skill-name>/
        ├── SKILL.md  # required
        ├── scripts/  # optional
        ├── references/
        └── assets/
```

## Available skills

None published yet. This file is the index — update the table below whenever a skill lands in
`skills/`.

| Skill | What it does | Install |
| --- | --- | --- |
| — | — | — |

## Installing

Install everything into the current project:

```bash
npx skills add JacksonHe04/sayless-skills
```

Install one skill globally, no prompts:

```bash
npx skills add JacksonHe04/sayless-skills --skill <skill-name> -g -a claude-code -y
```

Other entry points:

```bash
npx skills add JacksonHe04/sayless-skills --list          # see what exists without installing
npx skills add JacksonHe04/sayless-skills@v1.0.0          # pin to a release tag
gh skill install JacksonHe04/sayless-skills <skill-name>  # GitHub CLI path
```

The CLI symlinks skills into each agent's directory (`~/.claude/skills/`, `~/.agents/skills/`,
`~/.codex/skills/`, …). Use `--copy` if a host does not follow symlinks.

## Adding a public skill

1. Create `skills/<name>/SKILL.md`.
2. `name` in the frontmatter must equal `<name>`: lowercase letters, digits and hyphens, 1–64
   chars, no leading/trailing or doubled hyphens.
3. `description` (≤1024 chars) must state both **what it does** and **when to use it** — it is the
   only thing an agent sees before deciding to load the skill. Put the trigger words people
   actually type in it.
4. Keep `SKILL.md` under 500 lines. Move detail into `references/`, code into `scripts/`, and
   reference those files with paths relative to the skill root, one level deep.
5. Add the row to the table above.
6. Run the pre-publish checklist below. It is not optional.

## Pre-publish checklist

Everything here assumes the skill was **lifted from a working private setup**, which is almost
always the case. Public means public forever — a deleted commit still lives in forks and caches.

Strip before committing:

- **Credentials**: API keys, tokens, cookies, `~/.ssh` material, `.env` files, MCP config with
  secrets, signed URLs. Nothing that authenticates should ever reach this repo.
- **Real data**: customer or company records, real names, phone numbers, emails, chat logs,
  database dumps, screenshots with real accounts. Replace with synthetic examples.
- **Internal context**: private repo names and URLs, internal hostnames, ticket IDs, org names,
  unreleased product names, salary/HR content, anything under an NDA.
- **Local absolute paths**: `/Users/<name>/...`, `~/Codes/...`, machine-specific mounts. Use
  placeholders like `<project>` or relative paths.
- **Personal traces**: personal email addresses, calendars, notes-to-self that name real people.

Then grep for what you missed:

```bash
grep -rInE "(sk-|ghp_|gho_|AKIA|xox[bp]-|-----BEGIN [A-Z ]*PRIVATE KEY)" .
grep -rInE "(/Users/|~/[A-Z]|@[a-z0-9.-]+\.(com|cn|io))" .
grep -rIn "TODO\|FIXME\|internal\|confidential" .
```

Read every hit before dismissing it — a false positive takes ten seconds, a leaked token takes a
weekend.

## Validating

```bash
npx skills add JacksonHe04/sayless-skills --list   # collection parses, skills are discoverable
npx skills add ./skills/<name> --list              # local folder before pushing
skills-ref validate ./skills/<name>                # if skills-ref is installed
```

## Releasing

Tag when a skill's behaviour changes in a way users should be able to pin:

```bash
git tag v1.0.0 && git push origin v1.0.0
```

Tags are what `npx skills add owner/repo@v1.0.0` resolves to, so the tag must point at a commit
where every skill in the collection is in a working state.
