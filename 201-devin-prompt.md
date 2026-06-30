# 201-devin-prompt — Run Devin via the API (Phase 3)

Stand up the kanban Daily Task Tracker's **Run with Devin** integration locally so a
workshop participant can kick off a real Devin session from the app, using their own
Devin API credentials stored as **personal secrets**.

## 1. Use the finished files — do not rebuild

The complete, working integration already exists in `.finished/`. Do **not**
re-implement it from scratch. Copy it into `start/`:

- `.finished/server.js` → `start/server.js`
- `.finished/js/devin.js` → `start/js/devin.js`
- `.finished/.env.example` → `start/.env.example`
- Copy any other files `start/` is missing so the board renders with the Devin
  controls (`index.html`, `css/`, the rest of `js/`). When in doubt, prefer the
  `.finished/` version so the Run with Devin pieces are present and consistent.

`start/package.json` already has `"start": "node server.js"`, so no changes there.

## 2. Secrets — personal, never in code

The server needs three values. Ask the participant to provide them as **personal
secrets** (do not paste them into chat or commit them):

- `DEVIN_API_KEY` — from **Settings → Workshop-6-30 org → API Keys** (starts with `cog_`).
- `DEVIN_ORG_ID` — the org id (starts with `org-`).
- `DEVIN_USER_EMAIL` — the workshop account email; created sessions are attributed to this user.

Write them into a git-ignored `start/.env` (never commit it). `PORT` is optional and
defaults to `3000`.

## 3. Run and verify

1. `cd start && npm start` (Node 18+).
2. Open http://localhost:3000.
3. The **Run with Devin** controls only appear once all three secrets are set
   (`GET /api/devin/config` returns `{ "enabled": true }`). Add a task, click
   **Run with Devin**, and confirm a real session is created — the task auto-moves
   to Done when the session completes.

The app fully works without the secrets (the Devin UI just stays hidden), so set
everything up first and drop the secrets in last.
