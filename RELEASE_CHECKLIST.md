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
- [ ] Signed **`.aab`** built (not the unsigned convenience file alone)
- [ ] Privacy policy: contact email filled in `privacy/privacy-policy.html`
- [ ] Privacy policy hosted on public HTTPS
- [ ] Listing copy ready (`LISTING_COPY.md`)
- [ ] Feature graphic + icon ready (`store-assets/`)
- [ ] ≥2 phone screenshots captured (`store-assets/SCREENSHOTS_BRIEF.md`)
- [ ] Payments/ads decision documented (`PAYMENTS_AND_POLICY.md`)

## Play Console — create & sign

- [ ] Create app with package **`com.leemcq.fellowshipfaceoff`** (immutable)
- [ ] Upload signed AAB
- [ ] Enroll / confirm **Play App Signing**
- [ ] Copy **App signing key** SHA-256 from Setup → App signing

## Digital Asset Links

- [ ] Both SHA-256 fingerprints in `digital-asset-links/assetlinks.json`
- [ ] Published to logosliving: `.well-known/assetlinks.json`
- [ ] Live URL returns 200:  
      `https://leemcq.github.io/logosliving/.well-known/assetlinks.json`
- [ ] TWA opens without browser chrome (after install from internal/closed track)

## Store listing & policy forms

- [ ] Title / short / full / what’s new pasted from `LISTING_COPY.md`
- [ ] Graphics uploaded (feature + icon + screenshots)
- [ ] Privacy policy URL set
- [ ] Data safety form completed (match ads/Billing reality)
- [ ] Content rating questionnaire completed
- [ ] Target audience / news apps / COVID / etc. declarations completed as prompted
- [ ] Ads declaration matches build
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

**Reminder:** New Play apps need a signed **`.aab`**. APK is not for new app uploads. Unsigned AAB in `twa/dist/` is convenience only — see `twa/dist/README.md`.
