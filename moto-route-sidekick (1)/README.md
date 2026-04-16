# Moto Route Sidekick

A single-file motorcycle PWA: route planning, weather, fuel range calculator, gas-stop planner, ride log, and shareable route links. Works offline after first load. Zero backend. Zero API keys.

## Features

- **Route planning** — tap map to drop waypoints, drag to adjust, OSM tiles
- **Location search** — powered by Nominatim (OpenStreetMap)
- **Weather** — current + 12-hour + 7-day, rideability verdict, powered by Open-Meteo (no key)
- **Fuel range calculator** — tank × MPG × reserve buffer, with live route overlay
- **Gas stop planner** — tells you how many stops based on safe range
- **Ride log** — title, distance, duration, notes, running totals
- **Saved routes** — load, re-share, delete
- **Shareable routes** — encoded into URL hash, link IS the route
- **Offline** — service worker caches app shell + tiles you've viewed
- **Installable** — Add to Home Screen on iOS/Android, runs full-screen
- **Import/Export** — JSON backup of everything

## Files

| File | Purpose |
|---|---|
| `moto-route-sidekick.html` | Main app (HTML + CSS + JS, single file) |
| `manifest.webmanifest` | PWA manifest |
| `sw.js` | Service worker (offline) |
| `icon-192.svg` | App icon 192×192 |
| `icon-512.svg` | App icon 512×512 |
| `vercel.json` | Vercel routing + headers |

## Deploy to Vercel

### Option A — Drag & Drop (fastest)

1. Go to [vercel.com/new](https://vercel.com/new)
2. Click **"Deploy without Git"** → or drag the entire `moto-route-sidekick` folder into Vercel
3. Name the project (e.g. `moto-sidekick`) → Deploy
4. Open the live URL. Done.

### Option B — GitHub + Vercel

1. Create a new GitHub repo: `moto-route-sidekick`
2. Upload all 6 files to the repo root
3. In Vercel dashboard → **Add New → Project** → import the repo
4. Framework preset: **Other** (it's a static site)
5. Build command: leave empty · Output directory: leave empty (or `.`)
6. Deploy

### Option C — Vercel CLI

```bash
cd moto-route-sidekick
npx vercel --prod
```

## Local Testing

```bash
cd moto-route-sidekick
npx serve .     # or: python3 -m http.server 8000
```

Open `http://localhost:3000` (or `:8000`). The service worker needs HTTPS OR localhost — file:// won't work.

## Install on Phone

**iOS Safari:** Open the live URL → Share → **Add to Home Screen**
**Android Chrome:** Open the live URL → menu → **Install app**

After install it runs full-screen, standalone, with offline support.

## Privacy

- All data stored in `localStorage` on your device
- Nothing sent to any server except the map tile, weather, and geocoding APIs
- Shared routes encode waypoints directly into the URL — the link IS the data

## Tech

- Vanilla JS, no build step, no framework
- [Leaflet 1.9.4](https://leafletjs.com/) for maps
- [OpenStreetMap](https://www.openstreetmap.org/) tiles (free)
- [Nominatim](https://nominatim.org/) geocoding (free, rate-limited)
- [Open-Meteo](https://open-meteo.com/) weather (free, no key)

## Troubleshooting

- **SW doesn't register** → must be served over HTTPS or localhost
- **Nothing loads offline** → visit the app online once first so SW can cache
- **Tiles missing offline** → SW only caches tiles you've actually panned over
- **Shared link too long** → very long routes (50+ waypoints) may hit URL limits; save + share instead

## License

Personal use. Map data © OpenStreetMap contributors.
