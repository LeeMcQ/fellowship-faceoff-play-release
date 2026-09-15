# Dist artifacts (unsigned)

| File | Notes |
|------|--------|
| `fellowship-faceoff-unsigned.aab` | **Unsigned** Android App Bundle. For convenience / smoke checks only. |

## Important

- **New Google Play apps must upload a signed `.aab` (Android App Bundle).** An APK is not accepted for new app listings.
- This AAB is **unsigned**. You must sign it with your upload keystore before Play Console upload (or rebuild with Bubblewrap signing enabled).
- Do **not** commit keystores, passwords, or signed release artifacts that embed secrets.

## Sign before upload

From the `twa/` project (see `../PLAY_WRAP_README.md`):

```bash
# Create keystore once (do not commit it)
keytool -genkeypair -v \
  -keystore android.keystore \
  -alias upload \
  -keyalg RSA -keysize 2048 -validity 10000

export BUBBLEWRAP_KEYSTORE_PASSWORD='…'
export BUBBLEWRAP_KEY_PASSWORD='…'
bubblewrap build --skipPwaValidation
# Upload the signed .aab Play Console produces / Bubblewrap outputs
```

Or sign this existing AAB with `jarsigner` / Android Gradle signing after configuring the upload key — prefer a fresh Bubblewrap signed build so version codes and Play App Signing enrollment stay clean.
