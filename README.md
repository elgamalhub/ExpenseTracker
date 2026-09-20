# Ledger — Expense Tracker (PWA)

A self-contained, installable Progressive Web App. No build step, no
dependencies to install — just static files.

## Files

```
ledger-pwa/
├── index.html      the app
├── manifest.json    app name, icons, colors — makes it installable
├── sw.js            service worker — caches the app for offline use
└── icons/
    ├── icon-192.png
    ├── icon-512.png
    └── icon-512-maskable.png
```

## Important: this needs to be served over HTTPS (or localhost)

Browsers only register service workers — and only show the "Install
app" / "Add to Home Screen" prompt — for pages loaded over **HTTPS**
or from **localhost**. Opening `index.html` directly from your file
system (`file://...`) will *not* enable installation or offline
support, though the tracker itself will still run.

## Fastest ways to host it for free

**Netlify Drop** (no account needed)
1. Go to https://app.netlify.com/drop
2. Drag the whole `ledger-pwa` folder onto the page
3. You'll get a live HTTPS URL in a few seconds

**GitHub Pages**
1. Create a new GitHub repository and push these files to it
2. In the repo, go to Settings → Pages
3. Set the source to your main branch, root folder
4. Your app will be live at `https://<your-username>.github.io/<repo-name>/`

**Vercel**
1. `npm i -g vercel` (if you have Node.js installed)
2. Run `vercel` inside the `ledger-pwa` folder and follow the prompts

**Testing locally first**
If you have Python installed, run this from inside the `ledger-pwa`
folder, then open `http://localhost:8000` in your browser:
```
python3 -m http.server 8000
```

## Installing it on your phone

Once it's hosted somewhere with HTTPS:

- **iPhone (Safari):** open the link → Share button → **Add to Home Screen**
- **Android (Chrome):** open the link → menu (⋮) → **Install app**

It will launch full-screen with its own icon, no browser address bar.

## What works offline

After the first visit (while online), the app shell — the page
itself, its icons, and the manifest — is cached by the service
worker, so re-opening it without a connection still loads the
interface. Your expenses and budgets are stored in the browser's
`localStorage` on that device, independent of network access, so
adding, editing, and deleting expenses works offline too. Nothing is
sent to a server — all data stays on the device.

## Customizing

- Colors and fonts live in the `<style>` block at the top of `index.html`.
- Categories are defined in the `CATEGORIES` array near the top of
  the `<script>` block — add, remove, or recolor them there.
- To change the app icon, replace the three PNGs in `icons/` (keep
  the same filenames and sizes) — 192×192, 512×512, and a 512×512
  "maskable" version with extra padding for Android's adaptive icon
  shapes.
