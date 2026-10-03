---
name: threads-audit
description: Find out which of the user's own Threads posts work and why, using the Threads for Claude MCP server. Use when the user asks what is working on Threads, why some posts did better, what to post more of, or wants a post-mortem of recent posts. Runs threads_audit_posts; read-only.
---

# Threads audit

Explain which of the user's own Threads posts work and why, from their real numbers.

## Setup

If no `threads_*` tools are available, ask the user to add the MCP server `https://threads-mcp.app/mcp` (streamable HTTP):

- Claude (web, desktop, mobile): Settings → Connectors → Add custom connector → paste the URL → Connect.
- Claude Code: `claude mcp add --transport http threads https://threads-mcp.app/mcp`, then `/mcp` → Authenticate. Or install the plugin,
  which adds the server plus slash commands: `/plugin marketplace add pawlek/threads-plugin`, then `/plugin install threads@threads-for-claude`.

The user signs in with Threads (OAuth). Details: https://threads-mcp.app/auth.md

## Which tool

- "What's working?", "why did this post do well?", "what should I post more of?": call `threads_audit_posts`. It ranks
  the user's own posts by engagement rate ((likes + replies + reposts + quotes) / views), reply ratio and reach
  (views / followers) instead of raw views, compares format, length, questions, links, topic tags and timing, and
  returns findings with sample sizes and confidence. It refuses to name patterns from fewer than 6 posts.
- Plain numbers or a table for a period ("views last week", "top posts this month"): call `threads_get_posts_insights`
  once with `since`/`until` (YYYY-MM-DD) and `sort_by`.
- Report findings in plain language with their sample sizes; do not overstate weak patterns.

## Notes

- Metrics exist only for the user's own posts; Threads does not expose likes/views of other people's posts.
- The `audit_posts` prompt runs this flow and `plan_week` turns the findings into a week of post ideas, where the
  client shows MCP prompts.
