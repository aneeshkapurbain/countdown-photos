# Forever with Sukriti — Countdown App

A romantic countdown app that runs to September 12, 2026, with photos that change every day and rotate through your library.

## Files
- `index.html` — the app
- `manifest.json` — PWA config
- `icon-192.png`, `icon-512.png` — placeholder icons (replace if you want)

---

## Step 1 — Host your photos (one-time, ~10 min)

You need a place where photos can be fetched by URL. **GitHub is free, permanent, and works perfectly.**

### Using GitHub (recommended)
1. Go to https://github.com and create a free account if you don't have one.
2. Click "+" → "New repository".
3. Name it `countdown-photos`, set to **Public**, click "Create repository".
4. Click "uploading an existing file".
5. Drag in your photos. **Rename them to `photo1.jpg`, `photo2.jpg`, ... `photo7.jpg`** (or more — add as many as you want).
6. Click "Commit changes".

Your photos are now at URLs like:
```
https://raw.githubusercontent.com/YOUR_USERNAME/countdown-photos/main/photo1.jpg
```

### Update the app
Open `index.html` and find the `PHOTO_URLS` array. Replace `YOUR_USERNAME` with your actual GitHub username. Add or remove URLs to match your photo count. The app cycles through them based on the day of the year, so the rotation repeats automatically after it runs through the list.

### Alternative: Google Drive
Doable but fiddly. Share each photo publicly, then convert the URL from `https://drive.google.com/file/d/FILE_ID/view` to `https://drive.google.com/uc?export=view&id=FILE_ID`. Some users report intermittent rate-limiting. GitHub is more reliable.

---

## Step 2 — Test the app
Open `index.html` in any browser. You should see the countdown, the photo rotating, and floating hearts. If photos show a heart placeholder, double-check your URLs.

---

## Step 3 — Package as APK

You have three good options, easiest first.

### Option A — PWABuilder (easiest, no install, ~5 minutes)
1. Host the app on the web first. Easiest: push the folder to a new GitHub repo and turn on GitHub Pages (Settings → Pages → Deploy from branch `main`). You'll get a URL like `https://YOUR_USERNAME.github.io/countdown-app/`.
2. Go to https://www.pwabuilder.com
3. Paste your URL, click "Start".
4. Click "Package for stores" → "Android" → "Generate Package".
5. Download the `.apk` file (it'll be inside the zip — use the "test" or "unsigned" APK for personal install).
6. Send the APK to Sukriti.

### Option B — Capacitor (if you have Node.js)
```bash
npm install -g @capacitor/cli
mkdir sukriti-app && cd sukriti-app
npm init -y
npm install @capacitor/core @capacitor/android
npx cap init "Forever with Sukriti" "com.you.sukriti" --web-dir=www
mkdir www
# Copy index.html, manifest.json, icon-*.png into www/
npx cap add android
npx cap sync
npx cap open android   # opens Android Studio → Build → Build APK
```

### Option C — Bubblewrap (Google's official tool)
```bash
npm install -g @bubblewrap/cli
bubblewrap init --manifest=https://YOUR_URL/manifest.json
bubblewrap build
```

---

## Step 4 — Send the APK to Sukriti
1. Send the `.apk` file via WhatsApp, email, or Google Drive.
2. On her phone, she'll need to **allow installation from unknown sources** for whichever app she's downloading from (Settings → Apps → Special access → Install unknown apps).
3. She taps the APK to install. Done.

---

## Customization ideas
- Edit `MESSAGES` array in `index.html` to add your own love notes.
- Change `WEDDING_DATE` if needed.
- Replace `icon-192.png` and `icon-512.png` with a custom icon (a photo of you two works beautifully).
- Add more photos — just append URLs to `PHOTO_URLS`. The cycle adapts automatically.

---

## How it works
- Countdown ticks every second to Sep 12, 2026 at 11:00 AM IST.
- Photo selected by `dayOfYear % PHOTO_URLS.length`, so it changes daily and loops through your library.
- Same logic picks a love note for the day.
- On Sep 12, the countdown is replaced with a wedding-day message.
- Photos load from your hosted URLs, so the user never has to upload anything.
