# Fellowship Face-Off — Google Play TWA wrap

Trusted Web Activity (TWA) scaffold wrapping the live PWA:

- **PWA:** https://leemcq.github.io/logosliving/
- **Package ID:** `com.leemcq.fellowshipfaceoff`
- **App / launcher name:** Fellowship Face-Off
- **Theme / background:** `#0F0F1A`
- **targetSdk / compileSdk:** **36** (Bubblewrap `@bubblewrap/cli` 1.25.0 template)

This directory was set up for non-interactive use: `twa-manifest.json` is pre-written so you do **not** need `bubblewrap init` prompts.

## Prerequisites (local machine)

1. **Node.js** ≥ 18  
2. **`@bubblewrap/cli`**
   ```bash
   npm i -g @bubblewrap/cli
   ```
3. **JDK 17** (Bubblewrap rejects other major versions)  
4. **Android SDK** with:
   - platforms `android-36`
   - build-tools `36.1.0` (Bubblewrap’s expected version)
   - cmdline-tools (`sdkmanager`)

Point Bubblewrap at JDK + SDK (once):

```bash
bubblewrap updateConfig \
  --jdkPath="/path/to/jdk-17" \
  --androidSdkPath="/path/to/Android/Sdk"

bubblewrap doctor
```

> If `doctor` says the SDK path is wrong, ensure the SDK root contains a top-level `bin/` (or legacy `tools/`) with `sdkmanager`. Modern layouts often need:
> `ln -s cmdline-tools/latest/bin "$ANDROID_HOME/bin"`

## 1) Init / regenerate Android project

`bubblewrap init` is interactive and will block CI/agents. Prefer:

```bash
cd /path/to/fellowship-faceoff-twa

# Regenerates the Android Gradle project from twa-manifest.json
bubblewrap update --skipVersionUpgrade
```

Optional first-time interactive path (human only):

```bash
bubblewrap init --manifest="https://leemcq.github.io/logosliving/manifest.json" \
  --directory="/path/to/fellowship-faceoff-twa"
```

Then overwrite/edit `twa-manifest.json` to match this scaffold (package id, colors, portrait, etc.) and re-run `bubblewrap update --skipVersionUpgrade`.

## 2) Create an upload keystore (do NOT commit secrets)

```bash
keytool -genkeypair -v \
  -keystore android.keystore \
  -alias upload \
  -keyalg RSA -keysize 2048 -validity 10000 \
  -storepass 'CHANGE_ME_STORE_PASSWORD' \
  -keypass 'CHANGE_ME_KEY_PASSWORD' \
  -dname "CN=Fellowship Face-Off, OU=Mobile, O=LeeMcQ, L=Unknown, ST=Unknown, C=US"
```

- Put **real** passwords only in a local password manager / CI secrets.
- Keep `android.keystore` **out of git** (see `.gitignore`).
- Placeholders only in docs: `CHANGE_ME_STORE_PASSWORD` / `CHANGE_ME_KEY_PASSWORD`.

Get the upload-key SHA-256 for Digital Asset Links:

```bash
keytool -list -v -keystore android.keystore -alias upload
# Copy the SHA256 fingerprint
```

## 3) Build a release AAB

Unsigned / skip signing (useful for a smoke build):

```bash
bubblewrap build --skipPwaValidation --skipSigning
```

Signed release (Play upload):

```bash
export BUBBLEWRAP_KEYSTORE_PASSWORD='CHANGE_ME_STORE_PASSWORD'
export BUBBLEWRAP_KEY_PASSWORD='CHANGE_ME_KEY_PASSWORD'
bubblewrap build --skipPwaValidation
# Outputs typically include app-release-bundle.aab
```

Upload the **`.aab`** to Play Console (App bundle).

## 4) Play App Signing

1. Create the Play app with application id `com.leemcq.fellowshipfaceoff`.
2. Upload your AAB; enroll in **Play App Signing** (default).
3. In Play Console → **Setup → App signing**, copy:
   - **App signing key certificate** SHA-256 (used by devices that install from Play)
   - Confirm your **upload key** SHA-256 matches the local keystore
4. Put **both** SHA-256 values into Digital Asset Links (next section).

## 5) Digital Asset Links (`assetlinks.json`)

Stub files in this repo:

| File | Purpose |
|------|---------|
| `assetlinks.json.example` | Documented stub with placeholders |
| `.well-known/assetlinks.json` | Same stub — copy into the **`LeeMcQ/leemcq.github.io`** repo (domain root) |

**Must be live at:**

`https://leemcq.github.io/.well-known/assetlinks.json`

Android only checks the domain root, so a copy under `/logosliving/.well-known/` does not count.

See `ASSETLINKS_GITHUB_PAGES.md` for the exact copy path and verification curls.

Replace:

- `UPLOAD_KEY_SHA256_FINGERPRINT_PLACEHOLDER` ← `keytool -list -v`
- `PLAY_APP_SIGNING_KEY_SHA256_FINGERPRINT_PLACEHOLDER` ← Play Console App signing

Statement relation used: `delegate_permission/common.handle_all_urls` for package `com.leemcq.fellowshipfaceoff`.

Statement List Generator / verification:

https://developers.google.com/digital-asset-links/tools/generator

## 6) Notifications (off)

Notifications are **off** in the Play build (since 1.0.1 / versionCode 2): `twa-manifest.json` and `app/build.gradle` have `enableNotifications: false`, and the generated `AndroidManifest.xml` no longer declares `POST_NOTIFICATIONS`, the notification small icon, or `NotificationPermissionRequestActivity`. The app does not use notification delegation.

- To turn them back on later, set `enableNotifications` to `true`, run `bubblewrap update`, bump versionCode, and update the Data safety form and privacy policy to match.
- With notifications on, the PWA must request permission in the web UI, and on Android 13+ (API 33+) the system notification permission applies.

## 7) Paid unlocks / billing (Play policy)

If the web game has **paid unlocks, IAP, or subscriptions**:

- **Either** enable Play Billing in the TWA and implement the [Digital Goods API / Play Billing](https://developer.chrome.com/docs/android/trusted-web-activity/receive-payments-play-billing/) path:
  ```json
  "features": { "playBilling": { "enabled": true } }
  ```
  then `bubblewrap update --skipVersionUpgrade`, and wire SKUs in Play Console + web.
- **Or** remove / gate paid unlock UI in the Play-distributed experience so it does not bypass Google Play’s billing requirements.

Do not ship a Play build that sells digital goods only through a web checkout that bypasses Play Billing when Play policy requires it.

## 8) Useful Bubblewrap commands

```bash
bubblewrap doctor
bubblewrap update --skipVersionUpgrade
bubblewrap build --skipPwaValidation --skipSigning
bubblewrap validate --url=https://leemcq.github.io/logosliving/
bubblewrap fingerprint add <SHA256>
bubblewrap fingerprint generateAssetLinks --output=./assetlinks.generated.json
```

## Icon note

`icon-512.png` in this folder is a **copy** of `/workspace/logosliving/icon-512.png` for local reference. The Android project uses `iconUrl` / `maskableIconUrl` from the live site during `update`/`build`.
