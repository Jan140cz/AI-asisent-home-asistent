# 🎯 HACS Instalační Průvodce

Vítej! Instaluješ **AI Asistent (Ollama)** — konverzační agenta do Home Assistant,
který běží na tvém vlastním AI serveru (Ollama) bez posílání dat do cloudu.

## ✅ Co potřebuješ

- **Běžící Ollama server** — někde v síti (PC, NAS, Raspberry Pi…)
  ```bash
  # Stažení a spuštění Ollamy:
  curl https://ollama.ai/install.sh | sh
  ollama serve
  ```

- **Stažený model** — minimálně jeden:
  ```bash
  ollama pull llama3.1    # Doporučeno (nejlepší support tool-calling)
  # nebo:
  ollama pull qwen2.5     # Levnější, rychlejší
  ollama pull mistral-nemo # Malý, dobrý poměr výkonu/velikosti
  ```

- **Home Assistant 2024.7.0+**

## 🚀 Instalace (3 kroky)

### 1. Instalace skrze HACS

1. **HACS → Integrace**
2. Klikni vpravo nahoře **⋮** (tři tečky) → **Vlastní repozitáře**
3. Vlož: `https://github.com/USER/ollama-ha-assistant`
4. Vyber **Integrace** jako kategorii
5. Najdi **AI Asistent (Ollama)** → Klikni **Nainstaluj**
6. **Restartuj Home Assistant**

### 2. Přidání integrace

1. **Nastavení → Zařízení a služby**
2. Klikni **Přidat integraci**
3. Hledej **AI Asistent (Ollama)**
4. Zadej adresu Ollama serveru: `http://192.168.1.100:11434` (nebo `http://localhost:11434`)
5. Asistent automaticky **načte seznam dostupných modelů** — vyber jeden ze seznamu
6. Klikni **Vytvořit**

> 💡 **Novinkou v 2.1.0** je, že **už nemusíš psát název modelu** — asistent ho
> načte ze serveru a nabídne ti výběr! Pokud by načtení selhalo (např. offline),
> můžeš model zadat ručně.

### 3. Základní nastavení

1. Klikni na integraci v **Nastavení → Zařízení a služby** → **Možnosti**
2. Nastav:
   - **Jazyk odpovědí** — čeština/angličtina/apod.
   - **Systémový prompt** — jak se má asistent chovat
   - **Ovládání zařízení** — vyber **Home Assistant LLM**, aby mohl ovládat tvá zařízení

Hotovo! 🎉

## 🆕 Novinky ve verzi 2.1.0

- **🔊 Hlas asistenta** — vyber si TTS (text-to-speech) a konkrétní hlas,
  používej novou službu `ollama_assistant.speak` v automatizacích
- **📲 Telegram** — posílej si odpovědi asistenta i na Telegram
- **🎨 Vlastní ikona** — integrace má teď vlastní design
- **Automatický výběr modelů** — asistent si přednačte dostupné modely z Ollamy

Detaily: **[TELEGRAM_GUIDE.md](TELEGRAM_GUIDE.md)** pro hlas a Telegram.

## 🆘 Řešení problémů

| Problém | Řešení |
|---------|--------|
| "Nelze se připojit na Ollama" | Zkontroluj, že Ollama běží (`ollama serve`) a zadal/a správnou adresu |
| Žádné modely se nenačetly | Stáhni model: `ollama pull llama3.1` |
| Asistent neovládá zařízení | Vyber v Možnostech **Home Assistant LLM** a ujisti se, že model má support tool-calling |
| Odpovědi jsou příliš dlouhé/krátké | V Možnostech nastav **Kreativitu** (temperature) a **Systémový prompt** |

Více: **[README.md](README.md)** + **[UPGRADE_GUIDE.md](UPGRADE_GUIDE.md)**

## 📚 Pokročilé

- **[FACE_RECOGNITION_GUIDE.md](FACE_RECOGNITION_GUIDE.md)** — rozpoznávání obličejů z kamer
- **[LOCK_CONTROL_GUIDE.md](LOCK_CONTROL_GUIDE.md)** — automatické odemykání dveří
- **[TELEGRAM_GUIDE.md](TELEGRAM_GUIDE.md)** — hlasitost, Telegram, novinka v 2.1.0

## 🤝 Přispívání

Chceš pomoci? Podívej se na **[CONTRIBUTING.md](CONTRIBUTING.md)**.

---

**Příjemné používání! Máš dotaz? Otevři [GitHub Issue](https://github.com/USER/ollama-ha-assistant/issues).**
