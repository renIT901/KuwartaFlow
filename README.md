# Spendings — deploy to GitHub Pages

A freeform expense tracker. All data is stored **locally on the device** (the browser's
localStorage). No server, no account, no tracking.

## Files in this folder
- `index.html` — the app (entry point; must keep this name)
- `manifest.webmanifest` — makes it installable, sets the icon and full-screen mode
- `sw.js` — service worker; enables offline use and installability
- `icon-192.png`, `icon-512.png`, `apple-touch-icon.png` — home-screen icons
- `.nojekyll` — tells GitHub Pages to serve the files untouched

All paths inside the app are **relative**, so it works whether Pages serves it at
`username.github.io/` or at `username.github.io/repo-name/`.

## Deploy (GitHub Pages)
1. Create a new GitHub repository (public). Any name works, e.g. `spendings`.
2. Upload **everything in this folder** to the repo root — including the dot-file
   `.nojekyll`. (On github.com: "Add file" → "Upload files" → drag them in → Commit.)
3. Repo → **Settings** → **Pages**.
4. Under **Build and deployment**, set **Source = Deploy from a branch**,
   **Branch = main**, **Folder = / (root)**. Save.
5. Wait ~1 minute, then refresh the Pages settings page to get your live URL:
   `https://<your-username>.github.io/<repo-name>/`

### Updating later
Re-upload the changed files. If a change to `index.html` doesn't appear, bump the
cache name in `sw.js` (`spendings-v1` → `spendings-v2`) so the service worker refreshes.

## Install on iPhone
1. Open the Pages URL in **Safari** (must be Safari for install to work).
2. Tap **Share** → scroll down → **Add to Home Screen** → **Add**.
3. Launch it from the new icon. It opens full-screen and works offline.

Installing to the Home Screen is what makes the data durable — Safari's automatic
data-cleanup timer does not apply to installed Home Screen apps.

## Back up your data
Data lives only on that one device. Use **History → Export → Backup** to copy a JSON
snapshot somewhere safe (Notes, email, a file). To restore — on a new phone or after a
reset — use **History → Import backup** and paste it back.
