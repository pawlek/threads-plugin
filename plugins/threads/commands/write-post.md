---
description: "Turn a raw idea into a Threads post or thread in the user's own voice: hook options, a humanized draft checked with threads_check_draft, and publishing only after an explicit yes."
argument-hint: "<idea>"
---

Write a Threads post from this idea.

Idea: $ARGUMENTS

1. Context first. Call threads_get_profile, then threads_audit_posts (or threads_list_posts if that is unavailable) to learn the user's voice: sentence length, vocabulary, what they never say, which posts earned replies. Match that voice; do not invent one.
2. If the idea is thin (no concrete event), ask ONE batched question: what happened, to whom, and what it cost or returned. Wait for the answer.
3. Propose 3 hooks built on different angles (e.g. number/result, mistake, contrarian claim, scene), one line each, and recommend one in a sentence.
4. Draft on the chosen hook. Threads shape:
   - The first line carries the post on its own; the second line pays it off, not sets up the third.
   - Short lines, one idea. Two ideas means two posts; say so.
   - Specific numbers and names over adjectives. Conversational, not a press release.
   - Each part at most 500 characters. For a thread, every part must stand alone and earn the next.
   - No engagement-bait closers ("Thoughts?", "Agree?"). End on a line only this post could have, or a specific question.
   - No hashtags in the text. At most one topic, passed as topic_tag. Links go in link_attachment (preview card), not pasted mid-text.
   - Never fabricate metrics, clients, quotes or outcomes. If a number is missing, write {{your number}} and flag it.
5. Run threads_check_draft on the draft (each part, for a thread). Rewrite flagged lines yourself, keeping the voice; do not just paste cleaned_text over meaning. Repeat until it passes, or explain what you deliberately kept.
6. Show the exact final text in a copy-ready block, plus: character count per part, topic_tag, link_attachment, reply_control if set, any {{placeholders}} still open, and the account it will post as (call threads_list_accounts if several may be linked).
7. Posting, replying, reposting and deleting are public and act as the user: show the exact final text, say which account it goes out as (acting_as) when several are linked, and wait for an explicit yes before calling the tool. Only then call threads_create_post (or threads_create_thread with parts[]), and return the permalink.

If the "Idea:" line above is empty, ask the user for the idea first.
