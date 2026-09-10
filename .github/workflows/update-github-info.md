---
name: update-github-info
description: Keep the site's GitHub information current from official GitHub sources.
on:
  schedule: daily
  workflow_dispatch:

permissions:
  contents: read
  pull-requests: read

engine: copilot

tools:
  edit:
  web-fetch:
  github:
    toolsets: [repos]

network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com

safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: true
    labels: [documentation]
---

# Update GitHub Information

Maintain the repository's GitHub information page for Mona.

1. Read `notes/mona-notes.md`.
2. Use the web-fetch tool to read `https://github.blog/latest/`.
3. Use the web-fetch tool to read `https://github.blog/changelog/`.
4. Use the web-fetch tool to read `https://awesome-copilot.github.com/workflows/`.
5. Use GitHub repository API tools to read any repository guidance or reference files needed for this task. Do not use terminal commands, the GitHub CLI, or sandboxed commands to read repository guidance or reference files.
6. Update `site/content/github-info.md` with accurate, concise information based on the notes and official sources. Preserve the existing format and make only relevant changes.
7. Review the resulting diff for accuracy and scope.
8. Request the `create-pull-request` safe output with a clear title and body summarizing the changes and citing the official source URLs. Open the pull request for Mona to review; do not write directly to the default branch.

If the official sources do not provide a meaningful update, leave the content unchanged and do not request a pull request.