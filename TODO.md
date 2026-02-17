# TODO

## Completed

- [x] **Realistic 7-segment LED display** — DSEG7 font with ghost digits, VACANT/HIRED/STOP status indicators, mileage orange light
- [x] **GPS distance tracking** — `watchPosition` with high accuracy, Haversine formula, jitter filtering
- [x] **Time-based fare** — ticks when stationary (speed < 0.5 m/s)
- [x] **Extras management** — $10/$1 tap to add, hold to subtract; merge into fare on STOP
- [x] **Audio feedback** — beep on button press and fare tick; printer sound loops during receipt feed; tear sound on receipt dismiss
- [x] **TTS voice lines** — 語 cycles OFF → Cantonese → English; welcome message on hire (reads taxi plate number); arrival + fare on stop; double-click STOP to re-announce
- [x] **Receipt printer** — 3D animated printer slides in, dot-matrix paper feed, edge-on print animation, swing to face, drag to dismiss with Web Share API / PNG download
- [x] **Receipt surcharge tracking** — surcharge preserved on receipt after extras merge
- [x] **Ride persistence** — localStorage save/restore of ride state including fare mode; accounts for elapsed time while page was closed
- [x] **Urban / N.T. / Lantau fare modes** — each with own starting fare, increment rates, and reduced-fare threshold; color-coded (red/green/blue); locked during active fare with toast notification
- [x] **License plate overlay** — HK-style white plate, two-row display (letters / digits), screws, corner branding; fade-in card + chrome animation on open, fade-out on dismiss; downloadable as PNG
- [x] **Driver identity card overlay** — HK Taxi Driver Identity Plate design, orange header, driver info grid (serif), photo box; same open/close animations; downloadable as PNG
- [x] **Settings modal** — two-column layout (fields left, photo right); configure plate (two-line textarea), Chinese name, English name, driver photo; scrollable body with fixed titlebar and save button; gear button left-aligned in system controls
  - Plate split on newline → row-1 / row-2 on plate overlay and TTS; receipt shows plate on single line
  - Photo uploaded via camera or gallery; persists as Base64 in localStorage; 4s flash-from-white animation only on photo change (not on open)
  - Default driver photo (`driver-photo.png`) shown on first visit
  - Empty fields restore defaults on save
  - Full-bleed save button at card bottom
- [x] **Driver ID auto-generation** — random 6-digit 編號 on first visit; 發出日期 = today; 屆滿日期 = issue + 10 years
- [x] **Toast notification system** — drop-in from top toast; blue background, white border, bold text; for settings saved, photo updated, and fare mode lock
- [x] **PWA** — `manifest.json` with `display: fullscreen`, `orientation: landscape`, icons; `apple-mobile-web-app-capable` + `mobile-web-app-capable` meta tags

## Planned

- [ ] **Trip records / ride history** — keep a log of completed rides (date, fare, extras, distance, duration); viewable as a scrollable list
- [ ] **No GPS permission handling** — graceful UX when location is denied; prompt to re-grant; time-only fallback mode
- [ ] **Out of tape handling** — visual/audio feedback when receipt paper runs out mid-print
- [ ] **Onboarding** — first-time user guide or tutorial overlay explaining controls
