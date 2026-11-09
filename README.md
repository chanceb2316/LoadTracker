# LoadTracker

## Table of Contents
- [Project Vision & Core Goals](#project-vision--core-goals)
- [Core Feature Requirements](#core-feature-requirements)
  - [Direct Access & Header Toolbar](#direct-access--header-toolbar)
  - [Interactive Map & Geofencing](#interactive-map--geofencing)
  - [Dump & Load Management Configuration](#dump--load-management-configuration)
  - [POI & Hazard Logger](#poi--hazard-logger)
  - [Summary & Data Export](#summary--data-export)
- [Technical & Design Specifications](#technical--design-specifications)
- [Installation & Quick Start](#installation--quick-start)
- [Running the PWA Locally](#running-the-pwa-locally)
- [Development & Build Notes](#development--build-notes)
- [License](#license)

---

## Project Vision & Core Goals

LoadTracker is a high‑utility, responsive **single‑page Progressive Web App (PWA)** designed for heavy‑equipment operators and truck drivers in land‑clearing, disaster‑recovery, and storm‑debris cleanup operations.

- **Zero‑Login Experience** – Launches directly into the active map‑logging view; no authentication barriers.
- **Cab‑Optimized Ergonomics** – Dark, high‑contrast UI with extra‑large touch targets (≥48 px) for readability in high‑vibration, high‑glare environments.
- **Automated Field Accounting** – Real‑time calculation of daily load tallies, cubic‑yardage totals, and performance‑based bonuses ($1 / yd³ after a 300 yd³ daily threshold).
- **Offline Resilience** – Installable via a PWA manifest (“Add to Home Screen”). All session state persists locally (LocalStorage/IndexedDB) to survive intermittent connectivity.

---

## Core Feature Requirements

### Direct Access & Header Toolbar
- **No Login Screen** – Immediate entry.
- **GPS Active Status** – Visual indicator (green/amber/red) showing location lock status.
- **Quick‑Mode Toggles** – Header toolbar with one‑tap navigation to:
  - Map View  
  - Load Entry / Management  
  - POI Flagging  
  - Financial / Export Summary  

### Interactive Map & Geofencing (Google Maps JavaScript API)
- **Dynamic Boundary Selection** – Tap road segments to outline work sections.  
- **Real‑Time Geofence Visuals** – High‑contrast shaded polygons for active cleanup zones.  
- **Floating Controls**:  
  - **Quick Dump Log** – One‑tap recording of a completed haul.  
  - **+ Flag POI** – Drop a pin at the current GPS coordinate for hazards, debris pockets, or access blockages.  

### Dump & Load Management Configuration
- **Custom Truck Profiles** – Define haul capacities (e.g., Mack DM6116S, M817 5‑ton, or custom trailer yardage).  
- **Financial Parameters** – Base hourly rate, haul rate ($/yd³), and daily threshold limit.  
- **Dynamic Earnings Engine** – Auto‑tally volume, apply bonus rates once the threshold is crossed, and display running totals.  

### POI & Hazard Logger
- **Issue Flagging** – Drop‑pin overlay with category dropdown:  
  - Uncut Trees  
  - Down Powerlines  
  - High‑Tonnage Stumps  
  - Equipment Breakdown  
- **Custom Notes** – Free‑form observations attached to the map coordinate.  

### Summary & Data Export
- **Operational Dashboard** – Live breakdown of trips, cubic yards, base pay, bonus pay, and estimated daily earnings.  
- **Logged Entries Table** – Timestamped rows showing haul details, duration, capacity, and calculated value.  
- **One‑Tap Export** – CSV and formatted PDF reports ready for supervisor billing and pay verification.  

---

## Technical & Design Specifications

- **Architecture** – Single‑file HTML5 app (`index.html`) using standard Web APIs (Geolocation, LocalStorage/IndexedDB) and CDN‑served libraries:  
  - Tailwind CSS for responsive styling  
  - Google Maps JavaScript API for mapping and geofencing  
- **PWA Support** – `manifest.json` configured for:  
  - Standalone display mode  
  - Black‑translucent status‑bar themes  
  - High‑visibility launcher icons (512 px PNG, 192 px PNG)  
- **Color Palette – “Elegant Industrial”**  
  - Background / Base: Charcoal slate `#1E2530` / `#121820`  
  - Primary Accent: Safety amber `#FFC107`  
  - Active Controls / GPS: Visibility blue `#2196F3` and status green `#4CAF5`  
- **Typography & UI Elements** – Extra‑large touch targets (≥48 px height), bold monospace numbers for yardage/earnings, high‑contrast borders for sunlight readability.  

---

## Installation & Quick Start

1. **Clone the repository** (or copy the folder) to a local machine.  
   ```bash
   git clone https://<your-repo>/LoadTracker.git
   cd LoadTracker
   ```
2. **Open `index.html`** in a modern browser (Chrome, Edge, or Firefox). No build step is required because all assets are CDN‑served.  
3. **Add to Home Screen** – On a mobile device, open the app and use the browser’s *Add to Home Screen* option. The app installs as a PWA and launches in full‑screen mode.  
4. **Configure your truck** via the *Load Management* screen before the first shift.  
5. **Start logging** – The map will request GPS permission; once granted you can begin work.  

---

## Running the PWA Locally (Development)

While the production version is a static HTML file, a local dev server avoids CORS issues when testing the Google Maps API.

```powershell
# Python simple HTTP server
python -m http.server 8000
# Then navigate to http://localhost:8000 in your browser.
```

Or with Node.js:

```powershell
npm install -g serve
serve -s .
```

> **Note**: You need a valid Google Maps JavaScript API key. Add it to the `index.html` script tag as `key=YOUR_API_KEY`.

---

## Development & Build Notes

- **Tailwind CSS** – Imported via CDN (`https://cdn.jsdelivr.net/npm/tailwindcss@3.x/dist/tailwind.min.css`). For custom builds, run:  
  `npx tailwindcss -i ./src/input.css -o ./dist/tailwind.css --watch`  
- **State Management** – All runtime state (truck profiles, logged hauls, POIs) persists in **LocalStorage** (`window.localStorage`). For larger datasets or future offline sync, consider migrating to **IndexedDB**.  
- **Export Logic** – CSV export uses a `Blob` with `URL.createObjectURL`. PDF export leverages **jsPDF** (CDN) and builds a minimal report layout.  
- **Testing** – Validate GPS functionality on actual devices; emulator GPS may not reflect real‑world accuracy.  

---

## License

LoadTracker is released under the **MIT License**. See the `LICENSE` file for details.

---

*This README was written by the principal software architect and senior full‑stack developer overseeing the LoadTracker project.*