# How AI builds and grows Random Talker

These are the AI workflows behind [Random Talker](https://randomtalker.com), a voice chat site for talking to strangers that one person runs.
I shared them at AI Connect Kerala. Copy anything you like.

Every workflow below has the same four parts: **what it does**, **what you need**, **steps**, and **what you get**.

**Jump to:** [Before you start](#before-you-start) ·
[1. Reels on autopilot](#1-reels-on-autopilot) · [2. Feature videos](#2-feature-videos) ·
[3. Weekly Medium article](#3-weekly-medium-article) · [4. Weekly Quora answers](#4-weekly-quora-answers) ·
[5. Forum outreach](#5-forum-outreach) · [6. Get cited by ChatGPT](#6-get-cited-by-chatgpt) ·
[7. Admin console](#7-admin-console-in-plain-english) · [8. iOS release check](#8-ios-release-check) ·
[AI inside the app](#ai-inside-the-app)

---

## Before you start

Most workflows here are files for **[Claude Code](https://claude.com/claude-code)**. There are two kinds:

- **Skill:** a `SKILL.md` file that Claude follows whenever the task comes up.
- **Scheduled task:** a prompt file that runs by itself on a timer.

**To add a skill:**
1. Install Claude Code and open it in your project folder.
2. Create the folder `.claude/skills/<skill-name>/` in your project.
3. Copy the `SKILL.md` from this repo into that folder.
4. Ask Claude for the task in plain words, for example "make a video for the new login page", or type `/<skill-name>`.

**To add a scheduled task:**
1. Copy the task file into your project folder.
2. Change the parts about Random Talker to your own product: name, website, facts and file names.
3. In the Claude desktop app, ask Claude: "Make this file a scheduled task that runs every Monday at 9 AM." Use whatever schedule you want.
4. Run it once by hand and read what it produces before you trust the timer.

---

## 1. Reels on autopilot

**What it does:** posts short videos about your product three times a day to Instagram, YouTube, Facebook and X. Claude writes the script, Gemini voices it, Remotion renders it and Buffer posts it.

**What you need:** a GitHub account, a Claude Pro or Max subscription, a free [Buffer](https://buffer.com) account with your social channels connected, and optionally a free Gemini API key from [AI Studio](https://aistudio.google.com) for a better voice.

**Steps:**
1. Open [github.com/Akashno/reel-autopilot](https://github.com/Akashno/reel-autopilot) and click **Use this template** to make your own public copy.
2. Clone your copy and run `npm ci`.
3. Run `claude setup-token`, then save the token with `gh secret set CLAUDE_CODE_OAUTH_TOKEN`.
4. Save your Buffer key with `gh secret set BUFFER_API_KEY_1`, and the Gemini key with `gh secret set GEMINI_API_KEY` if you have one.
5. On GitHub, go to **Settings → Pages** and set **Source** to **GitHub Actions**.
6. Describe your product in the `brand/` folder: `brand.json` (name, colours, posting times), `brief.md` (facts and tone) and `angles.json` (video ideas).
7. Run a test with `gh workflow run daily.yml -f test=true` and watch it in the **Actions** tab.
8. Go live with `gh variable set DAILY --body on` and `gh variable set POSTING --body on`.

**What you get:** three videos a day, scheduled in Buffer, with no editing. The full guide is in that repo's README.

---

## 2. Feature videos

**What it does:** makes a 45–90 second tutorial or new-feature video: script, screen recordings, AI voice-over, then the final MP4.

**What you need:** Claude Code, a [Remotion](https://www.remotion.dev) project, and a Gemini API key for the voice. Without a key, you can paste the script into Google AI Studio instead.

**Steps:**
1. Add [skills/feature-video/SKILL.md](skills/feature-video/SKILL.md) as a skill (see [Before you start](#before-you-start)).
2. Change the path `~/video-kit` in the file to your own Remotion project.
3. Ask Claude: "Make a feature video for <feature>."
4. Claude reads your code and shows a table of scenes and voice lines. Approve it or ask for changes.
5. If the app needs a login, sign in yourself when Claude asks. Claude never types your password.
6. Claude records the screens, makes the voice-over and renders still images of every scene for you to check.
7. Say "render it". Claude makes the MP4 and copies it to your Desktop.

**What you get:** a finished MP4 and a list of anything Claude had to rebuild instead of recording.

---

## 3. Weekly Medium article

**What it does:** writes one article a week, adds an Unsplash photo and schedules it on Medium for Wednesday at 7:30 PM.

**What you need:** the Claude desktop app with its built-in browser, signed in to Medium there.

**Steps:**
1. Copy [scheduled-tasks/medium-weekly-article.md](scheduled-tasks/medium-weekly-article.md) into your project.
2. Make a `medium/` folder with a `README.md` holding your rules and a numbered list of article topics.
3. Make a voice file (copy [quora-voice.md](scheduled-tasks/quora-voice.md)) that says how your writing should sound.
4. In the task file, change Random Talker, the website link and the posting time to your own.
5. Make it a weekly scheduled task.
6. After each run, open the draft in `medium/` and the scheduled post on Medium, and read it before it goes out.

**What you get:** a new article scheduled every week, a draft saved in your project, and the topic ticked off your list.

---

## 4. Weekly Quora answers

**What it does:** every Monday, finds 5 Quora questions that AI assistants like ChatGPT cite and drafts an answer to each. **It never posts.** You post them yourself.

**What you need:** Claude Code with web search, plus a file of true facts about your product.

**Steps:**
1. Copy [scheduled-tasks/quora-weekly-answers.md](scheduled-tasks/quora-weekly-answers.md) and [scheduled-tasks/quora-voice.md](scheduled-tasks/quora-voice.md) into your project.
2. Edit `quora-voice.md` so it sounds like you: tone, length, words to avoid.
3. Make a facts file about your product. The task reads `directory-listings.md`, so rename it in the task if yours is different.
4. Change the search topics in step 4 of the task to your product's topics.
5. Make it a scheduled task for every Monday.
6. Open the new `quora-answers-<date>.md`, fix anything that's wrong, and post each answer on Quora yourself.

**What you get:** 5 ready-to-post answers a week, each with a line explaining why that question was picked.

---

## 5. Forum outreach

**What it does:** each day, drafts honest replies for 5 forum threads, Reddit posts or "best alternatives" lists. Friends post them, and each reply says a friend built the product.

**What you need:** Claude Code, and one Markdown file listing the threads you want to reply to.

**Steps:**
1. Copy [scheduled-tasks/forum-outreach-daily.md](scheduled-tasks/forum-outreach-daily.md) into your project.
2. Make `forum-outreach/forum-outreach.md` with three sections: **For friends who post**, **Queue** (a table of links with the status `todo`) and **Drafts**.
3. Add your voice file (see step 3 of the Medium workflow).
4. Make it a daily scheduled task.
5. Each day, send the new drafts to a friend, who posts them by hand.

**What you get:** 5 new drafts a day, appended to the same file, with each link marked `drafted`.

> **Never let AI post for you on forums.** Drafts only, posted by real people who say how they know you.

---

## 6. Get cited by ChatGPT

**What it does:** gets ChatGPT, Perplexity and Google's AI answers to mention and link to your site. For Random Talker, ChatGPT now sends more visitors than Google search.

**What you need:** your site, Google Search Console, Bing Webmaster Tools,  [Axpecto](https://axpecto.com) and [claude-seo](https://github.com/AgriciDaniel/claude-seo).

**Steps:**
1. Check that AI crawlers can read your site. Run `curl -I -A "OAI-SearchBot/1.0" https://yoursite.com` and make sure it returns `200`.
2. Add your site to Google Search Console **and** Bing Webmaster Tools, and submit your sitemap to both. ChatGPT search relies on Bing.
3. Write one detailed comparison page for the main question people ask, for example "best Omegle alternatives in India".
4. Make every fact about your product the same everywhere, and keep prices out of articles.
5. Use Axpecto to see which sites ChatGPT cites for your topic, then get your product mentioned on those sites.
6. Track AI visitors in GA4 (ChatGPT shows up as `chatgpt.com`).

**What you get:** the full checklist with priorities and mistakes to avoid in [seo/GEO_PLAYBOOK.md](seo/GEO_PLAYBOOK.md). Start at **section 8, "New-site checklist"**.

---

## 7. Admin console in plain English

**What it does:** you ask "who got reported this week?" or "how many calls yesterday?" and Claude answers from your real database, without you building a dashboard.

**What you need:** Claude Code, and a small read-only script that connects to your database.

**Steps:**
1. Write a script, for example `scripts/prod.mjs`, with commands like `summary`, `user <id>` and `reports`. Make it refuse any change unless you pass `--write`.
2. Copy [skills/admin-console/SKILL.md](skills/admin-console/SKILL.md) into `.claude/skills/admin/`.
3. Edit the command table in the file to match your script.
4. Ask Claude a question about your data, or type `/admin <question>`.

**What you get:** answers in tables with real ids. Claude only changes data when you ask for that exact change.

---

## 8. iOS release check

**What it does:** checks your iOS app against Apple's current App Store rules before you submit, so you're less likely to be rejected.

**What you need:** Claude Code and your iOS project.

**Steps:**
1. Add both skills: [skills/apple-review-docs](skills/apple-review-docs/SKILL.md) (reads Apple's live rules) and [skills/ios-release-audit](skills/ios-release-audit/SKILL.md) (checks your app).
2. In `ios-release-audit`, change the file paths to your own app's files.
3. Ask Claude: "Is my iOS app ready to submit?"

**What you get:** a one-line verdict (ready, ready after fixes, or blocked), then each problem with the guideline number, where it is in your code, and the smallest fix.

---

## AI inside the app

These run inside Random Talker itself. Each link takes you to the model so you can use it too.

| Feature | Model | Runs | How to use it |
|---|---|---|---|
| Gender filter | Voice gender classifier (ECAPA-TDNN, quantized ONNX) | On the phone | Load it with [Transformers.js](https://huggingface.co/docs/transformers.js) from [Hugging Face](https://huggingface.co/Alice-Sabrina-Ivy/voice-gender-classifier-onnx-q8-v2) |
| Photo safety | NSFWJS (MobileNetV2) | On the phone | `npm install nsfwjs` ([npm](https://www.npmjs.com/package/nsfwjs)) |
| Support chat | Gemini, with Groq as backup | Server | Free API key from [Google AI Studio](https://aistudio.google.com) |
| Chat translation | Gemma (free models) | Server | Through [OpenRouter](https://openrouter.ai) |

Running models on the phone means voice and photos never reach the server, and it costs nothing.

---

## Rules I keep for all of these

- AI drafts, a person posts. Nothing goes on Quora, Reddit or forums automatically.
- No invented numbers, reviews or user stories.
- Every claim about the product comes from one facts file, so AI repeats the same true facts everywhere.

Akash N O · [LinkedIn](https://www.linkedin.com/in/noakash)
