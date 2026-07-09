# Household Information Hub

Static GitHub Pages friendly household information tracker for Notion embeds.

It can run by itself in one browser, or sync shared service details through Firebase Firestore after you fill in `firebase-config.js`.

## Files

- `index.html` contains the full app.
- `firebase-config.js` is where the Firebase web app config goes.
- `DEPLOY.md` has the no-download GitHub Pages + Firebase setup steps.
- `.nojekyll` helps GitHub Pages serve the folder as plain static files.

## Notion Embed

1. Publish this folder with GitHub Pages.
2. Copy the public URL for the page.
3. In Notion, type `/embed`.
4. Paste the URL.

## Notes

Without Firebase, entries and uploaded documents are saved in the browser that opens the app.

With Firebase configured, household page details sync through Firestore. Uploaded documents still stay saved in the browser where they were added.
