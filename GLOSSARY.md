# Glossary

Domain and technical terms used in this project, one line each. Added as they come up.

- **ADR (architecture decision record)**: a short file in `docs/adr/` that records one decision, why it was made, and what was rejected.
- **Issue tracker**: the place where tasks (tickets) are written down and tracked. Here: GitHub Issues.
- **Sub-issue**: a GitHub issue linked under a parent issue, so a big task can be split into smaller ones.
- **REST API**: a way for programs to talk to a service over HTTP, using URLs for things (`/issues/5`) and verbs for actions (GET reads, POST creates, PATCH changes).
- **Package (Python)**: a folder of Python code that can be imported by name, here `src/juris_rag/` imported as `juris_rag`.
- **uv**: the tool that installs Python, creates the virtual environment and installs dependencies for this project.
- **Dependency**: someone else's code our project needs. Dev dependencies (pytest, ruff, mypy) are only needed while developing.
- **Virtual environment (`.venv`)**: a private folder of installed packages for one project, so projects don't clash. Never committed.
- **Lockfile (`uv.lock`)**: a file listing the exact version of every dependency, so every machine installs the same thing.
- **`pyproject.toml`**: the project's config file: name, Python version, dependencies and tool settings.
- **Linter (ruff check)**: a tool that reads code and flags likely bugs and style problems without running it.
- **Formatter (ruff format)**: a tool that rewrites code layout (spaces, line breaks) to one consistent style.
- **Type checker (mypy)**: a tool that reads type hints and reports values used as the wrong type, before the code runs.
- **Type hint**: a label on a variable or function saying what type it holds, e.g. `-> None`.
- **Test (pytest)**: a function starting with `test_` that checks code behaves as expected; pytest finds and runs them.
