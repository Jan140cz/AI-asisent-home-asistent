# 📲 Průvodce: Telegram notifikace a hlas asistenta

Tento návod popisuje dvě novinky ve verzi 2.1.0:

1. **Odpovědi AI Asistenta i na Telegram** — asistent ti může poslat každou
   svou odpověď (nejen mluvenou/psanou v HA) rovnou do Telegramu.
2. **Vlastní hlas asistenta (TTS)** — vybereš, jakým hlasem má asistent mluvit,
   a můžeš ho nechat "promluvit" na libovolný reproduktor přes novou službu
   `ollama_assistant.speak`.

Žádnou z těchto funkcí si integrace "nevymýšlí" sama — obě stojí na
zabudovaných funkcích Home Assistant (integrace **Telegram bot** a **Text
na řeč / TTS**), naše integrace je jen propojuje dohromady.

---

## 1️⃣ Nastavení Telegramu (krok za krokem)

### Krok 1: Vytvoř si Telegram bota

1. V Telegramu napiš zprávu **[@BotFather](https://t.me/BotFather)**
2. Pošli mu příkaz `/newbot`
3. Zadej jméno bota (cokoliv) a uživatelské jméno (musí končit na `bot`,
   např. `muj_domov_bot`)
4. BotFather ti pošle **API token** — něco jako
   `123456789:AAExxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx`. **Ulož si ho.**

### Krok 2: Zjisti své Chat ID

1. Napiš svému novému botovi cokoliv (např. "ahoj")
2. Otevři v prohlížeči (nahraď `TOKEN` svým tokenem):
   `https://api.telegram.org/botTOKEN/getUpdates`
3. Ve výsledku najdi `"chat":{"id":123456789, ...}` — to číslo je tvoje
   **Chat ID**

### Krok 3: Přidej integraci Telegram bot do Home Assistant

1. **Nastavení → Zařízení a služby → Přidat integraci**
2. Vyhledej **„Telegram bot"**
3. Vyber typ **Broadcast** (stačí pro posílání zpráv)
4. Vlož **API token** a **Chat ID** ze kroků výše
5. Ulož — Home Assistant automaticky vytvoří notifikační službu, typicky
   pojmenovanou **`notify.telegram`** (přesný název uvidíš v
   **Nastavení → Zařízení a služby → Služby**, hledej "notify")

### Krok 4: Zapni propojení v AI Asistentovi

1. **Nastavení → Zařízení a služby → AI Asistent (Ollama) → Možnosti**
2. Zapni ✅ **„Posílat odpovědi i na Telegram"**
3. Do pole **„Název Telegram notifikační služby"** napiš jenom část za
   tečkou, tedy `telegram` (pokud tvoje služba je `notify.telegram`)
4. Uložit

Hotovo! Od teď každá odpověď asistenta (na dotaz z appky, hlasem apod.)
přijde i jako zpráva v Telegramu.

> 💡 **Tip:** Pokud máš víc Telegram botů/notifikačních služeb (např.
> `notify.telegram_petr` a `notify.telegram_jana`), zvol tu, kterou chceš
> používat pro tohoto asistenta.

---

## 2️⃣ Nastavení hlasu asistenta (TTS)

### Předpoklad

Musíš mít v Home Assistant nastavený nějaký TTS engine — např. **Piper**
(offline, zdarma), **Google Translate TTS**, nebo cloudové služby typu
Azure/ElevenLabs (přes vlastní integraci). Pokud zatím žádný nemáš:

**Nastavení → Zařízení a služby → Přidat integraci → vyhledej „Piper"**
(doporučeno pro plně lokální provoz bez cloudu).

### Výběr hlasu

1. **Nastavení → Zařízení a služby → AI Asistent (Ollama) → Možnosti**
2. V poli **„Hlas asistenta (TTS)"** vyber TTS entitu, kterou sis nastavil/a
3. Volitelně do pole **„Název konkrétního hlasu"** napiš přesný název hlasu
   podle dokumentace tvého TTS enginu, například:
   - Piper: `cs_CZ-jirka-medium`
   - Google Translate TTS: nechte prázdné (nepodporuje výběr hlasu)
   - Azure/Edge TTS: `cs-CZ-VlastaNeural` nebo `cs-CZ-AntoninNeural`
4. Uložit

### Jak hlas skutečně použít

- **V hlasovém asistentovi (Assist)** — hlas pro celý hlasový pipeline se
  nastavuje v **Nastavení → Hlasoví asistenti → [tvůj pipeline] → Text na
  řeč**. Tam vyber stejnou TTS entitu a hlas jako v Možnostech AI Asistenta,
  ať sedí dohromady.
- **Pro ohlášení kdekoliv v domě** — použij novou službu
  `ollama_assistant.speak`, která rovnou využije hlas nastavený v Možnostech:

```yaml
service: ollama_assistant.speak
data:
  message: "Večeře je hotová!"
  media_player_entity_id: media_player.kuchyn
```

Tuto službu si můžeš zavolat z libovolné automatizace — třeba když AI
Asistent přes Face Recognition pozná, že jsi přišel/a domů.

---

## 🆘 Řešení problémů

| Příznak | Řešení |
|---------|--------|
| Zprávy nechodí na Telegram | Zkontroluj v logu (`Nastavení → Systém → Protokoly`, hledej `ollama_assistant`) chybové hlášení - obvykle špatný název notifikační služby |
| `notify.telegram` neexistuje | Ověř v **Nastavení → Zařízení a služby → Služby**, jak přesně se tvoje Telegram notifikační služba jmenuje, a použij tento název (bez `notify.`) |
| Služba `ollama_assistant.speak` nic nepřehraje | Zkontroluj, že vybraná TTS entita v Možnostech existuje a že cílový `media_player` podporuje přehrávání zvuku |
| Hlas zní jinak, než jsem čekal/a | Název konkrétního hlasu se liší podle TTS enginu — podívej se do dokumentace svého TTS (Piper/Azure/Google) na přesné názvy hlasů |

---

*Viz také: [FACE_RECOGNITION_GUIDE.md](FACE_RECOGNITION_GUIDE.md), [LOCK_CONTROL_GUIDE.md](LOCK_CONTROL_GUIDE.md)*
