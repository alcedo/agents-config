# agents-config

This repository is the reusable, project-agnostic agent setup that new projects start from.
It is the base agent container for Victor's future projects: standing rules in `agents.md`, plus the Cursor skills, agents, and docs under `.cursor/`.
A new project copies this tree or inherits it.
Nothing here is specific to one application.

## What's inside

Standing rules for agents live in `agents.md`.
Third-party skills and agents live under `.cursor/` so Cursor can load them when this repo, or a copy of it, is the workspace.

- `agents.md` - standing rules.
- Skills: `.cursor/skills/<name>/SKILL.md`.
- Agents: `.cursor/agents/` (`poteto-agent`, `comment-sicko`).
- Guide: `.cursor/docs/` (pstack guide and harness notes).
- `.cursor/README.md` - upstream pstack readme, kept here so `./skills`, `./agents`, and `./docs` links resolve.
- `.cursor/automations/benny/` - dormant pstack automation pack. Not registered as slash skills.
- Licences: `.cursor/licenses/`.
- Provenance, upstream commits, and skipped files: `.cursor/skills/THIRD_PARTY.md`.

### pstack

pstack is by Lauren Tan (poteto), vendored from [cursor/plugins](https://github.com/cursor/plugins/tree/main/pstack) (`pstack/`).
Licence: MIT, Copyright (c) 2026 Lauren Tan, at `.cursor/licenses/pstack/LICENSE`.
Invoke it with `/poteto-mode`.
The other pstack skills are the same kind of slash command.
The skill list is in `.cursor/README.md`.
The upstream commit and what this copy left out are in `.cursor/skills/THIRD_PARTY.md`.

### Ponytail

Ponytail is by DietrichGebert, vendored from [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail).
Licence: MIT, Copyright (c) 2026 DietrichGebert, at `.cursor/licenses/ponytail/LICENSE`.
Invoke it with `/ponytail`, `/ponytail-review`, `/ponytail-audit`, `/ponytail-debt`, `/ponytail-gain`, or `/ponytail-help`.
`/ponytail` takes `lite`, `full`, `ultra`, or `off` for that invocation.

Ponytail runs only when you invoke it.
It is not an always-on rule, because its rules clash with `agents.md`.
Ponytail wants the shortest diff and drops scope nobody asked for.
`agents.md` prefers quality, pixel perfection, and fixing lint, tests, and flakiness you notice.
The always-on copies were not installed (`AGENTS.md`, `.cursor/rules/ponytail.mdc`, and the same ruleset for other hosts).
No hooks are installed.
Ponytail's hooks run Node on session start and on every prompt, and none of `hooks/` or `scripts/cursor-hooks.js` is in this repo.
The skip list is in `.cursor/skills/THIRD_PARTY.md`.

## Use it in a new project

There is no install or sync script yet.
Copy by hand.

Into a new project, copy `agents.md` and these pieces of `.cursor/`:

- `.cursor/skills/`
- `.cursor/agents/`
- `.cursor/docs/`
- `.cursor/README.md`

`THIRD_PARTY.md` sits inside `.cursor/skills/`, so it comes with the skills.
Copy `.cursor/licenses/` as well if the new project should keep the MIT licence files.
Copy `.cursor/automations/benny/` only if you want the dormant Benny pack.

For global use, copy or symlink the same `.cursor` pieces into `~/.cursor/`:

- `.cursor/skills` to `~/.cursor/skills`
- `.cursor/agents` to `~/.cursor/agents`
- `.cursor/docs` to `~/.cursor/docs`
- `.cursor/README.md` to `~/.cursor/README.md`

Skill-to-skill links keep working from that copy.
`/poteto-help` links to `docs/` and `README.md` beside the skills directory, so the docs and readme copies are what make those guide links resolve.
Copy `agents.md` into each new project.
It is a project file.
Do not replace the rest of `~/.cursor`.
Do not symlink this whole `.cursor` directory onto `~/.cursor`.
