# 🛣️ PathSafe — India's Smartest Travel Safety Navigator

**PathSafe** is a free, real-time React web application that helps Indian travelers find the **safest road routes** by combining live weather data, multi-route analysis, and danger-zone alerts — all on an interactive map.

---

## ✨ Features

- **🔍 Smart Autocomplete** — Search any village, town, or city in India (Nominatim + Photon)
- **🛣️ Multi-Route Comparison** — Get 3 alternative routes via OSRM and pick the safest
- **🌤️ Live Weather Per Stop** — Real-time weather at every checkpoint along each route
- **🔐 Indian Weather API** — IMD (Indian Meteorological Department) data via [indianapi.in](https://indianapi.in/weather-api) with free Open-Meteo fallback
- **⚠️ Safety Classification** — Each stop rated as Safe ✅, Caution ⚡, or Danger 🚨
- **📍 Click-to-Weather** — Click any location on the map to instantly see live weather with smooth zoom
- **🔀 Click-to-Reroute** — Click any point to reroute your destination
- **🏙️ Smart Checkpoints** — Intermediate stops prefer major cities and popular towns instead of raw coordinates
- **🏞️ Scenic Discovery** — Scenic route shows route-adjacent tourist places with thumbnails, map markers, and TripAdvisor links
- **🚨 Danger Zone Alerts** — Visual callouts for hazardous segments
- **🗺️ Beautiful Map** — Dark-themed Leaflet map with CartoDB Voyager tiles

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Framework | React 18 + TypeScript |
| Build | Vite 5 |
| Styling | Tailwind CSS v3 (dark theme) |
| Map | Leaflet + CartoDB Voyager tiles |
| Weather | [Indian Weather API](https://indianapi.in/weather-api) + [Open-Meteo](https://open-meteo.com/) fallback |
| Routing | [OSRM](https://router.project-osrm.org/) |
| Geocoding | [Nominatim](https://nominatim.openstreetmap.org/) + [Photon](https://photon.komoot.io/) |

---

## 🚀 Quick Start

```bash
# 1. Install dependencies
npm install

# 2. (Optional) Add Indian Weather API key
cp .env.example .env
# Edit .env and add your API key from https://indianapi.in/weather-api

# 3. Start development server
npm run dev
```

The app runs at **http://localhost:8080**

> **No API key?** The app works perfectly with Open-Meteo (free, no key needed). The Indian Weather API adds IMD-sourced data for Indian cities.

📖 See [API_SETUP.md](./API_SETUP.md) for detailed API key setup instructions.

---

## 📁 Project Structure

```
src/
├── components/
│   ├── AutocompleteInput.tsx   — Location search with autocomplete
│   ├── HeroPage.tsx            — Landing page with search form
│   ├── TopBar.tsx              — Map view navigation bar
│   ├── SidePanel.tsx           — Route details, weather stops, safety
│   ├── RouteMap.tsx            — Leaflet map with routes & click-to-weather
│   ├── MapControls.tsx         — Recenter & reroute buttons
│   └── LoadingOverlay.tsx      — Loading spinner overlay
├── services/
│   ├── geocoding.ts            — Nominatim + Photon search & reverse geocode
│   ├── routing.ts              — OSRM route fetching & waypoint sampling
│   ├── routeStops.ts           — Smart checkpoint naming fallback logic
│   ├── scenicPlaces.ts         — Scenic place discovery along the route
│   ├── weather.ts              — Open-Meteo weather (free fallback)
│   ├── indianWeather.ts        — Indian Weather API (indianapi.in)
│   └── weatherCombined.ts      — Combined service (Indian API → Open-Meteo)
├── types/
│   └── pathsafe.ts             — TypeScript interfaces
├── pages/
│   └── Index.tsx               — Main orchestrator page
└── index.css                   — Design tokens & Leaflet overrides
```

---

## 🌤️ Weather API Integration

PathSafe uses a **dual-source weather system**:

1. **Indian Weather API** (primary, when API key is configured)
   - IMD data for Indian cities
   - Global coverage via lat/lng
   - Endpoint: `https://weather.indianapi.in/global/current?location=lat,lng`

2. **Open-Meteo** (free fallback, always available)
   - WMO/ECMWF weather data
   - No API key needed
   - Full coverage worldwide

---

## 🔒 Safety Thresholds

| Condition | ⚡ Caution | 🚨 Danger |
|-----------|-----------|----------|
| Wind speed | > 30 km/h | > 55 km/h |
| Rainfall | > 3 mm | > 15 mm |
| Visibility | < 1000 m | < 300 m |
| Precip probability | > 60% | — |
| Weather code | Drizzle, fog, showers | Thunderstorms, severe |

---

## 🎨 Design

- **Dark theme** with teal primary (`#2dd4bf`) and gold secondary (`#f5c842`)
- **Fonts**: Syne (headings), Outfit (body), JetBrains Mono (data)
- **Safety colors**: Green (safe), Amber (caution), Red (danger)
- Fully responsive layout

---

## 📄 License

MIT — Free to use, modify, and distribute.

---

## 🌐 APIs Used (All Free)

| API | Purpose | Key Required |
|-----|---------|-------------|
| [Indian Weather API](https://indianapi.in/weather-api) | IMD weather data | Yes (free tier: 1000 req) |
| [Open-Meteo](https://open-meteo.com/) | Weather fallback | No |
| [OSRM](https://router.project-osrm.org/) | Road routing | No |
| [Nominatim](https://nominatim.openstreetmap.org/) | Geocoding | No |
| [Photon](https://photon.komoot.io/) | Search fallback | No |
