# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

**Travel Explorer** — a single-file static travel guide web app (`index.html`). No build tools, no framework, no backend. Open the file directly in a browser.

## Running locally

```
Start-Process "c:\Users\patri\PROJECT\index.html"
```

Or drag `index.html` into any browser. No server required — all features work over `file://` except the Weather widget (which requires an OpenWeather API key regardless).

## Architecture

Everything lives in one file: `index.html`. It is divided into three logical blocks:

### 1. `<style>` — Design system
CSS custom properties at `:root` define the full design token set (`--navy`, `--gold`, `--light`, `--radius`, `--ease`, `--shadow`). All component styles follow below. Responsive breakpoints at `960px`, `768px`, and `580px`.

### 2. `<body>` — Static shell + section anchors
The HTML contains the nav, hero, and section wrappers. **City cards, modals, the safety accordion, and the currency grid are all rendered dynamically by JS** — do not add them to the HTML directly.

Anchor IDs used by nav links: `#home`, `#enquiry-form-section`, `#guides`, `#tools`, `#weather`, `#currency`, `#safety`.

### 3. `<script>` — Data + render functions

**Data arrays (edit these to update content):**
- `cities[]` — 12 city objects. Each has: `id`, `name`, `country`, `flight`, `budget`, `budgetDefault`, `season`, `risk`, `img` (Unsplash URL), `desc`, `overview`, `itinerary[]`, `food[]`, `transport`, `costs[][]`, `safetyTips[]`, `photos[]`, `scams`, `emergency`, `hospital`.
- `currencies[]` — exchange rate table (SGD base). Update `rate` values to refresh rates.
- `packItems{}` — packing checklist categories and items.

**Render functions (called once on page load):**
- `renderCards()` → injects city cards into `#cardsGrid`
- `renderModals()` → injects modal HTML into `#modalsContainer`
- `renderSafety()` → injects accordion into `#safetyAccordion`
- `renderCurrencyGrid()` → injects currency items into `#curGrid`
- `renderChecklist()` → injects packing list into `#checklistGrid`
- `renderItinerary()` → renders itinerary table from `localStorage`

**localStorage keys:**
- `travelEnquiries` — array of submitted enquiry objects
- `packList` — object of `"Category_index": boolean` for checklist state
- `travelItinerary` — array of itinerary row objects

## Weather API

The weather widget is stubbed. To enable it:
1. Get a free key at `openweathermap.org/api`
2. Set `OPENWEATHER_API_KEY` at the top of the script block
3. Uncomment the `fetch()` block inside `checkWeather()`

## Adding a city

Add an entry to the `cities[]` array following the existing object shape. The card, modal, safety accordion entry, and budget calculator dropdown must each be updated — the cards/modals/safety render automatically from the array, but the budget calculator `<select>` in the HTML and the enquiry form destination `<select>` must be updated manually (they are static HTML, not rendered from `cities[]`).

## Images

All images use Unsplash. Format: `https://images.unsplash.com/photo-{id}?w=800&q=80`. Modal images use `w=1200`. Use `images.unsplash.com/photo-{id}` (not `source.unsplash.com`) for stable, non-redirecting URLs.
