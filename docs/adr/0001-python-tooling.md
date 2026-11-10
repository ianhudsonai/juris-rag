# ADR-0001: Python tooling (uv, ruff, pytest, mypy)

- Status: accepted
- Date: 2026-11-10

## Context
The repository needs to become a real Python 3.12 project. A fresh clone must install
the exact same versions and run the tests with one command, on cloud threads, on Ian's PC
and in GitHub Actions. Project rules require a decision record for every new dependency.

## Decision
- **uv** manages Python, the virtual environment and dependencies. `uv.lock` and
  `.python-version` are committed. One tool replaces pip, venv, pip-tools and pyenv, and it is fast.
- **ruff** lints and formats. One tool replaces flake8, isort and black.
- **pytest** runs the tests. It is the standard, with plain `assert` statements.
- **mypy** in strict mode is the type checker.

All three checkers are dev dependencies only; the shipped package has no dependencies yet.

## Rejected
- **pip + venv + requirements.txt**: no lockfile by default, several tools to learn.
- **Poetry**: slower, and uv covers the same ground plus Python version management.
- **flake8 + black + isort**: three tools and three configs where ruff is one.
- **unittest**: more boilerplate (classes, `self.assertEqual`) for no gain here.
- **pyright**: faster and stricter in places, but its PyPI package downloads Node.js on first
  run, which is fragile behind the cloud proxy. mypy is pure Python and installs from the lockfile.

## What would change this
- mypy becomes too slow (over ~30 s in CI) or misses bugs pyright catches on our code.
- uv stops being maintained or breaks in GitHub Actions.
