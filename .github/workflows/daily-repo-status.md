---
description: |
  This workflow creates daily repo status reports. It gathers recent repository
  activity (issues, PRs, discussions, releases, code changes) and generates
  engaging GitHub issues with productivity insights, community highlights,
  and project recommendations.

on:
  schedule: daily
  workflow_dispatch:

permissions:
  contents: read
  issues: read
  pull-requests: read

network: defaults

tools:
  github:
    # If in a public repo, setting `lockdown: false` allows
    # reading issues, pull requests and comments from 3rd-parties
    # If in a private repo this has no particular effect.
    lockdown: false
    min-integrity: none # This workflow is allowed to examine and comment on any issues

safe-outputs:
  mentions: false
  allowed-github-references: []
  create-issue:
    title-prefix: "[repo-status] "
    labels: [report, daily-status]
    close-older-issues: true
---

# Repo Status

Create an upbeat daily status report for the repo as a GitHub issue.

## What to include

- Recent repository activity (issues, PRs, discussions, releases, code changes)
- Progress tracking, goal reminders and highlights
- Project status and recommendations
- Actionable next steps for maintainers

## Style

- Be positive, encouraging, and helpful 🌟
- Use emojis moderately for engagement
- Keep it concise - adjust length based on actual activity

## Process

1. Gather recent activity from the repository
2. Study the repository, its issues and its pull requests
3. Create a new GitHub issue with your findings and insights

## Troubleshooting

### Copilot CLI Installation Verification

The workflow includes built-in verification to ensure Copilot CLI is properly installed before execution. If you encounter ENOENT errors:

1. Verify `COPILOT_GITHUB_TOKEN` secret is set in repository settings
2. Ensure runner has sufficient disk space (at least 1GB free)
3. Check network connectivity to GitHub release servers
4. Review "Install GitHub Copilot CLI" step logs for specific errors
5. If issues persist, consider using the custom verification action: `.github/actions/verify-copilot-cli`

The installation step will validate:
- Binary existence at `/usr/local/bin/copilot`
- Execute permissions on the binary
- Binary functionality with `--version` check
