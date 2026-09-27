# Changelog

All notable changes to the Fellowship Face-Off Android wrapper (TWA,
package `com.leemcq.fellowshipfaceoff`) are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project uses [Semantic Versioning](https://semver.org/spec/v2.0.0.html)
for wrapper releases. Android `versionCode` goes up by 1 for every AAB uploaded
to Google Play. The web app (`LeeMcQ/logosliving`) ships separately and is
tagged `web-YYYY.MM.DD`.

## [Unreleased]

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

[Unreleased]: https://github.com/LeeMcQ/fellowship-faceoff-play-release/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/LeeMcQ/fellowship-faceoff-play-release/releases/tag/v1.0.0
