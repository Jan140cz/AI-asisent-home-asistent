# 📦 AI Asistent (Ollama) v2.1.0 — HACS Edition

## 🎉 Co je nového

Verze **2.1.0** je připravena pro HACS s těmito novinkami:

### 1️⃣ **Dynamický výběr modelů** ✨

**Hlavní novinka:** Místo zadávání názvu modelu ručně si ho teď **asistent
automaticky načte** ze serveru a nabídne ti výběr.

**Postup:**
1. Při instalaci zadej pouze **adresu Ollama serveru** (např. `http://192.168.1.100:11434`)
2. Asistent se připojí a načte seznam dostupných modelů
3. Vyber model ze seznamu → hotovo!

**Fallback:** Pokud se modely nenačtou (offline), můžeš model zadat ručně.

### 2️⃣ **Hlas asistenta (TTS)** 🔊

V Možnostech integrace můžeš vybrat:
- **TTS entitu** — kterou hlasitostí chceš asistenta slyšet
- **Konkrétní hlas** — např. `cs-CZ-VlastaNeural` pro Azure TTS

Nová služba `ollama_assistant.speak` — přehraje libovolný text vybraným hlasem
na zvoleném reproduktoru. Ideální pro automatizace.

### 3️⃣ **Telegram notifikace** 📲

Každou odpověď asistenta si můžeš nechat poslat také na Telegram. Postup:
1. Nastav si v HA integraci Telegram bot
2. V Možnostech AI Asistenta zapni "Posílat odpovědi na Telegram"
3. Hotovo — odpovědi chodí na Telegram i domů

Podrobnosti: **TELEGRAM_GUIDE.md**

### 4️⃣ **Vlastní ikona integrace** 🎨

Integrace má teď vlastní designovanou ikonu/logo (modro-fialová bublina se
zvukem). Zobrazuje se v detailu integrace v Nastavení → Zařízení a služby.

### 5️⃣ **HACS-ready strukturaª** 📋

Balíček obsahuje vše, co HACS potřebuje:
- ✅ Workflows pro GitHub Actions (validace, hassfest, HACS check)
- ✅ hacs.json s topics a metadaty
- ✅ README s HACS badges a install tlačítkem
- ✅ CONTRIBUTING.md pro příspěvatele
- ✅ GITHUB_SETUP.md — návod na GitHub přípravy
- ✅ HACS_QUICKSTART.md — začátek pro nové uživatele

---

## 📁 Obsah balíčku

```
ollama-ha-assistant-v2_1_0/
├── custom_components/ollama_assistant/
│   ├── __init__.py                    (s registrací speak služby)
│   ├── config_flow.py                 (nový krok: výběr modelu)
│   ├── conversation.py                (s Telegram notifikacemi)
│   ├── const.py                       (nové TTS/Telegram konstanty)
│   ├── face_recognition.py            (rozpoznávání obličejů)
│   ├── lock_control.py                (odemykání dveří)
│   ├── services.yaml                  (ℕOVÝ — speak služba)
│   ├── manifest.json                  (v2.1.0)
│   ├── brand/                         (ℕOVÉ — icon.png, logo.png atd.)
│   ├── translations/                  (cs.json, en.json)
│   └── ...
├── .github/
│   └── workflows/                     (validace, HACS, release)
├── README.md                          (s HACS badges)
├── CHANGELOG.md                       (záznam v2.1.0)
├── UPGRADE_GUIDE.md                   (aktualizace z v2.0.0)
├── TELEGRAM_GUIDE.md                  (ℕOVÉ — hlas a Telegram)
├── HACS_QUICKSTART.md                 (ℕOVÉ — začátek pro HACS)
├── CONTRIBUTING.md                    (jak přispět)
├── GITHUB_SETUP.md                    (nastavení GitHub repo)
├── hacs.json                          (metada, topics)
├── docker-compose.yml                 (testovací Ollama)
└── ...
```

---

