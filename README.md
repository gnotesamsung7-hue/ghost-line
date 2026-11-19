# Ghost Line — Android build

This folder is a ready-to-push Capacitor project that wraps the Ghost Line
web app (`www/index.html`) as a native Android app. It can't be built here
— this sandbox has no Android SDK and no access to your GitHub — so it's
built by **GitHub Actions**, the same way your other APK projects (Bible
Journey, Camera Radar, etc.) get built.

## One-time setup (5 minutes)

1. On github.com, create a new **empty** repository, e.g. `ghost-line`
   (don't add a README/license there — this zip already has one).
2. On your phone or any machine with a browser, open the repo's **Add file
   → Upload files** page and drag in everything from this zip, keeping the
   folder structure (`www/`, `android/`, `.github/`, `package.json`,
   `capacitor.config.ts`, etc.) — or, if you have `git` available anywhere,
   the usual:
   ```
   git init
   git remote add origin https://github.com/gnotesamsung7-hue/ghost-line.git
   git add .
   git commit -m "Ghost Line Android app"
   git branch -M main
   git push -u origin main
   ```
3. That push triggers `.github/workflows/build-apk.yml` automatically.

## Getting the APK onto your phone easily (QR codes)

The app has a **QR** button in its top bar. It shows two QR codes:
- one for the web version (works right now — links to the Claude artifact),
- one for the Android APK, pointing at
  `https://github.com/<owner>/<repo>/releases/latest/download/app-debug.apk`
  — GitHub's "latest release" link, which always resolves to your most
  recent build without you needing to update anything each time you push.

If you name your repo something other than `gnotesamsung7-hue/ghost-line`,
edit the "Repo" field in that same QR screen — the QR updates live and is
remembered on that device. Scan either QR with another phone to open the
link directly, or tap "Share" to send it some other way.

## Getting the APK

- Go to the repo's **Actions** tab → the "Build Ghost Line APK" run →
  under **Artifacts**, download `ghost-line-debug-apk` (a zip containing
  `app-debug.apk`).
- Or, a few minutes after the first push to `main`, check the repo's
  **Releases** tab — the workflow also attaches the APK to an auto-created
  release, which is an easier link to open directly on your phone.
- On your phone: download the APK, tap it, allow "install from unknown
  sources" when Android asks (only needed once), and it installs like any
  app.

## What's in here

- `www/index.html` — the app itself (same code as the Claude artifact
  version, so edits made in either place can be copied to the other).
- `android/` — the native Android project Capacitor generated.
- `.github/workflows/build-apk.yml` — builds a **debug** APK on every push
  to `main`/`master`, or on demand from the Actions tab ("Run workflow").
- `capacitor.config.ts` — app id `com.markdave.ghostline`, app name
  "Ghost Line".

This is a debug build (unsigned), which is fine for your own phone. If you
ever want to publish it to the Play Store, that needs a signed release
build with your own keystore — a separate step, ask if you want that set up.

## Updating the app later

1. Edit `www/index.html` (or copy over a new version from the Claude
   artifact).
2. Commit and push — the Action rebuilds the APK automatically.
3. Re-download from Actions/Releases and reinstall on your phone (same
   package id, so it updates in place; your data stays in `localStorage`
   either way since it's device-local, not cloud-synced).

## Permissions this app asks for

- **Location** (optional, only when you tap "Use my location") — used to
  show distance to a spot and sort by nearest. The app works fully without
  granting it.
- **Storage/Internet** — standard Capacitor/WebView plumbing (fonts,
  export/share).

No data leaves your phone: everything is stored locally, there's no
backend and no account.
