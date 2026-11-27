# How AI builds and grows Random Talker

These are the AI workflows behind [Random Talker](https://randomtalker.com), a voice chat site for talking to strangers that one person runs.
I shared them at AI Connect Kerala. Copy anything you like.

Most of these are **Claude Code** skills and scheduled tasks. A skill is a Markdown file with instructions, saved in
`.claude/skills/<name>/SKILL.md` (or `~/.claude/skills/`), and Claude follows it when the task comes up.
A scheduled task is the same kind of file that runs on a timer.

## AI inside the product

| Feature | Model | Runs | Link |
|---|---|---|---|
| Gender filter | Voice gender classifier (ECAPA-TDNN, quantized ONNX) via Transformers.js | On the phone | [Hugging Face](https://huggingface.co/Alice-Sabrina-Ivy/voice-gender-classifier-onnx-q8-v2) |
| Photo safety | NSFWJS (MobileNetV2) via TensorFlow.js | On the phone | [npm](https://www.npmjs.com/package/nsfwjs) |
| Support chat | Gemini, with Groq as backup | Server | [Google AI Studio](https://aistudio.google.com) |
| Chat translation | Gemma via OpenRouter (free models) | Server | [OpenRouter](https://openrouter.ai) |

## Videos

| What | File |
|---|---|
| **Reels on autopilot.** Claude writes and checks a script, Gemini voices it, Remotion renders it and Buffer posts it to Instagram, YouTube, Facebook and X, three times a day from a GitHub Action. Costs only a Claude subscription. | [github.com/Akashno/reel-autopilot](https://github.com/Akashno/reel-autopilot) |
| **Feature videos.** A tutorial or new-feature video from a script: shot list, screen capture, AI voice-over, preview stills, final MP4. | [skills/feature-video](skills/feature-video/SKILL.md) |

## Writing and outreach

| What | File |
|---|---|
| **Weekly Medium article.** Picks a topic, writes it, adds an Unsplash photo and schedules it for the best time slot. | [scheduled-tasks/medium-weekly-article.md](scheduled-tasks/medium-weekly-article.md) |
| **Quora answers every Monday.** Finds 5 Quora questions that AI assistants cite and drafts answers. I post them by hand. | [scheduled-tasks/quora-weekly-answers.md](scheduled-tasks/quora-weekly-answers.md) |
| **Voice guide.** One file that sets how every draft sounds. | [scheduled-tasks/quora-voice.md](scheduled-tasks/quora-voice.md) |
| **Forum outreach.** Drafts honest replies for 5 threads a day. Friends post them with a "a friend built this" line. | [scheduled-tasks/forum-outreach-daily.md](scheduled-tasks/forum-outreach-daily.md) |

## SEO and AI search

| What | File |
|---|---|
| **GEO playbook.** How Random Talker got cited by ChatGPT, step by step with priorities, and what not to copy. | [seo/GEO_PLAYBOOK.md](seo/GEO_PLAYBOOK.md) |
| **claude-seo.** An open-source Claude Code SEO toolkit, used for Search Console and GA4 reports. | [github.com/AgriciDaniel/claude-seo](https://github.com/AgriciDaniel/claude-seo) |
| **Axpecto.** Shows which sites ChatGPT cites for your topic, so you know where to get mentioned. | [axpecto.com](https://axpecto.com) |

## Running the app

| What | File |
|---|---|
| **Admin console in plain English.** Ask "who got reported this week?" and Claude reads production data through one read-only script. | [skills/admin-console](skills/admin-console/SKILL.md) |
| **iOS release audit.** Checks the app against the App Store rules before you submit. | [skills/ios-release-audit](skills/ios-release-audit/SKILL.md) |
| **Apple review docs.** Makes Claude read Apple's live rules instead of answering from memory. | [skills/apple-review-docs](skills/apple-review-docs/SKILL.md) |

## Rules I keep for all of them

- AI drafts, a person posts. Nothing goes on Quora, Reddit or forums automatically.
- No invented numbers, reviews or user stories.
- Every claim about the product comes from one facts file, so AI repeats the same true facts everywhere.

Akash N O · [LinkedIn](https://www.linkedin.com/in/noakash)
