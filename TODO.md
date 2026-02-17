# TODO

## Completed

- [x] **Local storage for current ride** — Persist the current ride state (fare, distance, time) to localStorage so it survives page refreshes or accidental closes
- [x] **Print receipt** — 3D animated receipt printer with dot-matrix paper feed, edge-on printing, swing-to-face presentation, drag-to-dismiss with Web Share API
- [x] **TTS voice lines** — 語 cycles OFF → Cantonese → English; welcome message on hire (往); arrival/fare announcement on stop (停); double-click STOP to re-announce fare; TTS cut off on any button press
- [x] **Receipt surcharge tracking** — Surcharge amount preserved on receipt even after extras are merged into fare
- [x] **Matrix printer sound effect** — Looping dot-matrix printing audio during receipt feed, stops when printing completes
- [x] **Paper tear sound effect** — Plays when user drags receipt to dismiss
- [x] **Unified responsive layout** — Desktop and mobile share the same element sizes; removed redundant media query overrides

## Planned Features

- [ ] **Out of tape handling** — Visual/audio feedback when receipt paper runs out
- [ ] **Onboarding** — First-time user guide / tutorial overlay
- [ ] **Vehicle license plate display** — Show configurable license plate on the meter display
- [ ] **Taxi driver identity plate** — Display driver identity information
- [ ] **Meter accounting display** — Show accounting/summary information on the meter
- [ ] **Trip records** — Keep a history of completed rides with date, fare, extras, distance, and duration; viewable as a log/list
- [ ] **No GPS permission handling** — Graceful UX when user denies or has not granted GPS permission (prompt, fallback, re-request)
- [ ] **Taxi fare mode selector** — Switch between Urban (red), New Territories (green), and Lantau (blue) taxi fare structures, each with their own starting fare and per-increment rates
