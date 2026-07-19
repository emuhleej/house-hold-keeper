# Deploy With GitHub Pages + Firebase

GitHub Pages hosts the household hub. Firebase Firestore stores the shared household pages, vendor details, contact info, service history, home maintenance calendar, and vehicle records. Firebase Storage stores uploaded documents.

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

## 5. Create Firebase Storage

1. In Firebase, open `Storage`.
2. Click `Get started`.
3. Start in production mode.
4. Use the same location as Firestore when possible.

## 6. Firestore Rules

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

## 7. Storage Rules

Use these rules for uploaded household documents:

```js
rules_version = '2';

service firebase.storage {
  match /b/{bucket}/o {
    match /household-documents/{allPaths=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

Anyone with the page link can anonymously read and edit this household data and documents, so keep the link private.

## 8. Upload To GitHub

Upload the contents of this folder, not the folder itself:

- `index.html`
- `firebase-config.js`
- `README.md`
- `DEPLOY.md`
- `.nojekyll`

## 9. Turn On GitHub Pages

In the GitHub repo:

1. Open `Settings`.
2. Open `Pages`.
3. Under `Build and deployment`, choose `Deploy from a branch`.
4. Choose branch `main`.
5. Choose folder `/root`.
6. Click `Save`.

GitHub will give you a link like:

`https://your-username.github.io/household-information-hub/`

## 10. Use It In Notion

1. Open Notion.
2. Type `/embed`.
3. Paste the GitHub Pages link.
4. Choose `Embed`.
