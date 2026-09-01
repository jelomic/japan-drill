# 🗾 Japan Drill — offline survival-Japanese trainer

A single-file, offline-first PWA for cramming **katakana reading** and
**~60 survival phrases** before a trip. Vanilla JS/CSS, no build step, no
framework, no CDN. All progress is stored in `localStorage`; once loaded, it
runs with **zero network**.

## Files

| File | Purpose |
|------|---------|
| `index.html` | The whole app — content, UI, spaced-repetition engine |
| `sw.js` | Service worker (cache-first, offline) |
| `manifest.json` | PWA manifest (installable, standalone) |
| `icon.svg` | App icon |

## What's inside

- **Katakana** — all 46 base + dakuten/handakuten + yōon combos (キャ etc), 104 total.
- **Numbers & money** — 1–10, 100, 1,000, 10,000, 円, people/night counters, time words.
- **60 phrases** across 6 scenarios: greetings, shopping, trains/directions,
  hostel, restaurant, temple etiquette.

### Modes
- **Katakana drill** — see the character, type romaji, instant feedback, timed;
  per-character accuracy tracked (see it under Browse → Katakana). Typing is
  tolerant of alternates (`si`=`shi`, `tu`=`tsu`, macrons, case, spaces).
- **Recognition** — romaji shown, pick the correct kana from 6 options.
- **Phrases & numbers** — English prompt, tap to reveal Japanese, self-grade
  **Again / Good / Easy**.
- **Browse** — filterable list by scenario tag, for reading on a train.

### Scheduling
- **SM-2 spaced repetition** with per-item interval + ease factor.
- Daily session **capped at 15 minutes** (or when the queue empties).
- **Streak** counter and **cards due today** on the home screen.
- **Weekly unlocks**: katakana weeks 1–2, numbers week 3, phrases weeks 4–6,
  counted from a start date you can edit. **Override any lock** in ⚙️ Settings
  (per category or "unlock everything now").

Set your start date in Settings so the weekly ramp lines up with your trip
(e.g. set it ~6 weeks before 20 Oct, or just tap "Unlock everything now").

## Run it locally

A service worker needs `http(s)` — it won't register from `file://`. Serve the
folder over localhost with any static server:

```bash
cd japan-drill

# Python (already on macOS)
python3 -m http.server 8000

# …or Node
npx serve .
```

Open <http://localhost:8000> and load it once online. After that it works
offline. On your phone: open the URL in the browser, then **Add to Home Screen**
to install it as a standalone app.

## Deploy to GitHub Pages

1. Create a repo and push these files to the repo root (or a `/docs` folder):
   ```bash
   git init
   git add .
   git commit -m "Japan Drill PWA"
   git branch -M main
   git remote add origin https://github.com/<you>/<repo>.git
   git push -u origin main
   ```
2. On GitHub: **Settings → Pages → Build and deployment → Source: Deploy from a
   branch**, pick `main` and `/ (root)`, save.
3. Wait ~1 minute, then open `https://<you>.github.io/<repo>/`.
4. Load once, then use offline / install to home screen.

> Paths in `index.html`, `sw.js`, and `manifest.json` are all **relative**
> (`./…`), so it works whether served from a domain root or a project subpath.

## Data & privacy

Everything is local to your browser. Settings → Data lets you **export**
progress (copies JSON to clipboard) or **reset** all progress. Clearing browser
site data or uninstalling will erase your streak and review history.
