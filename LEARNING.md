# Learning log

One entry per merged PR: what changed, why, and the quiz questions with Ian's answers.

## 2026-11-10: agent skills configuration

**What changed.** Added `docs/agents/issue-tracker.md` and `docs/agents/domain.md`, and an
`## Agent skills` section in `CLAUDE.md`. These tell skills like `/to-tickets` and `/implement`
where tickets live (GitHub Issues), how to reach them from a cloud thread (built-in GitHub tools
or `gh api`, since `gh issue` is blocked), and which files hold the project's vocabulary
(`GLOSSARY.md`) and decisions (`docs/adr/`).

**Quiz** (passed on the second try for 1 and 2)
1. Why does the issue tracker file use `gh api` instead of `gh issue create`?
   Ian: because those are blocked in a Claude cloud environment.
2. What is the difference between `GLOSSARY.md` and an ADR?
   Ian: the glossary acts as a dictionary, and an ADR as the decisions tracker.
3. What happens if we delete the `## Agent skills` section from `CLAUDE.md`?
   Ian: the agent won't have the context it needs to reach the skills' setup.
