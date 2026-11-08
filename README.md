# FreshFind — React (Vite) SPA

A modern React + Vite conversion of the original vanilla HTML/CSS/jQuery
FreshFind farmers-market app. All original features are preserved:

- Auth gate (sign up / log in / Google / guest), persisted in `localStorage`
- Sticky navbar with light/dark theme toggle
- Home page: hero, live clock, open-markets count, quick market finder
- Market directory with search + "open now" filter
- Market detail page: schedule table, product grid, embedded map
- Price comparison table across all markets for any product
- No-Waste basket calculator (finds the cheapest market for a scaled basket)
- Produce guide with category filters
- Seasonal recommendations
- Weight & price calculator modal (global, reachable from any product card)
- Bookmarks (favorites) sidebar with notes and print/export
- Contact page with embedded Google Map

## Getting started

```bash
npm install
npm run dev
```

Then open the printed local URL (typically http://localhost:5173).

To build for production:

```bash
npm run build
npm run preview
```

## Structure

```
src/
  main.jsx              # app entry (Router + AppProvider)
  App.jsx                # routes + layout chrome
  index.css              # global styles (ported from style.css)
  context/AppContext.jsx # global state: data, theme, bookmarks, auth, calculator
  hooks/useLocalStorage.js
  utils/market.js         # open/closed logic, produce image lookup
  data/*.json             # markets, produce, seasonal data (bundled at build time)
  components/             # Navbar, Footer, AuthOverlay, BookmarksSidebar,
                           # WeightCalculatorModal, MarketCard, ProduceCard, ScrollToTop
  pages/                  # Home, Markets, MarketDetail, Compare, NoWaste,
                           # Produce, Seasonal, Contact, About
```

## Notes on the conversion

- Routing now uses `react-router-dom` (real URLs like `/markets/market-1`)
  instead of the old `#hash` router.
- Global app state (theme, bookmarks, auth, catalog data) lives in
  `AppContext` instead of the old `window.FreshApp` object and jQuery DOM
  manipulation.
- The `markets.json` / `produce.json` / `seasonal.json` files are imported
  directly as ES modules and bundled by Vite, so the old `fetch()` +
  embedded-fallback-dataset trick (needed to work around `file://` CORS
  restrictions) is no longer necessary.
- Font Awesome and Google Fonts are still loaded via CDN `<link>` tags in
  `index.html`, exactly as before.
