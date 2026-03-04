# WebOSINT 🔍

> **Open Source Intelligence Terminal** — Phone number reconnaissance tool by [flandreiii](https://github.com/flandreiii)

---

## Overview

**WebOSINT** is a browser-based OSINT tool for phone number intelligence gathering. Enter any international phone number and instantly retrieve country data, timezone, line type, carrier info, region, population, currency, languages, and more — all from a slick terminal-themed interface with no backend required.

No server. No API key. No installation. Just open the HTML file and go.

---

## Features

- 📞 **Phone number parsing** — Supports international format with country code (e.g. `+40 712 345 678`)
- 🌍 **Country intelligence** — Country name, flag, capital, region, subregion
- 🕐 **Timezone detection** — Derived from country code via live API
- 📊 **Demographic data** — Population, currency, official languages
- 📡 **Line type detection** — Mobile, Landline, or VoIP (heuristic)
- ✅ **Validity check** — Detects whether the number format is valid
- ⚡ **Zero dependencies** — Pure HTML + CSS + JavaScript, single file
- 🔑 **No API key needed** — Uses [restcountries.com](https://restcountries.com), a free open CORS API

---

## Preview

```
┌─────────────────────────────────────────┐
│  WEBOSINT        ● SYSTEM ONLINE        │
│  Open Source Intelligence Terminal      │
├─────────────────────────────────────────┤
│  ▶ +40 712 345 678          [ SCAN ]    │
├─────────────────────────────────────────┤
│  Number          +40712345678           │
│  Status          ✓ VALID                │
│  Country         🇷🇴 Romania             │
│  Country Code    +40                    │
│  Line Type       MOBILE                 │
│  Timezone        Europe/Bucharest       │
│  Capital         Bucharest              │
│  Region          Europe / Eastern EU    │
│  Population      19,237,691             │
│  Currency        Romanian leu (lei)     │
│  Languages       Romanian               │
└─────────────────────────────────────────┘
```

---

## Usage

### Option 1 — Open directly

Download `webosint.html` and open it in any modern browser. No setup needed.

### Option 2 — Serve locally

```bash
# Python
python3 -m http.server 8080

# Node.js (npx)
npx serve .
```

Then visit `http://localhost:8080/webosint.html`.

---

## How It Works

WebOSINT uses a **two-step enrichment pipeline**:

**Step 1 — Local prefix parse**
The phone number is matched against a built-in prefix map covering 80+ country codes. This step extracts the country code, national number, ISO2 code, and performs a heuristic line type detection (mobile vs. landline based on number prefix patterns). This works instantly, fully offline.

**Step 2 — Live enrichment via restcountries.com**
Using the ISO2 code from Step 1, a request is made to `https://restcountries.com/v3.1/alpha/{iso2}`. This free, open-CORS API returns rich country metadata: official name, capital, region, subregion, population, currencies, languages, timezones, and flag emoji. No API key is required.

If the network request fails for any reason, the tool still displays all data derived from Step 1 gracefully.

---

## Data Sources

| Source | Type | Key Required |
|---|---|---|
| Built-in prefix map | Phone parsing & line type | ❌ None |
| [restcountries.com](https://restcountries.com) | Country enrichment | ❌ None |

---

## Tech Stack

- **HTML5** — Structure
- **CSS3** — Terminal aesthetic, animations, scanline overlay, CSS variables
- **Vanilla JavaScript** — Fetch API, async/await, DOM manipulation
- **Google Fonts** — `Orbitron` (display) + `Share Tech Mono` (monospace)
- **restcountries.com** — Free REST API, no auth, open CORS

---

## Extending with a Phone API

For even more detailed phone data (carrier name, exact line type, number portability), you can plug in a dedicated phone validation API. Both options below have free tiers:

**AbstractAPI** — [abstractapi.com/api/phone-validation-api](https://www.abstractapi.com/api/phone-validation-api)

```javascript
const r = await fetch(
  `https://phonevalidation.abstractapi.com/v1/?api_key=YOUR_KEY&phone=${phone}`
);
const data = await r.json();
```

**Numverify** — [numverify.com](https://numverify.com)

```javascript
const r = await fetch(
  `http://apilayer.net/api/validate?access_key=YOUR_KEY&number=${phone}`
);
const data = await r.json();
```

Replace the `lookup()` function's Step 2 block in `webosint.html` with either of the above.

---

## Disclaimer

This tool is intended for **educational and research purposes only**. Only look up phone numbers you own or have explicit permission to investigate. The author is not responsible for any misuse of this tool.

---

## Author

Made with 💚 by **[flandreiii](https://github.com/flandreiii)**

---

*WebOSINT — Open Source Intelligence Terminal*
