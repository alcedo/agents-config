# agents-config

Repository for agent configuration.

Standing rules for agents live in `agents.md`.
Third-party skills and agents live under `.cursor/` so Cursor can load them when this repo is the workspace.

- Skills: `.cursor/skills/<name>/SKILL.md`
- Agents: `.cursor/agents/`
- Provenance, licences, upstream commits, and skipped files: `.cursor/skills/THIRD_PARTY.md`

pstack (Lauren Tan) and Ponytail (DietrichGebert) are vendored there.
Invoke pstack with `/poteto-mode` and Ponytail with `/ponytail`.
Ponytail is not an always-on rule. See the third-party note for the clash with `agents.md` and for the hooks that were left out.

This repo has no install or sync script.
To use the skills and agents in every project, copy or symlink `.cursor/skills` to `~/.cursor/skills` and `.cursor/agents` to `~/.cursor/agents`.
Skill-to-skill links keep working from that copy.
`/poteto-help` also links to `docs/` and `README.md` beside the skills directory, so copy `.cursor/docs` to `~/.cursor/docs` and `.cursor/README.md` to `~/.cursor/README.md` when you want those guide links to resolve.
Do not replace the rest of `~/.cursor`.
