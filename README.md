# HK Taxi Meter 🚕

A web-based Hong Kong taxi meter simulator with a realistic 7-segment LED display, GPS distance tracking, and time-based fare calculation.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)

## Features

- **Realistic 7-segment LED display** using the DSEG7 font, with dim ghost digits behind the active display
- **Visual replica** of a real TAKERY TKR 787 taxi meter, including the FARE/EXTRAS sections, HIRED indicator, and colored control buttons
- **GPS-based distance tracking** using the browser Geolocation API with jitter filtering
- **Time-based fare** when stationary (speed < 0.5 m/s)
- **PWA support** — installable on Android/iOS home screen for fullscreen, chromeless experience
- **Responsive layout** — optimized for landscape phone use (fills the entire screen)

## Fare Structure

| Item | Rate |
|---|---|
| Starting fare | HK$29.0 |
| Per 200m traveled | HK$2.1 |
| Per minute stationary | HK$2.1 |

## Controls

| Button | Color | Function |
|---|---|---|
| START | Red | Start / Pause the meter |
| RESET | Orange | Reset fare, extras, and distance to zero |
| PAUSE | Yellow | Pause the meter (dedicated pause button) |
| +$10 | Yellow | Add HK$10 to the extras display |
| +$1 | Yellow | Add HK$1 to the extras display |

## Usage

### Quick start

Open `index.html` in a browser, or serve it locally:

```bash
python3 -m http.server 8080 --bind 0.0.0.0
```

Then visit `http://localhost:8080` on your device.

### Mobile (recommended)

For the best experience on a phone:

1. Open the page in Chrome/Safari on your phone
2. **Add to Home Screen** (via browser menu)
3. Launch from the home screen icon — it opens fullscreen in landscape with no browser chrome

> The app requests GPS permission on start. Grant location access for distance-based fare calculation.

## Tech Stack

- **Zero dependencies** — single HTML file with inline CSS and JS
- **DSEG7 font** loaded from jsDelivr CDN for authentic 7-segment digits
- **Geolocation API** (`watchPosition` with high accuracy) for real-time GPS tracking
- **Haversine formula** for distance calculation between GPS coordinates
- **Web App Manifest** for PWA installability

## File Structure

```
├── index.html       # Main app (HTML + CSS + JS, all-in-one)
├── manifest.json    # PWA manifest for home screen install
├── icon-192.png     # App icon (192x192)
├── icon-512.png     # App icon (512x512)
└── README.md
```

## Browser Support

- Chrome (desktop & Android) ✅
- Safari (iOS) ✅
- Firefox ✅
- Edge ✅

> GPS features require HTTPS in production, or `localhost` / `file://` for development.

## Roadmap

See [TODO.md](TODO.md) for details.

- [ ] Print receipt (generate a PNG)
- [ ] Local storage for current ride
- [ ] Fare record / ride history
- [ ] Switch between Urban / New Territories / Lantau taxi fare modes

## License

MIT
