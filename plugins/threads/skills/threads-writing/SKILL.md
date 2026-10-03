---
name: threads-writing
description: Write a Threads post with the user and check it before it goes out, using the Threads for Claude MCP server. Use when the user asks to draft, rewrite or polish a Threads post or thread, wants it to sound less like AI, or asks whether a draft is ready to publish. Runs threads_check_draft and never publishes without explicit approval.
---

# Threads writing

Draft a Threads post with the user, check it with `threads_check_draft`, and publish only after explicit approval.

## Setup

If no `threads_*` tools are available, ask the user to add the MCP server `https://threads-mcp.app/mcp` (streamable HTTP):

- Claude (web, desktop, mobile): Settings → Connectors → Add custom connector → paste the URL → Connect.
- Claude Code: `claude mcp add --transport http threads https://threads-mcp.app/mcp`, then `/mcp` → Authenticate. Or install the plugin,
  which adds the server plus slash commands: `/plugin marketplace add pawlek/threads-plugin`, then `/plugin install threads@threads-for-claude`.

The user signs in with Threads (OAuth). Details: https://threads-mcp.app/auth.md

## Steps

1. Ask for the idea and who it is for if that is unclear. Offer 2–3 opening lines and let the user pick one.
2. Draft in the user's voice: concrete details, plain words, no hashtag walls.
3. Call `threads_check_draft` with the draft. It strips invisible characters, em dashes, curly quotes and stock AI
   phrases, checks Threads limits (500 characters, 5 links, unfilled {{placeholders}}) and returns `cleaned_text`, a
   0–100 score with PASS/REVIEW/FLAGGED, and flags for structures it cannot fix itself.
4. Rewrite the flagged parts by hand (for example "not just X, it's Y", lists of three, "Thoughts?" bait), then check again.
5. Show the exact final text and wait for explicit approval. The check is local heuristics, not an AI detector: never
   promise a post is "undetectable".
6. Publish with `threads_create_post` (or `threads_create_thread` for longer text) only after the user says yes.

## Notes

- `threads_check_draft` runs locally and never publishes.
- Publishing, replying and reposting act publicly: always show the exact text first. Threads has no scheduling.
- The `write_post` prompt runs this flow where the client shows MCP prompts.
