# Learning log

One entry per merged PR: what changed, why, and the quiz questions with Ian's answers.

## 2026-11-10: agent skills configuration

**What changed.** Added `docs/agents/issue-tracker.md` and `docs/agents/domain.md`, and an
`## Agent skills` section in `CLAUDE.md`. These tell skills like `/to-tickets` and `/implement`
where tickets live (GitHub Issues), how to reach them from a cloud thread (built-in GitHub tools
or `gh api`, since `gh issue` is blocked), and which files hold the project's vocabulary
(`GLOSSARY.md`) and decisions (`docs/adr/`).

**Quiz** (answers pending)
1. Why does the issue tracker file use `gh api` instead of `gh issue create`?
2. What is the difference between `GLOSSARY.md` and an ADR?
3. What happens if we delete the `## Agent skills` section from `CLAUDE.md`?
