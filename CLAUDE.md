# FITCENTRUM W.M. – tréningová appka

Osobná Hevy-štýl appka na zapisovanie tréningov pre fitko FITCENTRUM W.M. (Rača, fitcentrum.sk).
Majiteľ (Marek) nie je programátor – komunikuj po slovensky, stručne, a zmeny rovno sprav, otestuj a nahraj.

## Štruktúra
- `index.html` – celá appka v jednom súbore (HTML + CSS + JS, logo a figúrky vložené ako base64).
- `manifest-v2.webmanifest`, `sw.js`, `icon-*.png`, `apple-touch-icon.png`, `logo.png` – PWA (inštalácia na plochu).
- Hosting: GitHub Pages z vetvy `main` – po pushnutí sa zmena prejaví na telefóne za ~2–3 min.

## Ako appka funguje
- Prihlásenie a dáta cez **Supabase** (shim na začiatku `index.html`, objekt `WMAuth`). Emuluje API `window.claude.use("db"|"user")`, na ktoré je napísaný zvyšok appky.
- Úložisko: `Store` (kľúče `catalog/...` = spoločný katalóg strojov, upravuje len admin; `data/users/<uid>` = súkromné dáta používateľa).
- Hlavné časti: `render()` (záložky Tréning / Profil / Tréneri / Nastavenia cez `location.hash`), akcie v objekte `ACT` (delegované cez `data-act`), vysúvacie okná `openSheet` / `closeSheet` / `pushSheet`, potvrdenia `askConfirm`.
- Dizajn: trieda `body.v2` (animovaný), `body.still` (statický), `body.light` (svetlý vzhľad). Preklady: `I18N_RAW` (sk|en|cs|de|pl, presná zhoda textu).
- Úvodná animácia: `#splash`; animácia po prihlásení: `.wmwipe` v `WMAuth`.

## Pravidlá
- Po každej zmene skontroluj syntax JS (napr. vytiahni `<script>` bloky a `node --check`).
- Pri zmene `sw.js` zvýš verziu cache (`const C="wm-vN"`).
- Commit a push na `main`, potom povedz Marekovi, že sa to prejaví o 2–3 min (appku zavrieť a otvoriť).
