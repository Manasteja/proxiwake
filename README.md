# ProxiWake — GPS Proximity Alarm for Travelers

**Never miss your bus stop, train station, or aerial sightseeing moment again.**

ProxiWake is a Progressive Web App (PWA) that triggers an alarm when you approach a destination. Set your target location, choose an alert radius, and rest — ProxiWake monitors your GPS and wakes you when you arrive.

## Features

- **Three travel modes**: Bus (200m–10km radius), Train (200m–10km), Flight (5km–50km)
- **Location search**: Type any place name — powered by OpenStreetMap Nominatim geocoding
- **Manual coordinates**: Enter lat/lng directly or use your current GPS position
- **Escalating alarms**: Gentle (vibrate), Moderate (vibrate + tone), Aggressive (full volume + screen flash)
- **Screen Wake Lock**: Prevents the phone from sleeping during tracking
- **Smart battery indicators**: Shows polling frequency based on distance remaining
- **Real-time tracking**: Live distance calculation using Haversine formula
- **Installable**: Add to home screen on iOS and Android for app-like experience
- **Offline capable**: Service Worker caches the app for offline use
- **No account required**: Zero backend, everything runs on-device

## Live Demo

**[https://YOUR_USERNAME.github.io/proxiwake/](https://YOUR_USERNAME.github.io/proxiwake/)**

## Deploy to GitHub Pages

1. Create a new repository on GitHub named `proxiwake`
2. Clone it locally:
   ```bash
   git clone https://github.com/YOUR_USERNAME/proxiwake.git
   cd proxiwake
   ```
3. Copy the project files (`index.html`, `manifest.json`, `sw.js`) into the repo
4. Push to GitHub:
   ```bash
   git add .
   git commit -m "Initial ProxiWake PWA"
   git push origin main
   ```
5. Go to **Settings → Pages** → Source: **Deploy from a branch** → Branch: **main** → Folder: **/ (root)**
6. Your app will be live at `https://YOUR_USERNAME.github.io/proxiwake/`

## How It Works

### PWA Architecture
```
index.html          — Complete single-file app (HTML + CSS + JS)
manifest.json       — PWA manifest for installability
sw.js               — Service Worker for offline caching
```

### Technical Details
- **Geolocation**: Uses `navigator.geolocation.watchPosition()` for continuous GPS updates
- **Distance calculation**: Haversine formula for accurate great-circle distance
- **Wake Lock**: `navigator.wakeLock.request('screen')` prevents device sleep
- **Alarms**: Web Audio API for tone generation + Vibration API
- **Search**: OpenStreetMap Nominatim API (debounced, 1 req/sec max per policy)
- **No frameworks**: Zero dependencies, pure vanilla HTML/CSS/JS

### Known PWA Limitations
- **Must stay open**: GPS tracking stops if the browser tab is backgrounded (this is a web platform limitation, not a bug)
- **Wake Lock keeps screen on**: The screen dims but stays active — required for continuous GPS
- **Underground**: GPS may not work in tunnels or underground metro (physics constraint)

## Roadmap to Native App

This PWA validates the core UX. The native app (React Native) will add:
- True background geofencing via native APIs
- Lock-screen notifications
- Apple Watch / WearOS companion
- OS-level battery optimization
- App Store / Play Store distribution

## Tech Stack

| Layer | Technology |
|-------|-----------|
| UI | Vanilla HTML/CSS/JS |
| Fonts | DM Sans + JetBrains Mono (Google Fonts) |
| GPS | Web Geolocation API |
| Search | OpenStreetMap Nominatim |
| Caching | Service Worker + Cache API |
| Installability | Web App Manifest |
| Wake | Screen Wake Lock API |
| Alerts | Web Audio API + Vibration API |

## License

MIT
