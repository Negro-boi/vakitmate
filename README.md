# 🌙 Vakitmate

> A beautifully designed, installable Progressive Web App for Ramadan prayer times, Qibla direction, fasting progress, and the full Ramazan calendar — built for Turkish cities with real-time API data.

![Vakti Preview](https://img.shields.io/badge/PWA-Ready-d4a44c?style=flat-square&logo=pwa) ![Offline](https://img.shields.io/badge/Offline-Supported-50c87a?style=flat-square) ![API](https://img.shields.io/badge/API-Aladhan.com-7ab4e0?style=flat-square) ![License](https://img.shields.io/badge/License-MIT-white?style=flat-square)

---

## ✨ Features

### 🕌 Prayer Times
- Real-time prayer times via the **Aladhan API** (Diyanet İşleri Başkanlığı method)
- Live countdown to the next prayer, updated every second
- Active prayer highlighted with a glowing indicator

### 📍 City & Geolocation
- 8 major Turkish cities in the dropdown (İstanbul, Ankara, İzmir, Bursa, Antalya, Adana, Konya, Gaziantep)
- **Auto-detect location** via browser geolocation for precise local times
- Instantly re-fetches all data when city or location changes

### 🍽️ Fasting Progress
- Visual progress bar from Sahur (Imsak) to İftar (Maghrib)
- Shows elapsed time, remaining time, and total fast duration
- Status updates automatically (before sahur / fasting / completed)

### 🧭 Qibla Compass
- Mathematically accurate Qibla bearing calculated from your coordinates
- Animated SVG compass needle that rotates to the correct direction
- Shows distance to Mecca and exact coordinates

### 📅 Ramazan Calendar
- Full 30-day calendar for Ramazan 1447H (Feb 18 – Mar 19, 2026)
- All 6 prayer times per day fetched from the API
- Today's row is highlighted and auto-scrolled into view
- Hijri dates shown alongside Gregorian dates

### 📱 Progressive Web App
- Fully installable on iOS and Android via "Add to Home Screen"
- Install prompt banner shown automatically on supported browsers
- Runs in standalone mode (no browser UI)
- Works offline using a cached app shell and stored API responses

### 🔌 Offline Support
- Service worker caches the full app on first load
- API responses cached in both the service worker cache and `localStorage`
- Falls back gracefully to saved times when there's no internet
- Online/offline status banners keep the user informed

---

## 📁 File Structure

```
vakti-pwa/
├── index.html      # Main app — all UI, logic, and styles
├── sw.js           # Service worker — caching & offline support
├── manifest.json   # PWA manifest — install metadata & icons
└── icon.svg        # App icon — crescent moon & star
```

---

## 🚀 Getting Started

### Option 1 — Open Locally
Just open `index.html` in a browser. Basic features work immediately.

> ⚠️ Service workers and geolocation require HTTPS or `localhost`. For full PWA features, use a local server or deploy online.

### Option 2 — Local Server (recommended for dev)

**Using Python:**
```bash
cd vakti-pwa
python3 -m http.server 8080
# Open http://localhost:8080
```

**Using Node.js:**
```bash
npx serve vakti-pwa
```

### Option 3 — Deploy (full PWA features)

Upload all 4 files to any static hosting provider that supports HTTPS:

| Platform | Command / Method |
|---|---|
| **Netlify** | Drag & drop the `vakti-pwa/` folder at netlify.com/drop |
| **Vercel** | `vercel --cwd vakti-pwa` |
| **GitHub Pages** | Push to a repo, enable Pages in Settings |
| **Cloudflare Pages** | Connect repo or upload folder |

Once deployed over HTTPS:
- ✅ Service worker activates
- ✅ Geolocation works
- ✅ Install prompt appears on Android/Chrome
- ✅ Offline mode fully functional

---

## 🔌 API

Prayer times are fetched from the free **[Aladhan API](https://aladhan.com/prayer-times-api)**.

| Endpoint | Usage |
|---|---|
| `/v1/timings` | Today's prayer times by lat/lng |
| `/v1/calendar/{year}/{month}` | Full month calendar by lat/lng |

**Calculation method:** `13` — Diyanet İşleri Başkanlığı (Turkey)

No API key required. Rate limits are generous for personal use.

### Caching Strategy
- API responses are cached in the **service worker cache** (network-first, 6-hour TTL)
- Additionally stored in **`localStorage`** as a secondary fallback
- Offline users see the last successfully fetched data with a clear status banner

---

## 🧭 Qibla Calculation

Qibla bearing is calculated locally using the **Great Circle formula** — no external API required:

```
ΔL = mecca_lng - user_lng
y  = sin(ΔL) × cos(mecca_lat)
x  = cos(user_lat) × sin(mecca_lat) − sin(user_lat) × cos(mecca_lat) × cos(ΔL)
bearing = atan2(y, x) converted to degrees [0–360]
```

Mecca coordinates used: `21.3891°N, 39.8579°E`

---

## 🎨 Design

| Element | Detail |
|---|---|
| **Color palette** | Deep navy `#060912` background with `#d4a44c` gold accents |
| **Typography** | Cinzel (display) + Nunito (body) from Google Fonts |
| **Background** | Animated star canvas rendered via `requestAnimationFrame` |
| **Footer** | SVG mosque silhouette |
| **Icons** | Handcrafted inline SVG for each prayer time |
| **Animations** | CSS keyframes for load-in, pulsing active dot, shimmer skeletons |

---

## 🗺️ Supported Cities

| City | Latitude | Longitude |
|---|---|---|
| İstanbul | 41.0082°N | 28.9784°E |
| Ankara | 39.9208°N | 32.8541°E |
| İzmir | 38.4237°N | 27.1428°E |
| Bursa | 40.1885°N | 29.0610°E |
| Antalya | 36.8841°N | 30.7056°E |
| Adana | 37.0000°N | 35.3213°E |
| Konya | 37.8746°N | 32.4932°E |
| Gaziantep | 37.0662°N | 37.3833°E |

Any location worldwide is supported via the **geolocation button**.

---

## 📲 Installing on Mobile

### Android (Chrome)
1. Open the app in Chrome
2. Tap the gold **"Ana Ekrana Ekle"** banner at the bottom
3. Tap **"Ekle"** in the system prompt

### iOS (Safari)
1. Open the app in Safari
2. Tap the **Share** button (box with arrow)
3. Scroll down and tap **"Add to Home Screen"**
4. Tap **"Add"**

---

## 🛣️ Roadmap

- [ ] Prayer time notifications / alarms
- [ ] Daily Quran verse or Hadith
- [ ] Dark / light mode toggle
- [ ] Laylatul Qadr countdown (27th night)
- [ ] Multi-language support (Arabic, English)
- [ ] Completed prayer tracker
- [ ] Share daily times via WhatsApp
- [ ] Weather at iftar time

---

<div align="center">
  Built with 🌙 for Ramazan 1447H &nbsp;·&nbsp; <strong>Vakti</strong>
</div>
