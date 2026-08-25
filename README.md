# Agent Usage Coach

A Cursor skill that coaches **how you use a coding agent**, not the code.

It classifies each turn by intent and session state, then:

| Action | When |
| --- | --- |
| **BLOCK** | Secrets, untrusted instructions, unattended destructive git or deploy |
| **ASK** | Thin brief at task start — no file, no done-criterion, or an unpicked design fork |
| **NUDGE** | Risky habit, then continue the work |
| **PROCEED** | Clean — stay silent |

Detection is model-judged. Listed examples are situations, not keyword matchers.

## Install

Clone into your personal Cursor skills folder:

```bash
git clone https://github.com/DomEscobar/agent-usage-coach.git ~/.cursor/skills/agent-usage-coach
```

Windows (PowerShell):

```powershell
git clone https://github.com/DomEscobar/agent-usage-coach.git $HOME\.cursor\skills\agent-usage-coach
```

Or copy the folder into a project's `.cursor/skills/agent-usage-coach/` to share it with the repo.

The skill auto-invokes (no `disable-model-invocation`). After install, start a new agent chat.

## Files

- `SKILL.md` — classifier, policy, anti-nag, response template
- `anti-patterns.md` — catalog, read only when a violation is suspected
- `good-briefs.md` — before/after brief rewrites, read only on ASK

## License

MIT
