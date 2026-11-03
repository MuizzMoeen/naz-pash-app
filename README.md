# Naz & Pash's Cozy Home — mobile app

A cozy cat-care game starring Nazbanoo and Pashmak. The whole game lives in `www/index.html`. Capacitor wraps it into native iOS and Android apps.

## How builds work (no Mac needed)
Every push to `main` runs two GitHub Actions workflows:

| Workflow | Always produces | Also, once secrets are added |
|---|---|---|
| **Android build** (`.github/workflows/android.yml`) | `naz-pash-test-apk`: an APK you can install on any Android phone | `naz-pash-play-bundle`: a signed `.aab` for Google Play |
| **iOS build** (`.github/workflows/ios.yml`) | A simulator build, to check that the app compiles | A signed build uploaded straight to **TestFlight** |

Download the APK and AAB from the workflow run page, under **Artifacts**.

## Secrets (repo → Settings → Secrets and variables → Actions)
**iOS (TestFlight):**
- `APPLE_TEAM_ID`: 10-character Team ID (developer.apple.com → Membership)
- `ASC_KEY_ID`, `ASC_ISSUER_ID`: from App Store Connect → Users and Access → Integrations → App Store Connect API (create a key with **App Manager** access)
- `ASC_KEY_P8_BASE64`: the downloaded `AuthKey_XXXX.p8` file, base64-encoded

You also need to create the app once in App Store Connect with bundle ID `com.nazandpash.cozyhome`.

**Android (Google Play):**
- `ANDROID_KEYSTORE_BASE64`, `ANDROID_KEYSTORE_PASSWORD`, `ANDROID_KEY_ALIAS`, `ANDROID_KEY_PASSWORD`: your upload key. Keep a safe copy of the keystore file and passwords forever.

## Updating the game
Replace `www/index.html` with the new version and push. `npx cap sync` runs in CI.

## IDs
- Bundle / application ID: `com.nazandpash.cozyhome`
- App name on the home screen: **Naz & Pash**
- Font: Fredoka (SIL Open Font License), embedded
