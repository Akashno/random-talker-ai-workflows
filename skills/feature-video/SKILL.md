---
name: feature-video
description: >
  Make a product tutorial or new-feature video with the Remotion video kit at ~/video-kit:
  script, shot list, screen capture, voiceover (Gemini TTS or AI Studio), preview stills and
  the final MP4. Use when the user asks for a video, tutorial video, feature announcement
  video, walkthrough or explainer for a feature, in any project.
user-invocable: true
argument-hint: "[feature or video id]"
---

# Feature video

> Uses a Remotion "video kit" (a Remotion project with reusable scenes, a capture script and TTS scripts). Point `~/video-kit` at your own Remotion project and keep the same commands, or adapt them.

The kit lives at `~/video-kit`. Read its `README.md` first; it is the reference for layout,
commands and the rules below. Work from the kit folder for every command.

The user should only have to: approve the script and shots, sign in once for captures, supply
the API key or the AI Studio take, and review the result. Do everything else.

## 1. Understand the feature (no questions yet)

- Read the code, docs and recent diff for the feature in the current project. Find: who it is
  for, what it lets them do, the exact UI path (pages, buttons, their ids), prerequisites,
  and any limits worth saying.
- Look at an existing storyboard (`videos/*/storyboard.tsx`) for tone and scene pacing.
- Check `brands/` for the project's brand. If there is none, make one (copy `brands/acme.ts`;
  take colours, font and logos from the project's design tokens and assets).

## 2. Checkpoint: script and shot list

Write a table for the user: scene id, chapter, what is on screen, the voice line(s), and the
asset each needs (captured page, phone screenshot to supply, or rebuilt UI). Aim for 45-90s.
Shape that works: title (2-3s) - hook (what it is) - what you need - steps - result - end card.

Voice lines: short, one instruction each, said once. Number steps in the captions, not
necessarily in speech. No stage directions inside the text.

**Stop and get approval before building.**

## 3. Build

- `npm run new -- <id> --brand <export> --title "..." --url <app url>`
- Browser steps: fill `videos/<id>/capture.ts` with the click path and a `shot` per screen,
  naming `targets` (prefer the element ids; the app's Playwright ids are stable). Run
  `npm run capture -- <id>`. If it needs a login, ask the user to run
  `! cd ~/video-kit && npm run capture -- <id> --login` (they sign in themselves; never type
  their credentials). Open the PNGs and check the privacy pass worked (no real numbers,
  emails, names); add `replace` / `blur` / `hide` rules until it does.
- Use `BrowserSteps` / `PhoneSteps` / `Checklist` / `TitleCard` / `EndCard` from `kit/scenes`
  before writing a custom scene. Custom scenes go in `videos/<id>/scenes/` and read colours
  from `useBrand()`.
- Phone screenshots come from the user. Find tap boxes by viewing the image; use 555 numbers
  in anything you rebuild. Never invent screens of an app that the user can screenshot; if
  you must rebuild one, say so in your summary.

## 4. Voice

- With `GEMINI_API_KEY` in `~/video-kit/.env`: `npm run tts -- <id>` (only new or changed
  lines are generated; hand-recorded clips are kept unless `--force`).
- Without a key: `npm run script -- <id>` prints a block to paste into Google AI Studio; when
  the user sends the take, `npm run split -- <id> <take.wav>`. Read the table: if it warns or
  a clip length looks wrong for its text, re-run with `--cuts t1,t2,...`. You cannot listen,
  so tell the user which clips to spot-check.
- The voice sets the timing: scenes stretch to fit their lines. If a line lands on the wrong
  moment, move its `at`, not the audio.

## 5. Checkpoint: review

- Render stills of every scene (`npx remotion still <id>--<scene> <out.png> --frame=<n>`)
  and look at them yourself first: cut-off buttons, highlights off target, overlapping text.
- `npm run render -- <id>`, check silent gaps:
  `ffmpeg -i out/<id>.mp4 -af silencedetect=n=-40dB:d=1.5 -f null -`
- Copy the MP4 to the Desktop and give the user: the file, its length, anything you rebuilt
  rather than captured, and lines whose wording you could not confirm.

## Rules

- Never delete takes in `videos/<id>/audio-src/`.
- One audio file per line (the Studio doubles trimmed audio).
- ffmpeg cuts: `-ss` before `-i`; check every clip's mean volume.
- Do not commit unless the user asks.
