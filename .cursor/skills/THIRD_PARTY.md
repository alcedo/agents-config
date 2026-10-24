# Third-party skills

These packs are vendored copies.
Skill text is unchanged except the one path note under pstack.
Licences are MIT and live next to this tree.

This repo had no skill directory, installer, or skill manifest.
Cursor loads project skills from `.cursor/skills/<name>/SKILL.md` and project agents from `.cursor/agents/<name>.md`.
pstack's README, guide, and skills link to `./skills`, `./agents`, `./docs`, and `../<skill>` from the plugin root, so that root is `.cursor/` here.
There is no sync script.
Copy or symlink `.cursor/skills` to `~/.cursor/skills` and `.cursor/agents` to `~/.cursor/agents` when you want them in every project.
Do not symlink this whole `.cursor` directory onto `~/.cursor`, because it also holds the pstack guide and licences.

coderbits pull request 21 was not readable from this environment (the repository returned 404).
The layout follows the choices named for that pull request: faithful skill text, both MIT licences, source URLs and upstream SHAs in this note, no Ponytail always-on ruleset, and no Ponytail hooks.

## pstack

- Source: https://github.com/cursor/plugins/tree/main/pstack
- Upstream commit: `9580c23696ac8d7abed0c166f2f9918800afb819` on `cursor/plugins` (tree `pstack/`, plugin version 0.15.32)
- Licence: MIT, Copyright (c) 2026 Lauren Tan. See [pstack licence](../licenses/pstack/LICENSE).
- Author: Lauren Tan (poteto)

Copied:

- Skills: `.cursor/skills/<name>/` for every directory under upstream `pstack/skills/` (58 skills).
- Agents: `.cursor/agents/poteto-agent.md`, `.cursor/agents/comment-sicko.md`.
- Guide and adapter: `.cursor/docs/` (upstream `pstack/docs/`).
- Readme: `.cursor/README.md` (upstream `pstack/README.md`), so `./skills`, `./agents`, and `./docs` links resolve.
- Benny automation pack: `.cursor/automations/benny/` (upstream `pstack/automations/benny/`). The readme and the overnight guide link here. Upstream describes these files as dormant setup sources, not slash skills. No `.cursor/settings.json` entry enables them.

Path edit: `.cursor/agents/poteto-agent.md` also searches the active workspace `.cursor/skills/poteto-mode/SKILL.md` and `~/.cursor/skills/poteto-mode/SKILL.md`.
Upstream only searched `~/.cursor/plugins/`.
Sibling skill links (`../<name>/SKILL.md`) are unchanged and resolve because every pstack skill is a direct child of `.cursor/skills/`.

Not copied:

- `harness/pstack/` at the plugins repo root. Generated Claude Code copy of the same tree. This repo has no Claude plugin layout. The adapter doc is at `.cursor/docs/harness/claude-code.md`.
- `pstack/.cursor-plugin/plugin.json`, `pstack/plugin.json`, and `pstack/assets/logo.png`. Cursor discovers these skills and agents from their directories. The logo is only referenced by the plugin manifest. A nested plugin manifest is not added, so this config repo is not also registered as a plugin.

## Ponytail

- Source: https://github.com/DietrichGebert/ponytail
- Upstream commit: `09c434ab73ca43761c5d8b0c5d341926c2fba710`
- Licence: MIT, Copyright (c) 2026 DietrichGebert. See [Ponytail licence](../licenses/ponytail/LICENSE).
- Author: DietrichGebert

Copied, with no text changes:

- `.cursor/skills/ponytail/SKILL.md`
- `.cursor/skills/ponytail-review/SKILL.md`
- `.cursor/skills/ponytail-audit/SKILL.md`
- `.cursor/skills/ponytail-debt/SKILL.md`
- `.cursor/skills/ponytail-gain/SKILL.md`
- `.cursor/skills/ponytail-help/SKILL.md`

Invoke with `/ponytail`, `/ponytail-review`, `/ponytail-audit`, `/ponytail-debt`, `/ponytail-gain`, and `/ponytail-help`.
`/ponytail` takes `lite`, `full`, `ultra`, or `off` when you want a level for that invocation.
Nothing here turns Ponytail on for every session.

