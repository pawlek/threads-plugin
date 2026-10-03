---
description: "Post-mortem on what the user already published: ranks posts by engagement rate and reach multiple and says what works, what to stop, and how confident the evidence is."
argument-hint: "[period, e.g. last 90 days]"
---

Audit the user's own Threads posts and say plainly what is working.

Period: $ARGUMENTS

1. Turn the period into since/until dates (YYYY-MM-DD; default the last 90 days) and call threads_audit_posts. If several accounts are linked, say which one you audited.
2. Show the metrics with their formulas, not just numbers:
   - Engagement rate = (likes + replies + reposts + quotes) / views.
   - Reach multiple = views / follower count: did it travel past the existing audience?
   - Reply ratio = replies / likes: did it start a conversation or just get a nod?
   Raw views mostly reflect follower count; rank by engagement rate and reach multiple, not views.
3. Top 5 and bottom 5 side by side: first line, format, length, metrics, date.
4. Findings: state each as a claim with the evidence attached, n, and confidence from the tool. Compare format, length, questions, links, topic tags. Check day and time last; it is rarely the cause. Be willing to say something unwelcome (for example, that the posts the user likes most underperform). If n is too small for a comparison, say so instead of inventing a pattern.
5. Do not draft or publish anything here. Insights cover only the user's own posts.
6. End with two lines:
   STOP: the one thing the evidence says to drop.
   DO MORE: the one thing it says to double down on.
   Then offer to run plan_week on these findings.

Posting, replying, reposting and deleting are public and act as the user: show the exact final text, say which account it goes out as (acting_as) when several are linked, and wait for an explicit yes before calling the tool.

If the "Period:" line above is empty, audit the last 90 days.
