# 🎯 Initiative Tracker

A single-file, dependency-free status dashboard for tracking initiatives across teams.
Sections hold tasks; each task has a team and a status color:

🟢 On track · 🟡 Some risk · 🔴 At risk · 🔵 Done · ⚪ Not started

## How sharing & updating works

- **`index.html`** — the whole app (HTML/CSS/JS, no build step).
- **`data.json`** — the *shared* board. On a visitor's **first** load the page reads this file,
  so whatever you commit here is what everyone sees. After that, each person's edits are kept
  in their own browser (localStorage).
- Toolbar buttons:
  - **↻ Sync from repo** — pull the latest `data.json` that was pushed to Git (overwrites the
    local copy). Use this after someone publishes an update.
  - **⤓ Export data.json** — download the current board as `data.json` to commit back to the repo.
  - **Import** — load a `data.json` file from disk.

### Updating the shared board (the Git workflow)

1. Open the live site, make your changes.
2. Click **⤓ Export data.json**.
3. Replace `data.json` in this repo with the downloaded file and push:
   ```bash
   git add data.json
   git commit -m "Update tracker status"
   git push
   ```
4. Netlify redeploys automatically. Teammates click **↻ Sync from repo** to pull it
   (or just open the site fresh).

## Hosting on Netlify

This repo is a static site — no build needed (`netlify.toml` already sets `publish = "."`).

**Option A — connect the Git repo (recommended, auto-deploys on every push):**
1. Push this repo to GitHub.
2. In Netlify: **Add new site → Import an existing project → GitHub →** pick this repo.
3. Leave build command empty, publish directory `.`, deploy.

**Option B — drag & drop:** drop this folder onto <https://app.netlify.com/drop> for a one-off deploy.

## Local preview

```bash
npx http-server . -p 4178
# open http://localhost:4178
```
(Opening `index.html` directly via `file://` works too, but `data.json` auto-load needs to be served over http.)
