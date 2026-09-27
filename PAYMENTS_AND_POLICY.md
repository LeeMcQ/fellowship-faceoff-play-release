# Payments, ads & Data safety — Play notes

This document is for **Google Play** policy alignment for Fellowship Face-Off (`com.leemcq.fellowshipfaceoff`). It is not legal advice; re-check current Play policy before submit.

## Play Billing vs web-only unlocks

The PWA may offer Full Edition / denomination unlocks via codes or web flows.

| Approach | When to use | Action |
|----------|-------------|--------|
| **Play Billing** | Digital goods sold *inside* the Play-distributed app | Enable Bubblewrap `features.playBilling`, implement Digital Goods API / Play Billing, declare products in Play Console |
| **Web-only unlocks** | Unlocks happen only on the open web, outside Play distribution requirements | Do **not** surface a Play-bypass checkout that sells the same digital goods inside the Play app if policy requires Play Billing |
| **No paid digital goods in Play build** | Simplest for first submit | Hide or gate paid unlock UI in the TWA experience until Billing is wired |

See `twa/PLAY_WRAP_README.md` §7 and Chrome’s TWA Play Billing docs.

**Do not** ask users to send card numbers over WhatsApp. Play purchases are processed by Google.

## Ads

- The **free web** experience may show NitroPay / related ads when enabled.
- For the **Play build**, decide before Data safety:
  - **No ads in Play TWA** → declare accordingly; consider disabling ad scripts when running inside TWA if feasible.
  - **Ads in Play TWA** → declare advertising ID / ad partner data collection in Data safety and update the privacy policy contact + ads section.

Paid / Full Edition users should not see ads when unlock is active (as described in `privacy/privacy-policy.html`).

## Privacy policy (required)

1. Edit `privacy/privacy-policy.html` — replace **`[ADD YOUR CONTACT EMAIL]`** before hosting.
2. Host at a stable **HTTPS** URL (e.g. GitHub Pages under logosliving or a dedicated path).
3. Paste that URL into Play Console → App content → Privacy policy.

## Data safety form (Play Console checklist)

Declare only what the shipped Play build actually does. Typical starting points for this TWA:

| Topic | Likely answer for a minimal offline-first build | Notes |
|-------|--------------------------------------------------|-------|
| Collects user accounts? | No | Unless you add login |
| Location? | No | |
| Personal info (name, email)? | Only if user shares via OS share / WhatsApp to you | You receive what they send; not automatic collection |
| App activity / device IDs for ads? | Yes only if ads ship in Play build | Match ads decision above |
| On-device game prefs / unlock flags | Stored on device (local storage) | Usually “not collected” by developer servers if never uploaded |
| Data encrypted in transit? | Yes (HTTPS) | |
| Users can request deletion? | Yes for messages they sent you | Via contact email in privacy policy |
| Children | Not directed primarily at under-13 | Supervise younger players; see privacy §7 |

Re-verify after any analytics, crash reporting, or Billing SDK is added.

## Notifications

Notifications are **off** in the Play build since 1.0.1 (versionCode 2): `twa-manifest.json` has `enableNotifications: false` and the app does not request `POST_NOTIFICATIONS`. If you turn them back on, rebuild and update the Data safety form and privacy policy.

## Content ratings / target audience

Complete Play’s content rating questionnaire honestly (party / word game, religious themes, no gambling). Target audience should match church/family groups — not designed as a kids-primary app under 13.
