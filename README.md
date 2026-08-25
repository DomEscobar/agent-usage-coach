# Agent Usage Coach

A portable **agent skill** that coaches **how the human uses a coding agent**, not the code.

It is not Cursor-specific. Any agent that can load a `SKILL.md` folder — or read `AGENTS.md` — can run it: Claude Code, Codex, Gemini CLI, Copilot, Cursor, and others.

Each turn is classified by intent and session state, then:

| Action | When |
| --- | --- |
| **BLOCK** | Secrets, untrusted instructions, unattended destructive git or deploy |
| **ASK** | Thin brief at task start — no file, no done-criterion, or an unpicked design fork |
| **NUDGE** | Risky habit, then continue the work |
| **PROCEED** | Clean — stay silent |

Detection is model-judged. Listed examples are situations, not keyword matchers.

## What this repo is

This repository **is** the skill directory. Clone it into whatever skills path your tool reads, or vendor it and point `AGENTS.md` at `SKILL.md`.

| File | Role |
| --- | --- |
| `SKILL.md` | Entry point — classifier, four NUDGE buckets, anti-nag, scorecard |
| `anti-patterns.md` | ~30 situations with measured costs, loaded only when a violation is suspected |
| `good-briefs.md` | 12 before/after brief rewrites, loaded only on ASK |
| `AGENTS.md` | Repo-level pointer so an agent in this folder still loads the coach |

## Install as a skill

Put this folder where your agent discovers skills. The folder name should stay `agent-usage-coach` and must contain `SKILL.md`.

**Personal (all your projects)**

| Tool | Path |
| --- | --- |
| Vendor-neutral | `~/.agents/skills/agent-usage-coach/` |
| Claude Code | `~/.claude/skills/agent-usage-coach/` |
| Codex | `~/.agents/skills/agent-usage-coach/` |
| Gemini CLI | `~/.gemini/skills/agent-usage-coach/` |
| GitHub Copilot | `~/.copilot/skills/agent-usage-coach/` or `~/.github/skills/` per your build |
| Cursor | `~/.cursor/skills/agent-usage-coach/` |

```bash
git clone https://github.com/DomEscobar/agent-usage-coach.git ~/.agents/skills/agent-usage-coach
```

Windows (PowerShell):

```powershell
git clone https://github.com/DomEscobar/agent-usage-coach.git $HOME\.agents\skills\agent-usage-coach
```

Copy or symlink that folder into any other tool path you actually use. One clone, many pointers.

**Project (shared with the team)**

Prefer the vendor-neutral location so mixed-tool teams see the same skill:

```text
.agents/skills/agent-usage-coach/SKILL.md
```

Then symlink or copy into `.claude/skills/`, `.gemini/skills/`, or `.cursor/skills/` only if a tool does not follow `.agents/skills/`.

Start a new agent session after install.

## Use without a skills loader

If the tool does not discover skills, add this to the project's `AGENTS.md` (or `CLAUDE.md` / `GEMINI.md` that points at it):

```md
On every coding turn, read and follow
path/to/agent-usage-coach/SKILL.md
```

Or clone this repo and work from it — root `AGENTS.md` already does that.

## License

MIT
