# Ferð Frontend Client

## Project Title
Ferð — Frontend UI

## Description
The Ferð frontend is a **static‑site client** built with vanilla HTML, CSS, and JavaScript. It provides a responsive, mobile‑first UI for discovering travel destinations, filtering them, and viewing detailed information. During local development a tiny **Node.js proxy server** (`frontend/server.js`) runs on port 3000 and forwards any request that starts with `/api/` to the backend API at `http://localhost:4000/api`. This removes CORS concerns and lets the UI use relative URLs (`/api/destinations`). In production the static files can be hosted on any CDN (Netlify, Vercel, GitHub Pages, etc.) and the UI will call the backend directly.

## File Structure (high‑level)
```
frontend/                     # Project root for the UI
├─ index.html                # Landing / discovery page (home)
├─ README.md                 # (this file)
├─ server.js                 # Tiny Node proxy – serves static files & forwards /api/*
├─ package.json              # npm scripts (start) – no external deps needed
├─ css/                      # Design‑system style sheets
│  ├─ main.css               # Unified typography, variables, layout helpers
│  ├─ variables.css          # Color tokens, spacing, font sizes
│  ├─ layout.css             # Grid & flex layout utilities
│  ├─ components.css         # Reusable component styling (cards, buttons, etc.)
│  └─ responsive.css        # Mobile‑first media queries
├─ js/                       # Modular UI logic (ES6 modules)
│  ├─ main.js                # Navigation drawer, router, UI initialization
│  ├─ featured.js            # Loads destination data from the API and renders the "featured" cards
│  ├─ destination-details.js# Loads a single destination (via `?id=`) and builds the detail view
│  ├─ filters.js             # Search, budget, interest, and season filters – builds query string for the API
│  ├─ favorites.js           # LocalStorage‑based bookmark persistence (add/remove favorites)
│  └─ recommendations.js     # Recommendation quiz UI and calls the `/api/recommendations` endpoint
├─ assets/                    # Images, SVG icons, and static media used by the UI
│  └─ images/                # Destination SVGs, photos, branding assets
├─ data/                     # Legacy backup JSON (not used at runtime)
│  └─ destinations.json      # Original static data source – UI now calls the backend API
└─ pages/                    # Individual HTML pages (loaded via the router)
   ├─ explore.html            # Main "Explore" page – grid of destination cards
   ├─ destination.html        # Destination detail view (populated via JS)
   ├─ favorites.html         # Saved/bookmarked destinations (reads from LocalStorage)
   ├─ about.html             # About / methodology page
   └─ food-culture.html      # Culinary & cultural highlights page
```

## Site Map (client‑side navigation)
| Page | URL (relative) | Purpose |
|------|----------------|----------|
| **Home / Landing** | `/` (served by `index.html`) | Brief intro and quick link to the Explore page |
| **Explore** | `/pages/explore.html` | Grid of destination cards, filter bar, search bar – pulls data from `GET /api/destinations` |
| **Destination Detail** | `/pages/destination.html?id=<id>` | Shows full details for a single destination (overview, images, attractions, local food, etc.) |
| **Favorites** | `/pages/favorites.html` | Lists destinations the user has bookmarked via `favorites.js` (stored in `localStorage`) |
| **About** | `/pages/about.html` | Project description, data source, methodology |
| **Food & Culture** | `/pages/food-culture.html` | Highlights culinary and cultural information for the destinations |

All navigation is handled by `js/main.js` which intercepts clicks on `<a>` elements and swaps the `<main>` content without a full page reload (single‑page‑app feel). The router respects the `?id=` query parameter for the detail view.

## How the Proxy Works (`frontend/server.js`)
```js
// When a request path begins with /api/ the server creates an HTTP request
// to the backend (default localhost:4000). It forwards method, headers, and body
// and streams the response back to the browser. Static assets (HTML, CSS, JS,
// images) are served directly from the filesystem.
```
The proxy adds the header `Access-Control-Allow-Origin: http://localhost:3000` so the browser can safely call the API during development.

## How to Run (local development)
```bash
# 1️⃣ Install (optional – creates a node_modules folder for the proxy script)
cd "c:/Users/8319j/OneDrive/Documents/jana project/Ferð/fero final/frontend"
npm ci

# 2️⃣ Make sure the backend API is running (see backend README) on http://localhost:4000

# 3️⃣ Start the frontend proxy
npm start   # runs `node server.js` → http://localhost:3000
```
Open a browser and navigate to:
```
http://localhost:3000
```
You should see the landing page, be able to click **Explore**, and the UI will fetch live destination data from the backend.

### Environment variables (optional)
| Variable | Default | Meaning |
|----------|---------|---------|
| `PORT` | `3000` | Port on which the proxy server listens |
| `BACKEND_PORT` | `4000` | Port of the backend API that the proxy forwards `/api/*` to |
You can override them by creating a `.env` file in the `frontend/` folder (the server reads them via `dotenv`).

## Production deployment
1. **Static host** – upload the entire `frontend/` directory (except `server.js` and `package.json`) to any static‑file CDN (Netlify, Vercel, GitHub Pages, etc.).
2. **Backend URL** – in production the proxy is unnecessary. Replace the `window.FERD_API_BASE_URL` value in `js/featured.js` (or set it via an environment variable) with the live backend endpoint, e.g., `https://api.myferd.com/api`.
3. **Optional – keep the proxy** – if you still want a simple Node server in production (e.g., on Render), just set `PORT` and `BACKEND_PORT` accordingly and deploy the server as a small Node service.

---
