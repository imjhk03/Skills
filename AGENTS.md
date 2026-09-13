## Apple Human Interface Guidelines

- Before starting work, check whether Apple Human Interface Guidelines (HIG) have relevant guidance; for any UI, UX, visual design, layout, interaction, or Apple-platform implementation work, consult the current HIG and use it to inform the result.
- For an HIG page at `https://developer.apple.com/design/...`, create the agent-readable URL by inserting `/tutorials/data/` immediately before `/design/` and appending `.md` to the page path (before any query string or fragment). Example: `https://developer.apple.com/design/human-interface-guidelines/typography` becomes `https://developer.apple.com/tutorials/data/design/human-interface-guidelines/typography.md`.
- Verify the transformed URL before relying on it. If the `.md` route is unavailable, use the equivalent verified DocC JSON URL ending in `.json` and read or render that content as Markdown.
