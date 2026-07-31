# PulseMap — Application Documentation

**PulseMap** is a modern, single-page web application designed for real-time global anonymous thought sharing and location-based visualization. Users anywhere in the world can publish posts without authentication, attach geographical coordinates via an interactive location picker, and search for content across a dark-themed world map featuring animated glowing green markers.

---

## 🌟 Key Features

### 1. 🔍 Keyword Search & Interactive World Map
- **Real-Time Keyword Filtering**: Type any search query (e.g. `coffee`, `code`, `music`, `sunset`, `tech`) to filter posts in real time.
- **Dynamic Green Dot Markers**: Matching posts are rendered on an interactive CartoDB Dark Matter map as glowing, pulsing green dots (`.green-pulse-marker`).
- **Map Focus & Fly-To**: Clicking any post card in the synchronized feed animates the world map (`worldMap.flyTo`) directly to the post's location with zoom.
- **Preset Query Chips**: Quick-access chips to instantly search popular keywords or display all global pulses.

### 2. 📝 Anonymous Post Creation & Location Picker Map
- **Zero Authentication Required**: Anyone can submit a post instantly without registration.
- **Custom Alias & Category Tagging**: Add an optional nickname and select from categories like *Tech*, *Daily Life*, *Music*, *Food*, or *Local Events*.
- **Interactive Location Pinning**: Click anywhere on the dedicated location picker map to pin latitude and longitude coordinates.
- **Auto-Detect Geolocation**: Uses browser `navigator.geolocation` and Nominatim reverse geocoding to automatically resolve city/country names.
- **Quick Location Presets**: One-tap location presets for global hubs (Tokyo, NYC, London, Paris, Sydney, Mumbai).

### 3. 📱 Mobile-Oriented UI & Ergonomics
- **Fixed Mobile Bottom App Bar**: Seamless bottom navigation on mobile devices with tabs for **Search Map**, **+ New Pulse (FAB)**, and **Pulse Feed**.
- **Touch-Optimized Elements**: Input font sizes fixed at `16px` to prevent unwanted auto-zooming on mobile viewports.
- **Swipeable Chip Containers**: Touch horizontal scrolling for category chips and location presets.
- **Viewport Safe-Area**: Full iPhone and Android notch/safe-area support (`env(safe-area-inset-bottom)`).

### 4. 💾 LocalStorage Persistence
- **Offline & Local Sync**: Posts automatically persist in browser `localStorage`.
- **Pre-populated Seeds**: Loaded with 15 global seed posts across major world cities upon first launch.

---

## 🏗️ Architecture & Technology Stack

| Component | Technology / Library | Description |
| :--- | :--- | :--- |
| **Frontend Standard** | Vanilla HTML5 / CSS3 / ES6 JS | Zero build step; single-file execution |
| **Styling & Design** | Vanilla CSS (Dark Glassmorphism) | Custom CSS variables, background image integration |
| **Interactive Map** | Leaflet.js (v1.9.4) | Map engine using CartoDB Dark Matter tiles |
| **Icons & Typography** | FontAwesome 6.4 & Google Fonts | Inter & Outfit font families |
| **Data Storage** | Browser `localStorage` | Client-side data management |

---

## 📁 Project Directory Layout

```
PulseMap/
├── index.html          # Monolithic application file (HTML, CSS, JS)
├── image.png           # Full-page fixed background wallpaper
└── DOCUMENTATION.md    # System & developer documentation
```

---

## 🚀 Getting Started

### Prerequisites
- Any modern web browser (Google Chrome, Mozilla Firefox, Apple Safari, Microsoft Edge).
- No web server setup required (runs directly via `file://` protocol or any standard HTTP server like Live Server or `python3 -m http.server`).

### Running the Application
1. Open the project folder `/home/user/Downloads/PulseMap/`.
2. Double-click `index.html` or open it directly in your web browser:
   ```bash
   file:///home/user/Downloads/PulseMap/index.html
   ```

---

## 🛠️ Codebase Overview & API Reference

### Key JavaScript Functions

| Function Name | Description |
| :--- | :--- |
| `switchView(viewName)` | Toggles between `'search'` view panel and `'post'` creation panel, updating header pills & mobile bottom nav. |
| `initWorldMap()` | Initializes Leaflet world map centered at `[20, 0]` with CartoDB Dark Matter tile layer. |
| `initPickerMap()` | Initializes Leaflet location picker map with click listener to drop pins & resolve reverse geocoding. |
| `updateWorldMapMarkers(posts)` | Clears existing markers and creates glowing green pulsing icons (`createGreenPulseIcon()`) for matching posts. |
| `submitPulsePost()` | Validates post form input, captures selected coordinates, appends post to state, saves to `localStorage`, and updates map. |
| `detectUserGeoLocation()` | Triggers browser HTML5 Geolocation API to fetch user's current location and set picker coordinates. |
| `renderPostsFeed(posts)` | Generates dynamic HTML post cards in the feed grid with highlighted search keyword matches. |
| `flyToPostLocation(lat, lng, title)` | Centers the world map on specified coordinates and opens marker popup. |

### CSS Theme Tokens (`:root`)

```css
:root {
    --bg-dark: #090d16;
    --bg-card: rgba(18, 26, 43, 0.75);
    --bg-card-border: rgba(255, 255, 255, 0.08);
    --primary-green: #00ff88;
    --primary-green-glow: rgba(0, 255, 136, 0.35);
    --primary-green-dark: #00b359;
    --accent-blue: #3b82f6;
    --accent-purple: #8b5cf6;
    --text-main: #f3f4f6;
    --text-muted: #9ca3af;
    --font-heading: 'Outfit', sans-serif;
    --font-body: 'Inter', sans-serif;
}
```

---

## 🔒 Security & Performance Notes

- **Input Sanitization**: Includes an `escapeHtml()` helper function to prevent cross-site scripting (XSS) when rendering user-submitted text.
- **Search Highlighting**: Uses safe regular expressions with standard HTML escaping to highlight matching query terms.
- **Performance**: Zero external runtime framework overhead; map markers use lightweight Leaflet `divIcon` CSS animations for smooth rendering even with hundreds of markers.

---

## 📄 License & Credits

- **Leaflet.js**: BSD 2-Clause License
- **CartoDB Dark Matter Tiles**: Map tiles by CARTO under CC BY 3.0
- **Font Awesome**: Free License Icons
