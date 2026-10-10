# Headcount — Attendance Tracker

A small, private attendance tracker built for iPhone and other devices.

## What it does

- **+1 / −1** for quick entry and exit counts.
- **Add custom / Remove custom** for groups of any size up to 999,999.
- **Total attendance** always shows how many people are currently counted inside.
- **Total entered / Total exited** show movements over the current session.
- **Undo**, **Reset** (with confirmation), and **Export CSV** of adjustments.
- Saves all changes to this browser's local storage, including the undo history. Doesn't need an account or server backend. No automatic cloud sync or multi-device collaboration.

The count cannot go below zero. The data is stored locally **per browser / installed app**. Clearing website data, removing the installed app, or switching browsers may erase or separate saved counts. Export attendance logs for backups.

## Put it on your iPhone home screen

The most reliable option is to host the files on any HTTPS static website. This is a **web app**, not a signed native Apple Shortcut. Host the contents of this folder together: `index.html`, the manifest, service worker, and icons.

### Option A — GitHub Pages (free)

1. Create a GitHub repository, e.g. `headcount`.
2. Upload all the files in this folder to the repository's root. (If uploading by zip, **unzip it first**.)
3. Under the repository's **Settings → Pages**, choose **Deploy from a branch**, select `main` and `/ (root)`, and save.
4. Open the resulting `https://YOUR-USERNAME.github.io/headcount/` address in **Safari on your iPhone**.
5. Tap **Share → Add to Home Screen → Add**. On newer iOS versions, choose **Open as Web App** if prompted.
6. Launch **Headcount** from your Home Screen. After initial loading, the installed web app can run offline.

### Option B — Other static hosting

Upload these files to Netlify, Cloudflare Pages, or another HTTPS static file host. Open that link in Safari and choose **Share → Add to Home Screen**.

## Launch through Apple Shortcuts (optional)

If you also want a Shortcut on your Home Screen:

1. Open **Shortcuts** → **+** and name it `Headcount`.
2. Add the **URL** action and enter your hosted app's HTTPS URL.
3. Add **Open URLs** below it.
4. In Shortcut details, choose **Add to Home Screen**.

This Shortcut launches the web app via Safari. For an entirely native menu-based Shortcut that stores the headcount in iCloud Drive and does not require hosting, see `APPLE_SHORTCUTS_NATIVE.md`.

## Test on a computer

Open `index.html` in a modern desktop browser. The controls work even without hosting, though the installable/offline app features require HTTPS hosting.

## Data and backups

Tap **Export** for a time-stamped CSV log of the current session. The exported file is a snapshot of count changes, not an automatic backup of the in-app state. Export before resetting if you want to preserve a record. Reset clears current session logs; **Undo** immediately restores the prior state.
