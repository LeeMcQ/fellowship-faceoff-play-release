# Fellowship Face-Off — Google Play release pack

**This repository is for Google Play only — not the Apple App Store.**

Public release kit for publishing **Fellowship Face-Off** as an Android Trusted Web Activity (TWA) that opens the live PWA:

- **PWA (game stays in logosliving):** https://leemcq.github.io/logosliving/
- **Package name (immutable once used):** `com.leemcq.fellowshipfaceoff`
- **Developer GitHub:** LeeMcQ

Game source code is **not** duplicated here. It lives in [`LeeMcQ/logosliving`](https://github.com/LeeMcQ/logosliving). This repo holds the Bubblewrap/TWA project, store assets, listing copy, privacy stub, and Digital Asset Links placeholders. No AAB/APK is committed (the repo is public); signed bundles are built locally and uploaded to Play. Release history is in [`CHANGELOG.md`](CHANGELOG.md).

---

## Critical Play facts

1. **Google Play**, not Apple.
2. **New Play apps require a signed `.aab` (Android App Bundle).** An APK is **not** accepted for new app listings. If someone said “just upload an APK,” that advice is outdated for new apps — use a signed AAB.
3. No AAB is committed to this repo. Build a **signed** AAB locally from [`twa/`](twa/) (see [`twa/PLAY_WRAP_README.md`](twa/PLAY_WRAP_README.md) §3). Each tagged release (`v<semver>`) records the uploaded AAB's versionCode and SHA-256.
4. Package ID **`com.leemcq.fellowshipfaceoff`** cannot be changed after first use on Play.
5. Digital Asset Links must be published at the **domain root** of `leemcq.github.io` (Android only checks `/.well-known/` at the host root, not under `/logosliving/`):  
   `https://leemcq.github.io/.well-known/assetlinks.json`  
   It is served from the `LeeMcQ/leemcq.github.io` user Pages site, not from logosliving.  
   (copy from [`digital-asset-links/`](digital-asset-links/); instructions in that folder’s README).

---

## Repo map

| Path | Purpose |
|------|---------|
| [`RELEASE_CHECKLIST.md`](RELEASE_CHECKLIST.md) | Printable day-of submit checklist |
| [`LISTING_COPY.md`](LISTING_COPY.md) | Title / short / full / what’s new + character counts |
| [`PAYMENTS_AND_POLICY.md`](PAYMENTS_AND_POLICY.md) | Play Billing vs web unlocks, ads, Data safety notes |
| [`store-assets/`](store-assets/) | Feature graphic, 512 icon, screenshot capture script |
| [`privacy/privacy-policy.html`](privacy/privacy-policy.html) | Privacy policy — **add contact email before hosting** |
| [`digital-asset-links/`](digital-asset-links/) | `assetlinks.json` placeholders + how to publish at the `leemcq.github.io` root |
| [`twa/`](twa/) | Bubblewrap TWA project (`twa-manifest.json`, Gradle app, `PLAY_WRAP_README.md`) |
| [`CHANGELOG.md`](CHANGELOG.md) | Release history (versionCode, versionName, AAB SHA-256) |

---

## Ordered release steps

Follow in order. Each step links to the file(s) that help.

### 1. Create upload keystore (do not commit)

Generate a local upload keystore and store passwords in a password manager.

→ Details: [`twa/PLAY_WRAP_README.md`](twa/PLAY_WRAP_README.md) §2  

Keep `*.keystore` / `*.jks` **out of git** (see `.gitignore`).

### 2. Build a **signed** AAB

```bash
cd twa
# After JDK 17 + Android SDK + bubblewrap config — see PLAY_WRAP_README.md
export BUBBLEWRAP_KEYSTORE_PASSWORD='…'
export BUBBLEWRAP_KEY_PASSWORD='…'
bubblewrap build --skipPwaValidation
```

→ [`twa/PLAY_WRAP_README.md`](twa/PLAY_WRAP_README.md) §3

Upload the **signed** `.aab` to Play Console. Never commit the `.aab`, keystore or `keystore.properties`.

### 3. Create the Play Console app

Create an application with package name **`com.leemcq.fellowshipfaceoff`**.

### 4. Play App Signing

Upload the signed AAB and enroll in **Play App Signing** (default).  
Copy the **App signing key certificate** SHA-256 from **Setup → App signing**.

→ [`twa/PLAY_WRAP_README.md`](twa/PLAY_WRAP_README.md) §4

### 5. Closed testing

Create a **closed** test track, add testers, install from Play, smoke-test Sing / Act / Explain / offline.

→ Day-of ticks: [`RELEASE_CHECKLIST.md`](RELEASE_CHECKLIST.md)

### 6. Privacy policy URL

1. Replace `[ADD YOUR CONTACT EMAIL]` in [`privacy/privacy-policy.html`](privacy/privacy-policy.html).
2. Host on HTTPS.
3. Paste URL into Play Console → App content → Privacy policy.

### 7. Listing assets & copy

- Copy: [`LISTING_COPY.md`](LISTING_COPY.md)  
  - Title: **Fellowship Face-Off** (19/30)  
  - Short: **Sing, act & explain Bible words with your group. Offline church party game.** (75/80)
- Graphics: [`store-assets/`](store-assets/)  
- Screenshots: [`store-assets/SCREENSHOTS_BRIEF.md`](store-assets/SCREENSHOTS_BRIEF.md) (capture live PWA — no fake UI)

### 8. Data safety, ads & payments declarations

Complete Data safety and related forms to match the **shipped** Play build.

→ [`PAYMENTS_AND_POLICY.md`](PAYMENTS_AND_POLICY.md)

### 9. Digital Asset Links at the leemcq.github.io root

Fill fingerprints in [`digital-asset-links/assetlinks.json`](digital-asset-links/assetlinks.json), then publish to:

`LeeMcQ/leemcq.github.io` → `.well-known/assetlinks.json`  
Live: https://leemcq.github.io/.well-known/assetlinks.json

→ [`digital-asset-links/README.md`](digital-asset-links/README.md) · [`twa/ASSETLINKS_GITHUB_PAGES.md`](twa/ASSETLINKS_GITHUB_PAGES.md)

### 10. Production access & rollout

Complete any **production access** / account verification Play requires for new developers, then promote from closed testing to production (staged rollout recommended).

→ [`RELEASE_CHECKLIST.md`](RELEASE_CHECKLIST.md)

---

## Quick listing preview

| Field | Text | Count |
|-------|------|-------|
| Title | Fellowship Face-Off | 19/30 |
| Short | Sing, act & explain Bible words with your group. Offline church party game. | 75/80 |

Full description and what’s-new: see [`LISTING_COPY.md`](LISTING_COPY.md).

---

## What “you said APK” means here

Older Android workflows distributed **APKs**. **Google Play now requires App Bundles (`.aab`) for new apps.** Sideloading an APK for personal testing is fine; **Play Console upload for a new app must be a signed AAB.** This repo holds the TWA source that builds the signed `.aab`; neither AABs nor APKs are committed.

---

## License / ownership

Release materials prepared for **Lee McQuire (LeeMcQ)**. Do not commit secrets. Game content remains with the logosliving project.
