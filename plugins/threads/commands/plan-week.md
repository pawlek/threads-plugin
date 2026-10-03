---
description: "Build next week's Threads plan from the user's own evidence: 4-5 post angles with hooks, honest timing notes and a list of accounts worth replying to. Nothing is scheduled."
argument-hint: "[what happened this week]"
---

Plan the user's next week on Threads.

This week: $ARGUMENTS

1. Evidence first: call threads_audit_posts for the last 90 days and use its findings, not generic advice. Do not repeat a theme the user posted in the last two weeks.
2. Use the material above. If the themes are unclear, infer them from the audit and confirm in one line.
3. Propose 4-5 posts across the week. Mix types and never put the same type back to back:
   - PROOF: something that happened, with a number.
   - OPINION: a position that could cost followers.
   - TEACH: one thing the reader can do today.
   - STORY: a scene with a cost.
   - OFFER: what the user sells, said plainly (at most one).
   For each: day, suggested time, type, the specific angle (not a topic: "AI" is not a plan), a one-line hook, and post vs thread. Use {{placeholders}} rather than inventing facts.
4. Timing: suggest times from the audit if it shows a real difference, otherwise a sensible default for the audience's timezone, and say plainly that the first line matters far more than the hour.
5. Engagement list: use threads_keyword_search on the themes and threads_profile_lookup to pick about 10 accounts worth replying to (mostly larger accounts in the niche, some peers, a couple of potential buyers), each with why and one sentence on what the user could add. Replies to others are public: draft only when asked.
6. Threads has no scheduling and this prompt publishes nothing: present the plan as a table the user runs. Offer "write Tuesday" to draft any slot with the write_post flow.

Posting, replying, reposting and deleting are public and act as the user: show the exact final text, say which account it goes out as (acting_as) when several are linked, and wait for an explicit yes before calling the tool.

If the "This week:" line above is empty, ask what actually happened this week first.
