# 🎨 Ikona integrace

Přidal jsem vlastní ikonu (`custom_components/ollama_assistant/brand/icon.png`,
`icon@2x.png`, `logo.png`, `logo@2x.png`) — modro-fialová bublina s vlnkou
hlasu, aby integrace nevypadala jako prázdný šedý čtverec (jako teď
"Room Summary Card" nebo "LLM Vision Card" ve tvém seznamu).

## Kde se ikona zobrazí

- ✅ **Stránka Nastavení → Zařízení a služby** (detail integrace) — funguje
  automaticky od Home Assistant **2026.3+** díky nové funkci "brand/ složka".
  Žádná další konfigurace není potřeba.

## Kde se (zatím) nezobrazí

- ⚠️ **Seznam v HACS** (přesně ten pohled, co je na tvém screenshotu) —
  HACS si ikony bere ze svého vlastního CDN (`data-v2.hacs.xyz`), ne přímo
  z integrace. Pro vlastní/custom integrace mimo oficiální repozitář
  `home-assistant/brands` HACS zatím (k červenci 2026) **neumí** ikonu
  z lokální `brand/` složky převzít — je to známé omezení, sledované v
  [hacs/integration#5171](https://github.com/hacs/integration/issues/5171).

**Shrnutí:** Ikona už reálně existuje a funguje v detailu integrace v HA.
Až HACS doplní podporu pro lokální `brand/` složky (viz odkaz výše), ukáže
se automaticky i v seznamu staženpiny — nebude potřeba nic měnit.
