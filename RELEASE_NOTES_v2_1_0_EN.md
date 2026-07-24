# 📦 AI Assistant (Ollama) v2.1.0 — HACS Edition

## 🎉 What's New

Version **2.1.0** is HACS-ready with these major features:

### 1️⃣ **Dynamic Model Selection** ✨

**Main feature:** Instead of typing the model name manually, the assistant
**automatically detects available models** from the Ollama server and offers
you a dropdown to choose.

**How it works:**
1. During setup, enter only the **Ollama server address** (e.g., `http://192.168.1.100:11434`)
2. Assistant connects and fetches available models
3. Pick a model from the dropdown → done!

**Fallback:** If model detection fails (offline), you can enter the model name manually.

### 2️⃣ **Assistant Voice (TTS)** 🔊

In integration Options, you can select:
- **TTS entity** — which text-to-speech provider to use
- **Voice name** — e.g., `en-US-JennyNeural` for Azure TTS

New service `ollama_assistant.speak` — speaks any text using the selected voice
on a media player of your choice. Perfect for automations.

### 3️⃣ **Telegram Notifications** 📲

Get every assistant response sent to your Telegram. Setup:
1. Configure Telegram bot integration in Home Assistant
2. In AI Assistant Options, enable "Send replies to Telegram"
3. Done — responses appear on Telegram too

Details: **TELEGRAM_GUIDE.md**

### 4️⃣ **Custom Integration Icon** 🎨

The integration now has a custom branded icon (blue-to-purple chat bubble with
voice waves). Shows in Settings → Devices & Services detail page.

### 5️⃣ **HACS-ready Structure** 📋

Package includes everything HACS needs:
- ✅ GitHub Actions workflows (validation, hassfest, HACS check)
- ✅ hacs.json with topics and metadata
- ✅ README with HACS badges and install button
- ✅ CONTRIBUTING.md for contributors
- ✅ GITHUB_SETUP.md — GitHub repository preparation
- ✅ HACS_QUICKSTART.md — quick start for new users

---

## 📁 Package Contents

```
ollama-ha-assistant-v2_1_0/
├── custom_components/ollama_assistant/
│   ├── __init__.py                    (with speak service registration)
│   ├── config_flow.py                 (NEW: model selection step)
│   ├── conversation.py                (with Telegram notifications)
│   ├── const.py                       (new TTS/Telegram constants)
│   ├── face_recognition.py            (face recognition)
│   ├── lock_control.py                (smart door unlock)
│   ├── services.yaml                  (NEW — speak service)
│   ├── manifest.json                  (v2.1.0)
│   ├── brand/                         (NEW — icon.png, logo.png etc.)
│   ├── translations/                  (cs.json, en.json)
│   └── ...
├── .github/
│   └── workflows/                     (validation, HACS, release)
├── README.md                          (with HACS badges)
├── CHANGELOG.md                       (v2.1.0 entry)
├── UPGRADE_GUIDE.md                   (upgrade from v2.0.0)
├── TELEGRAM_GUIDE.md                  (NEW — voice & Telegram)
├── HACS_QUICKSTART.md                 (NEW — HACS quick start)
├── CONTRIBUTING.md                    (how to contribute)
├── GITHUB_SETUP.md                    (GitHub repo setup)
├── hacs.json                          (metadata, topics)
├── docker-compose.yml                 (test Ollama setup)
└── ...
```

---

## 🚀 Installation

### Option 1: HACS (Recommended)

1. In Home Assistant: **HACS → Integrations → ⋮ → Custom repositories**
2. Add: `https://github.com/USER/ollama-ha-assistant`
3. Search for **AI Assistant (Ollama)** → Install → Restart HA
4. **Settings → Devices & Services → Create Integration → AI Assistant**
5. Enter Ollama address → **assistant auto-loads available models** → pick one

### Option 2: Manual Installation

```bash
# Extract zip to custom_components:
unzip ollama-ha-assistant-v2_1_0-HACS.zip
cp -r ollama_ha_assistant/custom_components/ollama_assistant \
      $HA_CONFIG_DIR/custom_components/

# Restart Home Assistant
```

---

## ✅ Pre-release Checklist

- ✅ All Python files compile without errors
- ✅ JSON files are valid
- ✅ GitHub Actions workflows pass (validate.yml, hassfest.yml, hacs.yml)
- ✅ README has HACS badges and install button
- ✅ Version in manifest.json = 2.1.0
- ✅ CHANGELOG updated
- ✅ Brand icons in brand/ folder exist
- ✅ Translations (cs.json, en.json) have all new fields
- ✅ services.yaml contains speak service

---

## 📖 Documentation

| File | For | Description |
|------|-----|-------------|
| **README.md** | Everyone | Overview, installation, features |
| **HACS_QUICKSTART.md** | New Users | 3-step HACS installation |
| **TELEGRAM_GUIDE.md** | Voice & Telegram | TTS & Telegram setup |
| **FACE_RECOGNITION_GUIDE.md** | Cameras | Face recognition setup |
| **LOCK_CONTROL_GUIDE.md** | Security | Auto door unlock |
| **UPGRADE_GUIDE.md** | Existing Users | Upgrade from v2.0.0 |
| **CONTRIBUTING.md** | Developers | How to contribute |
| **GITHUB_SETUP.md** | GitHub Admins | Repo setup |

---

## 🔧 Technical Details

### Config Flow (New Step)

```python
# Step 1: Enter Ollama address
async def async_step_user() -> Automatically fetches available models

# Step 2: Pick model from list
async def async_step_model() -> User chooses from SelectSelectorConfig
```

### Telegram Notifications

```python
# Automatically called after each response:
await _send_telegram_notification(reply_text)
```

### Speak Service

```yaml
service: ollama_assistant.speak
data:
  message: "Hello!"
  media_player_entity_id: media_player.living_room
  # Voice is automatically taken from integration Options
```

### Home Assistant Version

- **Minimum:** 2024.7.0 (from manifest.json)
- **Tested on:** 2024.7+ and 2026.3+

---

## 🔒 Security & Privacy

- ✅ All data stays on your local network
- ✅ No images/text sent to cloud
- ✅ Telegram bot token is yours (in HA config) — never sent externally
- ✅ Face recognition database stays at home

---

## 🆘 Support

- **Issues:** https://github.com/USER/ollama-ha-assistant/issues
- **Discussions:** https://github.com/USER/ollama-ha-assistant/discussions
- **Community:** Home Assistant Community forums

---

## 📝 Author & License

- **License:** MIT
- **Author:** USER (replace with your name)

**Happy automating! 🚀**

---

*Released: July 24, 2026*
*Version: 2.1.0*
*Status: Ready for HACS ✅*
