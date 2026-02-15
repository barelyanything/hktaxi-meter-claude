# HK Taxi Meter

A web-based Hong Kong taxi meter simulator with a realistic 7-segment LED display, GPS distance tracking, and time-based fare calculation.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)

## Features

- **Realistic 7-segment LED display** using the DSEG7 font, with dim ghost digits behind the active display
- **Visual replica** of a real DLLM DLM 667 taxi meter, including the FARE/EXTRAS sections and colored control buttons
- **Status indicators** — VACANT, HIRED, and STOP labels in the display area, glowing red when active
- **Mileage indicator** — orange light stays on while hired, blinks and beeps on each fare tick (every 200m after the first 2km)
- **GPS-based distance tracking** using the browser Geolocation API with jitter filtering
- **Time-based fare** when stationary (speed < 0.5 m/s)
- **Extras management** — add extras with $10/$1 buttons; hold to subtract; press STOP again to merge extras into fare
- **Audio feedback** — beep sound on button presses and fare ticks (mp3, 50% volume)
- **Ride persistence** — current ride state saved to localStorage, survives page refresh
- **PWA support** — installable on Android/iOS home screen for fullscreen, chromeless experience
- **Responsive layout** — optimized for both portrait and landscape phone use

## Fare Structure

| Item | Rate |
|---|---|
| Starting fare (first 2km) | HK$29.0 |
| Per 200m traveled (after 2km) | HK$2.1 |
| Per minute stationary | HK$2.1 |

## Controls

| Button | Label | Color | Function |
|---|---|---|---|
| For Hire | 空 | Red | Reset meter (only when stopped) |
| Hired | 往 | Yellow | Start or resume the meter |
| Stop | 停/講/印 | Yellow | Pause meter; press again to merge extras into fare |
| Language | 語 | Yellow | Language toggle (TBD) |
| +$10 | 附加 $10. | Yellow | Tap to add $10 extras; hold to subtract $10 |
| +$1 | $1. | Yellow | Tap to add $1 extras; hold to subtract $1 |

## Display Behavior

- **VACANT** — fare and extras displays are blank (no 0.0 shown)
- **HIRED** — fare counts up, mileage indicator (orange light) stays on, blinks on each fare increment
- **STOP** — fare and extras shown; mileage indicator off; extras hidden if zero

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
├── beep.mp3         # Button / fare tick audio feedback
├── manifest.json    # PWA manifest for home screen install
├── icon-192.png     # App icon (192x192)
├── icon-512.png     # App icon (512x512)
└── README.md
```

## Browser Support

- Chrome (desktop & Android)
- Safari (iOS)
- Firefox
- Edge

> GPS features require HTTPS in production, or `localhost` / `file://` for development.

## Roadmap

See [TODO.md](TODO.md) for details.

- [ ] Print receipt (generate a PNG)
- [ ] Fare record / ride history
- [ ] Switch between Urban / New Territories / Lantau taxi fare modes

## License

MIT
