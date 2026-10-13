---
description: "A repository contents overview, started manually"

on:
  workflow_dispatch:

permissions:
  contents: read

runs-on: ubuntu-latest

runs-on-slim: ubuntu-latest

network: defaults

safe-outputs:
  runs-on: ubuntu-latest
  threat-detection:
    runs-on: ubuntu-latest
  create-issue:
    title-prefix: "[GH AW tanulás] "
    max: 1
---

# Repository tour

Explore the checked-out repository and create one GitHub issue containing a
beginner-friendly tour.

Include:

- The purpose of the repository, based only on evidence in its files.
- The main directories and the role of the most important files.
- The commands a new contributor should use to build, test, or run the project.
- Three useful next steps for someone learning this codebase.

Do not guess when information is missing. Clearly say when the repository does
not contain enough information. Do not modify repository files or make any
other changes.
