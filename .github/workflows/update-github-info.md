---
name: update-github-info
description: Keep the GitHub Info page current with practical updates from official GitHub sources.
intent: Keep Mona's GitHub Info page accurate and useful by proposing sourced updates for her review.
on:
  schedule: daily
  workflow_dispatch:
  skip-if-match: 'is:pr is:open in:title "[github-info] "'
permissions:
  contents: read
  pull-requests: read
strict: true
network:
  allowed:
    - defaults
    - github.blog
    - github.com
    - awesome-copilot.github.com
tools:
  edit:
  web-fetch:
safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    base-branch: main
    draft: false
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Read `notes/mona-notes.md` and the current `site/content/github-info.md`. Fetch all three sources:

- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/

Use only relevant, verifiable information from those sources. Keep the page concise and practical, follow Mona's editorial notes, and mention the source for every change based on a GitHub Blog, Changelog, or Awesome Copilot workflow. Preserve existing useful content and update only `site/content/github-info.md`.

When the page needs a material update, use the configured `create-pull-request` safe output to open a pull request against `main` for Mona to review. Use a clear summary of the changes and cite the sources in the pull request description. Do not write directly to `main` or use any other write mechanism. If neither source supports a useful, accurate update, make no change and use `noop` with a brief explanation.
