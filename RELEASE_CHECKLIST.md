# Day-of submit checklist — Google Play (printable)

App: **Fellowship Face-Off** · Package: **`com.leemcq.fellowshipfaceoff`**  
PWA: https://leemcq.github.io/logosliving/  
**Not** Apple App Store.

Print or tick digitally. Details and file links live in `README.md`.

---

## Before you open Play Console

- [ ] Upload keystore created locally (not in git)
- [ ] Keystore passwords saved in a password manager
- [ ] Upload-key SHA-256 copied (`keytool -list -v`)
- [ ] Signed **`.aab`** built locally (never committed)
- [ ] Privacy policy live: https://leemcq.github.io/logosliving/privacy.html (contact: Mcquir4l@gmail.com)
- [ ] Listing copy ready (`LISTING_COPY.md`)
- [ ] Feature graphic + icon ready (`store-assets/`)
- [ ] ≥2 phone screenshots captured (`store-assets/SCREENSHOTS_BRIEF.md`)
- [ ] Payments decision documented (`PAYMENTS_AND_POLICY.md`)

## Play Console — create & sign

- [ ] Create app with package **`com.leemcq.fellowshipfaceoff`** (immutable)
- [ ] Upload signed AAB
- [ ] Enroll / confirm **Play App Signing**
- [ ] Copy **App signing key** SHA-256 from Setup → App signing

## Digital Asset Links

- [ ] Both SHA-256 fingerprints in `digital-asset-links/assetlinks.json`
- [ ] Published at the domain root via `LeeMcQ/leemcq.github.io`: `.well-known/assetlinks.json`
- [ ] Live URL returns 200:  
      `https://leemcq.github.io/.well-known/assetlinks.json`
- [ ] TWA opens without browser chrome (after install from internal/closed track)

## Store listing & policy forms

- [ ] Title / short / full / what’s new pasted from `LISTING_COPY.md`
- [ ] Graphics uploaded (feature + icon + screenshots)
- [ ] Privacy policy URL set to https://leemcq.github.io/logosliving/privacy.html
- [ ] Data safety form completed to match the shipped build (`PAYMENTS_AND_POLICY.md`)
- [ ] Content rating questionnaire completed
- [ ] Target audience / news apps / COVID / etc. declarations completed as prompted
- [ ] App content → Ads: "No, my app does not contain ads"
- [ ] Financial features / Billing declared if used

## Testing → production

- [ ] Closed testing track created; testers invited
- [ ] Install from Play (not sideload) and smoke-test modes + offline
- [ ] Asset Links verified on a Play-installed build
- [ ] Production access / review applied if required for new accounts
- [ ] Production rollout started (staged % recommended)

## After go-live

- [ ] Spot-check listing on a real device
- [ ] Monitor Play Console crashes / ANRs
- [ ] Keep keystore backed up offline forever

---

**Reminder:** New Play apps need a signed **`.aab`**. APK is not for new app uploads. No AAB is committed to this repo; build and sign locally, and record the versionCode and SHA-256 in `CHANGELOG.md` and the release tag.
