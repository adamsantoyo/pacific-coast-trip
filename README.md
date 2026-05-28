# Pacific Coast Trip

A single-file companion app for a 14-day Pacific Coast road trip
(Seattle → Long Beach → Seattle, Jul 31 – Aug 13, 2026). Built for two
audiences: the people on the road, and the family watching from afar.

## What it does

- Day-by-day itinerary with real dates and a "today" banner
- Sequential map navigation (Prev / Next / Overview) over baked driving
  routes
- Drive distance estimates per day (haversine over the polyline)
- Daily weather forecast from Open-Meteo (no API key required)
- Per-day photo strip + journal that sync live via Firebase (optional)
- Anonymous-auth gated editing — anyone can read, only the trip owner
  can write
- Installable PWA with offline support (cached map tiles, app shell)
- Family share view (`?view=family`) that hides editing controls

## 1. Local dev

Just open `road-trip-app.html` in a browser. No build step.

For service-worker / PWA testing you need to serve it over HTTP:

    python3 -m http.server 8000
    # then visit http://localhost:8000/road-trip-app.html

## 2. Firebase setup (optional — only needed for photos + journal)

The app fully works without Firebase; you simply won't see the photo
strip or journal sections.

1. Create a free Firebase project at https://console.firebase.google.com
2. In the project, **enable**:
   - **Authentication → Anonymous** sign-in
   - **Firestore Database** (start in production mode, rules go below)
   - **Storage** (start in production mode, rules go below)
3. In the project settings, copy the web-app config object.
4. Open `road-trip-app.html`, search for `TODO: replace with your project
   config`, and paste the values into the `firebaseConfig` object.
5. Deploy the security rules in `firestore.rules` to Firestore. For
   Storage, paste the commented-out block at the bottom of that file
   into the Storage rules editor.
6. Open the app, click **Sign in to edit**. The first sign-in creates
   your anonymous UID — copy it from the Firebase Authentication console
   and paste it into `firestore.rules` (and the Storage rules) in place
   of `OWNER_UID`, then redeploy the rules.

After that, journals and photos save in real time, and family viewers
see updates live.

## 3. Icons

`icon.svg` is the default install icon (works on most browsers). For
the highest-fidelity install experience on iOS / Android, drop in your
own `icon-192.png` and `icon-512.png` next to the HTML file. The
manifest already references all three.

## 4. Deploy to GitHub Pages

1. Create a new repo, push these files to `main`.
2. In the repo settings → **Pages**, set the source to `main` / root.
3. Wait ~1 minute. Your app is at
   `https://<your-user>.github.io/<repo>/road-trip-app.html`.
4. On iPhone: open the URL in Safari → Share → **Add to Home Screen**.

## 5. Family share link

Append `?view=family` to the URL:

    https://<host>/road-trip-app.html?view=family

This view:
- Hides the journal textarea — shows the journal text read-only
- Hides the photo upload button — photos are still visible
- Hides the sign-in button and the booking checklist sidebar
- Retitles the header to "Following Adam & Cori on the Coast"
  (swap "Cori" for your real travel partner's name in
  `road-trip-app.html`)

The "Share with family" button in the header copies this link to your
clipboard.

## 6. File map

- `road-trip-app.html` — the entire app
- `manifest.json`, `icon.svg`, `sw.js` — PWA bits
- `firestore.rules` — copy into Firebase console
- `README.md` — this file
