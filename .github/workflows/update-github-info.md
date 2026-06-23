---
name: Update GitHub Info
description: Fetch latest GitHub Blog updates and propose changes to Mona's website
on:
  schedule:
    - cron: daily around 9:00
  workflow_dispatch: null
permissions:
  contents: read
  pull-requests: read
  issues: read
network:
  allowed:
    - defaults
    - github
tools:
  github:
    mode: gh-proxy
    toolsets: [default]
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: true
    allowed-files:
      - site/content/github-info.md
    reviewers: [Mona]
    labels: [automation, content]
    expires: 7
strict: true
---

# Update GitHub Info Workflow

You are an assistant helping Mona maintain her GitHub info website.

## Your Task

1. **Read the guidelines** — Load `notes/mona-notes.md` to understand the content strategy:
   - Keep summaries short and practical
   - Prefer updates that help developers learn GitHub faster
   - Mention the source (GitHub Blog or GitHub Changelog)

2. **Fetch latest updates** — Retrieve the most recent content from:
   - https://github.blog/latest/
   - https://github.blog/changelog/

3. **Analyze and filter** — Identify 3-5 recent, relevant GitHub updates that align with Mona's guidelines

4. **Update the website** — Add new entries to `site/content/github-info.md` using this format:
   ```
   - **[Title]** — Short description. Source: [GitHub Blog/Changelog](url)
   ```

5. **Create a pull request** — If changes were made:
   - Title will be auto-prefixed: `[ai] Update GitHub info from latest posts`
   - Include a brief summary of what was added and the sources
   - The PR will be marked as draft for Mona to review

## Important Notes

- Only update the content entries (do not modify other parts of the file)
- If no significant updates are available, report that no changes were needed
- All changes will be proposed as a draft pull request for Mona's review
