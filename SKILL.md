---
name: release-changelog
description: Use when creating release notes or a changelog from a git commit range, especially for app store submissions, Play Store releases, App Store releases, release summaries, or "changes since <sha>" requests.
---

# Release Changelog

## Overview

Create a traceable release changelog from git history, with both internal detail and short app-store-ready copy. The output should be useful to product, QA, release managers, and store submission workflows.

## When To Use

Use this when the user asks for:

- A changelog, release notes, or release summary since a commit, tag, branch, or date.
- App Store or Play Store release copy from recent changes.
- A reusable "what changed" document for a mobile or web release.

Do not use this for code review; use the review workflow instead.

## Core Workflow

1. Confirm the range. Default to `<base>..HEAD` when the user says "since <sha>".
2. Inspect local conventions first: `rg --files -g 'CLAUDE.md' -g 'AGENTS.md' -g 'CHANGELOG*' -g 'changelogs/**'`.
3. Gather git metadata:
   - `git log --reverse --date=short --format='%h %ad %s' <range>`
   - `git diff --stat <range>`
   - `git rev-list --count <range>`
   - `git branch --show-current`
   - `git rev-parse HEAD`
   - `git status --short`
4. Create or update `changelogs/CHANGELOG-<base>.md` when the repo has no stronger convention.
5. Write the changelog from the actual commits and diff metadata, grouping related changes into readable sections.
6. Add `App Stores Summary` near the top with short, user-facing release copy.
7. Verify counts and read the generated file before reporting completion.

## Recommended Format

```markdown
# Changelog Since `<base-sha>`

Summary metadata:
- Date range
- Commits
- Files changed
- Diff summary
- Base commit
- Head commit / branch

## App Stores Summary

Short App Store / Play Store release copy. Keep it user-facing, compact, and free of implementation detail.

## Highlights

Grouped summary for internal release review.

## Chronological Commit List

Oldest-to-newest commit list for traceability.

## Notes

Caveats such as dirty worktree files, excluded unstaged changes, or assumptions.
```

## App Stores Summary Guidance

- Write for users, not engineers.
- Mention visible improvements, reliability, support, payments, onboarding, performance, and compatibility where relevant.
- Avoid commit hashes, internal module names, test details, and backend implementation details.
- Keep it short enough to paste into app-store release notes without editing.

## Common Mistakes

- Forgetting to verify the commit count with `git rev-list --count`.
- Including dirty worktree changes even though they are not part of the commit range.
- Dumping commits without grouping them into release themes.
- Writing app-store copy that exposes internal implementation details.
- Creating a duplicate changelog when an existing file for the base SHA should be updated.
