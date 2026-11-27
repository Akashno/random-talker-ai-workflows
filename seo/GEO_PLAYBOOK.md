# GEO Playbook — how Random Talker got cited by ChatGPT, and how to repeat it

_Written 2026-09-30 from the repo, GA4/GSC numbers already logged in those docs, and live checks of www.randomtalker.com._

GEO (Generative Engine Optimization) means getting ChatGPT, Perplexity, Google AI Overviews and similar tools to **mention, recommend and link to** your site in their answers.

---

## 0. How to read this

**Priority**
| Level | Meaning |
|---|---|
| **P0** | Do first. Without it AI engines can't read you, or have nothing worth citing. |
| **P1** | Do in the first 2–4 weeks. Makes you trustworthy and consistent enough to be recommended. |
| **P2** | Do once P0/P1 are live. Increases reach and measures results. |
| **P3** | Optional or low value. Cheap, but don't expect much. |

**Evidence** (how sure we are it matters)
| Tag | Meaning |
|---|---|
| **Data** | This project's own GA4/GSC data supports it |
| **Standard** | Standard search/AI-crawler practice; sensible, but not proven by our data |
| **Unproven** | No evidence AI engines use it; low cost, so it was done anyway |

---

## 1. Results, and what the data does and doesn't prove

| Fact | Number | Source |
|---|---|---|
| ChatGPT sessions per week (ISO wk 34 → 38, Aug 17 – Sep 20) | 7 → 82 → 128 → 266 → 419 | GA4 "AI Assistant" channel |
| ChatGPT vs Google organic (Sep 11–26) | **889 vs 465 sessions** | GA4 |
| Country split of ChatGPT traffic | 85%+ India | GA4 |
| Top ChatGPT landing pages (all-time to Sep 26) | `/` 569 · `/blog/best-apps-talk-to-strangers-india` 455 · `/voice-chat-india` 76 · `/meet` 37 · `/talk-to-strangers` 35 · `/blog/best-anonymous-voice-chat-sites` 16 · `/faq` 7 | GA4 |
| Google non-brand clicks (75 days) | **9** | GSC |

**What this tells us**
1. **One page earns most of the citations**: a neutral, fact-checked comparison article that answers a buying question ("best apps to talk to strangers in India"). ChatGPT even cites it **as its source for a competitor (OmeTV)**, so it treats the page as a reference, not an ad.
2. **The homepage gets the most AI clicks** (569). When ChatGPT recommends the brand by name it links to the homepage, so the homepage has to convert.
3. **Google rankings aren't what drives this.** Non-brand Google traffic is close to zero and only 21 of 41 sitemap URLs were indexed by Google. ChatGPT picked the site up anyway. ChatGPT search uses its own crawler (OAI-SearchBot) plus third-party search indexes, mainly Bing, so **Bing and crawler access matter more than Google rank for GEO**.
4. **Backlinks weren't the cause.** The outreach tracker (`backlink-tracker.xlsx`) shows every directory as "Not started". The only outreach was 5 emails on Sep 26, after the traffic had already grown. The result came from on-site work.

**What it does NOT prove.** ChatGPT traffic started in week 34–35 (late August), **before** the Sep 9 "geo" rewrite, so that rewrite didn't start it. Growth sped up after Sep 9 (128 → 266 → 419/week), which is consistent with the rewrite helping, but that is correlation, not proof. AI answers also vary from run to run. Treat every item below as "what was done and seems to work", not a guaranteed formula.

---

## 2. Timeline of everything done

