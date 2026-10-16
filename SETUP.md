# Home log – setup

A shared grocery list + to-do PWA. Static files only; live sync through Firebase Firestore (free Spark plan).
Share a list with the 8-character code or the invite link. Works offline.

## 1. Host the files
Put these files in your own GitHub repo and turn on Settings → Pages (branch `main`, root). Any static host works.

## 2. Firebase
1. console.firebase.google.com → Add project (Analytics not needed).
2. Build → Firestore Database → Create database (production mode, pick a nearby region).
3. Firestore → Rules → paste and publish:
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /lists/{listId}/{sub}/{id} {
      allow read, write: if true;
    }
  }
}
```
4. Project settings → Your apps → Web (`</>`) → register → copy the `firebaseConfig` values into `firebase-config.js`.

Rules are open on purpose: the unguessable list code is what keeps a list private. Firebase will warn about this; the web config values are not secrets.

## 3. Use it
Open your Pages URL, create a list, share the code or invite link, then install to the home screen
(Android: Chrome menu → Install app. iPhone: Safari Share → Add to Home Screen).

Data layout: `lists/{code}/items`, `catalog`, `cats`, `todos`.
