---
name: ios-release-audit
description: Audit the Random Talker iOS app in mobile/ for App Store submission risks - review guideline problems, permissions, privacy declarations, sign-in, account deletion, purchases, broken flows and build settings. Use when the user asks if the iOS app is ready to submit, wants a release or pre-submission check, or is preparing a TestFlight or App Store build.
---

# iOS release audit

Read-only. Report findings and change nothing unless the user then asks for fixes.

## Rules

- Load the `apple-review-docs` skill first and check each rule against the live guidelines. Note the page's "Last Updated" date in the report.
- Every finding needs evidence: `file:line`, a command's output, or an App Store Connect value. If you can't get evidence, list the item under "Not checked".
- Never suggest hiding functionality from review, wording the listing to mislead reviewers, or switching features off only during review. That breaks 2.3.1 and risks the developer account. For a policy conflict, describe the conflict and the real product options.
- Do not tap the call button in a simulator or on a device. Mobile builds use the production API, so it would match real users. Screen checks stop before matching.
- App Store Connect access is read-only. Never submit, release or edit anything there.

## Checks

Paths are relative to `mobile/`. If a path has moved, search for it. Don't assume the feature is gone.

### 1. Content policy (check this first; it can end the submission)

Guideline 1.2 lists random or anonymous chat among apps that don't belong on the App Store. Random Talker's main feature is matching with strangers, including guests. Read the current text and report plainly how it applies, including what is not settled.

Then check the safeguards 1.2 requires, separately for text, images and live voice:

- Filtering objectionable content: `src/utils/profanity.ts`, `src/services/call/chatImages.ts`. Live voice has no filter before it is heard, so say so if nothing covers it.
- Reporting: `src/app/components/modals/ReportModal.tsx`, plus whether reports reach someone who responds in time.
- Blocking: the user-facing control and whether the block really stops re-matching.
- Published contact details: reachable inside the app.

### 2. Age rating

- `src/app/components/modals/AgeGateModal.tsx`: what it enforces, and whether it can be skipped.
- Compare the App Store Connect age-rating answers with real features: stranger contact, user content, images.

### 3. Permissions and capabilities

In `ios/RandomTalker/Info.plist` and `ios/RandomTalker/RandomTalker.entitlements`:

- Each usage string matches a real use, and each permission the code or a native module requests has a string.
- Each `UIBackgroundModes` entry is justified. `remote-notification` needs Push set up: check for `aps-environment` and `GoogleService-Info.plist`.
- `ITSAppUsesNonExemptEncryption` is present, or export compliance is otherwise answered. WebRTC encrypts media, so this needs a real answer.
- `NSAllowsLocalNetworking` is needed in release builds.

### 4. Privacy

- `ios/RandomTalker/PrivacyInfo.xcprivacy` against the data the code actually collects, and against third-party SDK manifests in `ios/Pods`.
- Required-reason API entries match real use.
- Check the promise in `NSPhotoLibraryUsageDescription` that photos never reach the servers against `src/services/call/chatImages.ts` and any moderation path.
- Privacy policy URL is live, linked in the app, and matches the App Store Connect privacy labels.

### 5. Sign-in and account deletion

- `com.apple.developer.applesignin` is in the entitlements. An empty `<dict/>` here is a blocker for a store build while Apple sign-in is offered.
- Google sign-in is offered, so check 4.8 is met: `src/services/auth/useAuth.ts`, `src/app/components/ui/AppleSignInButton.tsx`.
- Deletion can be started in the app and finishes on the backend, including Apple token revocation: `src/app/components/AccountDrawer.tsx`, `src/services/api/backend.ts`.

### 6. Purchases

- Digital goods use native IAP only: `src/services/iap/purchases.ts`, `src/app/screens/PricingScreen.tsx`.
- A restore purchases control exists and works.
- No in-app link or wording steers users to Freemius, Cashfree or web checkout, unless the current rules allow it for the storefront.
- Product IDs in code match App Store Connect, and the backend verify path is configured.

### 7. Broken flows and leftovers

- Guest, sign-up, sign-in and sign-out, age gate, microphone permission denied, no network, and the `min_app_build` forced update.
- Dead ends from features not ported: Rooms, mini-games, private callbacks, and web game invites.
- Debug leftovers in release: localhost or LAN URLs, dev menus, test credentials, and the SampleTurboModule red screen in a Release build.
- App Review can't test matching alone. Check there's a workable plan in the review notes: how a reviewer gets a partner, plus a demo account.

### 8. Build and signing

Read `ios/RandomTalker.xcodeproj/project.pbxproj`:

- `DEVELOPMENT_TEAM` is a paid team. A free Personal Team can't distribute.
- Bundle ID, version, build number, deployment target and `TARGETED_DEVICE_FAMILY`.
- Icon set is complete, with a 1024px icon that has no alpha.
- Check `git status` in `mobile/`: a store build shouldn't come from uncommitted work.
- Check the Xcode and SDK minimums on the upcoming requirements page.

### 9. App Store Connect

Only if the App Store Connect MCP tools are available (`appstore-api`). Otherwise, put this whole section under "Not checked".

App record and version state, description and keywords against what the app really does, screenshots, support and privacy URLs, age rating, IAP status, build processing, export compliance, and review notes.

## Report

1. Verdict in one line: ready, ready after fixes, or blocked.
2. Blockers, then Likely rejections, then Worth fixing. For each: guideline number, evidence, why it matters, smallest fix.
3. Not checked: anything needing a device, a paid account or App Store Connect.

Keep it short and say nothing about items that passed unless the user asks. Prefer the smallest fix that satisfies the rule.
