# 2027 Recruiting — Coverage Book

A single-page recruiting tracker (applications + networking contacts) for the 2027 internship/full-time cycle. It's a self-contained static HTML app — no build step, no backend.

## What it is

`index.html` is the whole app. It renders a "Coverage Book" with two tabs:
- **Applications** — firm, role, track, status, dates, priority, notes
- **Contacts** — networking contacts, outreach status, follow-ups, meetings

By default (no login configured), data is saved to your browser's `localStorage`, so it persists between visits on the same device/browser but won't sync across devices or be shared with anyone else. Turn on **Google sign-in** (below) if you want to share the site with classmates and have each person keep their own private, cloud-saved list.

## Hovering to preview an application link

On a desktop/laptop (any pointer with hover), hovering over a 🔗 link pill opens a slide-in panel on the right with the link loaded in an iframe, plus an "Open in new tab" fallback. Some employer sites (Workday, Greenhouse, etc.) block being framed by other pages — the panel will show blank for those, but the fallback link still works. On phones/touch, links just open in a new tab as usual since there's no hover.

## Turning on Google sign-in (so classmates can each have their own tracker)

Login is off by default — the site works exactly as described above until you turn it on. Turning it on requires a free [Firebase](https://firebase.google.com) project (Google's backend-as-a-service; no cost at this scale):

1. Go to the [Firebase console](https://console.firebase.google.com), click **Add project**, and create one (any name, e.g. "2027-recruiting").
2. **Authentication** → **Get started** → under **Sign-in method**, enable **Google**.
3. **Firestore Database** → **Create database** → start in **Production mode** (any region is fine).
4. In Firestore, go to the **Rules** tab and replace the rules with:
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /users/{userId} {
         allow read, write: if request.auth != null && request.auth.uid == userId;
       }
     }
   }
   ```
   This makes sure each signed-in student can only read/write their *own* data.
5. Back in **Project settings** (gear icon) → **General** → under **Your apps**, click the **`</>`** (web) icon to register a new web app (no hosting needed). Copy the `firebaseConfig` object it gives you.
6. In `index.html`, find the `FIREBASE_CONFIG` object near the top (inside `<script id="firebase-config">`) and paste in your real values, replacing the `"REPLACE_ME"` placeholders.
7. Still in the Firebase console, under **Authentication** → **Settings** → **Authorized domains**, add your Vercel domain (e.g. `your-project.vercel.app`) so sign-in works there.
8. Commit and redeploy. The site will now show a "Sign in with Google" screen before the tracker loads.

Once this is set up, anyone with the link can sign in with their own Google account and get their own private applications/contacts list, saved to Firestore. If you already had data saved locally in your browser before signing in for the first time, it's automatically carried over into your new account.

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
