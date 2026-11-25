---
name: update-github-info
description: Keep Mona's GitHub Info page current with concise, source-backed updates.
intent: Keep Mona's GitHub Info page useful to developers with timely, practical guidance from official GitHub Blog and Changelog posts.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
strict: true
engine:
  id: copilot
  copilot-sdk: true
network:
  allowed:
    - defaults
    - copilot
    - github.blog
    - github.com
tools:
  edit:
  web-fetch:
safe-outputs:
  create-pull-request:
    base-branch: main
    draft: false
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info for Mona

Read `notes/mona-notes.md` and the current `site/content/github-info.md`. Fetch:

- https://github.blog/latest/
- https://github.blog/changelog/

Use only current, verifiable information from those official sources. Select
updates that are practical for developers, keep the page concise, preserve its
existing editorial direction, and cite the specific source post for every
change. Do not repeat existing information or add unsupported claims.

Edit only `site/content/github-info.md`. If neither source has a relevant new
item, or the page needs no change, call `noop` with a brief reason. If a
required source cannot be fetched or the evidence is insufficient to make a
reliable update, call `report_incomplete` and do not propose edits.

For a meaningful change, use the configured safe output to open one
non-draft pull request targeting `main`. Summarize the updates and link their
sources in the PR description, and ask Mona to review it. Do not write directly
to `main` or modify any other file.
