---
name: pr-review
description: Review GitHub pull requests. Use for code review, checking PR status, viewing diffs, and leaving comments.
---

# PR Review

Tools for reviewing GitHub pull requests.

## Quick Commands

### List PRs
```bash
gh pr list
gh pr list --state all --limit 10
```

### View PR details
```bash
gh pr view <number>
gh pr view <number> --web  # Open in browser
```

### View diff
```bash
gh pr diff <number>
gh pr diff <number> --patch  # Full patch format
```

### Check CI status
```bash
gh pr checks <number>
gh run list --branch <branch>
```

### Review workflow
```bash
# Checkout PR locally
gh pr checkout <number>

# Run tests locally
bun test  # or appropriate test command

# Leave review
gh pr review <number> --approve
gh pr review <number> --comment --body "LGTM"
gh pr review <number> --request-changes --body "Please fix X"
```

### Merge
```bash
gh pr merge <number> --squash
gh pr merge <number> --merge
gh pr merge <number> --rebase
```

## Review Checklist

1. **Read PR description** — understand intent
2. **Check file changes** — `gh pr diff`
3. **Look for:**
   - Missing tests
   - Error handling
   - Security issues (secrets, SQL injection, etc.)
   - Performance concerns
   - Breaking changes
4. **Run tests locally** if changes are significant
5. **Check CI status** — `gh pr checks`

## Comment Patterns

```bash
# Single comment
gh pr comment <number> --body "Nice work!"

# Review with line comments (use web UI for this)
gh pr view <number> --web
```
