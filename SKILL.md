---
name: sayless-skills
description: Index and publish workflow for Sayless's public agent skills collection (github.com/JacksonHe04/sayless-skills). Use when someone asks which skills sayless publishes, how to install them via `npx skills add` or `gh skill install`, or how to add a new public skill here — including the mandatory pre-publish checklist for stripping private data, credentials, internal paths and customer content before anything goes public.
license: MIT
compatibility: No runtime required. The install commands need Node.js 22.20+ (for npx skills) or the GitHub CLI with its skill command.
allowed-tools: Read Write Edit Bash Grep Glob
metadata:
  author: JacksonHe04
  version: "0.2.0"
  repo: "https://github.com/JacksonHe04/sayless-skills"
  homepage: "https://sayless.inon.space"
  language: en
  audience: agent
  updated: "2026-11-20"
---

# Sayless Skills

The public half of my agent skills: a small, curated collection published under the
[Agent Skills](https://agentskills.io) open standard. A skill is a directory with a `SKILL.md` —
no build step, no package registry, no npm package.

This file is the **agent-facing** side: the index, the install commands, the add-a-skill workflow
and the pre-publish checklist. Human-facing documentation (what this repo is, why it exists, how
to browse it) lives in [README.md](README.md) — do not answer a reader's "what is this" question
from this file alone.

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

None published yet. This table is the index — every skill under `skills/` gets a row here in the
same commit that adds it.

| Skill | What it does | Install |
| --- | --- | --- |
| — | — | — |

## Installing

Everything into the current project:

```bash
npx skills add JacksonHe04/sayless-skills
```

One skill, global, non-interactive:

```bash
npx skills add JacksonHe04/sayless-skills --skill <skill-name> -g -a claude-code -y
```

Other entry points:

```bash
npx skills add JacksonHe04/sayless-skills --list           # see what exists, install nothing
npx skills add JacksonHe04/sayless-skills@v0.2.0           # pin to a release tag
gh skill install JacksonHe04/sayless-skills <skill-name>   # GitHub CLI path
```

The CLI symlinks skills into each host's directory (`~/.claude/skills/`, `~/.agents/skills/`,
`~/.codex/skills/`, …). Add `--copy` when a host does not follow symlinks.

## Adding a public skill

1. Create `skills/<name>/SKILL.md`.
2. `name` must equal `<name>`: lowercase letters, digits and hyphens, 1–64 chars, no leading,
   trailing or doubled hyphens.
3. `description` (≤1024 chars) must state both **what it does** and **when to use it**. It is the
   only thing an agent sees before deciding to load the skill — put the words people actually type
   in it.
4. Fill the optional fields instead of the minimum: `license`, `compatibility` when the skill has
   environment needs, and `metadata` with at least `author`, `version`, `updated`. `version` lives
   inside `metadata` — the specification defines no top-level version field.
5. Keep `SKILL.md` under 500 lines. Details go to `references/`, code to `scripts/`, referenced
   with paths relative to the skill root, one level deep.
6. Add the row to the table above.
7. Run the checklist below. It is not optional.

## Pre-publish checklist

Everything here assumes the skill was **lifted from a working private setup**, which is almost
always the case. Public means public forever — a deleted commit still lives in forks and caches.

Strip before committing:

- **Credentials**: API keys, tokens, cookies, `~/.ssh` material, `.env` files, MCP config with
  secrets, signed URLs. Nothing that authenticates may reach this repo.
- **Real data**: customer or company records, real names, phone numbers, emails, chat logs,
  database dumps, screenshots with real accounts. Replace with synthetic examples.
- **Internal context**: private repo names and URLs, internal hostnames, ticket IDs, org names,
  unreleased product names, anything under an NDA.
- **Local absolute paths**: `/Users/<name>/...`, `~/Codes/...`, machine-specific mounts. Use
  placeholders such as `<project>` or relative paths.
- **Personal traces**: personal email addresses, calendars, notes-to-self naming real people.

Then grep for what you missed:

```bash
grep -rInE "(sk-|ghp_|gho_|AKIA|xox[bp]-|-----BEGIN [A-Z ]*PRIVATE KEY)" .
grep -rInE "(/Users/|~/[A-Z]|@[a-z0-9.-]+\.(com|cn|io))" .
grep -rIn "TODO\|FIXME\|internal\|confidential" .
```

Read every hit before dismissing it — a false positive costs ten seconds, a leaked token costs a
weekend.

## Validating

```bash
npx skills add JacksonHe04/sayless-skills --list   # collection parses, skills are discoverable
npx skills add ./skills/<name> --list              # local folder before pushing
skills-ref validate ./skills/<name>                # if skills-ref is installed
```

## Releasing

Bump `metadata.version` and tag the same commit, so the tag and the declared version agree:

```bash
git tag v0.2.0 && git push origin v0.2.0
```

`npx skills add owner/repo@v0.2.0` resolves to that tag, so it must point at a commit where every
skill in the collection works.
