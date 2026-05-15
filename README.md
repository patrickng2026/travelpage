# Travel Explorer

> We went, so you know where to go.

A modern single-page travel guide website for curated Asian city guides, travel tools, weather lookup, currency conversion, safety notes, and travel enquiries.

![Travel Explorer](screenshot.png)

🌐 **Live Site:** [patrickng2026.github.io/travelpage](https://patrickng2026.github.io/travelpage/)

---

## Features

- **12 City Guides** — Seoul, Tokyo, Bali, Bangkok, Singapore, Hong Kong, Kuala Lumpur, Maldives, Phuket & Krabi, Sydney, Taipei, Hanoi
- **Guide Modals** — 3-day itineraries, food picks, transport tips, cost breakdowns, safety tips, and photo spots per city
- **Trip Budget Calculator** — estimate total trip cost in SGD by destination, days, and travellers
- **Packing Checklist** — categorised checklist with persistent state via localStorage
- **Itinerary Planner** — add and save day-by-day travel plans
- **Weather Widget** — OpenWeather API integration (bring your own free key)
- **Currency Converter** — SGD to 9 currencies with live input
- **Safety Notes** — per-city risk ratings, scam alerts, and emergency contacts
- **Enquiry Form** — validated form with localStorage submission storage

## Tech Stack

- Pure HTML, CSS, JavaScript — no frameworks, no build tools
- Google Fonts (Playfair Display + Inter)
- Unsplash images
- localStorage for persistence
- OpenWeather API (optional)

## Run Locally

Open `index.html` directly in any browser — no server required.

## Weather API Setup

1. Get a free key at [openweathermap.org/api](https://openweathermap.org/api)
2. Open `index.html`, find `OPENWEATHER_API_KEY = "YOUR_API_KEY_HERE"`
3. Replace with your key and uncomment the `fetch()` block below it
