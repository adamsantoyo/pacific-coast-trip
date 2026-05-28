# Pacific Coast Trip

A companion app for a 14-day Pacific Coast road trip (Seattle → Long Beach → Seattle, Jul 31–Aug 13, 2026).

**Live:** https://adamsantoyo.github.io/pacific-coast-trip/road-trip-app.html

**Family view:** https://adamsantoyo.github.io/pacific-coast-trip/road-trip-app.html?view=family

## Firebase setup (optional)

To enable photos + journal:

1. Create a free Firebase project at https://console.firebase.google.com
2. Enable: Anonymous auth, Firestore Database, Storage (production mode)
3. In `road-trip-app.html`, find `TODO: replace with your project config` and paste your Firebase config
4. Deploy `firestore.rules` to your Firestore and Storage
5. Sign in once, copy your UID from Firebase Console, update `OWNER_UID` in `firestore.rules`, redeploy
