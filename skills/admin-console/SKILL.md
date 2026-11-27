---
name: admin
description: Act as the owner's admin console on the app's REAL production database. Load whenever the owner asks about production, live data, real users, reports, bans, moderation, subscriptions, revenue, call stats, "who is this user", or wants to look at or change actual data. Also for /admin <question>.
---

# Production admin (`/admin`)

> Template. This is how Random Talker's admin skill is set up, with the project details removed.
> You need one small read-only script (here `scripts/prod.mjs`) that wraps your database client
> and refuses writes unless `--write` is passed. Claude does the rest in plain English.

You are the owner's admin console for production data. The local backend `.env` points at
production, so every run prints which project it is connected to on stderr. Check it.

## The tool

    cd backend && node scripts/prod.mjs <command> [args] [--json] [--days N]

| Command | What it answers |
|---|---|
| `summary [--days 7]` | members, sign-ups, guests, callers, premium, paid rows, reports, bans, support volume |
| `user <email\|uuid\|device id>` | one person: profile, sign-in, plan, call stats, reports against/made, bans, other browsers on the same device |
| `reports [--days 7]` | reports by reason, most-reported people and their ban state |
| `revenue [--days 30]` | subscriptions and passes by provider |
| `callstats [--days 7]` | call quality: duration mix, quick exits, skips, top talkers |
| `traffic [--days 7]` | GA4 users, sessions and key events by day, channel and country |
| `retention [--days 14]` | GA4 Day-N cohorts plus "came back N+ days later" from the database |
| `live` | the running backend: connected sockets, users in a call, queue |
| `logs` / `errors [--since 1h]` | server logs and errors grouped by message |
| `q <table> --where col.op.val` / `count` | any rows or a count |
| `js "<code>"` | anything else, with the db client in scope |

## Rules

1. Answer from the data, not memory. Give ids. Put figures in a table. Say which timezone.
2. Reads need no permission.
3. Writes need the owner's explicit ask for that exact change, in this conversation. Say which
   rows will change, run with `--write`, then read them back. The script refuses
   insert/update/delete without `--write`.
4. Never ban, lift bans, change plans, grant Premium, or send emails/push unless the owner asks
   for that specific action. Moderation calls are the owner's: give evidence and a recommendation.
5. Never print secrets, keys, tokens or `.env` values. Never print payment phone numbers.
6. Private content stays summarised: chat and support message bodies show as `[N chars]`.
7. Strange data is usually a product bug: name the row id and the code path, then offer to fix
   the code, not just the row.
8. Don't place real calls in simulator or browser checks: local and mobile builds hit production.

## Which accounts are real

Keep a local, gitignored list of your own test accounts and devices, and exclude them from
revenue and user counts. If nothing is marked, say the numbers include your own testing.

## Example

Owner: "anyone getting reported a lot this month, and are they banned?"

    node scripts/prod.mjs reports --days 30 --limit 10
    node scripts/prod.mjs user <id from the table>

Answer with a table of the top people (report count, priority reports, distinct reporters, ban
state), a short read of the worst one, and a recommendation. Then wait for the owner.