### Always-on ruleset not installed

Ponytail's ruleset tells the agent to write the least code and to drop scope that nobody asked for.
This repo already has standing rules in `agents.md`, and those rules disagree with that:

- `agents.md` says not to weigh development cost heavily, and to prefer quality, simplicity, robustness, scalability, and long-term maintainability.
  Ponytail says the shortest working diff wins and to skip flexibility nobody asked for.
- `agents.md` says to be picky about pixel perfection and to fix UI that looks off even when it is outside the current task.
  Ponytail treats that extra work as out of scope.
- `agents.md` says to fix lint failures, test failures, and flakiness even when the current change did not cause them.
  Ponytail limits the change to the task and the callers it breaks.

`agents.md` also prefers small commits and shipping in small iterations.
That part agrees with a short diff.
The quality, pixel, and fix-what-you-notice rules still conflict with dropping scope, so the standing rules stay as they are.

Ponytail would also stay opt-in if this repo had no conflicting rules.
The always-on copies were not installed:

- `AGENTS.md`
- `.cursor/rules/ponytail.mdc` (`alwaysApply: true`)
- The same ruleset under `.agents/rules/`, `.windsurf/rules/`, `.clinerules/`, `.github/copilot-instructions.md`, `.kiro/steering/`, and `.qoder/rules/`

The `/ponytail` skill is still the full upstream skill, including its level instructions.
Its description says to use it on coding tasks.
That can make a host offer the skill without an always-on rule file.
It is not installed as an always-applied rule.

### Hooks not installed

Ponytail's hooks are not inert.
They run Node on session start and on every prompt.
None of `hooks/` or `scripts/cursor-hooks.js` is installed.

Cursor template `hooks/cursor-hooks.json` would register:

- `sessionStart`: `node hooks/ponytail-activate.js` (injects the ruleset, writes a mode flag)
- `beforeSubmitPrompt`: `node hooks/ponytail-mode-tracker.js` (watches `/ponytail` and injects the ruleset)

Also skipped, same reason (Node on lifecycle events for other hosts, or statusline and band UI that those hooks call):

- `hooks/claude-codex-hooks.json`
- `hooks/copilot-hooks.json`
- `hooks/qoder-hooks.json`
- `hooks/claude-band.json`
- `hooks/ponytail-activate.js`
- `hooks/ponytail-mode-tracker.js`
- `hooks/ponytail-subagent.js`
- `hooks/ponytail-runtime.js`
- `hooks/ponytail-instructions.js`
- `hooks/ponytail-config.js`
- `hooks/ponytail-map.js`
- `hooks/ponytail-band-import.js`
- `hooks/ponytail-statusline.sh`
- `hooks/ponytail-statusline.ps1`
- `hooks/band/`
- `scripts/cursor-hooks.js` (writes `~/.cursor/hooks.json` or `.cursor/hooks.json`)

### Other Ponytail files not installed

- `commands/*.toml` (`ponytail`, `ponytail-review`, `ponytail-audit`, `ponytail-debt`, `ponytail-gain`, `ponytail-help`). Host command adapters for Gemini, OpenCode, and similar. Cursor slash commands come from the skill names above. This repo has no command-adapter directory.
- `skills/plugin.json`. One-field manifest (`"skills": "."`) for hosts that load a plugin root. Cursor discovers `SKILL.md` on its own.

## How to invoke

In a Cursor session that can see these files, pick the skill from the `/` menu or type its name:

- `/poteto-mode` for pstack's entry point. Other pstack skills (`/how`, `/why`, `/architect`, `/arena`, `/interrogate`, `/tdd`, `/unslop`, `/reflect`, `/principle-*`, and the rest) are the same kind of slash command.
- `/setup-pstack` once, if you want pstack's per-role model rule written to `~/.cursor/rules/pstack-models.mdc`.
- `/ponytail` for Ponytail. Level switches are `/ponytail lite`, `/ponytail full`, `/ponytail ultra`, and `/ponytail off`.

Subagents, when the host loads `.cursor/agents/`:

- `poteto-agent` from `.cursor/agents/poteto-agent.md`
- `comment-sicko` from `.cursor/agents/comment-sicko.md`
