# SwiftRail — Railway Management System

A single-file, front-end railway booking demo (HTML/CSS/vanilla JS) covering search, seat selection, booking, ticket generation, a bookings history, and a basic admin panel for managing trains.

## Features

- **Search** — Pick origin, destination, and date across a seeded network of 15 stations and 10 trains (plus any trains added via Admin).
- **Results** — Departure/arrival times (with next-day arrival indicator), duration, and per-class pricing with live-looking seat counts (deterministically generated from date + train + class).
- **Seat selection** — Visual 3-coach seat map (3-2 layout with aisle), booked/available/selected states, up to 6 seats per booking.
- **Passenger details** — Name, age, gender per seat, with validation before continuing.
- **Booking confirmation** — Generates a PNR, a stylized e-ticket with a decorative QR-style graphic, and stores the booking.
- **My Bookings** — Lists all past tickets booked in this browser.
- **Admin panel**
  - *Trains & routes*: view all seed + custom trains, delete custom ones.
  - *Add a train*: define number, name, station-code route, cumulative km, departure time, average speed, run days, and per-class (SL/3A/2A) fare-per-km.
  - *Bookings overview*: session stats (bookings, passengers, revenue) and a bookings table, plus a "reset demo data" action.
- **Persistence** — Custom trains and bookings are saved to `localStorage`, so they survive a page reload on the same browser/device.
- **Theming** — Light/dark mode via `prefers-color-scheme`, fully responsive layout down to mobile widths.

## Tech

Plain HTML/CSS/JS, no build step, no dependencies. Everything (styles, markup, logic) lives in one `.html` file. Data lives only in the browser via `localStorage` — there is no backend or server.

## How to run

Just open the HTML file in a browser. No server or install required.

---

## What's left / not yet implemented

**Backend & data**
- No real backend — everything runs client-side and only persists in one browser via `localStorage`. Nothing is shared across devices or users, and clearing browser data wipes it.
- Seat availability and pricing are pseudo-randomly generated from a seed (train + class + date), not tracked against actual bookings — booking a seat doesn't reduce the "seats left" count shown in search results for other users, and seats can theoretically be double-booked across sessions.

**Accounts & security**
- No login/authentication for regular users — bookings aren't tied to an account, just to whatever's in the current browser.
- No admin authentication — the Admin tab is open to anyone who clicks it; no access control on adding/deleting trains.

**Booking lifecycle**
- No cancellation or refund flow — bookings can't be cancelled once confirmed.
- No PNR status lookup (search by PNR to check status independent of "My Bookings").
- "Confirm and pay" doesn't integrate any real or simulated payment gateway — it just confirms instantly.
- No waitlist/RAC (reservation against cancellation) logic — classes with 0 seats just block booking with an alert.

**Search & discovery**
- No filtering/sorting of results (by price, departure time, duration, class).
- No search by train number or name.
- No round-trip or multi-city search — one-way, single-leg only.
- No connecting/multi-train itineraries — only direct trains between two stations on a single train's route.

**Admin**
- No editing of existing trains (only add new / delete custom ones — seed trains can't be modified or removed).
- No input sanitization/limits beyond basic validation (e.g., no cap on fare values, no duplicate-route checks beyond train number uniqueness).

**Other polish**
- QR code on the ticket is a decorative deterministic pattern, not a real scannable QR encoding the PNR.
- No email/SMS confirmation (expected, since there's no backend).
- No automated tests.
- No printable/PDF export of the ticket.

If you want, I can prioritize this list and tackle the most impactful ones next — cancellation and a shared/real seat-inventory model would probably matter most for making this feel like a genuine booking system rather than a demo.
