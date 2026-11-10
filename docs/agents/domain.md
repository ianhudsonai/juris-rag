# Domain Docs

How the engineering skills should consume this repo's domain documentation when exploring the codebase.

Layout: **single-context**. One `GLOSSARY.md` and one `docs/adr/` at the repo root.

## Before exploring, read these

- **`GLOSSARY.md`** at the repo root.
- **`docs/adr/`**: read ADRs that touch the area you're about to work in.

If `docs/adr/` doesn't exist yet, proceed silently. The first ADR is created when
the first real decision needs one. Project rule: every new dependency needs a
line in an ADR, so adding a dependency is the most likely trigger.

## File structure

```
/
├── GLOSSARY.md
├── docs/
│   ├── spec.md
│   └── adr/
│       ├── 0001-<decision>.md
│       └── 0002-<decision>.md
└── src/
```

## Use the glossary's vocabulary

When your output names a domain concept (in an issue title, a refactor proposal,
a hypothesis, a test name), use the term as defined in `GLOSSARY.md`. Don't drift
to synonyms the glossary explicitly avoids.

If the concept you need isn't in the glossary yet, add it with a one-line
definition in plain English (project rule: every new term goes in). Domain terms
from TCU jurisprudence keep their Portuguese name, with an English gloss.

## Flag ADR and spec conflicts

If your output contradicts an existing ADR, or a locked decision in `docs/spec.md`,
surface it explicitly rather than silently overriding:

> _Contradicts ADR-0007 (exact search before ANN), but worth reopening because…_

Locked decisions reopen only with eval evidence.
