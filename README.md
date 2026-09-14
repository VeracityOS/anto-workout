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
