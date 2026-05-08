# Release Changelog Skill

Create release changelogs from a git commit range, including both internal release-review detail and short App Store / Play Store copy.

## What It Does

The `release-changelog` skill helps Codex turn git history into a traceable release document. It guides the agent to:

- Confirm the commit range, usually `<base-sha>..HEAD`.
- Inspect existing repo conventions before writing.
- Gather commit metadata, diff stats, branch, head commit, and worktree status.
- Generate `changelogs/CHANGELOG-<base-sha>.md` when the repo has no stronger convention.
- Include an `App Stores Summary` section for concise user-facing release notes.
- Verify commit counts and generated content before reporting completion.

## Install

Clone this repository into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/akhenda/release-changelog.git ~/.codex/skills/release-changelog
```

If you already have it installed, update it with:

```bash
git -C ~/.codex/skills/release-changelog pull
```

Restart Codex or start a new session after installing so the skill metadata is discovered.

## Use

Ask Codex to use the skill in a repo with git history:

```text
Use the release-changelog skill to create a changelog since 422e698.
```

Or request app-store copy from a range:

```text
Use release-changelog to summarize changes from v1.5.1..HEAD for App Store and Play Store release notes.
```

By default, the skill treats "since `<sha>`" as `<sha>..HEAD`.

## Expected Output

When no repo-specific convention overrides it, the generated file should live at:

```text
changelogs/CHANGELOG-<base-sha>.md
```

Typical sections:

- `App Stores Summary`
- `Highlights`
- `Chronological Commit List`
- `Notes`

## Files

- `SKILL.md`: the Codex skill loaded by agents when release changelog work is requested.
- `README.md`: human-facing install and usage instructions.
