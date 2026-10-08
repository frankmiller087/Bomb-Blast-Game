# Bomb Blast — Android APK

Offline bomb-dropping maze battler. The game itself is a single HTML5 file in `www/`;
`android/` is a thin WebView wrapper that packages it as an installable APK.

## Project layout

- `www/` — the game (source of truth). Host this folder to play in a browser / install as PWA.
  - `bomb-blast.html`, `manifest.json`, `sw.js`, `icon.webp`
- `android/` — native wrapper (Java + WebView, no frameworks).
  - A Gradle `copyWebAssets` task copies `www/` into `src/main/assets/www` on every build,
    so the APK always ships the latest game.

## Building the APK (GitHub Actions)

1. Create a **new private repo** on GitHub and push this folder to `main`.
2. In the repo on github.com, go to **Actions → "set up a workflow yourself"**
   (or **Add file → Create new file** at `.github/workflows/build-apk.yml`)
   and paste the contents of `build-apk.yml` from this folder, then commit.
3. The `push` triggers the workflow automatically. When it finishes, download
   **bomb-blast-apk** from the run's **Artifacts** section — that's your APK.
4. On your phone: allow "Install unknown apps" for your browser/files app once,
   open the APK, install, play. Fully offline.

To rebuild after changing the game: edit `www/`, commit, push — a fresh APK
is built automatically.
