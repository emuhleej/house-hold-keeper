# Deploy With GitHub Pages + Firebase

GitHub Pages hosts the household hub. Firebase Firestore stores the shared household details, and Firebase Storage (optional but recommended) syncs uploaded documents across devices.

If you already deployed an earlier version: just replace `index.html` in the repo and do step 6 below to turn on document sync. Existing data migrates automatically the first time each device opens the new version.

## 1. Create Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/).
2. Click `Add project`.
3. Name it something like `Household Information Hub`.
4. Google Analytics is optional.

## 2. Add A Web App

1. In Firebase, open `Project settings`.
2. Under `Your apps`, click the web icon `</>`.
3. Register the app.
4. Copy the Firebase config object.
5. Paste those values into `firebase-config.js`.

## 3. Turn On Anonymous Auth

1. In Firebase, open `Authentication`.
2. Click `Get started`.
3. Open `Sign-in method`.
4. Enable `Anonymous`.

## 4. Create Firestore Database

1. In Firebase, open `Firestore Database`.
2. Click `Create database`.
3. Start in production mode.
4. Choose a location.

## 5. Firestore Rules

For a simple household-only setup, use anonymous auth rules:

```js
rules_version = '2';

service cloud.firestore {
  match /databases/{database}/documents {
    match /households/home {
      allow read, write: if request.auth != null;
    }
  }
}
```

Anyone with the page link can anonymously read and edit this one household document, so keep the link private. For extra protection, set a PIN inside the app (the `PIN` button) - it locks the page on every synced device.

## 6. Turn On Firebase Storage (Document Sync)

This step makes uploaded documents appear on every device instead of only the one where they were added.

1. In Firebase, open `Storage` in the left menu.
2. Click `Get started` and accept the defaults (production mode, same location as Firestore).
3. Open the `Rules` tab and replace the rules with:

```js
rules_version = '2';

service firebase.storage {
  match /b/{bucket}/o {
    match /households/home/{allPaths=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

4. Click `Publish`.

That's it - no code changes needed. The app detects Storage automatically. If Storage is not set up, documents quietly fall back to browser-only storage and everything else still works.

Note: the Firebase free (Spark) plan includes 5 GB of Storage, which is plenty for household paperwork. If the Console asks you to upgrade to Blaze to enable Storage, you can add a budget alert of $0-1 for peace of mind - normal household use should stay within the free allowance.

## 7. Upload To GitHub

Upload the contents of this folder, not the folder itself:

- `index.html`
- `firebase-config.js`
- `README.md`
- `DEPLOY.md`
- `.nojekyll`

## 8. Turn On GitHub Pages

In the GitHub repo:

1. Open `Settings`.
2. Open `Pages`.
3. Under `Build and deployment`, choose `Deploy from a branch`.
4. Choose branch `main`.
5. Choose folder `/root`.
6. Click `Save`.

GitHub will give you a link like:

`https://your-username.github.io/household-information-hub/`

## 9. Use It In Notion

1. Open Notion.
2. Type `/embed`.
3. Paste the GitHub Pages link.
4. Choose `Embed`.

## Backups

Use `Export backup` in the app now and then. It downloads a single JSON file containing every page, the full service history, and document data, and `Import backup` restores it anywhere.
