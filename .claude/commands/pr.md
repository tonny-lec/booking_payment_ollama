---
allowed-tools: Bash(git:*), Bash(gh:*)
description: Create a draft PR on GitHub and print the PR URL
---

## Context
- Status: !`git status`
- Diff (base..HEAD): !`git diff --stat origin/HEAD...HEAD || true`
- Commits (base..HEAD): !`git log --oneline --decorate -20`
- PR template (if exists): @.github/pull_request_template.md

## Task
1) Ensure the current branch is pushed: `git push -u origin HEAD`
2) Create a *draft* PR using GitHub CLI:
   - Prefer: `gh pr create --draft --fill`
   - If --fill is insufficient, generate a clear title/body and pass them explicitly.
3) Print the PR URL by running:
   - `gh pr view --json url -q .url`

## Stop condition
You are NOT done until the PR URL is printed.
If PR creation fails, print the exact failing command + stderr, and propose the next command to fix it.
