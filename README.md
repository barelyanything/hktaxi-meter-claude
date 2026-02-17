# HK Taxi Meter

A web-based Hong Kong taxi meter simulator with a realistic 7-segment LED display, GPS distance tracking, fare calculation, and a full driver identity system.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)

## Features

- **Realistic 7-segment LED display** using the DSEG7 font, with dim ghost digits behind the active display
- **Status indicators** — VACANT, HIRED, and STOP labels in the display area, glowing red when active
- **Mileage indicator** — orange light stays on while hired, blinks and beeps on each fare tick (every 200m after the first 2km)
- **GPS-based distance tracking** using the browser Geolocation API with jitter filtering
- **Time-based fare** when stationary (speed < 0.5 m/s)
- **Extras management** — add extras with $10/$1 buttons; hold to subtract; press STOP again to merge extras into fare
- **Audio feedback** — beep sound on button presses and fare ticks; printer sound during receipt printing; tear sound on receipt dismissal
- **TTS voice lines** — 語 button cycles OFF → Cantonese → English; welcome message on hire (reads taxi plate); arrival/fare announcement on stop; double-click STOP to re-announce fare
- **Receipt printer** — triple-click STOP to print a receipt with a 3D animated printing experience:
  - Printer slides in from the bottom of the screen
  - Receipt paper feeds out with a dot-matrix stepping animation
  - Receipt is rotated edge-on (89°) during printing, then swings to face the user
  - Printer slides away, leaving the receipt centered on screen
  - Drag the receipt to dismiss and trigger Web Share API (or download as PNG)
  - Receipt includes: taxi number, start/end time, total km, paid km, paid minutes, surcharge, total fare
- **Taxi fare modes** — switch between Urban (red), New Territories (green), and Lantau (blue) fare structures; mode locked during active fare with toast notification
- **License plate overlay** — full-size HK-style white license plate with two-row display, screws, and branding; card fades in and slides up on open, fades out on dismiss; downloadable as PNG
- **Driver identity card** — HK Taxi Driver Identity Plate design with orange header, driver info grid, and photo; same open/close animations; downloadable as PNG
- **Settings modal** — two-column layout (fields left, photo right); configure license plate, driver Chinese/English name, and driver photo; scrollable body with fixed titlebar and save button
  - Plate stored as two-line text; receipt displays it on a single line
  - Photo taken with camera or uploaded from gallery; 4s flash-from-white animation plays only when photo is changed, not on open
  - Driver ID (編號) and issue date (發出日期) auto-generated on first visit; expiry = issue + 10 years
  - Empty fields fall back to defaults on save
  - Toast notifications: drop-in from top, blue background, white border and text
- **Fare sheet overlay** — view the current fare mode's rate table
- **Ride persistence** — current ride state saved to localStorage, survives page refresh
- **PWA support** — installable on Android/iOS home screen for fullscreen, chromeless experience

## Fare Structure

| Mode | Starting Fare | First | Per 200m / per min | Reduced after |
|---|---|---|---|---|
| Urban (紅的) | HK$29.0 | 2 km | HK$2.1 | HK$102.5 → $1.4 |
| New Territories (綠的) | HK$25.5 | 2 km | HK$1.9 | HK$82.5 → $1.4 |
| Lantau (藍的) | HK$24.0 | 2 km | HK$1.9 | HK$195.0 → $1.6 |

## Controls

| Button | Label | Color | Function |
|---|---|---|---|
| For Hire | 空 | Red | Reset meter (only when stopped) |
| Hired | 往 | Yellow | Start or resume the meter |
| Stop | 停/講/印 | Yellow | Single: pause; Double: TTS fare; Triple: print receipt; While stopped: merge extras |
| Language | 語 | Yellow | Cycle TTS: OFF → Cantonese → English → OFF |
| +$10 | 附加 $10. | Yellow | Tap to add $10 extras; hold to subtract $10 |
| +$1 | $1. | Yellow | Tap to add $1 extras; hold to subtract $1 |

### System Controls (bottom row)

| Icon | Function |
|---|---|
| ⚙ (gear) | Open settings — configure plate, name, photo |
| 🪪 (rectangle-ad) | Show license plate overlay |
| 🪪 (id-card) | Show driver identity card |
| 📋 (list) | Show fare sheet for current mode |
| 🚗 (car) | Cycle taxi fare mode (Urban → N.T. → Lantau) |

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

1. Serve over HTTPS or use a tunnel (e.g. `ngrok`)
2. Open in Chrome (Android) or Safari (iOS)
3. **Add to Home Screen** via browser menu
4. Launch from the home screen icon — opens fullscreen in landscape with no browser chrome

> The app requests GPS permission on start. Grant location access for distance-based fare calculation.
>
> PWA fullscreen on Android requires the page to be served over **HTTPS**. Chrome caches install state — if the address bar still appears after adding to home screen, remove the shortcut, clear site data in Chrome settings, and re-add.

## Tech Stack

- **Zero build step** — single HTML file with inline CSS and JS
- **DSEG7 font** loaded from jsDelivr CDN for authentic 7-segment digits
- **Font Awesome 6.5.1** for system control icons
- **html2canvas** for plate and driver card image capture
- **Geolocation API** (`watchPosition` with high accuracy) for real-time GPS tracking
- **Haversine formula** for distance calculation between GPS coordinates
- **SpeechSynthesis API** for TTS fare announcement
- **Web Share API** for sharing receipt images (with download fallback)
- **Web App Manifest** (`"display": "fullscreen"`) for PWA installability
- **localStorage** for ride persistence, settings, and driver photo (Base64)

## File Structure

```
├── index.html         # Main app (HTML + CSS + JS, all-in-one)
├── driver-photo.png   # Default driver photo
├── beep-2.mp3         # Button / fare tick audio feedback
├── print.mp3          # Dot-matrix printer sound effect (loops during printing)
├── tear.mp3           # Paper tear sound effect (on receipt dismiss)
├── printer.svg        # Receipt printer graphic
├── manifest.json      # PWA manifest (display: fullscreen, orientation: landscape)
├── icon-192.png       # App icon (192×192)
├── icon-512.png       # App icon (512×512)
├── .gitignore
├── TODO.md            # Planned features
└── README.md
```

## Browser Support

- Chrome (desktop & Android) — recommended
- Safari (iOS)
- Firefox
- Edge

> GPS and TTS features require HTTPS in production, or `localhost` for development.

## Roadmap

See [TODO.md](TODO.md) for details.

- [x] Realistic 7-segment LED display
- [x] GPS distance tracking with jitter filtering
- [x] Urban / New Territories / Lantau fare modes
- [x] Print receipt with 3D animated printer experience
- [x] TTS voice lines (welcome with plate number, arrival, fare announcement)
- [x] Web Share API for receipt sharing
- [x] Dot-matrix printer + paper tear sound effects
- [x] License plate overlay with open/close animations (downloadable PNG)
- [x] Driver identity card overlay with open/close animations (downloadable PNG)
- [x] Settings modal (plate, name, photo, scrollable, persisted to localStorage)
- [x] Driver ID and issue/expiry dates auto-generated on first visit
- [x] Fare mode lock with toast when ride is active
- [x] Toast system (drop-in from top, blue/white styled)
- [ ] Trip records / ride history
- [ ] Out of tape handling
- [ ] No GPS permission handling / graceful fallback
- [ ] Onboarding experience

## License

MIT
