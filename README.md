# KuwartaFlow

A freeform expense tracker. All data is stored **locally on the device** (the browser's/phone
localStorage). No server, no account, no tracking.

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