| Date | What was done | Commit / file |
|---|---|---|
| 2026-06-23 | Blog built on a **structured content model** (sections typed as `p`, `h2`, `ul`, `table`, `faq`, `callout`, `cta`, `links`) instead of raw HTML | `1bba7c2`, `data/blog/articles.ts` |
| 2026-07-12 | SEO foundation: `@nuxtjs/sitemap`, `@nuxtjs/robots`, `nuxt-schema-org`, `site.url`, dynamic sitemap source for blog and country URLs, blog enabled, country pages | `3da17ef`, `ec1e45f` |
| 2026-07-12/13 | Descriptive image alt text, robots exclusions, blog copy rewritten for search | `567dc11`, `463aa4c`, `2c2d986` |
| 2026-07-18 | Canonical-URL middleware (trailing slash and `/index.html` → 301), semantic `<main>`, heading hierarchy fixes, security headers/CSP | `5434b53`, `51d5779`, `bb0ddbd` |
| ~2026-07-18 | `public/llms.txt` added | — |
| 2026-08-02 | Full 10-part audit. **Fixed:** crawl trap (unknown URLs and `/faq` returned 302 → `/login` instead of 404/200); **fake `aggregateRating` (4.8★/1,240) removed**; **fake testimonials removed**; hidden `sr-only` keyword text made visible; duplicate Organization nodes merged into one; false `operatingSystem: iOS, Android` removed; blog schema given `image`, real `dateModified`, BreadcrumbList; related posts chosen by shared tags; unused image preloads removed | `voicechat/SEO_STATUS.md` |
| ~2026-08-02 | `public/.well-known/ai.txt` added | `1b0848b` |
| 2026-08-12 | `/omegle-alternative` landing page removed and 301-redirected (cannibalization) | `3aa1b23` |
| 2026-08-13 | After AdSense rejected the site for "low value content": 40 thin country pages set to `noindex, follow` and removed from the sitemap; the top 10 countries got unique copy; 2 thin blog posts expanded to 400+ words | `c11fc92` |
| **wk 34 (Aug 17–23)** | **First ChatGPT sessions appear (7/week)** | GA4 |
| 2026-09-07 | `/talk-to-strangers` landing page | `d4c76ea` |
| **2026-09-09** | **"geo" commit.** India article rewritten into a **verified multi-competitor comparison** (method, table, per-platform facts, own limitations, FAQ, sources with check dates); Omegle-alternatives article rewritten the same way; new article `best-anonymous-voice-chat-sites`; 3 new intent landing pages (`/anonymous-voice-chat`, `/voice-chat-without-signup`, `/voice-chat-india`), each with visible FAQ and FAQPage schema; blog renderer gained `table`/`faq`/`links` blocks with FAQPage schema generated from the visible FAQ; `llms.txt` expanded; AI-bot robots groups moved into config and **OAI-SearchBot added**; `sameAs` expanded to 4 social profiles; WebApplication schema restricted to the homepage; country-page `Service.provider` linked to the site identity; footer links to every landing page; `/blog/omegle-alternative` merged via 301 | `934b16d` |
| 2026-09-11 | `.well-known/security.txt`; GA4 chat-start event `partner_connected` added | `0e52fae` |
| 2026-09-15 | "Stranger Stories" user-story campaign; microphone-help article | `9e0dcc6` |
| 2026-09-26 | Data-driven plan (`SEO_STRATEGY.md`); **3-CTA experiment on the cited article** plus `blog_cta_click` GA4 event; owner/admin traffic excluded from GA4; manual "Request indexing" in GSC for 8 URLs; outreach emails to 5 roundup sites; **prices removed from llms.txt, articles and landing pages** so AI can't repeat stale prices; **IndexNow** key deployed and all URLs submitted; country-page noindex fixed so meta tag and `X-Robots-Tag` header agree | `1e077ac`, `036903d`, `0e843b8` |
| 2026-09-29 | Brand spelling standardized to "Random Talker" everywhere plus `pnpm check:brand` guard (cited article left untouched); `alternateName` for the other spellings; robots per-bot groups now repeat the disallow list (RFC 9309 fix); Safety page with monthly report/ban counts; Grievance officer page; legal pages | `c00bcb0` |

---

## 3. P0: foundations and the page that gets cited

### P0-1. Let AI crawlers in (and check that your CDN isn't blocking them). Evidence: Standard, and a hard requirement
**Done here:** `voicechat/frontend/nuxt.config.ts` → `robots.groups` has explicit groups for `GPTBot`, `OAI-SearchBot`, `ClaudeBot`, `PerplexityBot`, `Google-Extended`, `Applebot`, `Bingbot`, `anthropic-ai`, `cohere-ai`.

**How to do it on a new site**
- `OAI-SearchBot` is the one ChatGPT search results depend on. `GPTBot` is OpenAI's training crawler. Allow both unless you have a reason not to.
- **Gotcha (fixed here on Sep 29):** a bot that matches its own `User-agent` group **ignores** the `User-agent: *` group entirely (RFC 9309). An "Allow: /" group with no disallows re-opens `/admin`, `/login` and `/api/` to that bot. **Repeat your disallow list inside every per-bot group.**
- Keep one source of truth. Here, a leftover `public/_robots.txt` was being merged into the generated file and produced a second `User-agent: *` block and an old non-www sitemap line.
- **Cloudflare:** turn off "Block AI bots" / AI Scrapers and Crawlers (or allow verified bots), then check that `curl -A "OAI-SearchBot/1.0" https://yoursite/` returns **200 with real HTML**. Third-party audit tools often get a Cloudflare challenge page ("Just a moment…", 403) from datacenter IPs. That's a tool-side false positive, not what verified bots see.

