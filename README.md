<div align="center">

# 🌬️ AirCast

### AI-Powered Air Quality Forecasting from Space to Street

*Fusing NASA's geostationary TEMPO satellite, real-time ground sensors, live meteorology, and generative AI into a single, human-readable picture of the air you're breathing — and the air you'll breathe in the next six hours.*

<br>

<a href="https://www.spaceappschallenge.org/2025/find-a-team/relentless/?tab=project">
  <img src="assets/space-apps-2025-global-nominee.png" alt="2025 NASA International Space Apps Challenge — Global Nominee" width="320">
</a>

### 🏆 2025 NASA Space Apps Challenge — **Global Nominee**

**🔗 [Check out our team page on NASA's Space Apps site](https://www.spaceappschallenge.org/2025/find-a-team/relentless/?tab=project)**

<br>

[![NASA Space Apps 2025](https://img.shields.io/badge/NASA%20Space%20Apps-2025-0B3D91?style=for-the-badge&logo=nasa&logoColor=white)](https://www.spaceappschallenge.org/)
[![Global Nominee](https://img.shields.io/badge/🏆%20Global%20Nominee-Top%201%2C219%20of%2011%2C500%2B-FFD700?style=for-the-badge)](https://www.spaceappschallenge.org/)
[![Status](https://img.shields.io/badge/Status-Live%20Demo-00E400?style=for-the-badge)](#-running-aircast-locally)

<br>

![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=flat-square&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-3.0-000000?style=flat-square&logo=flask&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-gpt--4o--mini-412991?style=flat-square&logo=openai&logoColor=white)
![NASA TEMPO](https://img.shields.io/badge/NASA-TEMPO%20L2%20NO₂-E03C31?style=flat-square&logo=nasa&logoColor=white)
![Google Maps](https://img.shields.io/badge/Google%20Maps-Visualization-4285F4?style=flat-square&logo=googlemaps&logoColor=white)
![Chart.js](https://img.shields.io/badge/Chart.js-FF6384?style=flat-square&logo=chartdotjs&logoColor=white)
![Azure](https://img.shields.io/badge/Azure-App%20Service%20%2B%20Blob-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)

</div>

---

> ### 🏅 Recognition
> **AirCast** was selected as a **2025 NASA Space Apps Challenge Global Nominee** — placing in the **top 1,219 of 11,500+ teams** worldwide (over 11,500 projects submitted). Built by **Aahil Afraz** & **Allen Varghese** for **Team Relentless**.

---

## 📖 Table of Contents

- [The Problem](#-the-problem)
- [What AirCast Does](#-what-aircast-does)
- [Live Feature Tour](#-live-feature-tour)
- [System Architecture](#-system-architecture)
- [The Data Fusion Pipeline](#-the-data-fusion-pipeline)
- [Deep Dive: How Each Subsystem Works](#-deep-dive-how-each-subsystem-works)
- [The Science: AQI Math & Forecast Model](#-the-science-aqi-math--forecast-model)
- [API Reference](#-api-reference)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Running AirCast Locally](#-running-aircast-locally)
- [Deployment](#-deployment)
- [Resilience by Design](#-resilience-by-design)
- [Authors](#-authors)

---

## 🎯 The Problem

Air pollution kills an estimated **7 million people per year** (WHO), yet most people have no intuitive, *actionable* sense of the air around them. The data exists — but it's scattered across:

- **Satellites** that measure pollution columns from orbit (great coverage, coarse timing)
- **Ground stations** that measure surface concentration (precise, but sparse and patchy)
- **Weather systems** that *drive* how pollution disperses (wind clears it, heat brews ozone, rain washes it out)

Nobody fuses these into one answer to the only question that matters to a parent, a coach, or a senior citizen:

> *"Is it safe to go outside **right now** — and when will it be better?"*

**AirCast answers exactly that.**

---

## ✨ What AirCast Does

AirCast ingests **three independent data modalities**, reconciles them, projects them forward in time, and translates the result into plain-English guidance tailored to *who you are*.

| Capability | Description |
|---|---|
| 🛰️ **Satellite + Ground Fusion** | Cross-validates NASA TEMPO NO₂ satellite columns against live OpenAQ ground sensors, surfacing a real-time **correlation score** between the two sources. |
| 🔮 **6-Hour AQI Forecast** | A physics-informed model projects air quality forward using live wind, temperature, humidity, precipitation, and traffic-cycle patterns. |
| 🤖 **Generative AI Daily Brief** | GPT-4o-mini composes a warm, jargon-free "air quality report card" from the full fused dataset — graded A–F, with timing advice. |
| 💬 **Conversational AI Assistant** | A context-aware chatbot answers natural-language questions ("Should I cancel soccer practice?") grounded in the *current* readings. |
| 👥 **Per-Group Safety Engine** | Five distinct risk profiles — children, healthy adults, seniors, athletes, and care facilities — each with their own AQI thresholds and best/worst-time windows. |
| 🗺️ **Interactive Dark-Mode Map** | Google Maps with animated AQI markers, heatmap overlay, satellite toggle, geocoded search, and geolocation. |
| 📊 **Live Forecast Charts** | Chart.js line graphs that flip between AQI and weather projections, color-coded by EPA AQI category. |

---

## 🎬 Live Feature Tour

```
┌─────────────────────────────────────────────────────────────────────────┐
│  AirCast                              🛰️ TEMPO  📡 Ground  🌤️ Weather     │
├──────────────────┬──────────────────────────────────┬───────────────────┤
│  📍 LOCATION      │                                  │  📈 6-HR FORECAST  │
│  [ search...   ]  │                                  │  [ AQI ][ Weather ]│
│  ⌖ Use My Location│         🗺️  DARK MAP             │                    │
│                  │     ●  ●        ●                 │  ↑ Heat → ozone    │
│  CURRENT AQI      │        (animated AQI markers)    │  ↓ Wind clears air │
│      65           │      🔥 heatmap | 🛰️ satellite   │   ╱╲    ╱          │
│   Moderate        │                                  │  ╱  ╲__╱           │
│                  │                                  │                    │
│  🧠 AI DAILY BRIEF│                                  │  POLLUTANT LEVELS  │
│  "Good morning!   │                                  │  PM2.5 ████░ 12.5  │
│   Air's a solid B │                                  │  NO₂   ██░░░ 35    │
│   today..."       │                                  │  O₃    ███░░ 45    │
│                  │                                  │                    │
│  ⚠️ HEALTH ALERTS │                                  │  🛰️ vs 📡 COMPARE  │
│  👥 SAFETY GUIDE  │                                  │  Correlation: 91%  │
└──────────────────┴──────────────────────────────────┴───────────────────┘
                                                              💬 ← floating AI chat
```

---

## 🏗️ System Architecture

AirCast is a **Flask monolith** that serves both a static frontend *and* a JSON API from a single process — the backend resolves `/` to the SPA and `/api/*` to data endpoints. Every external dependency is wrapped in a **graceful-degradation layer** so the app never hard-crashes when a key is missing or a source is down.

```
                            ┌──────────────────────────────────────┐
                            │              BROWSER (SPA)            │
                            │  index.html · style.css · map.js      │
                            │  Google Maps JS · Chart.js            │
                            └───────────────────┬──────────────────┘
                                                │  fetch() /api/*
                                                ▼
        ┌───────────────────────────────────────────────────────────────────┐
        │                      FLASK APPLICATION (app.py)                      │
        │      flask-cors · static file server · 8 JSON endpoints             │
        │                                                                     │
        │  /api/air-quality   /api/weather   /api/tempo   /api/forecast       │
        │  /api/safety-groups /api/ai-summary /api/ai-chat                     │
        └───┬───────────────┬──────────────┬──────────────┬──────────────────┘
            │               │              │              │
            ▼               ▼              ▼              ▼
    ┌──────────────┐ ┌────────────┐ ┌────────────┐ ┌──────────────────┐
    │  api/openaq  │ │ api/weather│ │  api/tempo │ │   models/        │
    │   .py        │ │   .py      │ │   .py      │ │  forecast.py     │
    │              │ │            │ │            │ │  user_groups.py  │
    │ Ground       │ │ Live met.  │ │ Satellite  │ │ Physics model +  │
    │ sensors      │ │ data       │ │ NetCDF     │ │ safety engine    │
    └──────┬───────┘ └─────┬──────┘ └─────┬──────┘ └──────────────────┘
           │               │              │
           ▼               ▼              ▼
    ┌──────────────┐ ┌────────────┐ ┌──────────────────────────────┐
    │  OpenAQ v3   │ │OpenWeather │ │  Azure Blob Storage          │
    │  REST API    │ │ 2.5 API    │ │  TEMPO_NO2_L2_V04 .nc granule│
    └──────────────┘ └────────────┘ └──────────────────────────────┘

    ┌────────────────────────────────────────────────────────────────┐
    │  OpenAI gpt-4o-mini  ← consumed by /api/ai-summary & /api/ai-chat│
    └────────────────────────────────────────────────────────────────┘
```

---

## 🔬 The Data Fusion Pipeline

When the page loads, `fetchAllData()` in `map.js` orchestrates a deliberate, sequenced fan-out — AI brief first (highest perceived value), then the quantitative layers:

```
   USER LOCATION (geolocation / search / default: Philadelphia 39.95, -75.16)
                                  │
        ┌─────────────────────────┼─────────────────────────┐
        ▼                         ▼                         ▼
  /api/ai-summary          /api/air-quality           /api/forecast
        │                         │                         │
   gathers ALL              OpenAQ stations           current AQI ⊕ weather
   sources, builds          within 25 km radius       → physics projection
   GPT context              → EPA AQI per station      → 6 hourly predictions
        │                         │                         │
        ▼                         ▼                         ▼
   "Air's a B today"      animated map markers       color-coded Chart.js
                                  │
                                  ▼
                        /api/weather · /api/tempo · /api/safety-groups
                        weather cards · 🛰️vs📡 correlation · per-group advice
```

The genuinely novel step is **cross-source reconciliation** (`createComparisonVisualization()`): AirCast pulls the TEMPO satellite-derived AQI *and* the live ground AQI for the same coordinates, computes their absolute difference, and renders a **correlation percentage**:

```
accuracy = 100 − ( |tempoAQI − groundAQI| ÷ max(tempoAQI, groundAQI) × 100 )
```

This is the heart of the NASA challenge: *does the view from 35,786 km up agree with the sensor on the corner?*

---

## 🧠 Deep Dive: How Each Subsystem Works

### 🛰️ NASA TEMPO Satellite Ingestion — `backend/api/tempo.py`

TEMPO (Tropospheric Emissions: Monitoring of Pollution) is NASA's **geostationary** air-quality instrument, parked over North America at ~35,786 km, measuring pollution **hourly during daylight** at 2–8 km resolution. AirCast consumes its **Level-2 NO₂ vertical-column** product.

- **Format:** The raw granule is a `.nc` **NetCDF4** scientific file (`TEMPO_NO2_L2_V04_...Z.nc`), streamed from **Azure Blob Storage** into memory via `BytesIO` — no disk writes.
- **Structure-aware parsing:** TEMPO stores data in HDF-style *groups*. The reader reaches into `dataset.groups['geolocation']` for `latitude`/`longitude` arrays and `dataset.groups['product']` for `vertical_column_troposphere`.
- **Nearest-pixel lookup:** Given a user lat/lon, it builds a Manhattan-distance field over the satellite grid (`|Δlat| + |Δlon|`) and uses `np.argmin` + `np.unravel_index` to snap to the closest satellite pixel.
- **Column → surface → AQI:** A tunable parameterization (`convert_no2_to_aqi`) scales the molecules/cm² column down to an estimated surface NO₂ in ppb, then maps it through EPA-style NO₂ breakpoints.
- **Data provenance & freshness:** Every response carries a `freshness` block (observation timestamp, age in hours, 🟢/🟡/🟠 status) and a `metadata` block (product version, satellite, resolution, orbit altitude, units) — full scientific transparency baked into the API.

> 🏛️ **Real-world resilience:** AirCast was built **during the 2025 U.S. government shutdown**, when NASA's data portal updates were paused. Rather than fail, the app pins to the *last available* TEMPO granule, labels its exact age, and explains the funding lapse to the user — modeling exactly how a production system caches through an upstream outage.

### 📡 Ground-Station Air Quality — `backend/api/openaq.py`

- Queries the **OpenAQ v3** `/locations` endpoint for monitoring stations within a configurable radius (default **25 km**, converted to meters).
- For each of up to 5 nearest stations, fetches `/locations/{id}/latest` and extracts PM2.5, NO₂, and O₃.
- Converts raw **PM2.5 → AQI** using the official **EPA piecewise-linear breakpoint formula** (`pm25_to_aqi`).
- **Triple-layered fallback:** API key missing → public access; timeout/network error → realistic synthetic stations (`generate_sample_data`); per-station parse failure → estimated defaults. The map is *never* empty.

### 🌤️ Live Meteorology — `backend/api/weather.py`

- Pulls current conditions (`/weather`) and an 8-step forecast (`/forecast`) from the **OpenWeather 2.5 API** in imperial units.
- Surfaces temperature, wind speed & direction, humidity, pressure, and precipitation — the exact variables that physically govern pollutant dispersion.
- Ships a deterministic `generate_fallback_forecast()` so the forecast model always has weather to chew on, even with no API key.

### 🔮 The Forecast Engine — `backend/models/forecast.py`

A **physics-informed, explainable** projection (deliberately *not* a black box). Starting from the current AQI, each future hour is multiplicatively adjusted by live meteorology and human-activity cycles:

| Driver | Condition | AQI Multiplier | Physical Rationale |
|---|---|---|---|
| 💨 Wind | > 15 mph | ×0.75 | Strong winds disperse pollutants |
| 💨 Wind | > 10 mph | ×0.85 | Moderate dispersion |
| 💨 Wind | > 5 mph | ×0.92 | Light dispersion |
| 🌡️ Heat | > 85 °F | ×1.20 | Sunlight + heat brews ground-level ozone |
| 🌡️ Warm | > 75 °F | ×1.10 | Elevated photochemical activity |
| 🌧️ Rain | > 0 | ×0.65 | Precipitation scavenges particulates |
| 💧 Humidity | > 80% | ×1.05 | Promotes secondary particle formation |
| 🚗 Rush hour | 7–9 & 16–19 h | ×1.15 | Peak traffic emissions |
| 🌙 Overnight | 22–5 h | ×0.95 | Reduced human activity |

Each hour also gets ±5 points of stochastic variation and feeds forward into the next with a 0.9 decay factor (so trends compound naturally). Crucially, every prediction returns a **human-readable reason** (`"Improving due to strong winds dispersing pollution, rain washing out particulates"`) — the model *explains itself*, which is what makes the AI brief and health alerts so concrete.

### 👥 Per-Group Safety Engine — `backend/models/user_groups.py`

The same AQI means different things to different bodies. AirCast encodes **five risk profiles**, each with its own thresholds:

| Group | "Safe" below | Rationale |
|---|---|---|
| 🏥 Care Facilities | AQI 45 | Most vulnerable populations |
| 👶 Children | AQI 50 | Developing lungs, higher breathing rate |
| 👴 Seniors | AQI 50 | Cardiovascular sensitivity |
| ⚽ Athletes | AQI 75 | High exertion = high intake, but resilient |
| 💪 Healthy Adults | AQI 100 | Baseline EPA threshold |

The `/api/safety-groups` endpoint runs each group through the 6-hour forecast and computes **best and worst time windows** per group — e.g. *"Children: ✓ Best 3PM (AQI 48) · ✗ Avoid 6PM (AQI 112)."*

### 🤖 Generative AI Layer — `backend/app.py`

Two endpoints wrap **OpenAI `gpt-4o-mini`**, each fed a richly structured context block assembled from *all* upstream sources:

- **`/api/ai-summary`** — A "daily brief" persona grades the air A–F, uses traffic-light metaphors, and delivers one practical health tip in < 180 words. The prompt is fed current AQI, pollutant breakdown, TEMPO satellite reading, the full 6-hour forecast with reasons, and computed best/worst windows.
- **`/api/ai-chat`** — A session-aware assistant (in-memory `chat_sessions` keyed by client-generated session ID) that keeps the last 2 exchanges for continuity, injects live air-quality context into every turn, and stays scoped to air-quality questions.

Both are wrapped so that **if OpenAI is unavailable, the app still returns a graceful fallback** with HTTP 200 — the UI degrades, it never breaks.

---

## 🧮 The Science: AQI Math & Forecast Model

**PM2.5 → AQI** uses the EPA's piecewise-linear breakpoint interpolation:

$$AQI = \frac{AQI_{hi} - AQI_{lo}}{C_{hi} - C_{lo}} \times (C - C_{lo}) + AQI_{lo}$$

mapped across the six official categories:

| AQI | Category | Color |
|---|---|---|
| 0–50 | Good | 🟢 `#00E400` |
| 51–100 | Moderate | 🟡 `#FFFF00` |
| 101–150 | Unhealthy for Sensitive Groups | 🟠 `#FF7E00` |
| 151–200 | Unhealthy | 🔴 `#FF0000` |
| 201–300 | Very Unhealthy | 🟣 `#8F3F97` |
| 300+ | Hazardous | 🟤 `#7E0023` |

This palette is the single source of truth used consistently across the map markers, charts, legends, pollutant bars, and safety cards.

---

## 🔌 API Reference

All endpoints accept `lat` and `lon` query parameters (default: Philadelphia `39.9526, -75.1652`).

| Method | Endpoint | Returns |
|---|---|---|
| `GET` | `/api/` | API health check + endpoint catalog |
| `GET` | `/api/air-quality` | Nearby OpenAQ stations with AQI, level, pollutant measurements |
| `GET` | `/api/weather` | Current conditions + 24h forecast |
| `GET` | `/api/tempo` | NASA TEMPO NO₂ column, derived AQI, freshness & product metadata |
| `GET` | `/api/forecast` | 6-hour AQI predictions + weather-impact explanations |
| `GET` | `/api/safety-groups` | Per-group safety status + best/worst time windows |
| `GET` | `/api/ai-summary` | GPT-generated daily air-quality brief |
| `POST` | `/api/ai-chat` | Conversational AI response (body: `message`, `session_id`, `lat`, `lon`) |

<details>
<summary><b>Example: <code>GET /api/tempo?lat=39.95&lon=-75.16</code></b></summary>

```json
{
  "status": "success",
  "tempo": {
    "no2_column": 4.21e15,
    "aqi": 58,
    "latitude": 39.948,
    "longitude": -75.161,
    "source": "NASA TEMPO",
    "available": true,
    "freshness": {
      "observation_time_utc": "2025-10-04 16:44:23 UTC",
      "age_hours": 12.3,
      "status": "Cached",
      "status_emoji": "🔶",
      "shutdown_note": "NASA data portal updates paused due to federal funding lapse"
    },
    "metadata": {
      "product_name": "TEMPO L2 NO2",
      "product_version": "V04",
      "satellite": "NASA TEMPO (Geostationary)",
      "spatial_resolution": "2-8 km",
      "orbit_type": "Geostationary (35,786 km altitude)",
      "units": "molecules/cm²"
    }
  }
}
```
</details>

---

## 🛠️ Tech Stack

<table>
<tr><td valign="top" width="50%">

### Backend
- **Python 3.11**
- **Flask 3.0** + **flask-cors** — API & static serving
- **OpenAI 1.51** (`gpt-4o-mini`) — generative layer
- **netCDF4 1.6** + **NumPy 1.26** — satellite science
- **requests** — external API I/O
- **python-dotenv** — config
- **Gunicorn 21.2** — production WSGI server

</td><td valign="top" width="50%">

### Frontend
- **Vanilla JS (ES6+)** — zero framework, zero build step
- **Google Maps JS API** + Visualization library
- **Chart.js** — forecast & weather graphs
- **Glassmorphism CSS** — custom design system, animated gradient orbs, dark theme
- **Font Awesome 6** + **Inter** typeface

</td></tr>
<tr><td valign="top">

### Data Sources
- 🛰️ **NASA TEMPO** L2 NO₂ (Earthdata)
- 📡 **OpenAQ v3** ground network
- 🌤️ **OpenWeather 2.5**

</td><td valign="top">

### Infra / DevOps
- ☁️ **Azure App Service** (Production slot)
- 🗄️ **Azure Blob Storage** — TEMPO granule cache
- ⚙️ **GitHub Actions** — CI/CD on push to `main`

</td></tr>
</table>

---

## 📁 Project Structure

```
aircast-nasa-hackathon/
├── backend/
│   ├── app.py                  # Flask app: 8 endpoints, AI orchestration, static server
│   ├── api/
│   │   ├── tempo.py            # NASA TEMPO NetCDF ingestion + freshness/metadata
│   │   ├── openaq.py           # OpenAQ ground stations + EPA AQI conversion
│   │   └── weather.py          # OpenWeather current + forecast
│   ├── models/
│   │   ├── forecast.py         # Physics-informed 6-hr AQI projection + reasoning
│   │   └── user_groups.py      # Five-profile safety threshold engine
│   ├── test_openai.py          # OpenAI connectivity smoke test
│   └── requirements.txt
├── frontend/
│   ├── index.html              # Single-page glassmorphism UI
│   ├── css/style.css           # 1,800+ lines of custom design system
│   └── js/map.js               # 1,300+ lines: map, charts, fusion, chat
├── .github/workflows/
│   └── main_aircast.yml        # Azure CI/CD pipeline
├── startup.sh                  # Gunicorn launch (port 8000, 600s timeout)
└── requirements.txt
```

---

## 🚀 Running AirCast Locally

### Prerequisites
- Python 3.11+
- API keys (all optional — app degrades gracefully without them)

### 1. Clone & install

```bash
git clone https://github.com/allenvarghese05/aircast-nasa-hackathon.git
cd aircast-nasa-hackathon
pip install -r requirements.txt
```

### 2. Configure environment

Create `backend/.env`:

```bash
OPENAI_API_KEY=sk-...                # AI brief & chat
OPENWEATHER_API_KEY=...              # live weather
OPENAQ_API_KEY=...                   # higher rate limits (optional)
TEMPO_BLOB_URL=https://...nc         # defaults to bundled granule
```

> 🔑 You'll also want a **Google Maps JS API key** with the *Maps JavaScript* + *Geocoding* APIs enabled, set in `frontend/index.html`.

### 3. Run

```bash
cd backend
python app.py
# → http://localhost:8000   (frontend + API on one port)
```

Or production-style with Gunicorn:

```bash
./startup.sh
```

---

## ☁️ Deployment

AirCast ships to **Azure App Service** via **GitHub Actions** (`.github/workflows/main_aircast.yml`). On every push to `main`:

1. **Build** — checkout, set up Python 3.11, install dependencies, package artifact.
2. **Deploy** — push to the Azure Web App `aircast` (Production slot) via publish profile.

The runtime entrypoint is `startup.sh`, which binds Gunicorn to `0.0.0.0:8000` with a 600-second timeout to accommodate the large NetCDF download on cold start.

---

## 🛡️ Resilience by Design

AirCast was engineered to **never show a broken screen**, a principle proven under fire during the government shutdown:

- ✅ Every external call is wrapped in try/except with realistic fallback data
- ✅ Missing API keys are detected and degrade to synthetic/cached responses
- ✅ AI endpoints return HTTP 200 with friendly fallbacks even on failure
- ✅ TEMPO data freshness is transparently surfaced, never silently stale
- ✅ The map always renders stations; the forecast always has weather; the brief always has something kind to say

---

## 👥 Authors

<div align="center">

**Team Relentless** · 2025 NASA Space Apps Challenge · 🏆 Global Nominee

| [Aahil Afraz](https://github.com/) | [Allen Varghese](https://github.com/allenvarghese05) |
|:---:|:---:|
| Full-stack · Data fusion · AI integration | Full-stack · Backend · Cloud/DevOps |

*Top 1,219 of 11,500+ teams worldwide · 11,500+ projects submitted*

</div>

---

<div align="center">

### 🌍 Built so anyone can answer one question: *"Is the air okay right now?"*

*From a satellite 35,786 km in space to the sidewalk under your feet.*

⭐ **Star this repo if AirCast helped you breathe a little easier.**

</div>
