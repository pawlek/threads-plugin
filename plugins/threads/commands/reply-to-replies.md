---
description: "Triage the replies under the user's posts (lead, substance, peer, support, noise), draft answers in their voice, check each with threads_check_draft, and post only the ones the user approves."
argument-hint: "[post id or permalink]"
---

Handle the replies under the user's Threads posts.

Post: $ARGUMENTS

1. Find the conversation. Resolve the post above: an id goes straight to threads_get_replies; for a permalink, find the matching post in threads_list_posts and use its id. Fetch replies with threads_get_replies. Skim threads_list_posts briefly if you need the user's voice.
2. Triage every reply and state the counts first:
   - LEAD: describes the problem the user solves. Gets a real answer plus one sentence offering help.
   - SUBSTANCE: adds data, disagrees, extends. Gets the most considered reply.
   - PEER: someone worth being seen talking to. Give them something, not flattery.
   - SUPPORT: praise, emoji, tags. A few words at most, only for the first few.
   - NOISE: pitches, spam, bad faith. No reply; replying gives it reach.
3. Draft in that order and stop when the value stops:
   - Answer the actual question in public, in the reply. Do not push people to DMs for the answer.
   - Match their length. A one-line reply does not get a paragraph.
   - Critics: concede the true part first, in their words, then hold the line on the rest. One reply, never defensive.
   - At most 500 characters, no hashtags, no invented facts; use {{placeholder}} for anything you do not know.
4. Run each draft through threads_check_draft and fix flagged lines by hand.
5. Present all drafts grouped by bucket, each with the reply it answers and its character count. List NOISE as skipped. Suggest threads_hide_reply only for clear spam or abuse, and only hide after the user confirms each one.
6. Posting, replying, reposting and deleting are public and act as the user: show the exact final text, say which account it goes out as (acting_as) when several are linked, and wait for an explicit yes before calling the tool. Every threads_reply is a separate public post: send only the replies the user approves, exactly as approved, and report each permalink.

If the "Post:" line above is empty, use threads_get_activity and threads_get_mentions, or the latest posts from threads_list_posts, to find posts with replies the user has not answered; pick the most recent one or two and say which.
