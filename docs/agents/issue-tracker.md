# Issue tracker: GitHub

Issues and specs for this repo live as GitHub Issues in `ianhudsonai/juris-rag`.

## Cloud threads: no `gh issue`, no `gh pr`

In cloud threads the `gh issue` and `gh pr` subcommands are blocked. Use the
built-in GitHub tools (`mcp__github__*`) first, and `gh api` (the raw REST API)
as the fallback. Both are listed below. On a local thread the plain `gh issue`
commands also work.

## Conventions

- **Create an issue**: `issue_write` with method `create`, or
  `gh api repos/ianhudsonai/juris-rag/issues -f title="..." -f body="..."`.
  Use a heredoc (`-F body=@-`) for multi-line bodies.
- **Read an issue**: `issue_read`, or
  `gh api repos/ianhudsonai/juris-rag/issues/<n>` and
  `gh api repos/ianhudsonai/juris-rag/issues/<n>/comments`.
- **List issues**: `list_issues` (filter by state and labels), or
  `gh api 'repos/ianhudsonai/juris-rag/issues?state=open&labels=<label>' --jq '[.[] | select(.pull_request | not) | {number, title, labels: [.labels[].name]}]'`.
  The REST list endpoint also returns pull requests; the `select` drops them.
- **Make an issue a sub-issue of a parent**: `sub_issue_write`, or
  `gh api --method POST repos/ianhudsonai/juris-rag/issues/<parent>/sub_issues -F sub_issue_id=<child-db-id>`.
  The id is the child's numeric database id (`gh api repos/ianhudsonai/juris-rag/issues/<n> --jq .id`),
  not its `#number`. Without sub-issues, put `Part of #<parent>` at the top of the child body.
- **Blocking**: GitHub's native issue dependencies.
  `gh api --method POST repos/ianhudsonai/juris-rag/issues/<child>/dependencies/blocked_by -F issue_id=<blocker-db-id>`.
  Where that fails, fall back to a `Blocked by: #<n>, #<n>` line at the top of the child body.
  A ticket is unblocked when every blocker is closed.
- **Count open blockers**: `gh api repos/ianhudsonai/juris-rag/issues/<n> --jq .issue_dependencies_summary.blocked_by`
  (open blockers only; 0 means the ticket can start).
- **Comment on an issue**: `add_issue_comment`, or
  `gh api repos/ianhudsonai/juris-rag/issues/<n>/comments -f body="..."`.
- **Apply / remove labels**: `issue_write` with method `update` and `labels`, or
  `gh api repos/ianhudsonai/juris-rag/issues/<n>/labels -f 'labels[]=<label>'` /
  `gh api --method DELETE repos/ianhudsonai/juris-rag/issues/<n>/labels/<label>`.
- **Close**: comment first with the reason, then `issue_write` with method `update`,
  `state: closed` and a `state_reason`, or
  `gh api --method PATCH repos/ianhudsonai/juris-rag/issues/<n> -f state=closed -f state_reason=completed`.

File issues only into `ianhudsonai/juris-rag`. Never file into `mattpocock/skills`
(the repo these skills come from).

## Project rules that apply to issues

- One issue = one branch = one pull request. Ian merges; the agent never merges.
- No secrets in issue titles, bodies or comments.
- No AI attribution in issue or PR text.

## Pull requests as a triage surface

**PRs as a request surface: no.** _(Set to `yes` if this repo treats external PRs as feature requests; `/triage` reads this flag.)_

GitHub shares one number space across issues and PRs, so a bare `#42` may be
either. `gh api repos/ianhudsonai/juris-rag/issues/42` returns both; a
`pull_request` key in the result means it is a PR.

## When a skill says "publish to the issue tracker"

Create a GitHub issue.

## When a skill says "fetch the relevant ticket"

Read it as in **Read an issue** above.

## Wayfinding operations

Used by `/wayfinder`. The **map** is a single issue with **child** issues as tickets.

- **Map**: a single issue labelled `wayfinder:map`, holding the Notes / Decisions-so-far / Fog body.
- **Child ticket**: an issue linked to the map as a sub-issue (see above). Labels:
  `wayfinder:<type>` (`research`/`prototype`/`grilling`/`task`). Once claimed, the ticket is assigned to the driving dev.
- **Blocking**: see **Blocking** under Conventions.
- **Frontier query**: list the map's open sub-issues
  (`gh api repos/ianhudsonai/juris-rag/issues/<map>/sub_issues`), drop any with an
  open blocker or an assignee; first in map order wins.
- **Claim**: assign the issue (`issue_write` update with `assignees`), the session's first write.
- **Resolve**: comment the answer, close the issue, then append a context pointer
  (gist + link) to the map's Decisions-so-far.