**Verify:** `curl https://yoursite/robots.txt` and `curl -I -A "OAI-SearchBot/1.0" https://yoursite/<key-page>` → `200`.

### P0-2. Serve full content as HTML on the server. Evidence: Standard, and a hard requirement
AI crawlers generally don't run JavaScript. If your content only appears after JS runs, they see an empty page.

**Done here:** Nuxt SSR plus ISR (`routeRules: { '/blog/**': { isr: 3600 }, ... }`). Only the app screen (`/meet`) is client-only, and it's disallowed in robots.
**Verify:** `curl -A "OAI-SearchBot/1.0" <url> | grep "<table"`. On the cited article, the table, all 12 "verified" lines and all JSON-LD are in the raw HTML (checked 2026-09-30).

### P0-3. Get into Bing, not just Google. Evidence: Data (ChatGPT traffic grew with Google coverage at 21/41) plus Standard
**Done here:** Bing Webmaster Tools (it flagged the header/meta noindex conflict, so it's being used); **IndexNow**: key file `public/<key>.txt`, all sitemap URLs submitted to `api.indexnow.org` (HTTP 202).
**How:** verify the site in Bing Webmaster Tools, submit the sitemap, add an IndexNow key file, and **resubmit changed URLs after every content edit**. Google doesn't use IndexNow, so keep using GSC for Google.

### P0-4. Build ONE "reference-grade" comparison page for your main buying question. Evidence: Data (455 ChatGPT sessions, cited as a source even for a competitor)
This is the most important item in the playbook. The page is `/blog/best-apps-talk-to-strangers-india` (`data/blog/articles.ts`, slug `best-apps-talk-to-strangers-india`). Its structure is a template you can copy.

**Pick the question:** the literal prompt your buyers type into ChatGPT: "best [category] for [audience/location] in [year]". Here: "best apps to talk to strangers in India".

**Page anatomy (copy this order):**
1. **Title with the year**: "Best Apps to Talk to Strangers in India in 2026".
2. **Answer-first intro (2–3 sentences)** that names the categories of options and what the choice depends on. AI engines lift this directly.
3. **Scope sentence**: what was compared and "All competitor facts were verified against each platform's official public website on [date]."
4. **Early CTA** right after the intro (see P1-8).
5. **H2 "How We Compared These Platforms"**: a bullet list of 8–11 objective criteria.
6. **Honesty disclaimer**: "desk comparison of publicly stated information… no platform is ranked #1 across all metrics."
7. **H2 comparison table**: rows = platforms (yours plus 5 real competitors), columns = the criteria, last column **"Best for"**. Use "Unclear" instead of guessing, and explain what "Unclear" means under the table.
8. **H2 "Detailed Platform Breakdowns"**: one H3 per platform, "N. Name — one-line positioning", one paragraph, then the **same bullet fields for each**: Best for · Format · Signup · Matching · Free access · **Notable limitation** · **Source & check date**.
   - Put your own product first, **but include its real limitation** ("No dedicated India-only or regional language filter — matching is random"). This is why the page reads as neutral, and why AI engines trust it.
9. **Decision sections**: "Voice vs Video vs Text: which is best in India?", "No-signup vs account-based", "Key considerations for Indian users", audience sections (regional languages, English practice), safety guidelines.
10. **H2 FAQ (8–10 questions)** phrased the way people prompt AI ("Can I talk to strangers by voice in India?", "Which platforms work without signup?"). **Include questions that state your own limitations** ("Does RandomTalker have an India-only filter? No.").
11. **H2 "Sources and Verification Dates"**: one line per platform with its official domain and check date.
12. **H2 "Learn More"**: 8–10 internal links to your landing pages, FAQ, pricing and privacy pages.
13. **Bottom CTA.**

**Schema on the page** (`pages/blog/[slug].vue`): `Article` (headline, description, image, `datePublished`, **real `dateModified`**, author/publisher pointing to the site Organization `@id`), `BreadcrumbList`, and `FAQPage` **built from the same array that renders the visible FAQ**, so the schema can never differ from the page.

**Rules once it's cited:**
- **Freeze the text.** Once ChatGPT cites a page, don't rewrite it. Add CTAs around it, but leave the wording alone. (Here, the brand-spelling cleanup deliberately skipped this article, and `check-brand.mjs` has a `frozenArticle` exception for it.)
- **Refresh the facts on a schedule** (e.g. quarterly): re-check competitors, update the check dates and `updatedAt`, and resubmit via IndexNow.

A second page built the same way: `/blog/best-omegle-alternatives-voice-chat` (method, table, "Which alternative fits your situation", sources, and a "Last updated: September 2026" line).

### P0-5. Make every fact about your product accurate and the same everywhere. Evidence: Data (AI engines repeated our claims, including wrong ones)
AI engines repeat whatever you publish, including mistakes. Perplexity told users Random Talker "supports Hindi", and it doesn't.

**Done here:**
- **Prices removed from everywhere except `/pricing`** (llms.txt, articles, landing pages, FAQ, pricing meta, pricing Product/Offer schema). Copy now says "free to use, optional Premium". Reason: the ₹99 price was stale (everything was free), and AI answers were quoting it. (`036903d`)
- Explicit "No" answers for missing features (no India-only filter, no Hindi filter, no video).
- False schema claims removed: `operatingSystem: "Web, iOS, Android"` (no native app existed), made-up audience labels ("night owls, introverts").
- Off-brand FAQ answers comparing against an unrelated competitor ("AirTalk") replaced.

**How:** keep one fact sheet (what's free, what's paid, platforms, languages, age limit, data handling). Don't put numbers that change often (prices, user counts) in content AI will cache; link to the one page that holds them.

### P0-6. One canonical URL per page, real 404s, clean sitemap. Evidence: Standard
**Done here:**
- `brand.siteUrl = https://www.randomtalker.com`; the apex domain 308-redirects to www; every page sets `<link rel="canonical">` explicitly. (`useSeoMeta`'s `canonical` key doesn't work without the nuxt-seo-utils module, which silently broke canonicals on all blog posts once.)
- `server/middleware/canonical-redirects.ts`: trailing slash and `/index.html|php` → 301.
- **Crawl-trap fix**: the auth middleware sent unknown URLs to `/login` with an indexable 302. Replaced it with `middleware/global-auth.global.ts`, which lets real 404s through.
- Sitemap: static pages found automatically, and blog/country URLs come from `server/api/__sitemap__/urls.ts` with **`lastmod` taken from the article's real `updatedAt`**. Private routes excluded.
- Legacy URLs use a **single-hop 301** to the consolidated page (no chains).

**Verify:** the sitemap URL count matches the number of pages you actually want indexed (43 live today); `curl -I` on a made-up URL returns 404.

---

## 4. P1: trust, entity and coverage

### P1-1. One brand entity with consistent naming. Evidence: Data (GSC: "random talker" 261 clicks vs "randomtalker" 175) plus Standard
**Done here:**
- `nuxt.config.ts` → `schemaOrg.identity`: **one** Organization node (`@id …/#identity`) with `name`, `alternateName: ['RandomTalker', 'randomtalker.com']`, `url`, `description`, `email`, `sameAs` (X, Instagram, Facebook, LinkedIn). Every other schema node points to this `@id` instead of repeating an inline Organization.
- **Gotcha:** in `nuxt-schema-org`, adding `logo` to the identity splits it into two Organization nodes, so the logo was left out on purpose.
- The name is spelled "Random Talker" in all visible text, titles and schema; code uses `brand.appName` (`constants/brand.ts`); **`pnpm check:brand`** (`scripts/check-brand.mjs`) fails the build on other spellings (URLs and handles allowed).
- `sameAs` is kept in sync with the social links actually shown in the footer.

**How:** decide the exact brand spelling on day 1, put it in a constant, add a lint check, list the other spellings in `alternateName`, and create real social profiles that link back to the site.

### P1-2. Structured data that matches what's on the page. Evidence: Standard
| Page | Schema | File |
|---|---|---|
| Sitewide | `WebSite`, `Organization` (#identity) | `app.vue`, `nuxt.config.ts` |
| Homepage only | `WebApplication` (free Offer, featureList, `alternateName`, creator → #identity) | `pages/index.vue` |
| Blog post | `Article`, `BreadcrumbList`, `FAQPage` if the post has a FAQ section | `pages/blog/[slug].vue` |
| Blog index | `Blog` | `pages/blog/index.vue` |
| Landing pages | `BreadcrumbList` and `FAQPage` merged onto the page's own WebPage node | `voice-chat-india.vue`, `anonymous-voice-chat.vue`, `voice-chat-without-signup.vue`, `talk-to-strangers.vue`, `faq.vue` |
| About / Safety / Grievance | `AboutPage` / `WebPage` and `BreadcrumbList` | `about.vue`, `safety.vue`, `grievance.vue` |
| Country pages | `Service` (provider → #identity), `BreadcrumbList` | `pages/chat/[country].vue` |

**Rules learned the hard way:**
- **Build FAQ schema from the same data that renders the visible FAQ.** The homepage once had FAQPage schema with no visible FAQ, and `/faq` once had schema with different questions from the page. Both were removed.
- Don't put page-specific schema in the global head. `WebApplication` was once on every route (blog, admin, login), and `/meet` had a second, conflicting copy.
- **No `aggregateRating` without real, visible reviews.**

### P1-3. Landing pages for each search intent, written answer-first with FAQs. Evidence: Data (ChatGPT visitors to `/voice-chat-india` and `/talk-to-strangers` start a chat at ~26%)
**Done here:** `/voice-chat-india`, `/anonymous-voice-chat`, `/voice-chat-without-signup`, `/talk-to-strangers`.
**Structure every one of them uses:** H1 = the exact intent ("Anonymous Voice Chat in India") → "What is X?" definition H2 → "How it works" numbered steps → "Why voice instead of video?" → X without signup → audience sections → Safety → Privacy and data handling → Free vs Premium (no price) → FAQ (8 questions, including "No" answers) → final CTA.
**Warning:** don't create several pages for the same intent. Three pages chasing "India + voice chat" split the signals (`SEO_STRATEGY.md` P1-A). Give each page one intent and link between them.

### P1-4. Internal linking. Evidence: Standard
- The footer (`components/marketing/MarketingFooter.vue`) links every landing page, the blog, the FAQ and the countries hub.
- Every comparison article ends with a "Learn More" `links` block (about 10 descriptive internal links).
- Contextual links: About → anonymous-voice-chat guide; `/chat/india` → `/voice-chat-india`.
- "Continue reading" suggestions are chosen by shared tags, not by position in the array.
- A page that nothing links to gets ignored. `/omegle-alternative` once had zero internal links.

### P1-5. Trust pages (E-E-A-T). Evidence: Standard
`/about` (why the product exists, who it's for, how it stays safe), `/safety` (how reporting works plus **live monthly counts of reports and bans** from `/api/safety/stats`), `/grievance` (named Grievance Officer and address, as India's IT Rules 2021 require), `/privacy` (peer-to-peer WebRTC data handling), `/terms` (18+), `/contact`, `/.well-known/security.txt`.
AI engines and Google both look for a real, accountable operator, especially for anything that involves strangers, money or health.

### P1-6. Remove anything that looks like spam or manipulation. Evidence: Standard (Google spam policies)
All of these were in this project at some point and had to be removed:
- Fake `aggregateRating` (4.8★ from 1,240 ratings, no real reviews)
- Fake testimonials with generated avatars
- Hidden (`sr-only`) keyword block
- Fake live-activity numbers ("X people online")
- 40 near-duplicate country pages. The fix: unique content for the top 10 (`DEEP_CONTENT` map); the rest are `noindex, follow` via `useRobotsRule` so the meta tag **and** the `X-Robots-Tag` header agree.
- Thin blog posts (under 200 words), which were expanded.

### P1-7. Allow full snippets. Evidence: Standard
The live pages send `X-Robots-Tag: index, follow, max-image-preview:large, max-snippet:-1`. Never set `nosnippet` or a low `max-snippet` on pages you want quoted.

### P1-8. Turn AI traffic into users. Evidence: Data
AI visitors from comparison pages are shopping around: 11% of ChatGPT visitors to the India article started a chat, against 29% who landed on the homepage. The article's only CTA was at the very end.
**Done here:** CTAs at `top` (after the intro), `randomtalker-entry` (inside your own product's section) and `bottom`. Every click fires GA4 `blog_cta_click` with `article_slug`, `cta_position` and `cta_href`. The experiment runs Sep 26 – Oct 17; success is ≥18%.
**How:** add a CTA after the intro and one inside your own product's entry, and track which position gets clicked.

---

## 5. P2: reach, freshness and measurement

### P2-1. Measure AI traffic properly. Evidence: Data
- GA4: the "AI Assistant" channel (chatgpt.com, perplexity.ai…) → report **landing page × conversion event** (here `partner_connected`). Track conversions, not just sessions.
- Register the custom dimensions (`cta_position`, `article_slug`) in GA4 → Admin → Custom definitions.
- Exclude your own traffic (`plugins/internal-traffic.client.js` turns GA4 off in any browser holding an admin token).
- GSC: split **brand vs non-brand** at query × page level. Page-level positions look good only because of brand-search sitelinks.
- Scripts used: `claude-seo/scripts/gsc_query.py` and the GA4 scripts (venv and OAuth described in the `seo-data-access` note).

### P2-2. Monthly AI answer tracking. Evidence: Data
Once a month, ask logged-out ChatGPT (with web search on) and Perplexity the same 8 prompts, and record whether you're recommended, whether you're cited, and anything they get wrong. Template: `SEO_STRATEGY.md` §7. Results on 2026-09-26: recommended for "voice only app… India" and "…without signup voice call"; cited but not recommended for "best app to talk to strangers in india"; absent for "omegle alternative voice only", "anonymous voice chat online free", "best omegle alternative in india" and "practice english… india".
Use the "absent" prompts to decide the next comparison page to build.

### P2-3. Freshness signals. Evidence: Standard
The year in the title, a visible "Last updated: <Month Year>" line, a real `updatedAt` feeding schema `dateModified`, the sitemap `lastmod` and `article:modified_time`. Only change the date when you actually re-check the facts. Resubmit via IndexNow after each update.

### P2-4. Get mentioned elsewhere (corroboration). Evidence: Standard (not yet done here, so the upside is still open)
AI engines trust brands that other sites mention. Here: no presence in Common Crawl's link graph, no third-party mentions found (Aug 2 audit). Perplexity recommended us for some prompts and not others.
Plan (`backlink-action-plan.md`, `voicechat/SEO_BACKLINKS.md`, tracker `backlink-tracker.xlsx`):
1. **Get added to the roundups that already rank and get cited** ("best X alternatives 2026"). Pitch one specific, missing angle (here: "voice-only, no signup, browser").
2. **AlternativeTo** (list yourself as an alternative to the big competitors), SaaSHub, Product Hunt, BetaList, Indie Hackers, Crunchbase, G2/Capterra.
3. Reddit/Quora answers where you're genuinely the answer, **saying you're the founder**.
4. Real social profiles linked in `sameAs`. `voicechat/social-poster` is a small MCP server that posts to LinkedIn, Facebook, Instagram, Bluesky and Mastodon.
**Never pay for links.**

### P2-5. Manual indexing push. Evidence: Standard
In GSC → URL Inspection → "Request indexing" for your top 8–10 pages (quota is about 10/day). Don't use Google's Indexing API; it only supports job-posting and livestream pages.

### P2-6. Social and preview metadata. Evidence: Standard
`og:*` and `twitter:*` defaults in `nuxt.config.ts` and `app.vue`; a 1200×630 `/og-image.png`; per-page `ogUrl`/`ogTitle`/`ogDescription`; `og:type=article` plus published/modified times on posts.

### P2-7. Performance. Evidence: Standard
Unused `<link rel="preload">` hero images were removed (homepage LCP measured 6.7s, rated "Poor", on Aug 2); fonts load without blocking rendering; asset compression is on. Check real-user Core Web Vitals in GSC.

---

## 6. P3: optional or low value (done here, cheap, don't expect much)

| Item | Where | Why it's low priority |
|---|---|---|
| `llms.txt` (site summary plus annotated list of key pages and blog posts) | `public/llms.txt` | **Unproven.** No major AI engine has confirmed using it. It costs 10 minutes, so do it, but **keep it accurate** (prices were removed from it). |
| `.well-known/ai.txt` | `public/.well-known/ai.txt` | Not a recognized standard; no known consumer. |
| `SpeakableSpecification` on the homepage | `pages/index.vue` | Google uses it only for news publishers. |
| `keywords` meta | `app.vue` | Ignored by Google and Bing. |
| `hreflang` en / x-default pointing at the same URL | `app.vue` | Only matters with more than one language. |
| Google Trends for wording choices | — | Useful only to choose between phrasings. |

---

## 7. Don't copy these (mistakes made here)

| Mistake | Why it's bad | Status |
|---|---|---|
| Made-up `aggregateRating` in schema | Violates Google's structured-data spam policy; risk of a manual action | Removed Aug 2 |
| Fake testimonials and fake "online now" counts | Deceptive; hurts trust | Removed |
| Keyword text hidden with `sr-only` | Cloaking | Made visible Aug 2 |
| **Backdated `publishedAt` dates** (articles created 2026-06-23 show dates in Jan–Jun **2025**, some with `updatedAt: 2025-06-01`) | Dates in schema and sitemap should be true. This is a trust and accuracy risk | **Still live.** Don't do this on the new site. Use real dates |
| FAQ schema that doesn't match the visible page | Against Google's guidelines | Fixed (schema built from the same array) |
| Global JSON-LD that claims the homepage URL on every route | Conflicting entities | Fixed |
| Two Organization nodes (logo quirk and inline provider objects) | Splits the brand entity | Fixed |
| An Allow-only robots group per bot | Re-opened private paths to those bots (RFC 9309) | Fixed Sep 29 |
| Stale prices in content AI caches | AI keeps repeating the wrong price | Fixed Sep 26 |
| Schema claims that aren't true (`operatingSystem: iOS, Android`) | AI repeats false claims | Fixed |
| **`inLanguage: ["en", "hi"]`** in the homepage WebApplication schema, although the site is English-only | Likely one reason Perplexity says "supports Hindi" | **Still live**, worth fixing |
| 3 pages targeting the same intent (Omegle ×3, India ×3) | Cannibalization | Omegle merged via 301; India decision pending (Oct 24) |
| 50 template-generated location pages | Scaled-content risk; AdSense rejection | 40 set to noindex |
| Hardcoded non-www sitemap hostname | Sitemap entries that redirect | Fixed (inherits `site.url`) |

---

## 8. New-site checklist (in order)

**Day 1–2: foundation (P0)**
- [ ] Choose the canonical host (www or apex), set up the redirect, put `siteUrl` in one constant
- [ ] SSR/SSG for all public content; verify with `curl`
- [ ] robots.txt: `User-agent: *` disallows, plus per-bot groups for OAI-SearchBot, GPTBot, PerplexityBot, ClaudeBot, Google-Extended, Applebot, Bingbot, **each repeating the disallows**
- [ ] CDN: AI-bot blocking off; `curl -A "OAI-SearchBot/1.0"` returns 200 with real HTML
- [ ] Auto-generated sitemap with real `lastmod`; private routes excluded
- [ ] Canonical `<link>` on every page; trailing-slash normalization; real 404s
- [ ] GSC and **Bing Webmaster Tools** verified, sitemap submitted to both; IndexNow key deployed
- [ ] Product fact sheet written; no volatile numbers outside the pricing page

**Week 1: the cited page (P0-4)**
- [ ] Find 3–5 "best X for Y in [year]" prompts your buyers ask ChatGPT
- [ ] Build one comparison page using the anatomy in §3 P0-4: method, table, per-platform facts including **your own limitation**, FAQ, sources with check dates, Learn More links, 3 tracked CTAs
- [ ] Article, BreadcrumbList and FAQPage schema (FAQ built from the visible data)

**Week 2–3: trust and coverage (P1)**
- [ ] One Organization entity: `@id`, `alternateName`, `sameAs` → real social profiles
- [ ] Brand spelling constant plus a lint check
- [ ] 3–4 intent landing pages (answer-first, question H2s, 8-question FAQ with honest "No"s)
- [ ] Footer and contextual internal links; no orphan pages
- [ ] About, Safety/Trust, Contact, Privacy, Terms, security.txt (plus legally required pages for your country)
- [ ] `X-Robots-Tag` / meta allow full snippets
- [ ] No fake ratings, reviews, activity counts or hidden text; noindex thin template pages

**Week 3+: reach and measurement (P2)**
- [ ] GA4: AI Assistant channel × landing page × conversion event; exclude internal traffic
- [ ] Monthly prompt-tracking table (ChatGPT and Perplexity, same prompts)
- [ ] Outreach to ranking roundups; AlternativeTo and directories; founder-disclosed community answers
- [ ] Quarterly fact refresh of comparison pages, then IndexNow resubmit
- [ ] Once a page is being cited: **freeze its text** and only add CTAs around it

**Optional (P3):** llms.txt (accurate), OG image, speakable.

---
