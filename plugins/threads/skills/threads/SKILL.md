---
name: threads
description: Publish and manage posts on the user's Threads (threads.com) account and report on their performance through the Threads for Claude MCP server. Use when the user wants to post, thread or carousel to Threads, reply to or moderate replies, search Threads posts, or asks how their Threads posts performed.
---

# Threads

Work with the user's own Threads account through the Threads for Claude MCP server.

## Setup

If no `threads_*` tools are available, ask the user to add the MCP server `https://threads-mcp.app/mcp` (streamable HTTP):

- Claude (web, desktop, mobile): Settings → Connectors → Add custom connector → paste the URL → Connect.
- Claude Code: `claude mcp add --transport http threads https://threads-mcp.app/mcp`, then `/mcp` → Authenticate. Or install the plugin,
  which adds the server plus slash commands: `/plugin marketplace add pawlek/threads-plugin`, then `/plugin install threads@threads-for-claude`.

The user signs in with Threads (OAuth). Details: https://threads-mcp.app/auth.md

## Writing

1. Ask for the idea and who it is for if that is unclear. Offer 2–3 opening lines and let the user pick one.
2. Draft in the user's voice: concrete details, plain words, no hashtag walls.
3. Call `threads_check_draft` with the draft. It strips invisible characters, em dashes, curly quotes and stock AI
   phrases, checks Threads limits (500 characters, 5 links, unfilled {{placeholders}}) and returns `cleaned_text`, a
   0–100 score with PASS/REVIEW/FLAGGED, and flags for structures it cannot fix itself.
4. Rewrite the flagged parts by hand (for example "not just X, it's Y", lists of three, "Thoughts?" bait), then check again.
5. Show the exact final text and wait for explicit approval. The check is local heuristics, not an AI detector: never
   promise a post is "undetectable".
6. Publish with `threads_create_post` (or `threads_create_thread` for longer text) only after the user says yes.

## Publishing

1. Draft the text. Posts allow 500 characters and at most 5 links. Run `threads_check_draft` first (see Writing).
2. Show the exact text (and media URLs) to the user and wait for explicit approval. Publishing is public.
3. Pick the tool:
   - one post, optionally with one image or video: `threads_create_post`
   - 2–20 images/videos: `threads_create_carousel`
   - text longer than 500 characters: `threads_create_thread` (2–10 parts, published as a reply chain)
4. If the result says `processing`, call `threads_publish_container` with the `container_id` a minute later.
5. Return the permalink.

Media must be public URLs (images JPEG/PNG ≤ 8 MB, videos MP4/MOV ≤ 5 min). Threads has no scheduling: publish only when the user approves.

## Replies and moderation

- `threads_get_replies` lists replies to a post; `threads_get_mentions` lists mentions.
- `threads_reply` answers (confirm the text first); `threads_hide_reply` hides spam.
- `threads_delete_post` cannot be undone: confirm first.

## Reporting

- For a period ("this week", "last month", "best posts"), call `threads_get_posts_insights` once with `since`/`until` (YYYY-MM-DD) and `sort_by`. It returns totals, average/median views, engagement rate and a per-post table.
- For one post use `threads_get_post_insights`; for account totals and follower demographics use `threads_get_account_insights`.
- Metrics exist only for the user's own posts; Threads does not expose likes/views of other people's posts.

## Auditing

- "What's working?", "why did this post do well?", "what should I post more of?": call `threads_audit_posts`. It ranks
  the user's own posts by engagement rate ((likes + replies + reposts + quotes) / views), reply ratio and reach
  (views / followers) instead of raw views, compares format, length, questions, links, topic tags and timing, and
  returns findings with sample sizes and confidence. It refuses to name patterns from fewer than 6 posts.
- Plain numbers or a table for a period ("views last week", "top posts this month"): call `threads_get_posts_insights`
  once with `since`/`until` (YYYY-MM-DD) and `sort_by`.
- Report findings in plain language with their sample sizes; do not overstate weak patterns.

## Prompts

The server also ships prompts: `write_post`, `reply_to_replies`, `audit_posts` and `plan_week`. Clients that support
MCP prompts list them in a prompt menu. Not every client does: when they are missing, follow the same steps from the
user's plain request.

## Errors

- "Reconnect the Threads connector": the Threads token expired or was revoked; ask the user to reconnect.
- "no … permission yet": ask the user to open https://threads-mcp.app/account and click "Update permissions".
