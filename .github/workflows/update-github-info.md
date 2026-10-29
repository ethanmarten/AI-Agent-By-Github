---
name: update-github-info
description: Keep the Mona website's GitHub information current from official GitHub sources.
engine:
  id: copilot
  copilot-sdk: true
on:
  schedule:
    - cron: "0 9 * * *"
  workflow_dispatch:
permissions:
  contents: read
tools:
  edit:
  web-fetch:
network:
  allowed:
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    labels: [automation, needs-review]
    draft: true
    base-branch: main
    if-no-changes: warn
---

Read `notes/mona-notes.md` and `site/content/github-info.md` before making any changes.

Use web-fetch to review both the [GitHub Blog](https://github.blog/latest/) and the
[GitHub Changelog](https://github.blog/changelog/). Identify current, relevant
updates that help developers learn GitHub faster, keeping summaries short and
practical. Update only `site/content/github-info.md`, and mention the source for
each update from the GitHub Blog or GitHub Changelog.

Do not commit changes directly to the `main` branch. When the content needs an
update, use the `create-pull-request` safe output to open a draft pull request
for Mona to review. The pull request should describe the source-backed changes
and include only the website content update. If no relevant current information
is available, make no changes and do not create a pull request.
