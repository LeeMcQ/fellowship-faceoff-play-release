# Digital Asset Links for Fellowship Face-Off TWA

Publish `assetlinks.json` so Chrome / Android can verify that the Play app
`com.leemcq.fellowshipfaceoff` is allowed to open the PWA in Trusted Web Activity mode (chrome-less).

## Live URL (required)

`https://leemcq.github.io/logosliving/.well-known/assetlinks.json`

That path lives in the **logosliving** GitHub Pages site (`LeeMcQ/logosliving`), **not** in this release repo.

## Steps

1. Create your upload keystore and copy its SHA-256 fingerprint:
   ```bash
   keytool -list -v -keystore android.keystore -alias upload
   ```
2. After first AAB upload, open Play Console → **Setup → App signing** and copy the **App signing key certificate** SHA-256.
3. Edit `assetlinks.json` in this folder: replace both placeholders with the real fingerprints (colon-separated hex).
4. Copy the filled file into the logosliving repo as:
   ```
   .well-known/assetlinks.json
   ```
5. Commit, push, wait for Pages, then verify:
   ```bash
   curl -sI https://leemcq.github.io/logosliving/.well-known/assetlinks.json
   curl -s https://leemcq.github.io/logosliving/.well-known/assetlinks.json
   ```
6. Optional: [Statement List Generator](https://developers.google.com/digital-asset-links/tools/generator)

## Package name

`com.leemcq.fellowshipfaceoff` — immutable once used on Play. Change only if you intentionally create a different app.

Also see `../twa/ASSETLINKS_GITHUB_PAGES.md` and `../twa/assetlinks.json.example`.
