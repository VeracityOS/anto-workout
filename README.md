# anto-workout — WOD Planner

Single-file HTML workout PWA. Backup of the Vercel project `workouts`, live at
https://workouts-lemon.vercel.app

That Vercel project has **no Git repository connected** — this repo is the only
copy of the source outside the deployment.

## Contents

| Path | Purpose |
|---|---|
| `index.html` | The entire app — markup, CSS and JS in one file |
| `manifest.json` | PWA manifest (installable to home screen) |
| `service-worker.js` | Offline cache, `wod-v4` |
| `assets/` | Body-map graphics (front/back muscle diagram) |
| `icons/` | App and favicon icons |

## Running locally

No build step. Serve the directory over HTTP (a service worker will not
register from `file://`):

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Note on the service worker

`service-worker.js` is cache-first with no expiry: once a file is in the
`wod-v4` cache the device serves it forever and never re-checks the network.
A bad cached copy therefore persists until site data is cleared. Bump the
`CACHE` constant when shipping changes, or the update will not reach devices
that already have the app installed.

## Deployment

Deployed on Vercel as the project `workouts`, served at
https://workouts-lemon.vercel.app

Static site — no build step. Vercel settings should be:

| Setting | Value |
|---|---|
| Framework preset | Other |
| Build command | *(none)* |
| Output directory | *(repo root)* |
| Production branch | `main` |

Every push to `main` triggers a production deploy.

Note that deployments created before this repository was connected (the
original drag-and-drop upload) are not built from this source. Redeploying
or rolling back to one of those serves the old uploaded files, not the
code here.

### After deploying

`service-worker.js` is cache-first, so bump the `CACHE` constant on any
change to `index.html` or the assets — otherwise devices that already have
the app installed keep serving the cached copy and never see the update.
