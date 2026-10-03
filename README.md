# Threads for Claude: Claude Code plugin

Connects Claude Code to your Threads (threads.com) account through the [Threads for Claude](https://threads-mcp.app) MCP server
and adds slash commands and skills for writing, replying and auditing.

## Install

```
/plugin marketplace add pawlek/threads-plugin
/plugin install threads@threads-for-claude
```

Then run `/mcp`, pick the threads server and choose *Authenticate*: you sign in with Threads in the browser.

## Commands

- `/threads:write-post`: Turn a raw idea into a Threads post or thread in the user's own voice: hook options, a humanized draft checked with threads_check_draft, and publishing only after an explicit yes.
- `/threads:reply-to-replies`: Triage the replies under the user's posts (lead, substance, peer, support, noise), draft answers in their voice, check each with threads_check_draft, and post only the ones the user approves.
- `/threads:audit-posts`: Post-mortem on what the user already published: ranks posts by engagement rate and reach multiple and says what works, what to stop, and how confident the evidence is.
- `/threads:plan-week`: Build next week's Threads plan from the user's own evidence: 4-5 post angles with hooks, honest timing notes and a list of accounts worth replying to. Nothing is scheduled.

## Skills

- `threads`: Publish and manage posts on the user's Threads (threads.com) account and report on their performance through the Threads for Claude MCP server. Use when the user wants to post, thread or carousel to Threads, reply to or moderate replies, search Threads posts, or asks how their Threads posts performed.
- `threads-writing`: Write a Threads post with the user and check it before it goes out, using the Threads for Claude MCP server. Use when the user asks to draft, rewrite or polish a Threads post or thread, wants it to sound less like AI, or asks whether a draft is ready to publish. Runs threads_check_draft and never publishes without explicit approval.
- `threads-audit`: Find out which of the user's own Threads posts work and why, using the Threads for Claude MCP server. Use when the user asks what is working on Threads, why some posts did better, what to post more of, or wants a post-mortem of recent posts. Runs threads_audit_posts; read-only.

Nothing is published without your explicit yes: every post, reply and repost is shown to you first.

## How it works

This repository only holds text files. The plugin's `.mcp.json` points Claude Code at `https://threads-mcp.app/mcp`; from then on
Claude Code talks to that server directly, and your Threads token never leaves it. The commands and skills are the
same workflows the server ships as MCP prompts and agent skills. They are generated from the server's source, so do
not edit them here.

Privacy: https://threads-mcp.app/privacy · Terms: https://threads-mcp.app/terms
