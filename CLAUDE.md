# juris-rag

A small, measured RAG system in Portuguese over TCU jurisprudence (JurisTCU corpus).
The full plan is in `docs/spec.md`. Read the section for the current phase before working.

## Every session
1. Read `STATUS.md` to see the current phase and the next task.
2. Work on one GitHub issue at a time, on its own branch.
3. Open one pull request per task. Ian merges; the agent never merges.
4. With each PR, explain the change in plain English and add 2 to 3 quiz questions to `LEARNING.md`.
5. Update `STATUS.md` at the end of the session.

## Hard rules
- No secrets in code, prompts, issues or commits. Keys live in the environment.
- Never edit `evals/data/`, saved baselines or the held-out split.
- Ask before any run that could cost more than US$2. Budget cap is US$10 a month.
- No AI attribution in commit messages or PR descriptions (no `Co-Authored-By` trailers,
  no "Generated with" lines, no session links).
- New domain terms go in `GLOSSARY.md`.
- Ian hand-writes: `rrf()`, the nDCG/recall/MRR metrics, the citation validator,
  the token histogram script, and one SQL query per phase. Review these, do not write them.
- Code, comments and README in English. Product answers in Portuguese.

## Where work runs
- Cloud threads by default. Docker and PostgreSQL 16 are available; the dev database runs there.
- Neon is production only. Production ingest and migrations run from GitHub Actions.
- In cloud threads, `gh issue` and `gh pr` are blocked. Use the built-in GitHub tools or `gh api`.
