---
name: apple-review-docs
description: Look up Apple's current official App Store rules from developer.apple.com - App Review Guidelines, privacy manifests and labels, account deletion, age ratings, screenshots, upcoming requirements, App Store Connect API. Use when the user asks what Apple requires or allows, cites a guideline number, gets a rejection, or before stating any App Store rule from memory.
---

# Apple review docs

Apple changes these rules often, so read the live page and don't answer from memory. This skill holds pointers only, not copies of Apple's text.

## How to read

- Use WebFetch on the URL. If a page is too long for one call, continue with the `offset` it reports. The guidelines page needs a second call.
- WebFetch answers through a small summarizing model. For wording that decides something, such as a rejection reason or a yes/no on a rule, check the exact sentence: `curl -sL <url>` and search the text.
- Pages under `/documentation/` render with JavaScript. Fetch the `/tutorials/data/documentation/....json` form below instead.
- When citing, give the guideline number, the URL and the page's "Last Updated" date. Paraphrase, and quote only a short phrase where the wording matters.

## Sources

| Topic | URL |
|---|---|
| App Review Guidelines | https://developer.apple.com/app-store/review/guidelines/ |
| App Review process, contact, appeals | https://developer.apple.com/distribute/app-review/ |
| Upcoming requirements and deadlines | https://developer.apple.com/news/upcoming-requirements/ |
| Privacy nutrition labels | https://developer.apple.com/app-store/app-privacy-details/ |
| Tracking and data use | https://developer.apple.com/app-store/user-privacy-and-data-use/ |
| Privacy manifest files | https://developer.apple.com/tutorials/data/documentation/bundleresources/privacy-manifest-files.json |
| Required-reason APIs | https://developer.apple.com/tutorials/data/documentation/bundleresources/describing-use-of-required-reason-api.json |
| Account deletion | https://developer.apple.com/support/offering-account-deletion-in-your-app/ |
| Sign in with Apple token revocation | https://developer.apple.com/tutorials/data/documentation/signinwithapplerestapi/revoke-tokens.json |
| Age rating values | https://developer.apple.com/help/app-store-connect/reference/app-information/age-ratings-values-and-definitions/ |
| Screenshot specifications | https://developer.apple.com/help/app-store-connect/reference/app-information/screenshot-specifications/ |
| App Store Connect API | https://developer.apple.com/tutorials/data/documentation/appstoreconnectapi.json |

## Guideline sections that matter most for Random Talker

Numbers can move, so confirm them on the live page.

- 1.2 user-generated content, which also names random or anonymous chat
- 2.1 completeness and 2.3 accurate metadata, including age-rating answers
- 3.1.1 in-app purchase
- 4.8 login services
- 5.1.1 data collection and storage, with account deletion at 5.1.1(v)
- 5.1.2 data use and sharing

If a URL fails, search developer.apple.com for the new location, and update this table.
