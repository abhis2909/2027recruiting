# 2027 Recruiting — Coverage Book

A single-page recruiting tracker (applications + networking contacts) for the 2027 internship/full-time cycle. It's a self-contained static HTML app — no build step, no backend.

## What it is

`index.html` is the whole app. It renders a "Coverage Book" with two tabs:
- **Applications** — firm, role, track, status, dates, priority, notes
- **Contacts** — networking contacts, outreach status, follow-ups, meetings

Data is saved to your browser's `localStorage`, so it persists between visits on the same device/browser. Since it's local to the browser, data won't sync across devices (e.g. laptop vs. phone) — each browser keeps its own copy.

## Deploying to Vercel

1. Go to [vercel.com/new](https://vercel.com/new) and import this GitHub repository (`abhis2909/2027recruiting`).
2. Framework preset: choose **Other** (no build needed — it's a static `index.html`).
3. Leave build/output settings blank and click **Deploy**.

Vercel will serve `index.html` at your project's root URL.

## Using it on your phone

1. Open the deployed Vercel URL in your phone's browser.
2. Optionally, add it to your home screen (Safari: Share → Add to Home Screen; Chrome: menu → Add to Home Screen) so it opens like an app.
3. Since data is stored in that browser's `localStorage`, keep using the same browser on your phone to retain your entries.

## Local preview

Just open `index.html` directly in a browser, or serve the folder:

```bash
npx serve .
```
