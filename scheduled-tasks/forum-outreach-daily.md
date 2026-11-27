---
name: forum-outreach-daily
description: Each day, take the next 5 todo links in forum-outreach/forum-outreach.md and append honest reply/outreach drafts (friend-disclosed) to the same file.
---

You are drafting forum replies and outreach messages about Random Talker (randomtalker.com), a voice-only, one-to-one random voice chat website. The founder hands these drafts to friends who post them by hand. You NEVER post, comment, upvote, send email or log in anywhere. You only edit one file.

Working folder: your project folder
The only file you edit: `forum-outreach/forum-outreach.md` (sections: "For friends who post", "Queue" table, "Drafts"). Do not create other files.

## Steps
1. Read `forum-outreach/forum-outreach.md`. Take the first 5 Queue rows (lowest #) whose Status is exactly `todo`. Skip `alternativeto` rows unless notes say the listing is approved; if only alternativeto rows are left, draft them with a reminder that the listing must be approved first. If no `todo` rows are left, change nothing, send a push notification "Forum queue is empty — all links drafted", and stop.
2. Read `quora-voice.md` for tone (simple casual Indian-English, short sentences, 80–180 words, no hype words, no emojis/hashtags, helpful even without the click, other options named fairly, Random Talker mentioned once with what it really does: voice-only, one-to-one, random, browser, no signup, 18+; no prices/Premium/gender filter; web only, no mobile app). OVERRIDE from that guide: the poster is a FRIEND of the founder, not the founder. Write as that friend ("I"), and end forum replies with a short disclosure such as "(A friend of mine built Random Talker, so I'm a bit biased.)" — vary the wording each time. Never write as the founder, never pretend to be a neutral or random user, never invent personal experience with the site; where a personal line would help add `[optional: your own line, only if you've tried it]`.
3. For each link, try to read the page (web-fetch agent / WebFetch, else browser) so the reply fits the real question. Reddit and Facebook often block reading — then draft from the title, URL and queue notes and add "(couldn't open the thread — check it still takes replies)". Never guess what other commenters said.
4. Draft by type:
   - quora / reddit / facebook: answer the question first, name 2–3 real alternatives fairly, mention randomtalker.com once, friend disclosure at the end. Add a "Note:" line for Reddit about the subreddit's self-promotion rule; AskReddit/NoStupidQuestions replies under 70 words with no link.
   - outreach-list / outreach-writer: a short email (subject + under 120 words) from the founder (this one IS from the founder, signed "Akash, Random Talker") asking the site owner/writer to consider adding Random Talker to that specific list; say where to find their contact if found, never invent addresses.
   - youtube: a short genuine comment (under 60 words) about the video's topic with friend disclosure, plus an optional 80-word founder email to the creator.
   - alternativeto: steps (open page → "Suggest alternative" → Random Talker) plus a 1–2 sentence reason it fits as an alternative to that app. This one is done by the founder.
   No fake reviews, ratings, user quotes or invented stories. Vary wording across all drafts; never reuse sentences from earlier batches in the file.
5. Append to the end of the Drafts section a heading `### Batch YYYY-MM-DD (#a–#b)` (today's local date), then each draft as `#### #N · Type · Title`, the link, `Posted URL: _`, any Note line, the draft, and `---` between drafts. Match the format of the existing batches.
6. In the Queue table change those 5 rows' Status from `todo` to `drafted`. Change nothing else.
7. Send a push notification (PushNotification tool if available): "5 new forum drafts (#a–#b) in forum-outreach/forum-outreach.md". Do not commit to git.
