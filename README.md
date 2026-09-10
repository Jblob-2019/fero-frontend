# Ferð — Travel Discovery & Exploration Platform

A modern, responsive web application for discovering personalized travel destinations, exploring regional cultures and cuisines, and planning custom travel itineraries.

---

## 📖 Description

**Ferð** (meaning *journey* or *travel*) helps travelers discover destinations that truly fit their travel style, budget, and pace before committing to an itinerary. 

### Key Features:
- **Personalized Travel Match Quiz:** Interactive quiz ("Find my match") that scores and recommends destinations according to user preferences (pace, budget, climate, interests).
- **Interactive Destination Directory:** Browse and filter destinations dynamically by region, budget, and travel style.
- **Dynamic Destination Details:** Comprehensive destination pages (`/pages/destination.html?id=...`) with local highlights, food guides, and practical travel tips.
- **Favorites & Bookmarks:** Save and manage favorite destinations locally via browser `localStorage`.
- **Food & Culture Guides:** Curated highlights of local street foods, dishes, and cultural etiquette.
- **Modern Lightweight Stack:** Built with semantic HTML5, modern vanilla CSS design tokens, and modular ES6 JavaScript with no heavy front-end framework overhead.
- **Integrated Proxy Server:** Built-in lightweight Node.js HTTP server that serves static client assets and proxies `/api/*` requests to the backend server (port 4000) with static fallback data.

---

## 🚀 How to Run

### Prerequisites
Make sure you have **[Node.js](https://nodejs.org/)** (v16+ recommended) installed on your system.

### 1. Open Terminal in Project Directory
Ensure your terminal / PowerShell is in the project root:
```bash
cd "c:\Users\8319j\OneDrive\Desktop\fero frontend"
```

### 2. Start the Application
Run one of the following commands:

**Standard Start:**
```bash
npm start
```
*Or directly via Node:*
```bash
node server.js
```

**Development Mode (with auto-reload on file changes):**
```bash
npm run dev
```

### 3. Open in Browser
Once started, visit:
👉 **[http://localhost:3000](http://localhost:3000)**

---

## 📂 Project Structure

```
fero-frontend/
├── index.html              # Main Discovery / Landing Page & Hero
├── server.js               # Node.js static & API reverse proxy server (Port 3000)
├── package.json            # Project configuration & npm scripts
├── README.md               # Project documentation
├── pages/
│   ├── explore.html        # Interactive Explore & Filter Directory
│   ├── destination.html    # Dynamic Destination Detail Page (?id=...)
│   ├── favorites.html      # Saved Bookmarks & Shortlist Page
│   ├── about.html          # About & Methodology Page
│   └── food-culture.html   # Culinary & Cultural highlights
├── css/
│   ├── main.css            # Core styles and design system import
│   ├── variables.css       # Design tokens (colors, typography, spacing)
│   ├── layout.css          # Macro layout grids and flex wrappers
│   └── components.css      # Reusable UI component styling
├── js/
│   ├── main.js             # Navigation, drawer, and quiz logic
│   ├── featured.js         # Destination cards and API rendering
│   ├── destination-details.js # Single destination view controller
│   ├── filters.js          # Search, budget, and interest tagging
│   ├── favorites.js        # LocalStorage bookmark manager
│   └── recommendations.js  # Recommendation scoring algorithm
├── assets/
│   └── images/             # Vector SVGs and destination imagery
└── data/
    └── destinations.json   # Static fallback destination dataset
```
