# Digital Asset Links — GitHub Pages publish path

For the TWA to verify ownership of the PWA host, publish this file so it is served at:

**https://leemcq.github.io/.well-known/assetlinks.json**

Android only checks the domain root, so this belongs in the `LeeMcQ/leemcq.github.io` user Pages site, not in `logosliving` (a file under `/logosliving/.well-known/` is ignored).

## What to add in the `leemcq.github.io` repo

Copy the placeholder file from this scaffold:

- Source (in this TWA project): `.well-known/assetlinks.json`
- Destination (in `LeeMcQ/leemcq.github.io`): `.well-known/assetlinks.json`

After commit + push to that repo's Pages branch, verify:

```bash
curl -sI https://leemcq.github.io/.well-known/assetlinks.json
# Expect: HTTP/2 200 and content-type application/json (or text/plain is often OK)
curl -s https://leemcq.github.io/.well-known/assetlinks.json
```

## Filling fingerprints (required before Play release)

Replace the two placeholders with real SHA-256 fingerprints (colon-separated hex, uppercase as emitted by keytool / Play Console).

### 1) Upload key (local keystore)

```bash
keytool -list -v -keystore android.keystore -alias upload
# Copy the SHA256 line (e.g. AB:CD:...) into UPLOAD_KEY_SHA256_FINGERPRINT_PLACEHOLDER
```

### 2) Play App Signing key (Google Play Console)

Play Console → your app → **Setup → App signing** → **App signing key certificate** → SHA-256 certificate fingerprint.

Put that value in `PLAY_APP_SIGNING_KEY_SHA256_FINGERPRINT_PLACEHOLDER`.

Include **both** fingerprints so verification works for locally signed builds and Play-distributed builds.
