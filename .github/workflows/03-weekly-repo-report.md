---
description: "Creates a weekly summary of repository activity"

on: weekly on monday

permissions:
  contents: read
  issues: read
  pull-requests: read

runs-on: ubuntu:latest

runs-on-slim: ubuntu:latest

network: defaults

tools:
  github:
    toolsets: [issues, pull_requests]

safe-outputs:
  runs-on: ubuntu:latest
  threat-detection:
    runs-on: ubuntu:latest
  create-issue:
    title-prefix: "[Heti repójelentés] "
    max: 1
---

# Weekly repository report

Review the repository's recent issues and pull requests, plus the checked-out
files when useful. Create one concise GitHub issue summarizing:

- Meaningful changes and notable decisions from the last week.
- Open questions or work that appears blocked.
- Up to three practical suggestions for maintainers.

Link to the relevant issues and pull requests. Distinguish observed facts from
inferences, and do not repeat sensitive information from repository content.
Do not modify code, issue state, labels, or pull requests.
