---
description: |
  This workflow creates daily repo status reports. It gathers recent repository
  activity (issues, PRs, discussions, releases, code changes) and generates
  engaging GitHub issues with productivity insights,
  community highlights, and project recommendations.

on:
  schedule: daily
  workflow_dispatch:

permissions:
  contents: read
  issues: read
  pull-requests: read

network: defaults

model: gpt-4o

models:
  default-ai-credits-pricing:
    input: 3.0
    output: 15.0

tools:
  github:
    lockdown: false
    min-integrity: none

safe-outputs:
  mentions: false
  allowed-github-references: []
  create-issue:
    title-prefix: "[repo-status] "
    labels:
      - report
      - daily-status
    close-older-issues: true

---

# Daily Repository Status Report

Analyze the repository's recent activity and create a concise daily status
report as a GitHub issue.

Review, where available:

- Issues created, closed, or updated recently
- Pull requests opened, merged, or closed
- Discussions and community activity
- Releases and tags
- Significant code changes
- Contributor activity
- Open issues that may require attention
- Potential project improvements
- Productivity or engineering insights

The report should include:

## Repository Summary

Provide a short overview of the repository's current activity.

## Recent Activity

Summarize important issues, pull requests, releases, discussions, and code
changes.

## Community Highlights

Highlight meaningful contributor or community activity.

## Attention Required

Identify issues, pull requests, bugs, or other items that may need attention.

## Recommendations

Provide practical recommendations for improving project health,
productivity, maintainability, or community engagement.

Keep the report useful and concise. Avoid reporting insignificant activity.

Create the result as a GitHub issue using the configured `create-issue`
safe output.