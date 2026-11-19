# القطّة (Qatta)

Web app for splitting a pooled expense ("قطّة") among friends. Live at https://meshal00010-boop.github.io/qatta/ (GitHub Pages, branch `main`, root).

## How it works
1. The owner creates a pool and sets a deadline for the vote. Friends vote "معكم" or "أعتذر", like a WhatsApp poll. The owner is counted in "معكم" automatically and doesn't vote.
2. When the vote closes, the owner buys the items and logs them (item + price). Others can log what they paid from their own pocket.
3. The app splits the total. Everyone settles with the owner only (the owner is the hub). It tracks who has transferred. Finished pools move to the "المنتهية" tab.

## Files
- `index.html`: the whole app in one file. Plain HTML/CSS/JS, no framework. RTL Arabic, font IBM Plex Sans Arabic, inline SVG icons.
- `config.js`: the Firebase web config for project `qatta-6789e`. This config is public by design.
- `firestore.rules`: security rules. Publish them in the Firebase console after any change.
- `og.png`: the WhatsApp preview image.
- `icon-180/192/512.png`: the app icons.
- `manifest.json`: makes the site installable as a PWA.

## Tech
- **Firebase:** anonymous auth plus Firestore, modular SDK 10.12.2 loaded by dynamic import. When there is no config, the app falls back to `localDB()`, which uses localStorage key `qatta-v2` and exposes the same API.
- **Firestore data:**
  - `dinners/{id}`: `{title, place, lat, lng, cat, until, phase: vote|shop|pay, by, at}`
  - `dinners/{id}/people/{k}`: `{uid, nick, going, items[{n,p}], acct, paid{}, req, rej, photo}`
  - `users/{uid}`: `{pools[], name, photo}`
- **Layout:** app shell. `body` is fixed. `#scr` is the scroller. The tab bar sits in the normal flow, solid, never translucent.
- **Maps:** Leaflet with OSM tiles, plus an Esri satellite toggle and Nominatim search. Location links open Google Maps.
- **i18n:** Arabic is the source language. English comes from the `EN` dictionary, the `ENP` regex patterns and a MutationObserver. Use Latin digits.
- **Settings:** the theme, background and card colour are stored in localStorage (`qatta-theme`, `qatta-bg`, `qatta-surf`).
- **Logo:** a bimetal coin with a gold ring and a silver centre. The centre says "قطّة" in the Lalezar font. The ring is engraved with "اجمعها • قسّمها • حوّلها".

## Owner's preferences (important)
- Talk to him in short Gulf Arabic. Give the summary only and skip long explanations.
- He wants a polished UI that feels like an Apple app. Calm green, ivory and gold.
- Use no explanatory text or secondary labels. The layout must explain itself.
- Keep share messages short and the same on WhatsApp, Snapchat and Telegram. Put the pool link on the first line so WhatsApp shows the preview card.
- When a request is unclear, discuss it with him before building.
- He works from an iPhone only. Test on mobile sizes, with iOS Safari in mind.
