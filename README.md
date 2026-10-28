# Batch-Prep Macro Scaler: installable app

This folder is the complete app. It's a Progressive Web App (PWA): one set of files that runs in any browser and installs to the home screen on iPhone and Android, with its own icon, full-screen window, and offline support.

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole app (calculator, styles, logic) |
| `manifest.webmanifest` | App name, icon, colors, and full-screen mode for installs |
| `sw.js` | Service worker that caches the app so it works offline |
| `icons/` | Home-screen icons for Android, iOS, and browsers |

## 1. Put it online (free, about 5 minutes)

A PWA must be served over HTTPS. Any static host works. Two easy options:

**Netlify Drop (no account setup beyond sign-in)**
1. Go to app.netlify.com/drop.
2. Drag this whole folder onto the page.
3. You get a URL like `https://something.netlify.app`. Rename it in Site settings, or attach your own domain later.

**GitHub Pages**
1. Create a repository and upload these files to it.
2. Settings → Pages → Deploy from branch → `main`, root folder.
3. The app goes live at `https://<username>.github.io/<repo>/`.

To test on your own computer first: run `python3 -m http.server 8000` in this folder and open `http://localhost:8000`. Service workers are allowed on localhost.

## 2. Install it on a phone

**iPhone / iPad**: open the URL in Safari → Share button → **Add to Home Screen**.

**Android**: open the URL in Chrome → menu (⋮) → **Install app** (Chrome often shows an install banner automatically).

**Desktop**: Chrome and Edge show an install icon in the address bar.

Once installed it opens without browser bars and works with no signal after the first load.

## 3. Shipping updates

Edit `index.html`, then open `sw.js` and change `VERSION` (for example `macro-scaler-v2`). Redeploy. Installed copies pick up the new version the next time they're opened with a connection. If you skip the version bump, phones keep serving the old cached copy.

## 4. Optional: App Store and Google Play

The same files can be wrapped as native apps with Capacitor when you want store listings:

```bash
npm init -y
npm install @capacitor/core @capacitor/cli @capacitor/ios @capacitor/android
npx cap init "Macro Scaler" com.yourname.macroscaler --web-dir .
npx cap add android
npx cap add ios        # needs a Mac with Xcode
npx cap open android   # build and sign in Android Studio
```

Requirements: a Google Play developer account (one-time fee) and an Apple Developer Program membership (annual fee). Building for iOS needs a Mac. Apple may reject apps that are a thin wrapper around a website, so a store version should offer something the web version doesn't (saved templates, for example).

## 5. Charging for it

- **Web/PWA route:** sell access through Gumroad, Lemon Squeezy, or Stripe. The simplest version is a paid page that reveals the app URL, or bundling the URL with your meal-prep guide. Stronger protection (license keys, accounts) needs a small backend.
- **Store route:** charge an upfront price or use in-app purchase. The store takes a cut of each sale.