## 🚀 Jak instalovat

### Varianta 1: HACS (doporučeno)

1. V Home Assistant: **HACS → Integrace → ⋮ → Vlastní repozitáře**
2. Vlož: `https://github.com/USER/ollama-ha-assistant`
3. Hledej **AI Asistent (Ollama)** → Nainstaluj → Restart HA
4. **Nastavení → Zařízení a služby → Přidat integraci → AI Asistent**
5. Zadej adresu Ollama → **asistent si načte seznam modelů** → vyber

### Varianta 2: Manuální instalace

```bash
# Rozbal zip do custom_components:
unzip ollama-ha-assistant-v2_1_0-HACS.zip
cp -r ollama_ha_assistant/custom_components/ollama_assistant \
      $HA_CONFIG_DIR/custom_components/

# Restart Home Assistant
```

---

## ✅ Checklist před vydáním

- ✅ Všechny Python soubory se kompilují bez chyb
- ✅ JSON soubory jsou validní
- ✅ Workflow v GitHub Actions fungují (validate.yml, hassfest.yml, hacs.yml)
- ✅ README má HACS badges a install tlačítko
- ✅ Verze v manifest.json = 2.1.0
- ✅ Changelog aktualizován
- ✅ Ikony v brand/ složce existují
- ✅ Translations (cs.json, en.json) mají všechna nová pole
- ✅ services.yaml obsahuje speak službu

---

## 📖 Dokumentace

| Soubor | Pro | Popis |
|--------|-----|-------|
| **README.md** | Všichni | Přehled, instalace, features |
| **HACS_QUICKSTART.md** | Nováci | 3 kroky k instalaci skrze HACS |
| **TELEGRAM_GUIDE.md** | Hlasu & Telegram | Setup hlasu (TTS) a Telegramu |
| **FACE_RECOGNITION_GUIDE.md** | Kamery | Rozpoznávání obličejů |
| **LOCK_CONTROL_GUIDE.md** | Zabezpečení | Automatické odemykání |
| **UPGRADE_GUIDE.md** | Stávajícím | Jak upgradovat ze v2.0.0 |
| **CONTRIBUTING.md** | Vývojáři | Jak přispět |
| **GITHUB_SETUP.md** | GitHub Admini | Příprava GitHub repo |

---

## 🔧 Technické detaily

### Config Flow (nový krok)

```python
# Krok 1: Zadání adresy Ollama
async def async_step_user() -> Automaticky načte dostupné modely

# Krok 2: Výběr modelu ze seznamu
async def async_step_model() -> Uživatel vyvolí model ze SelectSelectorConfig
```

### Telegram notifikace

```python
# Automaticky se zavolá po každé odpovědi:
await _send_telegram_notification(reply_text)
```

### Speak služba

```yaml
service: ollama_assistant.speak
data:
  message: "Ahoj!"
  media_player_entity_id: media_player.obyvaci_pokoj
  # Hlas se automaticky vezme z Možnosti integrace
```

### Verze Home Assistant

- **Minimum:** 2024.7.0 (z manifest.json)
- **Testováno na:** 2024.7+ a 2026.3+

---

## 🔒 Bezpečnost & Soukromí

- ✅ Všechna data zůstávají v lokální síti
- ✅ Žádné posílání obrázků/textu do cloudu
- ✅ Telegram bot token je tvůj (v HA config) — neposílá se do projektu
- ✅ Databáze obličejů zůstává v domácnosti

---

## 🆘 Support

- **Issues:** https://github.com/USER/ollama-ha-assistant/issues
- **Discussions:** https://github.com/USER/ollama-ha-assistant/discussions
- **Community:** Home Assistant Community forums

---

## 📝 Autor & Licence

- **Licence:** MIT
- **Autor:** USER (nahraď si svým jménem)

**Příjemné používání! 🚀**

---

*Vydáno: 24. července 2026*
*Verze: 2.1.0*
*Status: Ready for HACS ✅*
