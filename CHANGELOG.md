# Changelog

All notable changes to the Fellowship Face-Off Android wrapper (TWA,
package `com.leemcq.fellowshipfaceoff`) are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project uses [Semantic Versioning](https://semver.org/spec/v2.0.0.html)
for wrapper releases. Android `versionCode` goes up by 1 for every AAB uploaded
to Google Play. The web app (`LeeMcQ/logosliving`) ships separately and is
tagged `web-YYYY.MM.DD`.

## [Unreleased]

## [1.0.1] - 2026-09-27

Rebuild for Google Play.

- versionCode: `2`
- versionName (manifest): `"1.0.1"`
- Signed AAB `FellowshipFaceOff-v2-release.aab` SHA-256:
  `51bc1db96ae8f6e4a00830b6bb8da90ef0c7674121e9ae06e9f2358df5c7701d`

### Changed
- Start URL is now `/logosliving/?src=twa` (was `/logosliving/index.html`), so
  TWA launches can be told apart in analytics. Built launch URL:
  `https://leemcq.github.io/logosliving/?src=twa`.
- Docs: the Digital Asset Links URL is now the domain root,
  `https://leemcq.github.io/.well-known/assetlinks.json` (served from
  `LeeMcQ/leemcq.github.io`), replacing
  `https://leemcq.github.io/logosliving/.well-known/assetlinks.json`, which
  Android ignores. Updated in README.md, RELEASE_CHECKLIST.md,
  digital-asset-links/README.md, twa/ASSETLINKS_GITHUB_PAGES.md and
  twa/PLAY_WRAP_README.md.
- Docs: removed the broken references to the deleted
  `twa/dist/fellowship-faceoff-unsigned.aab` and `twa/dist/README.md`.

### Removed
- Notifications are disabled (`enableNotifications: false`). The
  `POST_NOTIFICATIONS` permission, the notification small-icon meta-data and
  `NotificationPermissionRequestActivity` are no longer in the manifest, and the
  notification DelegationService is disabled. PLAY_WRAP_README.md and
  PAYMENTS_AND_POLICY.md now say notifications are off.

## [1.0.0] - 2026-09-27

First Google Play release.

- versionCode: `1`
- versionName (manifest): `"1"` (treated as semver 1.0.0)
- Signed AAB `FellowshipFaceOff-v1-release.aab` SHA-256:
  `8ca85bf42c0a010882b94b16227feb5bab16617d02b44c208f89629870bbf260`

### Added
- Release signing config in `twa/app/build.gradle`. It reads the store and key
  credentials from an external `keystore.properties` file that is never
  committed (location can be changed with `FELLOWSHIP_KEYSTORE_PROPERTIES`).
- This changelog.

### Changed
- `twa/` synced to the exact source that built the signed v1 AAB.
- `twa/build.gradle`: `jcenter()` repositories replaced with `mavenCentral()`.
- `twa/twa-manifest.json`: `signingKey.path` points to the upload keystore
  location (path only, no credentials).
- `.gitignore` files now cover build outputs, `.gradle/`, `local.properties`,
  keystores, `key.properties`/`keystore.properties`, `*.aab` and `*.apk`.

### Removed
- The unsigned convenience AAB `twa/dist/fellowship-faceoff-unsigned.aab` and
  `twa/dist/README.md` are no longer tracked. They were removed going forward
  only; git history was not rewritten.

[Unreleased]: https://github.com/LeeMcQ/fellowship-faceoff-play-release/compare/v1.0.1...HEAD
[1.0.1]: https://github.com/LeeMcQ/fellowship-faceoff-play-release/compare/v1.0.0...v1.0.1
[1.0.0]: https://github.com/LeeMcQ/fellowship-faceoff-play-release/releases/tag/v1.0.0
