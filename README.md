# Household Information Hub

Static GitHub Pages friendly household tracker for Notion embeds.

Each household page is named by its category (HVAC, Plumbing, Insurance...) and holds a collapsible contact card, page-level documents, and a full service history grouped by date. Every service entry has its own date, note, and attached documents.

It runs by itself in one browser, or syncs across devices through Firebase after you fill in `firebase-config.js`.

## Features

- Service history per page, grouped by collapsible dates, with a quick `+ Service` button on every card
- Documents attach to the page or to individual services; they sync through Firebase Storage when enabled, otherwise they stay in the browser (IndexedDB)
- Next-service-due date with Overdue and Due Soon badges, plus a "Next due soonest" sort
- Optional PIN lock that syncs to every device sharing the household
- Export and import full JSON backups, including document data
- Two-way sync merge with delete tombstones, so edits from different devices don't clobber each other

## Files

- `index.html` contains the full app.
- `firebase-config.js` is where the Firebase web app config goes.
- `DEPLOY.md` has the GitHub Pages + Firebase setup steps, including Firebase Storage for document sync.
- `.nojekyll` helps GitHub Pages serve the folder as plain static files.

## Notion Embed

1. Publish this folder with GitHub Pages.
2. Copy the public URL for the page.
3. In Notion, type `/embed`.
4. Paste the URL.

## Notes

Without Firebase, everything is saved in the browser that opens the app. Export a backup now and then as insurance.

With Firebase configured, page details, service history, the PIN, and deletions sync through Firestore. Documents sync too once Firebase Storage is enabled (step 6 in DEPLOY.md); without Storage, documents stay on the device where they were added and other devices see a friendly note instead.
