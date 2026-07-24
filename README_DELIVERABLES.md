# 📦 AI Asistent (Ollama) v2.1.0 — Kompletní balíček

Tady je vše, co potřebuješ k vydání verze **2.1.0** integrace AI Asistent
pro Home Assistant na HACS.

---

## 📋 Přílohy (v tomto adresáři)

### 🗂️ Hlavní instalační balíček

| Soubor | Velikost | Popis |
|--------|----------|-------|
| **`ollama-ha-assistant-v2_1_0-HACS.zip`** | 77 KB | ✅ **HACS-ready** — úplný balíček s novými HACS soubory, workflows, ikonami a všemi voicemi |
| `ollama-ha-assistant-v2_1_0.zip` | 74 KB | Stará verze bez některých souborů |

### 📖 Dokumentace & Průvodci

| Soubor | Řádky | Téma |
|--------|-------|------|
| **`RELEASE_NOTES_v2_1_0_CZ.md`** | 202 | 🇨🇿 Detailní release notes pro česky hovořící uživatele |
| **`RELEASE_NOTES_v2_1_0_EN.md`** | 203 | 🇬🇧 English version of release notes |
| **`HACS_QUICKSTART.md`** | 92 | ⚡ 3-kroku průvodce instalací skrze HACS |
| **`TELEGRAM_GUIDE.md`** | 117 | 📲 Návod na nastavení hlasu (TTS) a Telegramu |
| **`ICON_POZNAMKA.md`** | 25 | 🎨 Info o vlastní ikoně integrace |

---

## ✨ Novinky v 2.1.0

### 🔄 **Automatický výběr modelů**
```
Staré workflow (2.0.x):
Uživatel → Zadá adresu serveru → Zadá název modelu ✍️

Nové workflow (2.1.0):
Uživatel → Zadá adresu serveru → Asistent načte modely → Vybere ze seznamu ✅
```

### 🔊 **Hlas asistenta (TTS)** — nová funkcionalita
- Výběr TTS enginu v možnostech
- Výběr konkrétního hlasu (např. `cs-CZ-VlastaNeural`)
- Nová služba `ollama_assistant.speak` pro přehrávání textu

### 📲 **Telegram notifikace** — nová funkcionalita
- Automaticky posílá odpovědi asistenta na Telegram
- Integruje se s existující integrací Telegram bot v HA
- Jednoduché zapnutí/vypnutí v možnostech

### 🎨 **Vlastní ikona integrace**
- Modro-fialová bublina se zvukovými vlnami
- Zobrazuje se v detailu integrace (HA 2026.3+)
- V `custom_components/ollama_assistant/brand/`

### 📋 **HACS-ready struktura**
- ✅ GitHub Actions workflows (validate, hassfest, HACS check)
- ✅ hacs.json s topics a metadaty
- ✅ README s HACS badges
- ✅ Brand folder s ikonami
- ✅ Kompletní dokumentace

---

## 🚀 Jak používat

### Instalace

```bash
# 1. Rozbal HACS-ready zip
unzip ollama-ha-assistant-v2_1_0-HACS.zip

# 2. Nakopíruj do GitHub repo:
git clone https://github.com/TVOJE_JMENO/ollama-ha-assistant.git
cd ollama-ha-assistant
cp -r ollama_ha_assistant/* .

# 3. Push to GitHub
git add .
git commit -m "chore: update to v2.1.0 with model selection and TTS"
git push origin main

# 4. Vytvoř tag pro release
git tag 2.1.0
git push origin 2.1.0
```

### HACS instalace (pro uživatele)

1. **HACS → Vlastní repozitáře** → přidej repo
2. **AI Asistent (Ollama)** → Nainstaluj
3. **Nastavení → Zařízení → Přidat integraci**
4. Zadej Ollama adresu → asistent **si sám načte modely**
5. Vyber model ze seznamu → Hotovo! ✅

---

## ✅ Kontrolní seznam (pred publikací)

### Kód & Soubory
- [ ] Všechny .py soubory se kompilují (`python3 -m py_compile`)
- [ ] JSON soubory jsou validní (strings.json, cs.json, en.json, manifest.json, hacs.json)
- [ ] services.yaml je přítomný a správný
- [ ] Brand folder obsahuje: icon.png, icon@2x.png, logo.png, logo@2x.png

### GitHub Actions
- [ ] validate.yml — projde bez chyb
- [ ] hassfest.yml — projde bez chyb
- [ ] hacs.yml — projde bez chyb (ignorovat brands)
- [ ] release.yml — připraven (spustí se na git tag)

### Dokumentace
- [ ] README.md aktualizován
- [ ] CHANGELOG.md má vstup pro v2.1.0
- [ ] TELEGRAM_GUIDE.md existuje
- [ ] HACS_QUICKSTART.md existuje
- [ ] CONTRIBUTING.md je aktuální
- [ ] GITHUB_SETUP.md je aktuální

### Metadata
- [ ] manifest.json: `"version": "2.1.0"`
- [ ] hacs.json: má topics
- [ ] Translations: cs.json a en.json mají všechna nová pole
- [ ] Brand ikony: existují v `brand/` složce

---

## 📊 Statistika Změn v2.1.0

```
Soubory změněné: 12
Soubory přidané: 6
  - services.yaml (nová služba speak)
  - TELEGRAM_GUIDE.md (novinka)
  - HACS_QUICKSTART.md (novinka)
  - ICON_POZNAMKA.md (informace)
  - brand/icon.png, logo.png, atd. (4 ikony)

Řádky přidané: ~500
Řádky smazané: ~100

Nové features: 3
  - Dynamický výběr modelů
  - Telegram notifikace
  - TTS hlas asistenta + speak služba

Nové files: 6
Aktualizované workflows: 1 (hacs.yml)
```

---

## 🔄 Upgrade z v2.0.0

Uživatelé s verzí 2.0.0:
1. **Rozmnož HACS→ Aktualizovat** → v2.1.0
2. **Restartuj HA**
3. Nová nastavení (hlas, Telegram) mají bezpečné výchozí hodnoty → nic se nerozbije
4. Viz **UPGRADE_GUIDE.md** v balíčku

---

## 💡 Tipy pro vydání

1. **Release notes** — publikuj obsah `RELEASE_NOTES_v2_1_0_CZ.md` na GitHub Releases
2. **Discord/Fóra** — oznám novou verzi v Home Assistant komunitě
3. **Automatické workflow** — jakmile pushneš tag `2.1.0`, GitHub Actions
   automaticky vytvoří release s CHANGELOG.md tekstem
4. **HACS approval** — v2.1.0 by měla být schválena automaticky (HACS check projde)

---

## 🆘 Řešení problémů

| Problém | Řešení |
|---------|--------|
| HACS validation selhává | Spusť `hacs-cli validate .` lokálně |
| GitHub Actions failuje | Podívej se na log konkrétního workflow |
| Ikony se nezobrazují | Zkontroluj cestu `custom_components/ollama_assistant/brand/` |
| Model se nenačte | Testuj offline fallback — zadej model ručně |

---

## 📧 Kontakt & Support

Máš dotaz? Otevři issue na GitHubu:
→ https://github.com/USER/ollama-ha-assistant/issues/new

---

## 📝 Metadata

- **Verze:** 2.1.0
- **Datum:** 24. července 2026
- **Stav:** ✅ Ready for HACS
- **HA minimum:** 2024.7.0
- **Python:** 3.11+
- **Licence:** MIT

---

**Hotovo! Jsi připraven k vydání na HACS. 🚀**

*Stáhni si `ollama-ha-assistant-v2_1_0-HACS.zip` a pushni na GitHub.*
